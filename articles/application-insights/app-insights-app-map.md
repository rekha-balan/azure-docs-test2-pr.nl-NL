---
title: Application Map in Azure Application Insights | Microsoft Docs
description: A visual presentation of the dependencies between app components, labeled with KPIs and alerts.
services: application-insights
documentationcenter: ''
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: e771216c6f728aa7c7867f721001df7c1f13d932
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555470"
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="336c4-103">Application Map in Application Insights</span><span class="sxs-lookup"><span data-stu-id="336c4-103">Application Map in Application Insights</span></span>
<span data-ttu-id="336c4-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of the dependency relationships of your application components.</span><span class="sxs-lookup"><span data-stu-id="336c4-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of the dependency relationships of your application components.</span></span> <span data-ttu-id="336c4-105">Each component shows KPIs such as load, performance, failures, and alerts, to help you discover any component causing a performance issue or failure.</span><span class="sxs-lookup"><span data-stu-id="336c4-105">Each component shows KPIs such as load, performance, failures, and alerts, to help you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="336c4-106">You can click through from any component to more detailed diagnostics, such as Application Insights events.</span><span class="sxs-lookup"><span data-stu-id="336c4-106">You can click through from any component to more detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="336c4-107">If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.</span><span class="sxs-lookup"><span data-stu-id="336c4-107">If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="336c4-108">Like other charts, you can pin an application map to the Azure dashboard, where it is fully functional.</span><span class="sxs-lookup"><span data-stu-id="336c4-108">Like other charts, you can pin an application map to the Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-the-application-map"></a><span data-ttu-id="336c4-109">Open the application map</span><span class="sxs-lookup"><span data-stu-id="336c4-109">Open the application map</span></span>
<span data-ttu-id="336c4-110">Open the map from the overview blade for your application:</span><span class="sxs-lookup"><span data-stu-id="336c4-110">Open the map from the overview blade for your application:</span></span>

![open app map](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/01.png)

![app map](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/02.png)

<span data-ttu-id="336c4-113">The map shows:</span><span class="sxs-lookup"><span data-stu-id="336c4-113">The map shows:</span></span>

* <span data-ttu-id="336c4-114">Availability tests</span><span class="sxs-lookup"><span data-stu-id="336c4-114">Availability tests</span></span>
* <span data-ttu-id="336c4-115">Client-side component (monitored with the JavaScript SDK)</span><span class="sxs-lookup"><span data-stu-id="336c4-115">Client-side component (monitored with the JavaScript SDK)</span></span>
* <span data-ttu-id="336c4-116">Server-side component</span><span class="sxs-lookup"><span data-stu-id="336c4-116">Server-side component</span></span>
* <span data-ttu-id="336c4-117">Dependencies of the client and server components</span><span class="sxs-lookup"><span data-stu-id="336c4-117">Dependencies of the client and server components</span></span>

<span data-ttu-id="336c4-118">You can expand and collapse dependency link groups:</span><span class="sxs-lookup"><span data-stu-id="336c4-118">You can expand and collapse dependency link groups:</span></span>

![collapse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/03.png)

<span data-ttu-id="336c4-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span><span class="sxs-lookup"><span data-stu-id="336c4-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![grouped dependencies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="336c4-122">Spot problems</span><span class="sxs-lookup"><span data-stu-id="336c4-122">Spot problems</span></span>
<span data-ttu-id="336c4-123">Each node has relevant performance indicators, such as the load, performance, and failure rates for that component.</span><span class="sxs-lookup"><span data-stu-id="336c4-123">Each node has relevant performance indicators, such as the load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="336c4-124">Warning icons highlight possible problems.</span><span class="sxs-lookup"><span data-stu-id="336c4-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="336c4-125">An orange warning means there are failures in requests, page views or dependency calls.</span><span class="sxs-lookup"><span data-stu-id="336c4-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="336c4-126">Red means a failure rate above 5%.</span><span class="sxs-lookup"><span data-stu-id="336c4-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="336c4-127">If you want to adjust these thresholds, open Options.</span><span class="sxs-lookup"><span data-stu-id="336c4-127">If you want to adjust these thresholds, open Options.</span></span>

![failure icons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/04.png)

<span data-ttu-id="336c4-129">Active alerts also show up:</span><span class="sxs-lookup"><span data-stu-id="336c4-129">Active alerts also show up:</span></span> 

![active alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/05.png)

<span data-ttu-id="336c4-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span><span class="sxs-lookup"><span data-stu-id="336c4-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Azure recommendation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/06.png)

<span data-ttu-id="336c4-133">Click any icon to get more details:</span><span class="sxs-lookup"><span data-stu-id="336c4-133">Click any icon to get more details:</span></span>

