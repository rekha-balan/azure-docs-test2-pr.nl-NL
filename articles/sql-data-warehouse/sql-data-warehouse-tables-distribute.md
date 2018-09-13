---
title: Distributed tables design guidance - Azure SQL Data Warehouse | Microsoft Docs
description: Recommendations for designing hash-distributed and round-robin distributed tables in Azure SQL Data Warehouse.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: rortloff
ms.reviewer: igorstan
ms.openlocfilehash: 6b6d6dd5f000c4295ffdf64f7d2f1ece4f625678
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790457"
---
# <a name="guidance-for-designing-distributed-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="da702-103">Guidance for designing distributed tables in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="da702-103">Guidance for designing distributed tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="da702-104">Recommendations for designing hash-distributed and round-robin distributed tables in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da702-104">Recommendations for designing hash-distributed and round-robin distributed tables in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="da702-105">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da702-105">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="da702-106">For more information, see [Azure SQL Data Warehouse - Massively Parallel Processing (MPP) architecture](massively-parallel-processing-mpp-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="da702-106">For more information, see [Azure SQL Data Warehouse - Massively Parallel Processing (MPP) architecture](massively-parallel-processing-mpp-architecture.md).</span></span> 

## <a name="what-is-a-distributed-table"></a><span data-ttu-id="da702-107">What is a distributed table?</span><span class="sxs-lookup"><span data-stu-id="da702-107">What is a distributed table?</span></span>
<span data-ttu-id="da702-108">A distributed table appears as a single table, but the rows are actually stored across 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="da702-108">A distributed table appears as a single table, but the rows are actually stored across 60 distributions.</span></span> <span data-ttu-id="da702-109">The rows are distributed with a hash or round-robin algorithm.</span><span class="sxs-lookup"><span data-stu-id="da702-109">The rows are distributed with a hash or round-robin algorithm.</span></span>  

<span data-ttu-id="da702-110">**Hash-distributed tables** improve query performance on large fact tables, and are the focus of this article.</span><span class="sxs-lookup"><span data-stu-id="da702-110">**Hash-distributed tables** improve query performance on large fact tables, and are the focus of this article.</span></span> <span data-ttu-id="da702-111">**Round-robin tables** are useful for improving loading speed.</span><span class="sxs-lookup"><span data-stu-id="da702-111">**Round-robin tables** are useful for improving loading speed.</span></span> <span data-ttu-id="da702-112">These design choices have a significant impact on improving query and loading performance.</span><span class="sxs-lookup"><span data-stu-id="da702-112">These design choices have a significant impact on improving query and loading performance.</span></span>

