---
title: How To Use sys_schema for Performance Tuning and Database Maintenance in Azure Database for MySQL
description: This article describes how to use sys_schema to find performance issues and maintain database in Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 08/01/2018
ms.openlocfilehash: 1e10e3b1b5f4518732408f254eb5767acb8485c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866362"
---
# <a name="how-to-use-sysschema-for-performance-tuning-and-database-maintenance-in-azure-database-for-mysql"></a><span data-ttu-id="e4fd4-103">How to use sys_schema for performance tuning and database maintenance in Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="e4fd4-103">How to use sys_schema for performance tuning and database maintenance in Azure Database for MySQL</span></span>

<span data-ttu-id="e4fd4-104">The MySQL performance_schema, first available in MySQL 5.5, provides instrumentation for many vital server resources such as memory allocation, stored programs, metadata locking, etc. However, the performance_schema contains more than 80 tables, and getting the necessary information often requires joining tables within the performance_schema, as well as tables from the information_schema.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-104">The MySQL performance_schema, first available in MySQL 5.5, provides instrumentation for many vital server resources such as memory allocation, stored programs, metadata locking, etc. However, the performance_schema contains more than 80 tables, and getting the necessary information often requires joining tables within the performance_schema, as well as tables from the information_schema.</span></span> <span data-ttu-id="e4fd4-105">Building on both performance_schema and information_schema, the sys_schema provides a powerful collection of [user-friendly views](https://dev.mysql.com/doc/refman/5.7/en/sys-schema-views.html) in a read-only database and is fully enabled in Azure Database for MySQL version 5.7.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-105">Building on both performance_schema and information_schema, the sys_schema provides a powerful collection of [user-friendly views](https://dev.mysql.com/doc/refman/5.7/en/sys-schema-views.html) in a read-only database and is fully enabled in Azure Database for MySQL version 5.7.</span></span>

![views of sys_schema](./media/howto-troubleshoot-sys-schema/sys-schema-views.png)

<span data-ttu-id="e4fd4-107">There are 52 views in the sys_schema, and each view has one of the following prefixes:</span><span class="sxs-lookup"><span data-stu-id="e4fd4-107">There are 52 views in the sys_schema, and each view has one of the following prefixes:</span></span>

- <span data-ttu-id="e4fd4-108">Host_summary or IO: I/O related latencies.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-108">Host_summary or IO: I/O related latencies.</span></span>
- <span data-ttu-id="e4fd4-109">InnoDB: InnoDB buffer status and locks.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-109">InnoDB: InnoDB buffer status and locks.</span></span>
- <span data-ttu-id="e4fd4-110">Memory: Memory usage by the host and users.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-110">Memory: Memory usage by the host and users.</span></span>
- <span data-ttu-id="e4fd4-111">Schema: Schema-related information, such as auto increment, indexes, etc.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-111">Schema: Schema-related information, such as auto increment, indexes, etc.</span></span>
- <span data-ttu-id="e4fd4-112">Statement: Information on SQL statements; it can be statement that resulted in full table scan, or long query time.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-112">Statement: Information on SQL statements; it can be statement that resulted in full table scan, or long query time.</span></span>
- <span data-ttu-id="e4fd4-113">User: Resources consumed and grouped by users.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-113">User: Resources consumed and grouped by users.</span></span> <span data-ttu-id="e4fd4-114">Examples are file I/Os, connections, and memory.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-114">Examples are file I/Os, connections, and memory.</span></span>
- <span data-ttu-id="e4fd4-115">Wait: Wait events grouped by host or user.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-115">Wait: Wait events grouped by host or user.</span></span>

<span data-ttu-id="e4fd4-116">Now let’s look at some common usage patterns of the sys_schema.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-116">Now let’s look at some common usage patterns of the sys_schema.</span></span> <span data-ttu-id="e4fd4-117">To begin with, we’ll group the usage patterns into two categories: **Performance tuning** and **Database maintenance**.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-117">To begin with, we’ll group the usage patterns into two categories: **Performance tuning** and **Database maintenance**.</span></span>

## <a name="performance-tuning"></a><span data-ttu-id="e4fd4-118">Performance tuning</span><span class="sxs-lookup"><span data-stu-id="e4fd4-118">Performance tuning</span></span>

### <a name="sysusersummarybyfileio"></a><span data-ttu-id="e4fd4-119">*sys.user_summary_by_file_io*</span><span class="sxs-lookup"><span data-stu-id="e4fd4-119">*sys.user_summary_by_file_io*</span></span>

<span data-ttu-id="e4fd4-120">IO is the most expensive operation in the database.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-120">IO is the most expensive operation in the database.</span></span> <span data-ttu-id="e4fd4-121">We can find out the average IO latency by querying the *sys.user_summary_by_file_io* view.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-121">We can find out the average IO latency by querying the *sys.user_summary_by_file_io* view.</span></span> <span data-ttu-id="e4fd4-122">With the default 125 GB of provisioned storage, my IO latency is about 15 seconds.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-122">With the default 125 GB of provisioned storage, my IO latency is about 15 seconds.</span></span>

![io latency: 125 GB](./media/howto-troubleshoot-sys-schema/io-latency-125GB.png)

<span data-ttu-id="e4fd4-124">Because Azure Database for MySQL scales IO with respect to storage, after increasing my provisioned storage to 1 TB, my IO latency reduces to 571 ms.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-124">Because Azure Database for MySQL scales IO with respect to storage, after increasing my provisioned storage to 1 TB, my IO latency reduces to 571 ms.</span></span>

![io latency: 1TB](./media/howto-troubleshoot-sys-schema/io-latency-1TB.png)

### <a name="sysschematableswithfulltablescans"></a><span data-ttu-id="e4fd4-126">*sys.schema_tables_with_full_table_scans*</span><span class="sxs-lookup"><span data-stu-id="e4fd4-126">*sys.schema_tables_with_full_table_scans*</span></span>

<span data-ttu-id="e4fd4-127">Despite careful planning, many queries can still result in full table scans.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-127">Despite careful planning, many queries can still result in full table scans.</span></span> <span data-ttu-id="e4fd4-128">For additional information about the types of indexes and how to optimize them, you can refer to this article: [How to troubleshoot query performance](./howto-troubleshoot-query-performance.md).</span><span class="sxs-lookup"><span data-stu-id="e4fd4-128">For additional information about the types of indexes and how to optimize them, you can refer to this article: [How to troubleshoot query performance](./howto-troubleshoot-query-performance.md).</span></span> <span data-ttu-id="e4fd4-129">Full table scans are resource-intensive and degrade your database performance.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-129">Full table scans are resource-intensive and degrade your database performance.</span></span> <span data-ttu-id="e4fd4-130">The quickest way to find tables with full table scan is to query the *sys.schema_tables_with_full_table_scans* view.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-130">The quickest way to find tables with full table scan is to query the *sys.schema_tables_with_full_table_scans* view.</span></span>

![full table scans](./media/howto-troubleshoot-sys-schema/full-table-scans.png)

### <a name="sysusersummarybystatementtype"></a><span data-ttu-id="e4fd4-132">*sys.user_summary_by_statement_type*</span><span class="sxs-lookup"><span data-stu-id="e4fd4-132">*sys.user_summary_by_statement_type*</span></span>

<span data-ttu-id="e4fd4-133">To troubleshoot database performance issues, it may be beneficial to identify the events happening inside of your database, and using the *sys.user_summary_by_statement_type* view may just do the trick.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-133">To troubleshoot database performance issues, it may be beneficial to identify the events happening inside of your database, and using the *sys.user_summary_by_statement_type* view may just do the trick.</span></span>

![summary by statement](./media/howto-troubleshoot-sys-schema/summary-by-statement.png)

<span data-ttu-id="e4fd4-135">In this example Azure Database for MySQL spent 53 minutes flushing the slog query log 44579 times.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-135">In this example Azure Database for MySQL spent 53 minutes flushing the slog query log 44579 times.</span></span> <span data-ttu-id="e4fd4-136">That’s a long time and many IOs.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-136">That’s a long time and many IOs.</span></span> <span data-ttu-id="e4fd4-137">You can reduce this activity by either disable your slow query log or decrease the frequency of slow query login Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-137">You can reduce this activity by either disable your slow query log or decrease the frequency of slow query login Azure portal.</span></span>

## <a name="database-maintenance"></a><span data-ttu-id="e4fd4-138">Database maintenance</span><span class="sxs-lookup"><span data-stu-id="e4fd4-138">Database maintenance</span></span>

### <a name="sysinnodbbufferstatsbytable"></a><span data-ttu-id="e4fd4-139">*sys.innodb_buffer_stats_by_table*</span><span class="sxs-lookup"><span data-stu-id="e4fd4-139">*sys.innodb_buffer_stats_by_table*</span></span>

<span data-ttu-id="e4fd4-140">The InnoDB buffer pool resides in memory and is the main cache mechanism between the DBMS and storage.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-140">The InnoDB buffer pool resides in memory and is the main cache mechanism between the DBMS and storage.</span></span> <span data-ttu-id="e4fd4-141">The size of the InnoDB buffer pool is tied to the performance tier and cannot be changed unless a different product SKU is chosen.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-141">The size of the InnoDB buffer pool is tied to the performance tier and cannot be changed unless a different product SKU is chosen.</span></span> <span data-ttu-id="e4fd4-142">As with memory in your operating system, old pages are swapped out to make room for fresher data.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-142">As with memory in your operating system, old pages are swapped out to make room for fresher data.</span></span> <span data-ttu-id="e4fd4-143">To find out which tables consume most of the InnoDB buffer pool memory, you can query the *sys.innodb_buffer_stats_by_table* view.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-143">To find out which tables consume most of the InnoDB buffer pool memory, you can query the *sys.innodb_buffer_stats_by_table* view.</span></span>

![InnoDB buffer status](./media/howto-troubleshoot-sys-schema/innodb-buffer-status.png)

<span data-ttu-id="e4fd4-145">In the graphic above, it is apparent that other than system tables and views, each table in the mysqldatabase033 database, which hosts one of my WordPress sites, occupies 16 KB, or 1 page, of data in memory.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-145">In the graphic above, it is apparent that other than system tables and views, each table in the mysqldatabase033 database, which hosts one of my WordPress sites, occupies 16 KB, or 1 page, of data in memory.</span></span>

### <a name="sysschemaunusedindexes--sysschemaredundantindexes"></a><span data-ttu-id="e4fd4-146">*Sys.schema_unused_indexes* & *sys.schema_redundant_indexes*</span><span class="sxs-lookup"><span data-stu-id="e4fd4-146">*Sys.schema_unused_indexes* & *sys.schema_redundant_indexes*</span></span>

<span data-ttu-id="e4fd4-147">Indexes are great tools to improve read performance, but they do incur additional costs for inserts and storage.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-147">Indexes are great tools to improve read performance, but they do incur additional costs for inserts and storage.</span></span> <span data-ttu-id="e4fd4-148">*Sys.schema_unused_indexes* and *sys.schema_redundant_indexes* provide insights into unused or duplicate indexes.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-148">*Sys.schema_unused_indexes* and *sys.schema_redundant_indexes* provide insights into unused or duplicate indexes.</span></span>

![unused indexes](./media/howto-troubleshoot-sys-schema/unused-indexes.png)

![redundant indexes](./media/howto-troubleshoot-sys-schema/redundant-indexes.png)

## <a name="conclusion"></a><span data-ttu-id="e4fd4-151">Conclusion</span><span class="sxs-lookup"><span data-stu-id="e4fd4-151">Conclusion</span></span>

<span data-ttu-id="e4fd4-152">In summary, the sys_schema is a great tool for both performance tuning and database maintenance.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-152">In summary, the sys_schema is a great tool for both performance tuning and database maintenance.</span></span> <span data-ttu-id="e4fd4-153">Make sure to take advantage of this feature in your Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="e4fd4-153">Make sure to take advantage of this feature in your Azure Database for MySQL.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e4fd4-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="e4fd4-154">Next steps</span></span>
- <span data-ttu-id="e4fd4-155">To find peer answers to your most concerned questions or post a new question/answer, visit [MSDN forum](https://social.msdn.microsoft.com/forums/security/en-US/home?forum=AzureDatabaseforMySQL) or [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-database-mysql).</span><span class="sxs-lookup"><span data-stu-id="e4fd4-155">To find peer answers to your most concerned questions or post a new question/answer, visit [MSDN forum](https://social.msdn.microsoft.com/forums/security/en-US/home?forum=AzureDatabaseforMySQL) or [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-database-mysql).</span></span>
