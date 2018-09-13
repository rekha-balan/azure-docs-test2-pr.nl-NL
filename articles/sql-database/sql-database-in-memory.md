---
title: Azure SQL Database In-Memory technologies | Microsoft Docs
description: Azure SQL Database In-Memory technologies greatly improve the performance of transactional and analytics workloads. Learn how to take advantage of these technologies.
services: sql-database
documentationCenter: ''
author: jodebrui
manager: jhubbard
editor: ''
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: development
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: jodebrui
ms.openlocfilehash: f827b76b8164e4eae286c9a1247e64d4f5ee9ea8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564689"
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="6ac92-104">Optimize performance by using In-Memory technologies in SQL Database</span><span class="sxs-lookup"><span data-stu-id="6ac92-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="6ac92-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="6ac92-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="6ac92-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span><span class="sxs-lookup"><span data-stu-id="6ac92-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="6ac92-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span><span class="sxs-lookup"><span data-stu-id="6ac92-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="6ac92-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span><span class="sxs-lookup"><span data-stu-id="6ac92-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="6ac92-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span><span class="sxs-lookup"><span data-stu-id="6ac92-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="6ac92-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs (i.e., resource consumption) by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="6ac92-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs (i.e., resource consumption) by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
- <span data-ttu-id="6ac92-111">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="6ac92-111">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>

<span data-ttu-id="6ac92-112">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span><span class="sxs-lookup"><span data-stu-id="6ac92-112">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="6ac92-113">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6ac92-113">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="6ac92-114">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span><span class="sxs-lookup"><span data-stu-id="6ac92-114">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="6ac92-115">Azure SQL Database has the following In-Memory technologies:</span><span class="sxs-lookup"><span data-stu-id="6ac92-115">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="6ac92-116">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span><span class="sxs-lookup"><span data-stu-id="6ac92-116">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="6ac92-117">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span><span class="sxs-lookup"><span data-stu-id="6ac92-117">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="6ac92-118">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span><span class="sxs-lookup"><span data-stu-id="6ac92-118">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="6ac92-119">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span><span class="sxs-lookup"><span data-stu-id="6ac92-119">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="6ac92-120">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span><span class="sxs-lookup"><span data-stu-id="6ac92-120">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="6ac92-121">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span><span class="sxs-lookup"><span data-stu-id="6ac92-121">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="6ac92-122">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span><span class="sxs-lookup"><span data-stu-id="6ac92-122">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="6ac92-123">You can also combine In-Memory OLTP and columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="6ac92-123">You can also combine In-Memory OLTP and columnstore indexes.</span></span> <span data-ttu-id="6ac92-124">You can have a memory-optimized table with a columnstore index.</span><span class="sxs-lookup"><span data-stu-id="6ac92-124">You can have a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="6ac92-125">This allows you to both perform very fast transaction processing and run analytics queries very quickly on the same data.</span><span class="sxs-lookup"><span data-stu-id="6ac92-125">This allows you to both perform very fast transaction processing and run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="6ac92-126">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span><span class="sxs-lookup"><span data-stu-id="6ac92-126">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="6ac92-127">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span><span class="sxs-lookup"><span data-stu-id="6ac92-127">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="6ac92-128">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ac92-128">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="6ac92-129">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples.</span><span class="sxs-lookup"><span data-stu-id="6ac92-129">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples.</span></span> <span data-ttu-id="6ac92-130">First, you'll see the impact of these technologies on storage and data size limits.</span><span class="sxs-lookup"><span data-stu-id="6ac92-130">First, you'll see the impact of these technologies on storage and data size limits.</span></span> <span data-ttu-id="6ac92-131">Then, you'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="6ac92-131">Then, you'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span> <span data-ttu-id="6ac92-132">Finally, you'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6ac92-132">Finally, you'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="6ac92-133">See the following resources for more information.</span><span class="sxs-lookup"><span data-stu-id="6ac92-133">See the following resources for more information.</span></span>

<span data-ttu-id="6ac92-134">In-depth information about the technologies:</span><span class="sxs-lookup"><span data-stu-id="6ac92-134">In-depth information about the technologies:</span></span>

