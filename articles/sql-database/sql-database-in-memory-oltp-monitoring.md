---
title: Monitor XTP in-memory storage | Microsoft Docs
description: Estimate and monitor XTP in-memory storage use, capacity; resolve capacity error 41823
services: sql-database
documentationcenter: ''
author: jodebrui
manager: jhubbard
editor: ''
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: f53fa3763edb1d9164278d1e3c418e200d7ada89
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555077"
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="8fd22-103">Monitor In-Memory OLTP Storage</span><span class="sxs-lookup"><span data-stu-id="8fd22-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="8fd22-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span><span class="sxs-lookup"><span data-stu-id="8fd22-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="8fd22-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="8fd22-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="8fd22-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span><span class="sxs-lookup"><span data-stu-id="8fd22-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="8fd22-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span><span class="sxs-lookup"><span data-stu-id="8fd22-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="8fd22-108">Determine whether data will fit within the in-memory storage cap</span><span class="sxs-lookup"><span data-stu-id="8fd22-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="8fd22-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span><span class="sxs-lookup"><span data-stu-id="8fd22-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="8fd22-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8fd22-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="8fd22-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fd22-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="8fd22-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span><span class="sxs-lookup"><span data-stu-id="8fd22-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="8fd22-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span><span class="sxs-lookup"><span data-stu-id="8fd22-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="8fd22-114">Monitoring and alerting</span><span class="sxs-lookup"><span data-stu-id="8fd22-114">Monitoring and alerting</span></span>
<span data-ttu-id="8fd22-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="8fd22-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="8fd22-116">On the Database blade, locate the Resource utilization box and click on Edit.</span><span class="sxs-lookup"><span data-stu-id="8fd22-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="8fd22-117">Then select the metric `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="8fd22-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="8fd22-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span><span class="sxs-lookup"><span data-stu-id="8fd22-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="8fd22-119">Or use the following query to show the in-memory storage utilization:</span><span class="sxs-lookup"><span data-stu-id="8fd22-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="8fd22-120">Correct out-of-memory situations - Error 41823</span><span class="sxs-lookup"><span data-stu-id="8fd22-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="8fd22-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span><span class="sxs-lookup"><span data-stu-id="8fd22-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="8fd22-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span><span class="sxs-lookup"><span data-stu-id="8fd22-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="8fd22-123">To resolve this error, either:</span><span class="sxs-lookup"><span data-stu-id="8fd22-123">To resolve this error, either:</span></span>

* <span data-ttu-id="8fd22-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span><span class="sxs-lookup"><span data-stu-id="8fd22-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="8fd22-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span><span class="sxs-lookup"><span data-stu-id="8fd22-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fd22-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fd22-126">Next steps</span></span>
<span data-ttu-id="8fd22-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="8fd22-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
