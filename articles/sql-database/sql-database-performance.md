---
title: Azure SQL Database Performance Insight | Microsoft Docs
description: The Azure SQL Database provides performance tools to help you identify areas that can improve current query performance.
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor and tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 51c1a7346c9e2f03beca2903199e49f280aa2c12
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563727"
---
# <a name="sql-database-performance-insight"></a><span data-ttu-id="ca034-103">SQL Database Performance Insight</span><span class="sxs-lookup"><span data-stu-id="ca034-103">SQL Database Performance Insight</span></span>
<span data-ttu-id="ca034-104">Azure SQL Database provides performance tools to help you identify and improve the performance of your databases by providing intelligent tuning actions and recommendations.</span><span class="sxs-lookup"><span data-stu-id="ca034-104">Azure SQL Database provides performance tools to help you identify and improve the performance of your databases by providing intelligent tuning actions and recommendations.</span></span> 

1. <span data-ttu-id="ca034-105">Browse to your database in the [Azure Portal](http://portal.azure.com) and click **All settings** > \*\*Performance \*\* > **Overview** to open the **Performance** page.</span><span class="sxs-lookup"><span data-stu-id="ca034-105">Browse to your database in the [Azure Portal](http://portal.azure.com) and click **All settings** > \*\*Performance \*\* > **Overview** to open the **Performance** page.</span></span> 
2. <span data-ttu-id="ca034-106">Click **Recommendations** to open the [SQL Database Advisor](#sql-database-advisor), and click **Queries** to open [Query Performance Insight](#query-performance-insight).</span><span class="sxs-lookup"><span data-stu-id="ca034-106">Click **Recommendations** to open the [SQL Database Advisor](#sql-database-advisor), and click **Queries** to open [Query Performance Insight](#query-performance-insight).</span></span>
   
    ![View Performance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-performance/entries.png)

## <a name="performance-overview"></a><span data-ttu-id="ca034-108">Performance Overview</span><span class="sxs-lookup"><span data-stu-id="ca034-108">Performance Overview</span></span>
<span data-ttu-id="ca034-109">Clicking on **Overview** or on the **Performance** tile will take you to the performance dashboard for your database.</span><span class="sxs-lookup"><span data-stu-id="ca034-109">Clicking on **Overview** or on the **Performance** tile will take you to the performance dashboard for your database.</span></span> <span data-ttu-id="ca034-110">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="ca034-110">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Performance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-performance/performance.png)

* <span data-ttu-id="ca034-112">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top 3 recommendations are shown if there are more).</span><span class="sxs-lookup"><span data-stu-id="ca034-112">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top 3 recommendations are shown if there are more).</span></span> <span data-ttu-id="ca034-113">Clicking this tile takes you to **SQL Database Advisor**.</span><span class="sxs-lookup"><span data-stu-id="ca034-113">Clicking this tile takes you to **SQL Database Advisor**.</span></span> 
* <span data-ttu-id="ca034-114">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span><span class="sxs-lookup"><span data-stu-id="ca034-114">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="ca034-115">Clicking this tile takes you to the full tuning history view for your database.</span><span class="sxs-lookup"><span data-stu-id="ca034-115">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="ca034-116">The **Auto-tuning** tile shows the auto-tuning configuration for your database (which tuning actions are configured to be automatically applied to your database).</span><span class="sxs-lookup"><span data-stu-id="ca034-116">The **Auto-tuning** tile shows the auto-tuning configuration for your database (which tuning actions are configured to be automatically applied to your database).</span></span> <span data-ttu-id="ca034-117">Clicking this tile opens the automation configuration dialog.</span><span class="sxs-lookup"><span data-stu-id="ca034-117">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="ca034-118">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span><span class="sxs-lookup"><span data-stu-id="ca034-118">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="ca034-119">Clicking this tile takes you to **Query Performance Insight**.</span><span class="sxs-lookup"><span data-stu-id="ca034-119">Clicking this tile takes you to **Query Performance Insight**.</span></span>

## <a name="sql-database-advisor"></a><span data-ttu-id="ca034-120">SQL Database Advisor</span><span class="sxs-lookup"><span data-stu-id="ca034-120">SQL Database Advisor</span></span>
<span data-ttu-id="ca034-121">[SQL Database Advisor](sql-database-advisor.md) provides intelligent tuning recommendations that can help improve your database's performance.</span><span class="sxs-lookup"><span data-stu-id="ca034-121">[SQL Database Advisor](sql-database-advisor.md) provides intelligent tuning recommendations that can help improve your database's performance.</span></span> 

* <span data-ttu-id="ca034-122">Recommendations on which indexes to create or drop (and an option to apply index recommendations automatically without any user interaction and automatically rolling back recommendations that have a negative impact on performance).</span><span class="sxs-lookup"><span data-stu-id="ca034-122">Recommendations on which indexes to create or drop (and an option to apply index recommendations automatically without any user interaction and automatically rolling back recommendations that have a negative impact on performance).</span></span>
* <span data-ttu-id="ca034-123">Recommendations when schema issues are identified in the database.</span><span class="sxs-lookup"><span data-stu-id="ca034-123">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="ca034-124">Recommendations when queries can benefit from parameterized queries.</span><span class="sxs-lookup"><span data-stu-id="ca034-124">Recommendations when queries can benefit from parameterized queries.</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="ca034-125">Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="ca034-125">Query Performance Insight</span></span>
<span data-ttu-id="ca034-126">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span><span class="sxs-lookup"><span data-stu-id="ca034-126">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="ca034-127">Deeper insight into your databases resource (DTU) consumption.</span><span class="sxs-lookup"><span data-stu-id="ca034-127">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="ca034-128">The top CPU consuming queries, which can potentially be tuned for improved performance.</span><span class="sxs-lookup"><span data-stu-id="ca034-128">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="ca034-129">The ability to drill down into the details of a query.</span><span class="sxs-lookup"><span data-stu-id="ca034-129">The ability to drill down into the details of a query.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ca034-130">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ca034-130">Additional resources</span></span>
* [<span data-ttu-id="ca034-131">Azure SQL Database performance guidance for single databases</span><span class="sxs-lookup"><span data-stu-id="ca034-131">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="ca034-132">When should an elastic pool be used?</span><span class="sxs-lookup"><span data-stu-id="ca034-132">When should an elastic pool be used?</span></span>](sql-database-elastic-pool.md)



