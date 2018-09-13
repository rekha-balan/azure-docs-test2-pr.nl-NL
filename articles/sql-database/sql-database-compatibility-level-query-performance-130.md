---
title: Database compatibility level 130 - Azure SQL Database | Microsoft Docs
description: In this article, we explore the benefits of running your Azure SQL Database at compatibility level 130, and using the benefits of the new query optimizer and query processor features. We also address the possible side effects on the query performance for the existing SQL applications.
services: sql-database
documentationcenter: ''
author: alainlissoir
manager: jhubbard
editor: ''
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 03/03/2017
ms.author: alainl
ms.openlocfilehash: ba3d8f87d8ba8351fab5d7d359f2e719df796a89
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555427"
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="2b0da-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="2b0da-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="2b0da-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span><span class="sxs-lookup"><span data-stu-id="2b0da-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="2b0da-106">In this article, we explore the benefits of running your Azure SQL Database at compatibility level 130, and using the benefits of the new query optimizer and query processor features.</span><span class="sxs-lookup"><span data-stu-id="2b0da-106">In this article, we explore the benefits of running your Azure SQL Database at compatibility level 130, and using the benefits of the new query optimizer and query processor features.</span></span> <span data-ttu-id="2b0da-107">We also address the possible side effects on the query performance for the existing SQL applications.</span><span class="sxs-lookup"><span data-stu-id="2b0da-107">We also address the possible side effects on the query performance for the existing SQL applications.</span></span>

<span data-ttu-id="2b0da-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span><span class="sxs-lookup"><span data-stu-id="2b0da-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span></span>

