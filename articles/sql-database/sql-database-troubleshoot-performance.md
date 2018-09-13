---
title: SQL Database performance tuning tips | Microsoft Docs
description: Tips for performance tuning in Azure SQL Database through evaluation and improvement.
services: sql-database
documentationcenter: ''
author: v-shysun
manager: felixwu
editor: ''
keywords: sql performance tuning, database performance tuning, sql performance tuning tips, sql database performance tuning
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: v-shysun
ms.openlocfilehash: faf2d9632462c434c38dc9c2d65f7c9e58f801d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551266"
---
# <a name="sql-database-performance-tuning-tips"></a><span data-ttu-id="975ee-104">SQL Database performance tuning tips</span><span class="sxs-lookup"><span data-stu-id="975ee-104">SQL Database performance tuning tips</span></span>
<span data-ttu-id="975ee-105">You can change the [service tier](sql-database-service-tiers.md) of a standalone database or increase the eDTUs of an elastic pool at any time to improve performance, but you may want to identify opportunities to improve and optimize query performance first.</span><span class="sxs-lookup"><span data-stu-id="975ee-105">You can change the [service tier](sql-database-service-tiers.md) of a standalone database or increase the eDTUs of an elastic pool at any time to improve performance, but you may want to identify opportunities to improve and optimize query performance first.</span></span> <span data-ttu-id="975ee-106">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span><span class="sxs-lookup"><span data-stu-id="975ee-106">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="975ee-107">This article provides guidance for performance tuning in SQL Database.</span><span class="sxs-lookup"><span data-stu-id="975ee-107">This article provides guidance for performance tuning in SQL Database.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="steps-to-evaluate-and-tune-database-performance"></a><span data-ttu-id="975ee-108">Steps to evaluate and tune database performance</span><span class="sxs-lookup"><span data-stu-id="975ee-108">Steps to evaluate and tune database performance</span></span>
1. <span data-ttu-id="975ee-109">In the [Azure Portal](https://portal.azure.com), click **SQL databases**, select the database, and then use the Monitoring chart to look for resources approaching their maximum.</span><span class="sxs-lookup"><span data-stu-id="975ee-109">In the [Azure Portal](https://portal.azure.com), click **SQL databases**, select the database, and then use the Monitoring chart to look for resources approaching their maximum.</span></span> <span data-ttu-id="975ee-110">DTU consumption is shown by default.</span><span class="sxs-lookup"><span data-stu-id="975ee-110">DTU consumption is shown by default.</span></span> <span data-ttu-id="975ee-111">Click **Edit** to change the time range and values shown.</span><span class="sxs-lookup"><span data-stu-id="975ee-111">Click **Edit** to change the time range and values shown.</span></span>
2. <span data-ttu-id="975ee-112">Use [Query Performance Insight](sql-database-query-performance.md) to evaluate the queries using DTUs, and then use [SQL Database Advisor](sql-database-advisor.md) to view recommendations for creating and dropping indexes, parameterizing queries, and fixing schema issues.</span><span class="sxs-lookup"><span data-stu-id="975ee-112">Use [Query Performance Insight](sql-database-query-performance.md) to evaluate the queries using DTUs, and then use [SQL Database Advisor](sql-database-advisor.md) to view recommendations for creating and dropping indexes, parameterizing queries, and fixing schema issues.</span></span>
3. <span data-ttu-id="975ee-113">You can use dynamic management views (DMVs), Extended Events (Xevents), and the Query Store in SSMS to get performance parameters in real time.</span><span class="sxs-lookup"><span data-stu-id="975ee-113">You can use dynamic management views (DMVs), Extended Events (Xevents), and the Query Store in SSMS to get performance parameters in real time.</span></span> <span data-ttu-id="975ee-114">See the [performance guidance topic](sql-database-performance-guidance.md) for detailed monitoring and tuning tips.</span><span class="sxs-lookup"><span data-stu-id="975ee-114">See the [performance guidance topic](sql-database-performance-guidance.md) for detailed monitoring and tuning tips.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="975ee-115">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="975ee-115">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="975ee-116">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="975ee-116">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
>

## <a name="steps-to-improve-database-performance-with-more-resources"></a><span data-ttu-id="975ee-117">Steps to improve database performance with more resources</span><span class="sxs-lookup"><span data-stu-id="975ee-117">Steps to improve database performance with more resources</span></span>
1. <span data-ttu-id="975ee-118">For standalone databases, you can [change service tiers](sql-database-service-tiers.md) on-demand to improve database performance.</span><span class="sxs-lookup"><span data-stu-id="975ee-118">For standalone databases, you can [change service tiers](sql-database-service-tiers.md) on-demand to improve database performance.</span></span>
2. <span data-ttu-id="975ee-119">For multiple databases, consider using [elastic pools](sql-database-elastic-pool.md) to scale resources automatically.</span><span class="sxs-lookup"><span data-stu-id="975ee-119">For multiple databases, consider using [elastic pools](sql-database-elastic-pool.md) to scale resources automatically.</span></span>