- <span data-ttu-id="6ac92-135">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span><span class="sxs-lookup"><span data-stu-id="6ac92-135">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="6ac92-136">Documentation for In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="6ac92-136">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="6ac92-137">Columnstore Indexes Guide</span><span class="sxs-lookup"><span data-stu-id="6ac92-137">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="6ac92-138">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="6ac92-138">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="6ac92-139">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span><span class="sxs-lookup"><span data-stu-id="6ac92-139">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="6ac92-140">In-depth videos about the technologies:</span><span class="sxs-lookup"><span data-stu-id="6ac92-140">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="6ac92-141">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span><span class="sxs-lookup"><span data-stu-id="6ac92-141">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- [<span data-ttu-id="6ac92-142">In-Memory OLTP Videos: What it is and When/How to use it</span><span class="sxs-lookup"><span data-stu-id="6ac92-142">In-Memory OLTP Videos: What it is and When/How to use it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="6ac92-143">Columnstore Index: In-Memory Analytics (i.e. columnstore index) Videos from Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="6ac92-143">Columnstore Index: In-Memory Analytics (i.e. columnstore index) Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="6ac92-144">Storage and data size</span><span class="sxs-lookup"><span data-stu-id="6ac92-144">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="6ac92-145">Data size and storage cap for In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="6ac92-145">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="6ac92-146">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span><span class="sxs-lookup"><span data-stu-id="6ac92-146">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="6ac92-147">These tables are required to fit in memory.</span><span class="sxs-lookup"><span data-stu-id="6ac92-147">These tables are required to fit in memory.</span></span> <span data-ttu-id="6ac92-148">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span><span class="sxs-lookup"><span data-stu-id="6ac92-148">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="6ac92-149">This idea is referred to as *In-Memory OLTP storage*.</span><span class="sxs-lookup"><span data-stu-id="6ac92-149">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="6ac92-150">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span><span class="sxs-lookup"><span data-stu-id="6ac92-150">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="6ac92-151">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span><span class="sxs-lookup"><span data-stu-id="6ac92-151">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="6ac92-152">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span><span class="sxs-lookup"><span data-stu-id="6ac92-152">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="6ac92-153">The following counts toward your In-Memory OLTP storage cap:</span><span class="sxs-lookup"><span data-stu-id="6ac92-153">The following counts toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="6ac92-154">Active user data rows in memory-optimized tables and table variables.</span><span class="sxs-lookup"><span data-stu-id="6ac92-154">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="6ac92-155">Note that old row versions don't count toward the cap.</span><span class="sxs-lookup"><span data-stu-id="6ac92-155">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="6ac92-156">Indexes on memory-optimized tables.</span><span class="sxs-lookup"><span data-stu-id="6ac92-156">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="6ac92-157">Operational overhead of ALTER TABLE operations.</span><span class="sxs-lookup"><span data-stu-id="6ac92-157">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="6ac92-158">If you hit the cap, you'll receive an out-of-quota error and will no longer be able to insert or update data.</span><span class="sxs-lookup"><span data-stu-id="6ac92-158">If you hit the cap, you'll receive an out-of-quota error and will no longer be able to insert or update data.</span></span> <span data-ttu-id="6ac92-159">To mitigate this, delete data or increase the pricing tier of the database or pool.</span><span class="sxs-lookup"><span data-stu-id="6ac92-159">To mitigate this, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="6ac92-160">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="6ac92-160">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="6ac92-161">About elastic pools</span><span class="sxs-lookup"><span data-stu-id="6ac92-161">About elastic pools</span></span>

<span data-ttu-id="6ac92-162">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span><span class="sxs-lookup"><span data-stu-id="6ac92-162">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="6ac92-163">Therefore, the usage in one database can potentially affect other databases.</span><span class="sxs-lookup"><span data-stu-id="6ac92-163">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="6ac92-164">Two mitigations for this are:</span><span class="sxs-lookup"><span data-stu-id="6ac92-164">Two mitigations for this are:</span></span>

- <span data-ttu-id="6ac92-165">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span><span class="sxs-lookup"><span data-stu-id="6ac92-165">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="6ac92-166">This caps the In-Memory OLTP storage utilization in any database in the pool to the size that corresponds to the eDTU count.</span><span class="sxs-lookup"><span data-stu-id="6ac92-166">This caps the In-Memory OLTP storage utilization in any database in the pool to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="6ac92-167">Configure a Min-eDTU that is greater than 0.</span><span class="sxs-lookup"><span data-stu-id="6ac92-167">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="6ac92-168">This guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span><span class="sxs-lookup"><span data-stu-id="6ac92-168">This guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="6ac92-169">Data size and storage for columnstore indexes</span><span class="sxs-lookup"><span data-stu-id="6ac92-169">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="6ac92-170">Columnstore indexes aren't required to fit in memory.</span><span class="sxs-lookup"><span data-stu-id="6ac92-170">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="6ac92-171">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span><span class="sxs-lookup"><span data-stu-id="6ac92-171">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="6ac92-172">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span><span class="sxs-lookup"><span data-stu-id="6ac92-172">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="6ac92-173">This can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span><span class="sxs-lookup"><span data-stu-id="6ac92-173">This can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="6ac92-174">And this can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="6ac92-174">And this can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="6ac92-175">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span><span class="sxs-lookup"><span data-stu-id="6ac92-175">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="6ac92-176">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span><span class="sxs-lookup"><span data-stu-id="6ac92-176">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="6ac92-177">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span><span class="sxs-lookup"><span data-stu-id="6ac92-177">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="6ac92-178">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="6ac92-178">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="6ac92-179">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span><span class="sxs-lookup"><span data-stu-id="6ac92-179">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="6ac92-180">Moving databases that use In-Memory technologies between pricing tiers</span><span class="sxs-lookup"><span data-stu-id="6ac92-180">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="6ac92-181">You don't need to have special considerations for increasing the pricing tier for a database that uses In-Memory technologies because higher pricing tiers always have more functionality and more resources.</span><span class="sxs-lookup"><span data-stu-id="6ac92-181">You don't need to have special considerations for increasing the pricing tier for a database that uses In-Memory technologies because higher pricing tiers always have more functionality and more resources.</span></span> <span data-ttu-id="6ac92-182">Decreasing the pricing tier can have implications for your database.</span><span class="sxs-lookup"><span data-stu-id="6ac92-182">Decreasing the pricing tier can have implications for your database.</span></span> <span data-ttu-id="6ac92-183">This is especially true when you're moving from Premium to Standard or Basic, and when you're moving a database that uses In-Memory OLTP to a lower Premium tier.</span><span class="sxs-lookup"><span data-stu-id="6ac92-183">This is especially true when you're moving from Premium to Standard or Basic, and when you're moving a database that uses In-Memory OLTP to a lower Premium tier.</span></span> <span data-ttu-id="6ac92-184">The same considerations apply when you're lowering the pricing tier of an elastic pool or moving databases with In-Memory technologies into a Standard or Basic elastic pool.</span><span class="sxs-lookup"><span data-stu-id="6ac92-184">The same considerations apply when you're lowering the pricing tier of an elastic pool or moving databases with In-Memory technologies into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="6ac92-185">In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="6ac92-185">In-Memory OLTP</span></span>

<span data-ttu-id="6ac92-186">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span><span class="sxs-lookup"><span data-stu-id="6ac92-186">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="6ac92-187">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span><span class="sxs-lookup"><span data-stu-id="6ac92-187">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="6ac92-188">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span><span class="sxs-lookup"><span data-stu-id="6ac92-188">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="6ac92-189">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span><span class="sxs-lookup"><span data-stu-id="6ac92-189">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="6ac92-190">You can execute the following Transact-SQL query:</span><span class="sxs-lookup"><span data-stu-id="6ac92-190">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="6ac92-191">If the query returns **1**, In-Memory OLTP is supported in this database.</span><span class="sxs-lookup"><span data-stu-id="6ac92-191">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="6ac92-192">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span><span class="sxs-lookup"><span data-stu-id="6ac92-192">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="6ac92-193">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation will fail.</span><span class="sxs-lookup"><span data-stu-id="6ac92-193">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation will fail.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="6ac92-194">Columnstore indexes</span><span class="sxs-lookup"><span data-stu-id="6ac92-194">Columnstore indexes</span></span>

<span data-ttu-id="6ac92-195">*Downgrading to Basic/Standard*: Columnstore indexes aren't supported in databases in the Standard or Basic tier.</span><span class="sxs-lookup"><span data-stu-id="6ac92-195">*Downgrading to Basic/Standard*: Columnstore indexes aren't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="6ac92-196">When you downgrade a database to Standard/Basic, columnstore indexes will become unavailable.</span><span class="sxs-lookup"><span data-stu-id="6ac92-196">When you downgrade a database to Standard/Basic, columnstore indexes will become unavailable.</span></span> <span data-ttu-id="6ac92-197">If you use a clustered columnstore index, this means that the table as a whole becomes unavailable.</span><span class="sxs-lookup"><span data-stu-id="6ac92-197">If you use a clustered columnstore index, this means that the table as a whole becomes unavailable.</span></span>

<span data-ttu-id="6ac92-198">Before you downgrade the database to Standard/Basic, drop all clustered columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="6ac92-198">Before you downgrade the database to Standard/Basic, drop all clustered columnstore indexes.</span></span>

<span data-ttu-id="6ac92-199">*Downgrading to a lower Premium tier*: This will succeed as long as the database as a whole fits within the maximum database size for the target pricing tier or available storage in the elastic pool.</span><span class="sxs-lookup"><span data-stu-id="6ac92-199">*Downgrading to a lower Premium tier*: This will succeed as long as the database as a whole fits within the maximum database size for the target pricing tier or available storage in the elastic pool.</span></span> <span data-ttu-id="6ac92-200">There is no specific impact from the columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="6ac92-200">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="6ac92-201">1. Install the In-Memory OLTP sample</span><span class="sxs-lookup"><span data-stu-id="6ac92-201">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="6ac92-202">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6ac92-202">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="6ac92-203">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span><span class="sxs-lookup"><span data-stu-id="6ac92-203">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="6ac92-204">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span><span class="sxs-lookup"><span data-stu-id="6ac92-204">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="6ac92-205">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="6ac92-205">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="6ac92-206">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="6ac92-206">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="6ac92-207">Installation steps</span><span class="sxs-lookup"><span data-stu-id="6ac92-207">Installation steps</span></span>

1. <span data-ttu-id="6ac92-208">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span><span class="sxs-lookup"><span data-stu-id="6ac92-208">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="6ac92-209">Set the **Source** to the AdventureWorksLT sample database.</span><span class="sxs-lookup"><span data-stu-id="6ac92-209">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="6ac92-210">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6ac92-210">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="6ac92-211">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ac92-211">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="6ac92-212">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="6ac92-212">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="6ac92-213">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span><span class="sxs-lookup"><span data-stu-id="6ac92-213">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="6ac92-214">Paste the T-SQL script into SSMS, and then execute the script.</span><span class="sxs-lookup"><span data-stu-id="6ac92-214">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="6ac92-215">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span><span class="sxs-lookup"><span data-stu-id="6ac92-215">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="6ac92-216">For example:</span><span class="sxs-lookup"><span data-stu-id="6ac92-216">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="6ac92-217">Error 40536</span><span class="sxs-lookup"><span data-stu-id="6ac92-217">Error 40536</span></span>


<span data-ttu-id="6ac92-218">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span><span class="sxs-lookup"><span data-stu-id="6ac92-218">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="6ac92-219">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span><span class="sxs-lookup"><span data-stu-id="6ac92-219">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="6ac92-220">To diagnose the problem, ensure that the database is at the Premium service tier.</span><span class="sxs-lookup"><span data-stu-id="6ac92-220">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="6ac92-221">About the created memory-optimized items</span><span class="sxs-lookup"><span data-stu-id="6ac92-221">About the created memory-optimized items</span></span>

<span data-ttu-id="6ac92-222">**Tables**: The sample contains the following memory-optimized tables:</span><span class="sxs-lookup"><span data-stu-id="6ac92-222">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="6ac92-223">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="6ac92-223">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="6ac92-224">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="6ac92-224">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="6ac92-225">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="6ac92-225">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="6ac92-226">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="6ac92-226">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="6ac92-227">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="6ac92-227">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="6ac92-228">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="6ac92-228">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="6ac92-229">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span><span class="sxs-lookup"><span data-stu-id="6ac92-229">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="6ac92-230">The value equals 1.</span><span class="sxs-lookup"><span data-stu-id="6ac92-230">The value equals 1.</span></span>


<span data-ttu-id="6ac92-231">Or you can query the catalog views, such as:</span><span class="sxs-lookup"><span data-stu-id="6ac92-231">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="6ac92-232">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span><span class="sxs-lookup"><span data-stu-id="6ac92-232">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="6ac92-233">Run the sample OLTP workload</span><span class="sxs-lookup"><span data-stu-id="6ac92-233">Run the sample OLTP workload</span></span>

<span data-ttu-id="6ac92-234">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span><span class="sxs-lookup"><span data-stu-id="6ac92-234">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="6ac92-235">SalesLT **.** usp_InsertSalesOrder **_inmem**</span><span class="sxs-lookup"><span data-stu-id="6ac92-235">SalesLT **.** usp_InsertSalesOrder **_inmem**</span></span>
- <span data-ttu-id="6ac92-236">SalesLT **.** usp_InsertSalesOrder **_ondisk**</span><span class="sxs-lookup"><span data-stu-id="6ac92-236">SalesLT **.** usp_InsertSalesOrder **_ondisk**</span></span>


<span data-ttu-id="6ac92-237">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span><span class="sxs-lookup"><span data-stu-id="6ac92-237">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="6ac92-238">You can compare how long it takes for the two stress runs to finish.</span><span class="sxs-lookup"><span data-stu-id="6ac92-238">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="6ac92-239">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span><span class="sxs-lookup"><span data-stu-id="6ac92-239">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="6ac92-240">Run a large number of concurrent connections, by using -n100.</span><span class="sxs-lookup"><span data-stu-id="6ac92-240">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="6ac92-241">Have each connection loop hundreds of times, by using -r500.</span><span class="sxs-lookup"><span data-stu-id="6ac92-241">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="6ac92-242">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span><span class="sxs-lookup"><span data-stu-id="6ac92-242">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="6ac92-243">Script for ostress.exe</span><span class="sxs-lookup"><span data-stu-id="6ac92-243">Script for ostress.exe</span></span>


<span data-ttu-id="6ac92-244">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span><span class="sxs-lookup"><span data-stu-id="6ac92-244">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="6ac92-245">The script uses items that were created by the T-SQL script that you installed earlier.</span><span class="sxs-lookup"><span data-stu-id="6ac92-245">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="6ac92-246">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span><span class="sxs-lookup"><span data-stu-id="6ac92-246">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="6ac92-247">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="6ac92-247">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="6ac92-248">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="6ac92-248">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="6ac92-249">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would simply replace both occurrences of the *_inmem* substring with *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="6ac92-249">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would simply replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="6ac92-250">These replacements affect the names of tables and stored procedures.</span><span class="sxs-lookup"><span data-stu-id="6ac92-250">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="6ac92-251">Install RML utilities and ostress</span><span class="sxs-lookup"><span data-stu-id="6ac92-251">Install RML utilities and ostress</span></span>


<span data-ttu-id="6ac92-252">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="6ac92-252">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="6ac92-253">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span><span class="sxs-lookup"><span data-stu-id="6ac92-253">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="6ac92-254">But you can run ostress.exe on your laptop instead.</span><span class="sxs-lookup"><span data-stu-id="6ac92-254">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="6ac92-255">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span><span class="sxs-lookup"><span data-stu-id="6ac92-255">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="6ac92-256">The utilities include ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="6ac92-256">The utilities include ostress.exe.</span></span>

<span data-ttu-id="6ac92-257">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="6ac92-257">For more information, see:</span></span>
- <span data-ttu-id="6ac92-258">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ac92-258">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="6ac92-259">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ac92-259">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="6ac92-260">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ac92-260">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="6ac92-261">Run the *_inmem* stress workload first</span><span class="sxs-lookup"><span data-stu-id="6ac92-261">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="6ac92-262">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span><span class="sxs-lookup"><span data-stu-id="6ac92-262">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="6ac92-263">The command-line parameters direct ostress to:</span><span class="sxs-lookup"><span data-stu-id="6ac92-263">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="6ac92-264">Run 100 connections concurrently (-n100).</span><span class="sxs-lookup"><span data-stu-id="6ac92-264">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="6ac92-265">Have each connection run the T-SQL script 50 times (-r50).</span><span class="sxs-lookup"><span data-stu-id="6ac92-265">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="6ac92-266">To run the preceding ostress.exe command line:</span><span class="sxs-lookup"><span data-stu-id="6ac92-266">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="6ac92-267">Reset the database data content by running the following command in SSMS to delete all the data that was inserted by any previous runs:</span><span class="sxs-lookup"><span data-stu-id="6ac92-267">Reset the database data content by running the following command in SSMS to delete all the data that was inserted by any previous runs:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="6ac92-268">Copy the text of the preceding ostress.exe command line to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="6ac92-268">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="6ac92-269">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span><span class="sxs-lookup"><span data-stu-id="6ac92-269">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="6ac92-270">Run your edited command line in an RML Cmd window.</span><span class="sxs-lookup"><span data-stu-id="6ac92-270">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="6ac92-271">Result is a duration</span><span class="sxs-lookup"><span data-stu-id="6ac92-271">Result is a duration</span></span>


<span data-ttu-id="6ac92-272">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span><span class="sxs-lookup"><span data-stu-id="6ac92-272">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="6ac92-273">For example, a shorter test run lasted about 1.5 minutes:</span><span class="sxs-lookup"><span data-stu-id="6ac92-273">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="6ac92-274">Reset, edit for *_ondisk*, then rerun</span><span class="sxs-lookup"><span data-stu-id="6ac92-274">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="6ac92-275">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span><span class="sxs-lookup"><span data-stu-id="6ac92-275">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="6ac92-276">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span><span class="sxs-lookup"><span data-stu-id="6ac92-276">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="6ac92-277">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="6ac92-277">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="6ac92-278">Rerun ostress.exe for the second time, and capture the duration result.</span><span class="sxs-lookup"><span data-stu-id="6ac92-278">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="6ac92-279">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span><span class="sxs-lookup"><span data-stu-id="6ac92-279">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="6ac92-280">Expected comparison results</span><span class="sxs-lookup"><span data-stu-id="6ac92-280">Expected comparison results</span></span>

<span data-ttu-id="6ac92-281">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span><span class="sxs-lookup"><span data-stu-id="6ac92-281">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="6ac92-282">2. Install the In-Memory Analytics sample</span><span class="sxs-lookup"><span data-stu-id="6ac92-282">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="6ac92-283">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span><span class="sxs-lookup"><span data-stu-id="6ac92-283">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="6ac92-284">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span><span class="sxs-lookup"><span data-stu-id="6ac92-284">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="6ac92-285">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ac92-285">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="6ac92-286">Prepare the columnstore analytics test</span><span class="sxs-lookup"><span data-stu-id="6ac92-286">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="6ac92-287">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span><span class="sxs-lookup"><span data-stu-id="6ac92-287">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="6ac92-288">Use that exact name.</span><span class="sxs-lookup"><span data-stu-id="6ac92-288">Use that exact name.</span></span>
 - <span data-ttu-id="6ac92-289">Choose any Premium service tier.</span><span class="sxs-lookup"><span data-stu-id="6ac92-289">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="6ac92-290">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="6ac92-290">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="6ac92-291">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span><span class="sxs-lookup"><span data-stu-id="6ac92-291">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="6ac92-292">The script creates the Dimension table and two fact tables.</span><span class="sxs-lookup"><span data-stu-id="6ac92-292">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="6ac92-293">The fact tables are populated with 3.5 million rows each.</span><span class="sxs-lookup"><span data-stu-id="6ac92-293">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="6ac92-294">The script might take 15 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="6ac92-294">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="6ac92-295">Paste the T-SQL script into SSMS, and then execute the script.</span><span class="sxs-lookup"><span data-stu-id="6ac92-295">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="6ac92-296">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span><span class="sxs-lookup"><span data-stu-id="6ac92-296">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="6ac92-297">Set AdventureWorksLT to compatibility level 130:</span><span class="sxs-lookup"><span data-stu-id="6ac92-297">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="6ac92-298">Level 130 is not directly related to In-Memory features.</span><span class="sxs-lookup"><span data-stu-id="6ac92-298">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="6ac92-299">But level 130 generally provides faster query performance than 120.</span><span class="sxs-lookup"><span data-stu-id="6ac92-299">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="6ac92-300">Key tables and columnstore indexes</span><span class="sxs-lookup"><span data-stu-id="6ac92-300">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="6ac92-301">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span><span class="sxs-lookup"><span data-stu-id="6ac92-301">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="6ac92-302">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span><span class="sxs-lookup"><span data-stu-id="6ac92-302">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="6ac92-303">Key queries to compare the columnstore index</span><span class="sxs-lookup"><span data-stu-id="6ac92-303">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="6ac92-304">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span><span class="sxs-lookup"><span data-stu-id="6ac92-304">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="6ac92-305">In step 2 in the T-SQL script, pay attention to this pair of queries.</span><span class="sxs-lookup"><span data-stu-id="6ac92-305">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="6ac92-306">They differ only on one line:</span><span class="sxs-lookup"><span data-stu-id="6ac92-306">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="6ac92-307">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span><span class="sxs-lookup"><span data-stu-id="6ac92-307">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="6ac92-308">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span><span class="sxs-lookup"><span data-stu-id="6ac92-308">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="6ac92-309">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span><span class="sxs-lookup"><span data-stu-id="6ac92-309">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="6ac92-310">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span><span class="sxs-lookup"><span data-stu-id="6ac92-310">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6ac92-311">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ac92-311">Next steps</span></span>

- [<span data-ttu-id="6ac92-312">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span><span class="sxs-lookup"><span data-stu-id="6ac92-312">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="6ac92-313">Use In-Memory OLTP in an existing Azure SQL application</span><span class="sxs-lookup"><span data-stu-id="6ac92-313">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="6ac92-314">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="6ac92-314">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6ac92-315">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6ac92-315">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="6ac92-316">Deeper information</span><span class="sxs-lookup"><span data-stu-id="6ac92-316">Deeper information</span></span>

- [<span data-ttu-id="6ac92-317">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span><span class="sxs-lookup"><span data-stu-id="6ac92-317">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="6ac92-318">Learn about In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="6ac92-318">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="6ac92-319">Learn about columnstore indexes</span><span class="sxs-lookup"><span data-stu-id="6ac92-319">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="6ac92-320">Learn about real-time operational analytics</span><span class="sxs-lookup"><span data-stu-id="6ac92-320">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="6ac92-321">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span><span class="sxs-lookup"><span data-stu-id="6ac92-321">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="6ac92-322">Application design</span><span class="sxs-lookup"><span data-stu-id="6ac92-322">Application design</span></span>

- [<span data-ttu-id="6ac92-323">In-Memory OLTP (In-Memory Optimization)</span><span class="sxs-lookup"><span data-stu-id="6ac92-323">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="6ac92-324">Use In-Memory OLTP in an existing Azure SQL application</span><span class="sxs-lookup"><span data-stu-id="6ac92-324">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="6ac92-325">Tools</span><span class="sxs-lookup"><span data-stu-id="6ac92-325">Tools</span></span>

- [<span data-ttu-id="6ac92-326">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6ac92-326">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="6ac92-327">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="6ac92-327">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="6ac92-328">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="6ac92-328">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
