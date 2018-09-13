---
title: Application Insights telemetry in Visual Studio CodeLens | Microsoft Docs
description: Quickly access your Application Insights request and exception telemetry with CodeLens in Visual Studio.
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: daviste
ms.openlocfilehash: 75f663ef81b7d473ac4b071d0b79e9d02aa24f18
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660539"
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a><span data-ttu-id="0cc62-103">Application Insights telemetry in Visual Studio CodeLens</span><span class="sxs-lookup"><span data-stu-id="0cc62-103">Application Insights telemetry in Visual Studio CodeLens</span></span>
<span data-ttu-id="0cc62-104">Methods in the code of your web app can be annotated with telemetry about run-time exceptions and request response times.</span><span class="sxs-lookup"><span data-stu-id="0cc62-104">Methods in the code of your web app can be annotated with telemetry about run-time exceptions and request response times.</span></span> <span data-ttu-id="0cc62-105">If you install [Azure Application Insights](app-insights-overview.md) in your application, the telemetry appears in Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) - the notes at the top of each function where you're used to seeing useful information such as the number of places the function is referenced or the last person who edited it.</span><span class="sxs-lookup"><span data-stu-id="0cc62-105">If you install [Azure Application Insights](app-insights-overview.md) in your application, the telemetry appears in Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) - the notes at the top of each function where you're used to seeing useful information such as the number of places the function is referenced or the last person who edited it.</span></span>

