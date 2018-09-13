---
title: Azure Advisor Performance recommendations | Microsoft Docs
description: Use Advisor to optimize the performance of your Azure deployments.
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: makohli
ms.openlocfilehash: 9516534216c4a2c0f61e33ea3cbf1bbcb2ab58c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808729"
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="0eec5-103">Advisor Performance recommendations</span><span class="sxs-lookup"><span data-stu-id="0eec5-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="0eec5-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span><span class="sxs-lookup"><span data-stu-id="0eec5-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="0eec5-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span><span class="sxs-lookup"><span data-stu-id="0eec5-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

## <a name="reduce-dns-time-to-live-on-your-traffic-manager-profile-to-fail-over-to-healthy-endpoints-faster"></a><span data-ttu-id="0eec5-106">Reduce DNS time to live on your Traffic Manager profile to fail over to healthy endpoints faster</span><span class="sxs-lookup"><span data-stu-id="0eec5-106">Reduce DNS time to live on your Traffic Manager profile to fail over to healthy endpoints faster</span></span>

<span data-ttu-id="0eec5-107">[Time to Live (TTL) settings](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-performance-considerations) on your Traffic Manager profile allow you to specify how quickly to switch endpoints if a given endpoint stops responding to queries.</span><span class="sxs-lookup"><span data-stu-id="0eec5-107">[Time to Live (TTL) settings](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-performance-considerations) on your Traffic Manager profile allow you to specify how quickly to switch endpoints if a given endpoint stops responding to queries.</span></span> <span data-ttu-id="0eec5-108">Reducing the TTL values means that clients will be routed to functioning endpoints faster.</span><span class="sxs-lookup"><span data-stu-id="0eec5-108">Reducing the TTL values means that clients will be routed to functioning endpoints faster.</span></span>

<span data-ttu-id="0eec5-109">Azure Advisor identifies Traffic Manager profiles with a longer TTL configured and recommends configuring the TTL to either 20 seconds or 60 seconds depending on whether the profile is configured for [Fast Failover](https://azure.microsoft.com/roadmap/fast-failover-and-tcp-probing-in-azure-traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="0eec5-109">Azure Advisor identifies Traffic Manager profiles with a longer TTL configured and recommends configuring the TTL to either 20 seconds or 60 seconds depending on whether the profile is configured for [Fast Failover](https://azure.microsoft.com/roadmap/fast-failover-and-tcp-probing-in-azure-traffic-manager/).</span></span>

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="0eec5-110">Improve database performance with SQL DB Advisor</span><span class="sxs-lookup"><span data-stu-id="0eec5-110">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="0eec5-111">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="0eec5-111">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="0eec5-112">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span><span class="sxs-lookup"><span data-stu-id="0eec5-112">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="0eec5-113">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span><span class="sxs-lookup"><span data-stu-id="0eec5-113">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="0eec5-114">It then offers recommendations that are best suited for running the database’s typical workload.</span><span class="sxs-lookup"><span data-stu-id="0eec5-114">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="0eec5-115">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span><span class="sxs-lookup"><span data-stu-id="0eec5-115">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="0eec5-116">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span><span class="sxs-lookup"><span data-stu-id="0eec5-116">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="0eec5-117">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="0eec5-117">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/documentation/articles/sql-database-advisor/).</span></span>

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="0eec5-118">Improve Redis Cache performance and reliability</span><span class="sxs-lookup"><span data-stu-id="0eec5-118">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="0eec5-119">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span><span class="sxs-lookup"><span data-stu-id="0eec5-119">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="0eec5-120">Advisor also provides best practices recommendations to help you avoid potential issues.</span><span class="sxs-lookup"><span data-stu-id="0eec5-120">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="0eec5-121">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="0eec5-121">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="0eec5-122">Improve App Service performance and reliability</span><span class="sxs-lookup"><span data-stu-id="0eec5-122">Improve App Service performance and reliability</span></span>

<span data-ttu-id="0eec5-123">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span><span class="sxs-lookup"><span data-stu-id="0eec5-123">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="0eec5-124">Examples of App Services recommendations are:</span><span class="sxs-lookup"><span data-stu-id="0eec5-124">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="0eec5-125">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span><span class="sxs-lookup"><span data-stu-id="0eec5-125">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="0eec5-126">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span><span class="sxs-lookup"><span data-stu-id="0eec5-126">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="0eec5-127">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="0eec5-127">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/documentation/articles/app-service-best-practices/).</span></span>

## <a name="remove-data-skew-on-your-sql-data-warehouse-table-to-increase-query-performance"></a><span data-ttu-id="0eec5-128">Remove data skew on your SQL data warehouse table to increase query performance</span><span class="sxs-lookup"><span data-stu-id="0eec5-128">Remove data skew on your SQL data warehouse table to increase query performance</span></span>

