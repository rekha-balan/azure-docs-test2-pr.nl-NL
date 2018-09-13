---
title: Azure Advisor Performance recommendations | Microsoft Docs
description: Use Advisor to optimize the performance of your Azure deployments.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 46fa51fd38f9152ffe386bf79f6066de402a787e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670351"
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="2695a-103">Advisor Performance recommendations</span><span class="sxs-lookup"><span data-stu-id="2695a-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="2695a-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span><span class="sxs-lookup"><span data-stu-id="2695a-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="2695a-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span><span class="sxs-lookup"><span data-stu-id="2695a-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Advisor Performance tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="2695a-107">Improve database performance with SQL DB Advisor</span><span class="sxs-lookup"><span data-stu-id="2695a-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="2695a-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="2695a-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="2695a-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span><span class="sxs-lookup"><span data-stu-id="2695a-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="2695a-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span><span class="sxs-lookup"><span data-stu-id="2695a-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="2695a-111">It then offers recommendations that are best suited for running the database’s typical workload.</span><span class="sxs-lookup"><span data-stu-id="2695a-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="2695a-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span><span class="sxs-lookup"><span data-stu-id="2695a-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="2695a-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span><span class="sxs-lookup"><span data-stu-id="2695a-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="2695a-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="2695a-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![SQL database recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="2695a-116">Improve Redis Cache performance and reliability</span><span class="sxs-lookup"><span data-stu-id="2695a-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="2695a-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span><span class="sxs-lookup"><span data-stu-id="2695a-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="2695a-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span><span class="sxs-lookup"><span data-stu-id="2695a-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="2695a-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="2695a-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="2695a-120">Improve App Service performance and reliability</span><span class="sxs-lookup"><span data-stu-id="2695a-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="2695a-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span><span class="sxs-lookup"><span data-stu-id="2695a-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="2695a-122">Examples of App Services recommendations are:</span><span class="sxs-lookup"><span data-stu-id="2695a-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="2695a-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span><span class="sxs-lookup"><span data-stu-id="2695a-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="2695a-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span><span class="sxs-lookup"><span data-stu-id="2695a-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="2695a-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="2695a-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="2695a-126">![App Services recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="2695a-126">![App Services recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="2695a-127">How to access Performance recommendations in Advisor</span><span class="sxs-lookup"><span data-stu-id="2695a-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="2695a-128">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2695a-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2695a-129">In the left pane, click **More services**.</span><span class="sxs-lookup"><span data-stu-id="2695a-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="2695a-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="2695a-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="2695a-131">The Advisor dashboard is displayed.</span><span class="sxs-lookup"><span data-stu-id="2695a-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="2695a-132">On the Advisor dashboard, click the **Performance** tab.</span><span class="sxs-lookup"><span data-stu-id="2695a-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="2695a-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span><span class="sxs-lookup"><span data-stu-id="2695a-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="2695a-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span><span class="sxs-lookup"><span data-stu-id="2695a-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="2695a-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span><span class="sxs-lookup"><span data-stu-id="2695a-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="2695a-136">This is a *one-time operation*.</span><span class="sxs-lookup"><span data-stu-id="2695a-136">This is a *one-time operation*.</span></span> <span data-ttu-id="2695a-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span><span class="sxs-lookup"><span data-stu-id="2695a-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2695a-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="2695a-138">Next steps</span></span>

<span data-ttu-id="2695a-139">To learn more about Advisor recommendations, see:</span><span class="sxs-lookup"><span data-stu-id="2695a-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="2695a-140">Introduction to Advisor</span><span class="sxs-lookup"><span data-stu-id="2695a-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="2695a-141">Get started with Advisor</span><span class="sxs-lookup"><span data-stu-id="2695a-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="2695a-142">Advisor Cost recommendations</span><span class="sxs-lookup"><span data-stu-id="2695a-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="2695a-143">Advisor High Availability recommendations</span><span class="sxs-lookup"><span data-stu-id="2695a-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="2695a-144">Advisor Security recommendations</span><span class="sxs-lookup"><span data-stu-id="2695a-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)