![CodeLens](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> <span data-ttu-id="0cc62-107">Application Insights in CodeLens is available in Visual Studio 2015 Update 3 and later, or with the latest version of [Developer Analytics Tools extension](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a).</span><span class="sxs-lookup"><span data-stu-id="0cc62-107">Application Insights in CodeLens is available in Visual Studio 2015 Update 3 and later, or with the latest version of [Developer Analytics Tools extension](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a).</span></span> <span data-ttu-id="0cc62-108">CodeLens is available in the Enterprise and Professional editions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0cc62-108">CodeLens is available in the Enterprise and Professional editions of Visual Studio.</span></span>
> 
> 

## <a name="where-to-find-application-insights-data"></a><span data-ttu-id="0cc62-109">Where to find Application Insights data</span><span class="sxs-lookup"><span data-stu-id="0cc62-109">Where to find Application Insights data</span></span>
<span data-ttu-id="0cc62-110">Look for Application Insights telemetry in the CodeLens indicators of the public request methods of your web application.</span><span class="sxs-lookup"><span data-stu-id="0cc62-110">Look for Application Insights telemetry in the CodeLens indicators of the public request methods of your web application.</span></span> <span data-ttu-id="0cc62-111">CodeLens indicators are shown above method and other declarations in C# and Visual Basic code.</span><span class="sxs-lookup"><span data-stu-id="0cc62-111">CodeLens indicators are shown above method and other declarations in C# and Visual Basic code.</span></span> <span data-ttu-id="0cc62-112">If Application Insights data is available for a method, you'll see indicators for requests and exceptions such as "100 requests, 1% failed" or "10 exceptions."</span><span class="sxs-lookup"><span data-stu-id="0cc62-112">If Application Insights data is available for a method, you'll see indicators for requests and exceptions such as "100 requests, 1% failed" or "10 exceptions."</span></span> <span data-ttu-id="0cc62-113">Click a CodeLens indicator for more details.</span><span class="sxs-lookup"><span data-stu-id="0cc62-113">Click a CodeLens indicator for more details.</span></span> 

> [!TIP]
> <span data-ttu-id="0cc62-114">Application Insights request and exception indicators may take a few extra seconds to load after other CodeLens indicators appear.</span><span class="sxs-lookup"><span data-stu-id="0cc62-114">Application Insights request and exception indicators may take a few extra seconds to load after other CodeLens indicators appear.</span></span>
> 
> 

## <a name="exceptions-in-codelens"></a><span data-ttu-id="0cc62-115">Exceptions in CodeLens</span><span class="sxs-lookup"><span data-stu-id="0cc62-115">Exceptions in CodeLens</span></span>
![TBD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-codelens/codelens-exceptions.png)

<span data-ttu-id="0cc62-117">The exception CodeLens indicator shows the number of exceptions that have occurred in the past 24 hours from the 15 most frequently occurring exceptions in your application during that period, while processing the request served by the method.</span><span class="sxs-lookup"><span data-stu-id="0cc62-117">The exception CodeLens indicator shows the number of exceptions that have occurred in the past 24 hours from the 15 most frequently occurring exceptions in your application during that period, while processing the request served by the method.</span></span>

<span data-ttu-id="0cc62-118">To see more details, click the exceptions CodeLens indicator:</span><span class="sxs-lookup"><span data-stu-id="0cc62-118">To see more details, click the exceptions CodeLens indicator:</span></span>

* <span data-ttu-id="0cc62-119">The percentage change in number of exceptions from the most recent 24 hours relative to the prior 24 hours</span><span class="sxs-lookup"><span data-stu-id="0cc62-119">The percentage change in number of exceptions from the most recent 24 hours relative to the prior 24 hours</span></span>
* <span data-ttu-id="0cc62-120">Choose **Go to code** to navigate to the source code for the function throwing the exception</span><span class="sxs-lookup"><span data-stu-id="0cc62-120">Choose **Go to code** to navigate to the source code for the function throwing the exception</span></span>
* <span data-ttu-id="0cc62-121">Choose **Search** to query all instances of this exception that have occurred in the past 24 hours</span><span class="sxs-lookup"><span data-stu-id="0cc62-121">Choose **Search** to query all instances of this exception that have occurred in the past 24 hours</span></span>
* <span data-ttu-id="0cc62-122">Choose **Trend** to view a trend visualization for occurrences of this exception in the past 24 hours</span><span class="sxs-lookup"><span data-stu-id="0cc62-122">Choose **Trend** to view a trend visualization for occurrences of this exception in the past 24 hours</span></span>
* <span data-ttu-id="0cc62-123">Choose **View all exceptions in this app** to query all exceptions that have occurred in the past 24 hours</span><span class="sxs-lookup"><span data-stu-id="0cc62-123">Choose **View all exceptions in this app** to query all exceptions that have occurred in the past 24 hours</span></span>
* <span data-ttu-id="0cc62-124">Choose **Explore exception trends** to view a trend visualization for all exceptions that have occurred in the past 24 hours.</span><span class="sxs-lookup"><span data-stu-id="0cc62-124">Choose **Explore exception trends** to view a trend visualization for all exceptions that have occurred in the past 24 hours.</span></span> 

> [!TIP]
> <span data-ttu-id="0cc62-125">If you see "0 exceptions" in CodeLens but you know there should be exceptions, check to make sure the right Application Insights resource is selected in CodeLens.</span><span class="sxs-lookup"><span data-stu-id="0cc62-125">If you see "0 exceptions" in CodeLens but you know there should be exceptions, check to make sure the right Application Insights resource is selected in CodeLens.</span></span> <span data-ttu-id="0cc62-126">To select another resource, right-click on your project in the Solution Explorer and choose **Application Insights > Choose Telemetry Source**.</span><span class="sxs-lookup"><span data-stu-id="0cc62-126">To select another resource, right-click on your project in the Solution Explorer and choose **Application Insights > Choose Telemetry Source**.</span></span> <span data-ttu-id="0cc62-127">CodeLens is only shown for the 15 most frequently occurring exceptions in your application in the past 24 hours, so if an exception is the 16th most frequently or less, you'll see "0 exceptions."</span><span class="sxs-lookup"><span data-stu-id="0cc62-127">CodeLens is only shown for the 15 most frequently occurring exceptions in your application in the past 24 hours, so if an exception is the 16th most frequently or less, you'll see "0 exceptions."</span></span> <span data-ttu-id="0cc62-128">Exceptions from ASP.NET views may not appear on the controller methods that generated those views.</span><span class="sxs-lookup"><span data-stu-id="0cc62-128">Exceptions from ASP.NET views may not appear on the controller methods that generated those views.</span></span>
> 
> [!TIP]
> <span data-ttu-id="0cc62-129">If you see "?</span><span class="sxs-lookup"><span data-stu-id="0cc62-129">If you see "?</span></span> <span data-ttu-id="0cc62-130">exceptions" in CodeLens, you need to associate your Azure account with Visual Studio or your Azure account credential may have expired.</span><span class="sxs-lookup"><span data-stu-id="0cc62-130">exceptions" in CodeLens, you need to associate your Azure account with Visual Studio or your Azure account credential may have expired.</span></span> <span data-ttu-id="0cc62-131">In either case, click "?</span><span class="sxs-lookup"><span data-stu-id="0cc62-131">In either case, click "?</span></span> <span data-ttu-id="0cc62-132">exceptions" and choose **Add an account...** to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="0cc62-132">exceptions" and choose **Add an account...** to enter your credentials.</span></span>
> 
> 

## <a name="requests-in-codelens"></a><span data-ttu-id="0cc62-133">Requests in CodeLens</span><span class="sxs-lookup"><span data-stu-id="0cc62-133">Requests in CodeLens</span></span>
![TBD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-codelens/codelens-requests.png)

<span data-ttu-id="0cc62-135">The request CodeLens indicator shows the number of HTTP requests that been serviced by a method in the past 24 hours, plus the percentage of those requests that failed.</span><span class="sxs-lookup"><span data-stu-id="0cc62-135">The request CodeLens indicator shows the number of HTTP requests that been serviced by a method in the past 24 hours, plus the percentage of those requests that failed.</span></span>

<span data-ttu-id="0cc62-136">To see more details, click the requests CodeLens indicator:</span><span class="sxs-lookup"><span data-stu-id="0cc62-136">To see more details, click the requests CodeLens indicator:</span></span>

* <span data-ttu-id="0cc62-137">The absolute and percentage changes in number of requests, failed requests, and average response times over the past 24 hours compared to the prior 24 hours</span><span class="sxs-lookup"><span data-stu-id="0cc62-137">The absolute and percentage changes in number of requests, failed requests, and average response times over the past 24 hours compared to the prior 24 hours</span></span>
* <span data-ttu-id="0cc62-138">The reliability of the method, calculated as the percentage of requests that did not fail in the past 24 hours</span><span class="sxs-lookup"><span data-stu-id="0cc62-138">The reliability of the method, calculated as the percentage of requests that did not fail in the past 24 hours</span></span>
* <span data-ttu-id="0cc62-139">Choose **Search** for requests or failed requests to query all the (failed) requests that occurred in the past 24 hours</span><span class="sxs-lookup"><span data-stu-id="0cc62-139">Choose **Search** for requests or failed requests to query all the (failed) requests that occurred in the past 24 hours</span></span>
* <span data-ttu-id="0cc62-140">Choose **Trend** to view a trend visualization for requests, failed requests, or average response times in the past 24 hours.</span><span class="sxs-lookup"><span data-stu-id="0cc62-140">Choose **Trend** to view a trend visualization for requests, failed requests, or average response times in the past 24 hours.</span></span>
* <span data-ttu-id="0cc62-141">Choose the name of the Application Insights resource in the upper left corner of the CodeLens details view to change which resource is the source for CodeLens data.</span><span class="sxs-lookup"><span data-stu-id="0cc62-141">Choose the name of the Application Insights resource in the upper left corner of the CodeLens details view to change which resource is the source for CodeLens data.</span></span>

## <a name="next"></a><span data-ttu-id="0cc62-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="0cc62-142">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="0cc62-143">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="0cc62-143">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="0cc62-144">Search telemetry, see data in CodeLens, and configure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0cc62-144">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="0cc62-145">All within Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0cc62-145">All within Visual Studio.</span></span> |![Right-click the project and choose Application Insights, Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-codelens/34.png) |
| <span data-ttu-id="0cc62-147">**[Add more data](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="0cc62-147">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="0cc62-148">Monitor usage, availability, dependencies, exceptions.</span><span class="sxs-lookup"><span data-stu-id="0cc62-148">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="0cc62-149">Integrate traces from logging frameworks.</span><span class="sxs-lookup"><span data-stu-id="0cc62-149">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="0cc62-150">Write custom telemetry.</span><span class="sxs-lookup"><span data-stu-id="0cc62-150">Write custom telemetry.</span></span> |![Visual studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-codelens/64.png) |
| <span data-ttu-id="0cc62-152">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="0cc62-152">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="0cc62-153">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span><span class="sxs-lookup"><span data-stu-id="0cc62-153">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-visual-studio-codelens/62.png) |