![azure recommendation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="336c4-135">Diagnostic click through</span><span class="sxs-lookup"><span data-stu-id="336c4-135">Diagnostic click through</span></span>
<span data-ttu-id="336c4-136">Each of the nodes on the map offers targeted click through for diagnostics.</span><span class="sxs-lookup"><span data-stu-id="336c4-136">Each of the nodes on the map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="336c4-137">The options vary depending on the type of the node.</span><span class="sxs-lookup"><span data-stu-id="336c4-137">The options vary depending on the type of the node.</span></span>

![server options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/09.png)

<span data-ttu-id="336c4-139">For components that are hosted in Azure, the options include direct links to them.</span><span class="sxs-lookup"><span data-stu-id="336c4-139">For components that are hosted in Azure, the options include direct links to them.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="336c4-140">Filters and time range</span><span class="sxs-lookup"><span data-stu-id="336c4-140">Filters and time range</span></span>
<span data-ttu-id="336c4-141">By default, the map summarizes all the data available for the chosen time range.</span><span class="sxs-lookup"><span data-stu-id="336c4-141">By default, the map summarizes all the data available for the chosen time range.</span></span> <span data-ttu-id="336c4-142">But you can filter it to include only specific operation names or dependencies.</span><span class="sxs-lookup"><span data-stu-id="336c4-142">But you can filter it to include only specific operation names or dependencies.</span></span>

* <span data-ttu-id="336c4-143">Operation name: This includes both page views and server-side request types.</span><span class="sxs-lookup"><span data-stu-id="336c4-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="336c4-144">With this option, the map shows the KPI on the server/client-side node for the selected operations only.</span><span class="sxs-lookup"><span data-stu-id="336c4-144">With this option, the map shows the KPI on the server/client-side node for the selected operations only.</span></span> <span data-ttu-id="336c4-145">It shows the dependencies called in the context of those specific operations.</span><span class="sxs-lookup"><span data-stu-id="336c4-145">It shows the dependencies called in the context of those specific operations.</span></span>
* <span data-ttu-id="336c4-146">Dependency base name: This includes the AJAX browser dependencies and server-side dependencies.</span><span class="sxs-lookup"><span data-stu-id="336c4-146">Dependency base name: This includes the AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="336c4-147">If you report custom dependency telemetry with the TrackDependency API, they also appear here.</span><span class="sxs-lookup"><span data-stu-id="336c4-147">If you report custom dependency telemetry with the TrackDependency API, they also appear here.</span></span> <span data-ttu-id="336c4-148">You can select the dependencies to show on the map.</span><span class="sxs-lookup"><span data-stu-id="336c4-148">You can select the dependencies to show on the map.</span></span> <span data-ttu-id="336c4-149">Currently this selection does not filter the server-side requests, or the client-side page views.</span><span class="sxs-lookup"><span data-stu-id="336c4-149">Currently this selection does not filter the server-side requests, or the client-side page views.</span></span>

![Set filters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="336c4-151">Save filters</span><span class="sxs-lookup"><span data-stu-id="336c4-151">Save filters</span></span>
<span data-ttu-id="336c4-152">To save the filters you have applied, pin the filtered view onto a [dashboard](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="336c4-152">To save the filters you have applied, pin the filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Pin to dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/12.png)

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="336c4-154">End-to-end system app maps</span><span class="sxs-lookup"><span data-stu-id="336c4-154">End-to-end system app maps</span></span>

<span data-ttu-id="336c4-155">If your application has several components - for example, a back-end service in addition to the web app - then you can show them all on one integrated app map.</span><span class="sxs-lookup"><span data-stu-id="336c4-155">If your application has several components - for example, a back-end service in addition to the web app - then you can show them all on one integrated app map.</span></span>

![Set filters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="336c4-157">The app map finds server nodes by looking for all Application Insights resources within the current resource group.</span><span class="sxs-lookup"><span data-stu-id="336c4-157">The app map finds server nodes by looking for all Application Insights resources within the current resource group.</span></span> <span data-ttu-id="336c4-158">It also detects server nodes by following any dependency calls tracked by Application Insights resources in the current resource group.</span><span class="sxs-lookup"><span data-stu-id="336c4-158">It also detects server nodes by following any dependency calls tracked by Application Insights resources in the current resource group.</span></span>


### <a name="setting-up"></a><span data-ttu-id="336c4-159">Setting up</span><span class="sxs-lookup"><span data-stu-id="336c4-159">Setting up</span></span>

> [!NOTE] 
> <span data-ttu-id="336c4-160">End-to-end system app map is in preview.</span><span class="sxs-lookup"><span data-stu-id="336c4-160">End-to-end system app map is in preview.</span></span> <span data-ttu-id="336c4-161">You have to instrument your components with a special version of the SDK, and you have to use a special URL to see the app map.</span><span class="sxs-lookup"><span data-stu-id="336c4-161">You have to instrument your components with a special version of the SDK, and you have to use a special URL to see the app map.</span></span> <span data-ttu-id="336c4-162">[Learn how to set up end-to-end system app maps](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/app-insights-app-map-preview.md).</span><span class="sxs-lookup"><span data-stu-id="336c4-162">[Learn how to set up end-to-end system app maps](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/app-insights-app-map-preview.md).</span></span>

## <a name="video"></a><span data-ttu-id="336c4-163">Video</span><span class="sxs-lookup"><span data-stu-id="336c4-163">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="336c4-164">Feedback</span><span class="sxs-lookup"><span data-stu-id="336c4-164">Feedback</span></span>
<span data-ttu-id="336c4-165">Please provide feedback through the portal feedback option.</span><span class="sxs-lookup"><span data-stu-id="336c4-165">Please provide feedback through the portal feedback option.</span></span>

![MapLink-1 image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="336c4-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="336c4-167">Next steps</span></span>

* [<span data-ttu-id="336c4-168">Azure portal</span><span class="sxs-lookup"><span data-stu-id="336c4-168">Azure portal</span></span>](https://portal.azure.com)