<span data-ttu-id="0eec5-129">Data skew can cause unnecessary data movement or resource bottlenecks when running your workload.</span><span class="sxs-lookup"><span data-stu-id="0eec5-129">Data skew can cause unnecessary data movement or resource bottlenecks when running your workload.</span></span> <span data-ttu-id="0eec5-130">Advisor will detect distribution data skew greater than 15% and recommend that you redistribute your data and revisit your table distribution key selections.</span><span class="sxs-lookup"><span data-stu-id="0eec5-130">Advisor will detect distribution data skew greater than 15% and recommend that you redistribute your data and revisit your table distribution key selections.</span></span> <span data-ttu-id="0eec5-131">To learn more about identifying and removing skew, see [troubleshooting skew](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-distribute#how-to-tell-if-your-distribution-column-is-a-good-choice).</span><span class="sxs-lookup"><span data-stu-id="0eec5-131">To learn more about identifying and removing skew, see [troubleshooting skew](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-distribute#how-to-tell-if-your-distribution-column-is-a-good-choice).</span></span>

## <a name="create-or-update-outdated-table-statistics-on-your-sql-data-warehouse-table-to-increase-query-performance"></a><span data-ttu-id="0eec5-132">Create or update outdated table statistics on your SQL data warehouse table to increase query performance</span><span class="sxs-lookup"><span data-stu-id="0eec5-132">Create or update outdated table statistics on your SQL data warehouse table to increase query performance</span></span>

<span data-ttu-id="0eec5-133">Advisor identifies tables that do not have up-to-date [table statistics](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-statistics) and recommends creating or updating table statistics.</span><span class="sxs-lookup"><span data-stu-id="0eec5-133">Advisor identifies tables that do not have up-to-date [table statistics](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-statistics) and recommends creating or updating table statistics.</span></span> <span data-ttu-id="0eec5-134">The SQL data warehouse query optimizer uses up-to-date statics to estimate the cardinality or number of rows in the query result which enables the query optimizer to create a high quality query plan for fastest performance.</span><span class="sxs-lookup"><span data-stu-id="0eec5-134">The SQL data warehouse query optimizer uses up-to-date statics to estimate the cardinality or number of rows in the query result which enables the query optimizer to create a high quality query plan for fastest performance.</span></span>

## <a name="migrate-your-storage-account-to-azure-resource-manager-to-get-all-of-the-latest-azure-features"></a><span data-ttu-id="0eec5-135">Migrate your Storage Account to Azure Resource Manager to get all of the latest Azure features</span><span class="sxs-lookup"><span data-stu-id="0eec5-135">Migrate your Storage Account to Azure Resource Manager to get all of the latest Azure features</span></span>

<span data-ttu-id="0eec5-136">Migrate your Storage Account deployment model to Azure Resource Manager (ARM) to take advantage of template deployments, additional security options, and the ability to upgrade to a GPv2 account for utilization of Azure Storage's latest features.</span><span class="sxs-lookup"><span data-stu-id="0eec5-136">Migrate your Storage Account deployment model to Azure Resource Manager (ARM) to take advantage of template deployments, additional security options, and the ability to upgrade to a GPv2 account for utilization of Azure Storage's latest features.</span></span> <span data-ttu-id="0eec5-137">Advisor will identify any stand-alone storage accounts that are using the Classic deployment model and recommends migrating to the ARM deployment model.</span><span class="sxs-lookup"><span data-stu-id="0eec5-137">Advisor will identify any stand-alone storage accounts that are using the Classic deployment model and recommends migrating to the ARM deployment model.</span></span> 

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="0eec5-138">How to access Performance recommendations in Advisor</span><span class="sxs-lookup"><span data-stu-id="0eec5-138">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="0eec5-139">Sign in to the [Azure portal](https://portal.azure.com), and then open [Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="0eec5-139">Sign in to the [Azure portal](https://portal.azure.com), and then open [Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2.  <span data-ttu-id="0eec5-140">On the Advisor dashboard, click the **Performance** tab.</span><span class="sxs-lookup"><span data-stu-id="0eec5-140">On the Advisor dashboard, click the **Performance** tab.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0eec5-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="0eec5-141">Next steps</span></span>

<span data-ttu-id="0eec5-142">To learn more about Advisor recommendations, see:</span><span class="sxs-lookup"><span data-stu-id="0eec5-142">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="0eec5-143">Introduction to Advisor</span><span class="sxs-lookup"><span data-stu-id="0eec5-143">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="0eec5-144">Get started with Advisor</span><span class="sxs-lookup"><span data-stu-id="0eec5-144">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="0eec5-145">Advisor Cost recommendations</span><span class="sxs-lookup"><span data-stu-id="0eec5-145">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="0eec5-146">Advisor High Availability recommendations</span><span class="sxs-lookup"><span data-stu-id="0eec5-146">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="0eec5-147">Advisor Security recommendations</span><span class="sxs-lookup"><span data-stu-id="0eec5-147">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