* <span data-ttu-id="2b0da-109">100: in SQL Server 2008 and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2b0da-109">100: in SQL Server 2008 and Azure SQL Database.</span></span>
* <span data-ttu-id="2b0da-110">110: in SQL Server 2012 and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2b0da-110">110: in SQL Server 2012 and Azure SQL Database.</span></span>
* <span data-ttu-id="2b0da-111">120: in SQL Server 2014 and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2b0da-111">120: in SQL Server 2014 and Azure SQL Database.</span></span>
* <span data-ttu-id="2b0da-112">130: in SQL Server 2016 and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2b0da-112">130: in SQL Server 2016 and Azure SQL Database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b0da-113">The default compatibility level is 130 for **newly created** databases.</span><span class="sxs-lookup"><span data-stu-id="2b0da-113">The default compatibility level is 130 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="2b0da-114">Databases created before mid-June 2016 have the compatibility level in place at their creation time.</span><span class="sxs-lookup"><span data-stu-id="2b0da-114">Databases created before mid-June 2016 have the compatibility level in place at their creation time.</span></span> <span data-ttu-id="2b0da-115">Databases that migrated from an earlier version of Azure SQL Database have a compatibility level of either 100 or 110.</span><span class="sxs-lookup"><span data-stu-id="2b0da-115">Databases that migrated from an earlier version of Azure SQL Database have a compatibility level of either 100 or 110.</span></span> <span data-ttu-id="2b0da-116">The compatibility level of the master database for a server created prior to mid-June 2016 has the compatibility level in place when the server was created and cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="2b0da-116">The compatibility level of the master database for a server created prior to mid-June 2016 has the compatibility level in place when the server was created and cannot be changed.</span></span> <span data-ttu-id="2b0da-117">A different compatibility level between the master database and a user database is not something that impacts functionality or performance for user databases.</span><span class="sxs-lookup"><span data-stu-id="2b0da-117">A different compatibility level between the master database and a user database is not something that impacts functionality or performance for user databases.</span></span>
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="2b0da-118">About compatibility level 130</span><span class="sxs-lookup"><span data-stu-id="2b0da-118">About compatibility level 130</span></span>
<span data-ttu-id="2b0da-119">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="2b0da-119">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="2b0da-120">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some basic query examples, and see how anyone can benefit from it.</span><span class="sxs-lookup"><span data-stu-id="2b0da-120">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="2b0da-121">Query processing in relational databases can be very complex and require a deep background in computer science and mathematics to understand the inherent design choices and behaviors.</span><span class="sxs-lookup"><span data-stu-id="2b0da-121">Query processing in relational databases can be very complex and require a deep background in computer science and mathematics to understand the inherent design choices and behaviors.</span></span> <span data-ttu-id="2b0da-122">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span><span class="sxs-lookup"><span data-stu-id="2b0da-122">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="2b0da-123">Let’s have a quick look at what the compatibility level 130 brings at the table.</span><span class="sxs-lookup"><span data-stu-id="2b0da-123">Let’s have a quick look at what the compatibility level 130 brings at the table.</span></span>  <span data-ttu-id="2b0da-124">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span><span class="sxs-lookup"><span data-stu-id="2b0da-124">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="2b0da-125">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span><span class="sxs-lookup"><span data-stu-id="2b0da-125">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="2b0da-126">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded.</span><span class="sxs-lookup"><span data-stu-id="2b0da-126">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded.</span></span>
* <span data-ttu-id="2b0da-127">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span><span class="sxs-lookup"><span data-stu-id="2b0da-127">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="2b0da-128">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span><span class="sxs-lookup"><span data-stu-id="2b0da-128">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="2b0da-129">Batch mode v/s Row Mode changes with Column Store indexes</span><span class="sxs-lookup"><span data-stu-id="2b0da-129">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="2b0da-130">Sorts on a table with a Column Store index are now in batch mode.</span><span class="sxs-lookup"><span data-stu-id="2b0da-130">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="2b0da-131">Windowing aggregates now operate in batch mode such as T-SQL LAG/LEAD statements.</span><span class="sxs-lookup"><span data-stu-id="2b0da-131">Windowing aggregates now operate in batch mode such as T-SQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="2b0da-132">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span><span class="sxs-lookup"><span data-stu-id="2b0da-132">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="2b0da-133">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span><span class="sxs-lookup"><span data-stu-id="2b0da-133">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="2b0da-134">Last, Cardinality Estimation improvements come with compatibility level 120, but for those of you running at a lower Compatibility level (that is 100, or 110), the move to compatibility level 130 also brings these improvements, and these can also benefit the query performance of your applications.</span><span class="sxs-lookup"><span data-stu-id="2b0da-134">Last, Cardinality Estimation improvements come with compatibility level 120, but for those of you running at a lower Compatibility level (that is 100, or 110), the move to compatibility level 130 also brings these improvements, and these can also benefit the query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="2b0da-135">Practicing compatibility level 130</span><span class="sxs-lookup"><span data-stu-id="2b0da-135">Practicing compatibility level 130</span></span>
<span data-ttu-id="2b0da-136">First let’s get some tables, indexes, and random data created to practice some of these new capabilities.</span><span class="sxs-lookup"><span data-stu-id="2b0da-136">First let’s get some tables, indexes, and random data created to practice some of these new capabilities.</span></span> <span data-ttu-id="2b0da-137">The T-SQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2b0da-137">The T-SQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="2b0da-138">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span><span class="sxs-lookup"><span data-stu-id="2b0da-138">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- the second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="2b0da-139">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span><span class="sxs-lookup"><span data-stu-id="2b0da-139">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="2b0da-140">Parallel INSERT</span><span class="sxs-lookup"><span data-stu-id="2b0da-140">Parallel INSERT</span></span>
<span data-ttu-id="2b0da-141">Executing the following T-SQL statements executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span><span class="sxs-lookup"><span data-stu-id="2b0da-141">Executing the following T-SQL statements executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- The INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- The INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="2b0da-142">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span><span class="sxs-lookup"><span data-stu-id="2b0da-142">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="2b0da-143">Looking at the plans side by side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span><span class="sxs-lookup"><span data-stu-id="2b0da-143">Looking at the plans side by side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span></span> <span data-ttu-id="2b0da-144">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span><span class="sxs-lookup"><span data-stu-id="2b0da-144">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span></span> <span data-ttu-id="2b0da-145">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, performs better; up to a 100 times faster depending on your situation!</span><span class="sxs-lookup"><span data-stu-id="2b0da-145">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, performs better; up to a 100 times faster depending on your situation!</span></span>

<span data-ttu-id="2b0da-146">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span><span class="sxs-lookup"><span data-stu-id="2b0da-146">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span></span>

