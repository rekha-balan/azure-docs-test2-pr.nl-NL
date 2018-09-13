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
# <a name="advisor-performance-recommendations"></a>Advisor Performance recommendations

Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications. You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.

## <a name="reduce-dns-time-to-live-on-your-traffic-manager-profile-to-fail-over-to-healthy-endpoints-faster"></a>Reduce DNS time to live on your Traffic Manager profile to fail over to healthy endpoints faster

[Time to Live (TTL) settings](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-performance-considerations) on your Traffic Manager profile allow you to specify how quickly to switch endpoints if a given endpoint stops responding to queries. Reducing the TTL values means that clients will be routed to functioning endpoints faster.

Azure Advisor identifies Traffic Manager profiles with a longer TTL configured and recommends configuring the TTL to either 20 seconds or 60 seconds depending on whether the profile is configured for [Fast Failover](https://azure.microsoft.com/roadmap/fast-failover-and-tcp-probing-in-azure-traffic-manager/).

## <a name="improve-database-performance-with-sql-db-advisor"></a>Improve database performance with SQL DB Advisor

Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources. It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database. SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history. It then offers recommendations that are best suited for running the database’s typical workload. 

> [!NOTE]
> To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity. SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.

For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/documentation/articles/sql-database-advisor/).

## <a name="improve-redis-cache-performance-and-reliability"></a>Improve Redis Cache performance and reliability

Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections. Advisor also provides best practices recommendations to help you avoid potential issues. For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>Improve App Service performance and reliability

Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities. Examples of App Services recommendations are:
* Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.
* Detection of instances where collocating resources like web apps and databases can improve performance and lower cost. 

For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/documentation/articles/app-service-best-practices/).

## <a name="remove-data-skew-on-your-sql-data-warehouse-table-to-increase-query-performance"></a>Remove data skew on your SQL data warehouse table to increase query performance

Data skew can cause unnecessary data movement or resource bottlenecks when running your workload. Advisor will detect distribution data skew greater than 15% and recommend that you redistribute your data and revisit your table distribution key selections. To learn more about identifying and removing skew, see [troubleshooting skew](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-distribute#how-to-tell-if-your-distribution-column-is-a-good-choice).

## <a name="create-or-update-outdated-table-statistics-on-your-sql-data-warehouse-table-to-increase-query-performance"></a>Create or update outdated table statistics on your SQL data warehouse table to increase query performance

Advisor identifies tables that do not have up-to-date [table statistics](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-statistics) and recommends creating or updating table statistics. The SQL data warehouse query optimizer uses up-to-date statics to estimate the cardinality or number of rows in the query result which enables the query optimizer to create a high quality query plan for fastest performance.

## <a name="migrate-your-storage-account-to-azure-resource-manager-to-get-all-of-the-latest-azure-features"></a>Migrate your Storage Account to Azure Resource Manager to get all of the latest Azure features

Migrate your Storage Account deployment model to Azure Resource Manager (ARM) to take advantage of template deployments, additional security options, and the ability to upgrade to a GPv2 account for utilization of Azure Storage's latest features. Advisor will identify any stand-alone storage accounts that are using the Classic deployment model and recommends migrating to the ARM deployment model. 

## <a name="how-to-access-performance-recommendations-in-advisor"></a>How to access Performance recommendations in Advisor

1. Sign in to the [Azure portal](https://portal.azure.com), and then open [Advisor](https://aka.ms/azureadvisordashboard).

2.  On the Advisor dashboard, click the **Performance** tab.

## <a name="next-steps"></a>Next steps

To learn more about Advisor recommendations, see:

* [Introduction to Advisor](advisor-overview.md)
* [Get started with Advisor](advisor-get-started.md)
* [Advisor Cost recommendations](advisor-performance-recommendations.md)
* [Advisor High Availability recommendations](advisor-high-availability-recommendations.md)
* [Advisor Security recommendations](advisor-security-recommendations.md)