<span data-ttu-id="da702-113">Another table storage option is to replicate a small table across all the Compute nodes.</span><span class="sxs-lookup"><span data-stu-id="da702-113">Another table storage option is to replicate a small table across all the Compute nodes.</span></span> <span data-ttu-id="da702-114">For more information, see [Design guidance for replicated tables](design-guidance-for-replicated-tables.md).</span><span class="sxs-lookup"><span data-stu-id="da702-114">For more information, see [Design guidance for replicated tables](design-guidance-for-replicated-tables.md).</span></span> <span data-ttu-id="da702-115">To quickly choose among the three options, see Distributed tables in the [tables overview](sql-data-warehouse-tables-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da702-115">To quickly choose among the three options, see Distributed tables in the [tables overview](sql-data-warehouse-tables-overview.md).</span></span> 

<span data-ttu-id="da702-116">As part of table design, understand as much as possible about your data and how the data is queried.</span><span class="sxs-lookup"><span data-stu-id="da702-116">As part of table design, understand as much as possible about your data and how the data is queried.</span></span>  <span data-ttu-id="da702-117">For example, consider these questions:</span><span class="sxs-lookup"><span data-stu-id="da702-117">For example, consider these questions:</span></span>

- <span data-ttu-id="da702-118">How large is the table?</span><span class="sxs-lookup"><span data-stu-id="da702-118">How large is the table?</span></span>   
- <span data-ttu-id="da702-119">How often is the table refreshed?</span><span class="sxs-lookup"><span data-stu-id="da702-119">How often is the table refreshed?</span></span>   
- <span data-ttu-id="da702-120">Do I have fact and dimension tables in a data warehouse?</span><span class="sxs-lookup"><span data-stu-id="da702-120">Do I have fact and dimension tables in a data warehouse?</span></span>   


### <a name="hash-distributed"></a><span data-ttu-id="da702-121">Hash distributed</span><span class="sxs-lookup"><span data-stu-id="da702-121">Hash distributed</span></span>
<span data-ttu-id="da702-122">A hash-distributed table distributes table rows across the Compute nodes by using a deterministic hash function to assign each row to one [distribution](massively-parallel-processing-mpp-architecture.md#distributions).</span><span class="sxs-lookup"><span data-stu-id="da702-122">A hash-distributed table distributes table rows across the Compute nodes by using a deterministic hash function to assign each row to one [distribution](massively-parallel-processing-mpp-architecture.md#distributions).</span></span> 

<span data-ttu-id="da702-123">![Distributed table](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "Distributed table")</span><span class="sxs-lookup"><span data-stu-id="da702-123">![Distributed table](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "Distributed table")</span></span>  

<span data-ttu-id="da702-124">Since identical values always hash to the same distribution, the data warehouse has built-in knowledge of the row locations.</span><span class="sxs-lookup"><span data-stu-id="da702-124">Since identical values always hash to the same distribution, the data warehouse has built-in knowledge of the row locations.</span></span> <span data-ttu-id="da702-125">SQL Data Warehouse uses this knowledge to minimize data movement during queries, which improves query performance.</span><span class="sxs-lookup"><span data-stu-id="da702-125">SQL Data Warehouse uses this knowledge to minimize data movement during queries, which improves query performance.</span></span> 

<span data-ttu-id="da702-126">Hash-distributed tables work well for large fact tables in a star schema.</span><span class="sxs-lookup"><span data-stu-id="da702-126">Hash-distributed tables work well for large fact tables in a star schema.</span></span> <span data-ttu-id="da702-127">They can have very large numbers of rows and still achieve high performance.</span><span class="sxs-lookup"><span data-stu-id="da702-127">They can have very large numbers of rows and still achieve high performance.</span></span> <span data-ttu-id="da702-128">There are, of course, some design considerations that help you to get the performance the distributed system is designed to provide.</span><span class="sxs-lookup"><span data-stu-id="da702-128">There are, of course, some design considerations that help you to get the performance the distributed system is designed to provide.</span></span> <span data-ttu-id="da702-129">Choosing a good distribution column is one such consideration that is described in this article.</span><span class="sxs-lookup"><span data-stu-id="da702-129">Choosing a good distribution column is one such consideration that is described in this article.</span></span> 

<span data-ttu-id="da702-130">Consider using a hash-distributed table when:</span><span class="sxs-lookup"><span data-stu-id="da702-130">Consider using a hash-distributed table when:</span></span>

- <span data-ttu-id="da702-131">The table size on disk is more than 2 GB.</span><span class="sxs-lookup"><span data-stu-id="da702-131">The table size on disk is more than 2 GB.</span></span>
- <span data-ttu-id="da702-132">The table has frequent insert, update, and delete operations.</span><span class="sxs-lookup"><span data-stu-id="da702-132">The table has frequent insert, update, and delete operations.</span></span> 

### <a name="round-robin-distributed"></a><span data-ttu-id="da702-133">Round-robin distributed</span><span class="sxs-lookup"><span data-stu-id="da702-133">Round-robin distributed</span></span>
<span data-ttu-id="da702-134">A round-robin distributed table distributes table rows evenly across all distributions.</span><span class="sxs-lookup"><span data-stu-id="da702-134">A round-robin distributed table distributes table rows evenly across all distributions.</span></span> <span data-ttu-id="da702-135">The assignment of rows to distributions is random.</span><span class="sxs-lookup"><span data-stu-id="da702-135">The assignment of rows to distributions is random.</span></span> <span data-ttu-id="da702-136">Unlike hash-distributed tables, rows with equal values are not guaranteed to be assigned to the same distribution.</span><span class="sxs-lookup"><span data-stu-id="da702-136">Unlike hash-distributed tables, rows with equal values are not guaranteed to be assigned to the same distribution.</span></span> 

<span data-ttu-id="da702-137">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span><span class="sxs-lookup"><span data-stu-id="da702-137">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="da702-138">This extra step can slow down your queries.</span><span class="sxs-lookup"><span data-stu-id="da702-138">This extra step can slow down your queries.</span></span> <span data-ttu-id="da702-139">For example, joining a round-robin table usually requires reshuffling the rows, which is a performance hit.</span><span class="sxs-lookup"><span data-stu-id="da702-139">For example, joining a round-robin table usually requires reshuffling the rows, which is a performance hit.</span></span>

<span data-ttu-id="da702-140">Consider using the round-robin distribution for your table in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="da702-140">Consider using the round-robin distribution for your table in the following scenarios:</span></span>

- <span data-ttu-id="da702-141">When getting started as a simple starting point since it is the default</span><span class="sxs-lookup"><span data-stu-id="da702-141">When getting started as a simple starting point since it is the default</span></span>
- <span data-ttu-id="da702-142">If there is no obvious joining key</span><span class="sxs-lookup"><span data-stu-id="da702-142">If there is no obvious joining key</span></span>
- <span data-ttu-id="da702-143">If there is not good candidate column for hash distributing the table</span><span class="sxs-lookup"><span data-stu-id="da702-143">If there is not good candidate column for hash distributing the table</span></span>
- <span data-ttu-id="da702-144">If the table does not share a common join key with other tables</span><span class="sxs-lookup"><span data-stu-id="da702-144">If the table does not share a common join key with other tables</span></span>
- <span data-ttu-id="da702-145">If the join is less significant than other joins in the query</span><span class="sxs-lookup"><span data-stu-id="da702-145">If the join is less significant than other joins in the query</span></span>
- <span data-ttu-id="da702-146">When the table is a temporary staging table</span><span class="sxs-lookup"><span data-stu-id="da702-146">When the table is a temporary staging table</span></span>

<span data-ttu-id="da702-147">The tutorial [Load New York taxicab data to Azure SQL Data Warehouse](load-data-from-azure-blob-storage-using-polybase.md#load-the-data-into-your-data-warehouse) gives an example of loading data into a round-robin staging table.</span><span class="sxs-lookup"><span data-stu-id="da702-147">The tutorial [Load New York taxicab data to Azure SQL Data Warehouse](load-data-from-azure-blob-storage-using-polybase.md#load-the-data-into-your-data-warehouse) gives an example of loading data into a round-robin staging table.</span></span>


## <a name="choosing-a-distribution-column"></a><span data-ttu-id="da702-148">Choosing a distribution column</span><span class="sxs-lookup"><span data-stu-id="da702-148">Choosing a distribution column</span></span>
<span data-ttu-id="da702-149">A hash-distributed table has a distribution column that is the hash key.</span><span class="sxs-lookup"><span data-stu-id="da702-149">A hash-distributed table has a distribution column that is the hash key.</span></span> <span data-ttu-id="da702-150">For example, the following code creates a hash-distributed table with ProductKey as the distribution column.</span><span class="sxs-lookup"><span data-stu-id="da702-150">For example, the following code creates a hash-distributed table with ProductKey as the distribution column.</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
``` 

<span data-ttu-id="da702-151">Choosing a distribution column is an important design decision since the values in this column determine how the rows are distributed.</span><span class="sxs-lookup"><span data-stu-id="da702-151">Choosing a distribution column is an important design decision since the values in this column determine how the rows are distributed.</span></span> <span data-ttu-id="da702-152">The best choice depends on several factors, and usually involves tradeoffs.</span><span class="sxs-lookup"><span data-stu-id="da702-152">The best choice depends on several factors, and usually involves tradeoffs.</span></span> <span data-ttu-id="da702-153">However, if you don't choose the best column the first time, you can use [CREATE TABLE AS SELECT (CTAS)](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to re-create the table with a different distribution column.</span><span class="sxs-lookup"><span data-stu-id="da702-153">However, if you don't choose the best column the first time, you can use [CREATE TABLE AS SELECT (CTAS)](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to re-create the table with a different distribution column.</span></span> 

### <a name="choose-a-distribution-column-that-does-not-require-updates"></a><span data-ttu-id="da702-154">Choose a distribution column that does not require updates</span><span class="sxs-lookup"><span data-stu-id="da702-154">Choose a distribution column that does not require updates</span></span>
<span data-ttu-id="da702-155">You cannot update a distribution column unless you delete the row and insert a new row with the updated values.</span><span class="sxs-lookup"><span data-stu-id="da702-155">You cannot update a distribution column unless you delete the row and insert a new row with the updated values.</span></span> <span data-ttu-id="da702-156">Therefore, select a column with static values.</span><span class="sxs-lookup"><span data-stu-id="da702-156">Therefore, select a column with static values.</span></span> 

### <a name="choose-a-distribution-column-with-data-that-distributes-evenly"></a><span data-ttu-id="da702-157">Choose a distribution column with data that distributes evenly</span><span class="sxs-lookup"><span data-stu-id="da702-157">Choose a distribution column with data that distributes evenly</span></span>

<span data-ttu-id="da702-158">For best performance, all of the distributions should have approximately the same number of rows.</span><span class="sxs-lookup"><span data-stu-id="da702-158">For best performance, all of the distributions should have approximately the same number of rows.</span></span> <span data-ttu-id="da702-159">When one or more distributions have a disproportionate number of rows, some distributions finish their portion of a parallel query before others.</span><span class="sxs-lookup"><span data-stu-id="da702-159">When one or more distributions have a disproportionate number of rows, some distributions finish their portion of a parallel query before others.</span></span> <span data-ttu-id="da702-160">Since the query can't complete until all distributions have finished processing, each query is only as fast as the slowest distribution.</span><span class="sxs-lookup"><span data-stu-id="da702-160">Since the query can't complete until all distributions have finished processing, each query is only as fast as the slowest distribution.</span></span>

- <span data-ttu-id="da702-161">Data skew means the data is not distributed evenly across the distributions</span><span class="sxs-lookup"><span data-stu-id="da702-161">Data skew means the data is not distributed evenly across the distributions</span></span>
- <span data-ttu-id="da702-162">Processing skew means that some distributions take longer than others when running parallel queries.</span><span class="sxs-lookup"><span data-stu-id="da702-162">Processing skew means that some distributions take longer than others when running parallel queries.</span></span> <span data-ttu-id="da702-163">This can happen when the data is skewed.</span><span class="sxs-lookup"><span data-stu-id="da702-163">This can happen when the data is skewed.</span></span>
  
<span data-ttu-id="da702-164">To balance the parallel processing, select a distribution column that:</span><span class="sxs-lookup"><span data-stu-id="da702-164">To balance the parallel processing, select a distribution column that:</span></span>

- <span data-ttu-id="da702-165">**Has many unique values.**</span><span class="sxs-lookup"><span data-stu-id="da702-165">**Has many unique values.**</span></span> <span data-ttu-id="da702-166">The column can have some duplicate values.</span><span class="sxs-lookup"><span data-stu-id="da702-166">The column can have some duplicate values.</span></span> <span data-ttu-id="da702-167">However, all rows with the same value are assigned to the same distribution.</span><span class="sxs-lookup"><span data-stu-id="da702-167">However, all rows with the same value are assigned to the same distribution.</span></span> <span data-ttu-id="da702-168">Since there are 60 distributions, the column should have at least 60 unique values.</span><span class="sxs-lookup"><span data-stu-id="da702-168">Since there are 60 distributions, the column should have at least 60 unique values.</span></span>  <span data-ttu-id="da702-169">Usually the number of unique values is much greater.</span><span class="sxs-lookup"><span data-stu-id="da702-169">Usually the number of unique values is much greater.</span></span>
- <span data-ttu-id="da702-170">**Does not have NULLs, or has only a few NULLs.**</span><span class="sxs-lookup"><span data-stu-id="da702-170">**Does not have NULLs, or has only a few NULLs.**</span></span> <span data-ttu-id="da702-171">For an extreme example, if all values in the column are NULL, all the rows are assigned to the same distribution.</span><span class="sxs-lookup"><span data-stu-id="da702-171">For an extreme example, if all values in the column are NULL, all the rows are assigned to the same distribution.</span></span> <span data-ttu-id="da702-172">As a result, query processing is skewed to one distribution, and does not benefit from parallel processing.</span><span class="sxs-lookup"><span data-stu-id="da702-172">As a result, query processing is skewed to one distribution, and does not benefit from parallel processing.</span></span> 
- <span data-ttu-id="da702-173">**Is not a date column**.</span><span class="sxs-lookup"><span data-stu-id="da702-173">**Is not a date column**.</span></span> <span data-ttu-id="da702-174">All data for the same date lands in the same distribution.</span><span class="sxs-lookup"><span data-stu-id="da702-174">All data for the same date lands in the same distribution.</span></span> <span data-ttu-id="da702-175">If several users are all filtering on the same date, then only 1 of the 60 distributions do all the processing work.</span><span class="sxs-lookup"><span data-stu-id="da702-175">If several users are all filtering on the same date, then only 1 of the 60 distributions do all the processing work.</span></span> 

### <a name="choose-a-distribution-column-that-minimizes-data-movement"></a><span data-ttu-id="da702-176">Choose a distribution column that minimizes data movement</span><span class="sxs-lookup"><span data-stu-id="da702-176">Choose a distribution column that minimizes data movement</span></span>

<span data-ttu-id="da702-177">To get the correct query result queries might move data from one Compute node to another.</span><span class="sxs-lookup"><span data-stu-id="da702-177">To get the correct query result queries might move data from one Compute node to another.</span></span> <span data-ttu-id="da702-178">Data movement commonly happens when queries have joins and aggregations on distributed tables.</span><span class="sxs-lookup"><span data-stu-id="da702-178">Data movement commonly happens when queries have joins and aggregations on distributed tables.</span></span> <span data-ttu-id="da702-179">Choosing a distribution column that helps minimize data movement is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="da702-179">Choosing a distribution column that helps minimize data movement is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>

<span data-ttu-id="da702-180">To minimize data movement, select a distribution column that:</span><span class="sxs-lookup"><span data-stu-id="da702-180">To minimize data movement, select a distribution column that:</span></span>

- <span data-ttu-id="da702-181">Is used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER`, and `HAVING` clauses.</span><span class="sxs-lookup"><span data-stu-id="da702-181">Is used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER`, and `HAVING` clauses.</span></span> <span data-ttu-id="da702-182">When two large fact tables have frequent joins, query performance improves when you distribute both tables on one of the join columns.</span><span class="sxs-lookup"><span data-stu-id="da702-182">When two large fact tables have frequent joins, query performance improves when you distribute both tables on one of the join columns.</span></span>  <span data-ttu-id="da702-183">When a table is not used in joins, consider distributing the table on a column that is frequently in the `GROUP BY` clause.</span><span class="sxs-lookup"><span data-stu-id="da702-183">When a table is not used in joins, consider distributing the table on a column that is frequently in the `GROUP BY` clause.</span></span>
- <span data-ttu-id="da702-184">Is *not* used in `WHERE` clauses.</span><span class="sxs-lookup"><span data-stu-id="da702-184">Is *not* used in `WHERE` clauses.</span></span> <span data-ttu-id="da702-185">This could narrow the query to not run on all the distributions.</span><span class="sxs-lookup"><span data-stu-id="da702-185">This could narrow the query to not run on all the distributions.</span></span> 
- <span data-ttu-id="da702-186">Is *not* a date column.</span><span class="sxs-lookup"><span data-stu-id="da702-186">Is *not* a date column.</span></span> <span data-ttu-id="da702-187">WHERE clauses often filter by date.</span><span class="sxs-lookup"><span data-stu-id="da702-187">WHERE clauses often filter by date.</span></span>  <span data-ttu-id="da702-188">When this happens, all the processing could run on only a few distributions.</span><span class="sxs-lookup"><span data-stu-id="da702-188">When this happens, all the processing could run on only a few distributions.</span></span>

### <a name="what-to-do-when-none-of-the-columns-are-a-good-distribution-column"></a><span data-ttu-id="da702-189">What to do when none of the columns are a good distribution column</span><span class="sxs-lookup"><span data-stu-id="da702-189">What to do when none of the columns are a good distribution column</span></span>

<span data-ttu-id="da702-190">If none of your columns have enough distinct values for a distribution column, you can create a new column as a composite of one or more values.</span><span class="sxs-lookup"><span data-stu-id="da702-190">If none of your columns have enough distinct values for a distribution column, you can create a new column as a composite of one or more values.</span></span> <span data-ttu-id="da702-191">To avoid data movement during query execution, use the composite distribution column as a join column in queries.</span><span class="sxs-lookup"><span data-stu-id="da702-191">To avoid data movement during query execution, use the composite distribution column as a join column in queries.</span></span>

<span data-ttu-id="da702-192">Once you design a hash-distributed table, the next step is to load data into the table.</span><span class="sxs-lookup"><span data-stu-id="da702-192">Once you design a hash-distributed table, the next step is to load data into the table.</span></span>  <span data-ttu-id="da702-193">For loading guidance, see [Loading overview](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="da702-193">For loading guidance, see [Loading overview](sql-data-warehouse-overview-load.md).</span></span> 

## <a name="how-to-tell-if-your-distribution-column-is-a-good-choice"></a><span data-ttu-id="da702-194">How to tell if your distribution column is a good choice</span><span class="sxs-lookup"><span data-stu-id="da702-194">How to tell if your distribution column is a good choice</span></span>
<span data-ttu-id="da702-195">After data is loaded into a hash-distributed table, check to see how evenly the rows are distributed across the 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="da702-195">After data is loaded into a hash-distributed table, check to see how evenly the rows are distributed across the 60 distributions.</span></span> <span data-ttu-id="da702-196">The rows per distribution can vary up to 10% without a noticeable impact on performance.</span><span class="sxs-lookup"><span data-stu-id="da702-196">The rows per distribution can vary up to 10% without a noticeable impact on performance.</span></span> 

### <a name="determine-if-the-table-has-data-skew"></a><span data-ttu-id="da702-197">Determine if the table has data skew</span><span class="sxs-lookup"><span data-stu-id="da702-197">Determine if the table has data skew</span></span>
<span data-ttu-id="da702-198">A quick way to check for data skew is to use [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="da702-198">A quick way to check for data skew is to use [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql).</span></span> <span data-ttu-id="da702-199">The following SQL code returns the number of table rows that are stored in each of the 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="da702-199">The following SQL code returns the number of table rows that are stored in each of the 60 distributions.</span></span> <span data-ttu-id="da702-200">For balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span><span class="sxs-lookup"><span data-stu-id="da702-200">For balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="da702-201">To identify which tables have more than 10% data skew:</span><span class="sxs-lookup"><span data-stu-id="da702-201">To identify which tables have more than 10% data skew:</span></span>

1. <span data-ttu-id="da702-202">Create the view dbo.vTableSizes that is shown in the [Tables overview](sql-data-warehouse-tables-overview.md#table-size-queries) article.</span><span class="sxs-lookup"><span data-stu-id="da702-202">Create the view dbo.vTableSizes that is shown in the [Tables overview](sql-data-warehouse-tables-overview.md#table-size-queries) article.</span></span>  
2. <span data-ttu-id="da702-203">Run the following query:</span><span class="sxs-lookup"><span data-stu-id="da702-203">Run the following query:</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="check-query-plans-for-data-movement"></a><span data-ttu-id="da702-204">Check query plans for data movement</span><span class="sxs-lookup"><span data-stu-id="da702-204">Check query plans for data movement</span></span>
<span data-ttu-id="da702-205">A good distribution column enables joins and aggregations to have minimal data movement.</span><span class="sxs-lookup"><span data-stu-id="da702-205">A good distribution column enables joins and aggregations to have minimal data movement.</span></span> <span data-ttu-id="da702-206">This affects the way joins should be written.</span><span class="sxs-lookup"><span data-stu-id="da702-206">This affects the way joins should be written.</span></span> <span data-ttu-id="da702-207">To get minimal data movement for a join on two hash-distributed tables, one of the join columns needs to be the distribution column.</span><span class="sxs-lookup"><span data-stu-id="da702-207">To get minimal data movement for a join on two hash-distributed tables, one of the join columns needs to be the distribution column.</span></span>  <span data-ttu-id="da702-208">When two hash-distributed tables join on a distribution column of the same data type, the join does not require data movement.</span><span class="sxs-lookup"><span data-stu-id="da702-208">When two hash-distributed tables join on a distribution column of the same data type, the join does not require data movement.</span></span> <span data-ttu-id="da702-209">Joins can use additional columns without incurring data movement.</span><span class="sxs-lookup"><span data-stu-id="da702-209">Joins can use additional columns without incurring data movement.</span></span>

<span data-ttu-id="da702-210">To avoid data movement during a join:</span><span class="sxs-lookup"><span data-stu-id="da702-210">To avoid data movement during a join:</span></span>

- <span data-ttu-id="da702-211">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span><span class="sxs-lookup"><span data-stu-id="da702-211">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
- <span data-ttu-id="da702-212">The data types of the join columns must match between both tables.</span><span class="sxs-lookup"><span data-stu-id="da702-212">The data types of the join columns must match between both tables.</span></span>
- <span data-ttu-id="da702-213">The columns must be joined with an equals operator.</span><span class="sxs-lookup"><span data-stu-id="da702-213">The columns must be joined with an equals operator.</span></span>
- <span data-ttu-id="da702-214">The join type may not be a `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="da702-214">The join type may not be a `CROSS JOIN`.</span></span>

<span data-ttu-id="da702-215">To see if queries are experiencing data movement, you can look at the query plan.</span><span class="sxs-lookup"><span data-stu-id="da702-215">To see if queries are experiencing data movement, you can look at the query plan.</span></span>  


## <a name="resolve-a-distribution-column-problem"></a><span data-ttu-id="da702-216">Resolve a distribution column problem</span><span class="sxs-lookup"><span data-stu-id="da702-216">Resolve a distribution column problem</span></span>
<span data-ttu-id="da702-217">It is not necessary to resolve all cases of data skew.</span><span class="sxs-lookup"><span data-stu-id="da702-217">It is not necessary to resolve all cases of data skew.</span></span> <span data-ttu-id="da702-218">Distributing data is a matter of finding the right balance between minimizing data skew and data movement.</span><span class="sxs-lookup"><span data-stu-id="da702-218">Distributing data is a matter of finding the right balance between minimizing data skew and data movement.</span></span> <span data-ttu-id="da702-219">It is not always possible to minimize both data skew and data movement.</span><span class="sxs-lookup"><span data-stu-id="da702-219">It is not always possible to minimize both data skew and data movement.</span></span> <span data-ttu-id="da702-220">Sometimes the benefit of having the minimal data movement might outweigh the impact of having data skew.</span><span class="sxs-lookup"><span data-stu-id="da702-220">Sometimes the benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="da702-221">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span><span class="sxs-lookup"><span data-stu-id="da702-221">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span> <span data-ttu-id="da702-222">You can use the steps in the [Query monitoring](sql-data-warehouse-manage-monitor.md) article to monitor the impact of skew on query performance.</span><span class="sxs-lookup"><span data-stu-id="da702-222">You can use the steps in the [Query monitoring](sql-data-warehouse-manage-monitor.md) article to monitor the impact of skew on query performance.</span></span> <span data-ttu-id="da702-223">Specifically, look for how long it takes large queries to complete on individual distributions.</span><span class="sxs-lookup"><span data-stu-id="da702-223">Specifically, look for how long it takes large queries to complete on individual distributions.</span></span>

<span data-ttu-id="da702-224">Since you cannot change the distribution column on an existing table, the typical way to resolve data skew is to re-create the table with a different distribution column.</span><span class="sxs-lookup"><span data-stu-id="da702-224">Since you cannot change the distribution column on an existing table, the typical way to resolve data skew is to re-create the table with a different distribution column.</span></span>  

### <a name="re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="da702-225">Re-create the table with a new distribution column</span><span class="sxs-lookup"><span data-stu-id="da702-225">Re-create the table with a new distribution column</span></span>
<span data-ttu-id="da702-226">This example uses [CREATE TABLE AS SELECT](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?view=aps-pdw-2016-au7) to re-create a table with a different hash distribution column.</span><span class="sxs-lookup"><span data-stu-id="da702-226">This example uses [CREATE TABLE AS SELECT](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?view=aps-pdw-2016-au7) to re-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="da702-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="da702-227">Next steps</span></span>

<span data-ttu-id="da702-228">To create a distributed table, use one of these statements:</span><span class="sxs-lookup"><span data-stu-id="da702-228">To create a distributed table, use one of these statements:</span></span>

- [<span data-ttu-id="da702-229">CREATE TABLE (Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="da702-229">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="da702-230">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="da702-230">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)