![Figure 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="2b0da-148">SERIAL Batch Mode</span><span class="sxs-lookup"><span data-stu-id="2b0da-148">SERIAL Batch Mode</span></span>
<span data-ttu-id="2b0da-149">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span><span class="sxs-lookup"><span data-stu-id="2b0da-149">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="2b0da-150">First, batch mode operations are only available when you have a column store index in place.</span><span class="sxs-lookup"><span data-stu-id="2b0da-150">First, batch mode operations are only available when you have a column store index in place.</span></span> <span data-ttu-id="2b0da-151">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span><span class="sxs-lookup"><span data-stu-id="2b0da-151">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span></span> <span data-ttu-id="2b0da-152">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span><span class="sxs-lookup"><span data-stu-id="2b0da-152">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span></span> <span data-ttu-id="2b0da-153">This shared number of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span><span class="sxs-lookup"><span data-stu-id="2b0da-153">This shared number of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="2b0da-154">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b0da-154">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="2b0da-155">By observing the query plans side by side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span><span class="sxs-lookup"><span data-stu-id="2b0da-155">By observing the query plans side by side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="2b0da-156">Increase the dataset, increase the benefit.</span><span class="sxs-lookup"><span data-stu-id="2b0da-156">Increase the dataset, increase the benefit.</span></span>

<span data-ttu-id="2b0da-157">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span><span class="sxs-lookup"><span data-stu-id="2b0da-157">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span></span>

![Figure 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="2b0da-159">Batch mode on Sort Execution</span><span class="sxs-lookup"><span data-stu-id="2b0da-159">Batch mode on Sort Execution</span></span>
<span data-ttu-id="2b0da-160">Similar to the preceding example, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span><span class="sxs-lookup"><span data-stu-id="2b0da-160">Similar to the preceding example, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="2b0da-161">Visible side by side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span><span class="sxs-lookup"><span data-stu-id="2b0da-161">Visible side by side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span></span>

<span data-ttu-id="2b0da-162">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span><span class="sxs-lookup"><span data-stu-id="2b0da-162">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span></span>

![Figure 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="2b0da-164">Obviously, these samples only contain tens of thousands of rows, which are nothing when looking at the data available in most SQL Servers these days.</span><span class="sxs-lookup"><span data-stu-id="2b0da-164">Obviously, these samples only contain tens of thousands of rows, which are nothing when looking at the data available in most SQL Servers these days.</span></span> <span data-ttu-id="2b0da-165">Project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span><span class="sxs-lookup"><span data-stu-id="2b0da-165">Project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="2b0da-166">Cardinality Estimation (CE) improvements</span><span class="sxs-lookup"><span data-stu-id="2b0da-166">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="2b0da-167">Introduced with SQL Server 2014, any database running at a compatibility level 120 or higher makes use of the new Cardinality Estimation functionality.</span><span class="sxs-lookup"><span data-stu-id="2b0da-167">Introduced with SQL Server 2014, any database running at a compatibility level 120 or higher makes use of the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="2b0da-168">Essentially, cardinality estimation is the logic used to determine how SQL server executes a query based on its estimated cost.</span><span class="sxs-lookup"><span data-stu-id="2b0da-168">Essentially, cardinality estimation is the logic used to determine how SQL server executes a query based on its estimated cost.</span></span> <span data-ttu-id="2b0da-169">The estimation is calculated using input from statistics associated with objects involved in that query.</span><span class="sxs-lookup"><span data-stu-id="2b0da-169">The estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="2b0da-170">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span><span class="sxs-lookup"><span data-stu-id="2b0da-170">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span></span> <span data-ttu-id="2b0da-171">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (that is TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span><span class="sxs-lookup"><span data-stu-id="2b0da-171">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (that is TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span></span> <span data-ttu-id="2b0da-172">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span><span class="sxs-lookup"><span data-stu-id="2b0da-172">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span></span> <span data-ttu-id="2b0da-173">On the other side, better estimates, more accurate estimates, leads to better query executions!</span><span class="sxs-lookup"><span data-stu-id="2b0da-173">On the other side, better estimates, more accurate estimates, leads to better query executions!</span></span>

<span data-ttu-id="2b0da-174">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span><span class="sxs-lookup"><span data-stu-id="2b0da-174">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="2b0da-175">Which Cardinality Estimation do you currently use?</span><span class="sxs-lookup"><span data-stu-id="2b0da-175">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="2b0da-176">To determine under which Cardinality Estimation your queries are running, use the following query samples.</span><span class="sxs-lookup"><span data-stu-id="2b0da-176">To determine under which Cardinality Estimation your queries are running, use the following query samples.</span></span> <span data-ttu-id="2b0da-177">This first example runs under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span><span class="sxs-lookup"><span data-stu-id="2b0da-177">This first example runs under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="2b0da-178">Once execution is complete, click the XML link, and look at the properties of the first iterator.</span><span class="sxs-lookup"><span data-stu-id="2b0da-178">Once execution is complete, click the XML link, and look at the properties of the first iterator.</span></span> <span data-ttu-id="2b0da-179">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span><span class="sxs-lookup"><span data-stu-id="2b0da-179">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="2b0da-180">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the preceding T-SQL statements), but the value 70 represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span><span class="sxs-lookup"><span data-stu-id="2b0da-180">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the preceding T-SQL statements), but the value 70 represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="2b0da-181">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or lower.*</span><span class="sxs-lookup"><span data-stu-id="2b0da-181">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or lower.*</span></span>

![Figure 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="2b0da-183">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b0da-183">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="2b0da-184">This is the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span><span class="sxs-lookup"><span data-stu-id="2b0da-184">This is the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span></span> <span data-ttu-id="2b0da-185">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (that is batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span><span class="sxs-lookup"><span data-stu-id="2b0da-185">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (that is batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="2b0da-186">Changing the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span><span class="sxs-lookup"><span data-stu-id="2b0da-186">Changing the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="2b0da-187">In such a case, the default CardinalityEstimationModelVersion is set to 120 or 130.</span><span class="sxs-lookup"><span data-stu-id="2b0da-187">In such a case, the default CardinalityEstimationModelVersion is set to 120 or 130.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="2b0da-188">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span><span class="sxs-lookup"><span data-stu-id="2b0da-188">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span></span>

![Figure 5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a><span data-ttu-id="2b0da-190">Witnessing the Cardinality Estimation differences</span><span class="sxs-lookup"><span data-stu-id="2b0da-190">Witnessing the Cardinality Estimation differences</span></span>
<span data-ttu-id="2b0da-191">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span><span class="sxs-lookup"><span data-stu-id="2b0da-191">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="2b0da-192">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span><span class="sxs-lookup"><span data-stu-id="2b0da-192">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="2b0da-193">Obviously, as said before, these row count results also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span><span class="sxs-lookup"><span data-stu-id="2b0da-193">Obviously, as said before, these row count results also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span></span> <span data-ttu-id="2b0da-194">Obviously, the predicates in your query also have an influence on the actual estimation aside from the table shape, data content, and how this data correlate with each other.</span><span class="sxs-lookup"><span data-stu-id="2b0da-194">Obviously, the predicates in your query also have an influence on the actual estimation aside from the table shape, data content, and how this data correlate with each other.</span></span>

<span data-ttu-id="2b0da-195">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span><span class="sxs-lookup"><span data-stu-id="2b0da-195">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span></span>

![Figure 6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="2b0da-197">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span><span class="sxs-lookup"><span data-stu-id="2b0da-197">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="2b0da-198">We now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span><span class="sxs-lookup"><span data-stu-id="2b0da-198">We now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span></span>

<span data-ttu-id="2b0da-199">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span><span class="sxs-lookup"><span data-stu-id="2b0da-199">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span></span>

![Figure 7](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="2b0da-201">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the T-SQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span><span class="sxs-lookup"><span data-stu-id="2b0da-201">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the T-SQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span></span> <span data-ttu-id="2b0da-202">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span><span class="sxs-lookup"><span data-stu-id="2b0da-202">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span></span> <span data-ttu-id="2b0da-203">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span><span class="sxs-lookup"><span data-stu-id="2b0da-203">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="2b0da-204">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span><span class="sxs-lookup"><span data-stu-id="2b0da-204">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="2b0da-205">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows, and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span><span class="sxs-lookup"><span data-stu-id="2b0da-205">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows, and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="2b0da-206">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how the old and new estimates are affected, while some could become more off from the reality, or some others closer to the actual row counts returned in the result sets.</span><span class="sxs-lookup"><span data-stu-id="2b0da-206">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how the old and new estimates are affected, while some could become more off from the reality, or some others closer to the actual row counts returned in the result sets.</span></span> <span data-ttu-id="2b0da-207">All of it depends on the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span><span class="sxs-lookup"><span data-stu-id="2b0da-207">All of it depends on the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span></span> <span data-ttu-id="2b0da-208">If you just created your Azure SQL Database instance, the query optimizer has to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span><span class="sxs-lookup"><span data-stu-id="2b0da-208">If you just created your Azure SQL Database instance, the query optimizer has to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span></span> <span data-ttu-id="2b0da-209">So, the estimates are very contextual and almost specific to every server and application situation.</span><span class="sxs-lookup"><span data-stu-id="2b0da-209">So, the estimates are very contextual and almost specific to every server and application situation.</span></span> <span data-ttu-id="2b0da-210">It is an important aspect to keep in mind!</span><span class="sxs-lookup"><span data-stu-id="2b0da-210">It is an important aspect to keep in mind!</span></span>

## <a name="some-considerations-to-take-into-account"></a><span data-ttu-id="2b0da-211">Some considerations to take into account</span><span class="sxs-lookup"><span data-stu-id="2b0da-211">Some considerations to take into account</span></span>
<span data-ttu-id="2b0da-212">Although most workloads would benefit from the compatibility level 130, before adopting the compatibility level for your production environment, you basically have 3 options:</span><span class="sxs-lookup"><span data-stu-id="2b0da-212">Although most workloads would benefit from the compatibility level 130, before adopting the compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="2b0da-213">You move to compatibility level 130, and see how things perform.</span><span class="sxs-lookup"><span data-stu-id="2b0da-213">You move to compatibility level 130, and see how things perform.</span></span> <span data-ttu-id="2b0da-214">In case you notice some regressions, you set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As preciously explained, this alone could address the issue).</span><span class="sxs-lookup"><span data-stu-id="2b0da-214">In case you notice some regressions, you set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As preciously explained, this alone could address the issue).</span></span>
2. <span data-ttu-id="2b0da-215">You thoroughly test your existing applications under similar production load, fine-tune, and validate the performance before going to production.</span><span class="sxs-lookup"><span data-stu-id="2b0da-215">You thoroughly test your existing applications under similar production load, fine-tune, and validate the performance before going to production.</span></span> <span data-ttu-id="2b0da-216">In case of issues, same as the preceding, you can always go back to the original compatibility level, or reverse the Cardinality Estimation back to the legacy mode.</span><span class="sxs-lookup"><span data-stu-id="2b0da-216">In case of issues, same as the preceding, you can always go back to the original compatibility level, or reverse the Cardinality Estimation back to the legacy mode.</span></span>
3. <span data-ttu-id="2b0da-217">As a final option, and the most recent way to address these questions, is to use Query Store.</span><span class="sxs-lookup"><span data-stu-id="2b0da-217">As a final option, and the most recent way to address these questions, is to use Query Store.</span></span> <span data-ttu-id="2b0da-218">That’s today’s recommended option!</span><span class="sxs-lookup"><span data-stu-id="2b0da-218">That’s today’s recommended option!</span></span> <span data-ttu-id="2b0da-219">To assist the analysis of your queries under compatibility level 120 or lower versus 130, we cannot encourage you enough to use Query Store.</span><span class="sxs-lookup"><span data-stu-id="2b0da-219">To assist the analysis of your queries under compatibility level 120 or lower versus 130, we cannot encourage you enough to use Query Store.</span></span> <span data-ttu-id="2b0da-220">Query Store is available with the latest version of Azure SQL Database, and it’s designed to help you with query performance troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="2b0da-220">Query Store is available with the latest version of Azure SQL Database, and it’s designed to help you with query performance troubleshooting.</span></span> <span data-ttu-id="2b0da-221">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span><span class="sxs-lookup"><span data-stu-id="2b0da-221">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="2b0da-222">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span><span class="sxs-lookup"><span data-stu-id="2b0da-222">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span></span> <span data-ttu-id="2b0da-223">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="2b0da-223">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="2b0da-224">At the high level, if you already have a set of databases running at compatibility level 120 or lower, and plan to move some of them to 130, or because your workload automatically provision new databases that are set by default to 130, please consider the followings:</span><span class="sxs-lookup"><span data-stu-id="2b0da-224">At the high level, if you already have a set of databases running at compatibility level 120 or lower, and plan to move some of them to 130, or because your workload automatically provision new databases that are set by default to 130, please consider the followings:</span></span>

* <span data-ttu-id="2b0da-225">Before changing to the new compatibility level in production, enable Query Store.</span><span class="sxs-lookup"><span data-stu-id="2b0da-225">Before changing to the new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="2b0da-226">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="2b0da-226">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="2b0da-227">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span><span class="sxs-lookup"><span data-stu-id="2b0da-227">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="2b0da-228">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span><span class="sxs-lookup"><span data-stu-id="2b0da-228">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="2b0da-229">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span><span class="sxs-lookup"><span data-stu-id="2b0da-229">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span></span>
* <span data-ttu-id="2b0da-230">If you want to use the new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span><span class="sxs-lookup"><span data-stu-id="2b0da-230">If you want to use the new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="2b0da-231">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span><span class="sxs-lookup"><span data-stu-id="2b0da-231">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="2b0da-232">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span><span class="sxs-lookup"><span data-stu-id="2b0da-232">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="2b0da-233">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span><span class="sxs-lookup"><span data-stu-id="2b0da-233">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span></span> <span data-ttu-id="2b0da-234">It is not a mandate; it really depends on how your application is affected by the compatibility level.</span><span class="sxs-lookup"><span data-stu-id="2b0da-234">It is not a mandate; it really depends on how your application is affected by the compatibility level.</span></span>
* <span data-ttu-id="2b0da-235">Last, regarding the Cardinality Estimation, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span><span class="sxs-lookup"><span data-stu-id="2b0da-235">Last, regarding the Cardinality Estimation, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="2b0da-236">Conclusion</span><span class="sxs-lookup"><span data-stu-id="2b0da-236">Conclusion</span></span>
<span data-ttu-id="2b0da-237">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span><span class="sxs-lookup"><span data-stu-id="2b0da-237">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="2b0da-238">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span><span class="sxs-lookup"><span data-stu-id="2b0da-238">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span></span> <span data-ttu-id="2b0da-239">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while using new query processing functions, and new Cardinality Estimation.</span><span class="sxs-lookup"><span data-stu-id="2b0da-239">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while using new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="2b0da-240">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span><span class="sxs-lookup"><span data-stu-id="2b0da-240">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="2b0da-241">And again, the Query Store can be of a great help in doing this work!</span><span class="sxs-lookup"><span data-stu-id="2b0da-241">And again, the Query Store can be of a great help in doing this work!</span></span>

## <a name="references"></a><span data-ttu-id="2b0da-242">References</span><span class="sxs-lookup"><span data-stu-id="2b0da-242">References</span></span>
* [<span data-ttu-id="2b0da-243">What’s New in Database Engine</span><span class="sxs-lookup"><span data-stu-id="2b0da-243">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="2b0da-244">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span><span class="sxs-lookup"><span data-stu-id="2b0da-244">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="2b0da-245">ALTER DATABASE Compatibility Level (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="2b0da-245">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="2b0da-246">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="2b0da-246">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="2b0da-247">Compatibility Level 130 for Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="2b0da-247">Compatibility Level 130 for Azure SQL Database</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="2b0da-248">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span><span class="sxs-lookup"><span data-stu-id="2b0da-248">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="2b0da-249">Columnstore Indexes Guide</span><span class="sxs-lookup"><span data-stu-id="2b0da-249">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="2b0da-250">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span><span class="sxs-lookup"><span data-stu-id="2b0da-250">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)








