---
title: Indexing tables in Azure SQL Data Warehouse | Microsoft Azure
description: Recommendations and examples for indexing tables in Azure SQL Data Warehouse.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: rortloff
ms.reviewer: igorstan
ms.openlocfilehash: d709acfe378583a21b72971f465e4b5d73818bcd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784425"
---
# <a name="indexing-tables-in-sql-data-warehouse"></a><span data-ttu-id="79a29-103">Indexing tables in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="79a29-103">Indexing tables in SQL Data Warehouse</span></span>
<span data-ttu-id="79a29-104">Recommendations and examples for indexing tables in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="79a29-104">Recommendations and examples for indexing tables in Azure SQL Data Warehouse.</span></span>

## <a name="what-are-index-choices"></a><span data-ttu-id="79a29-105">What are index choices?</span><span class="sxs-lookup"><span data-stu-id="79a29-105">What are index choices?</span></span>

<span data-ttu-id="79a29-106">SQL Data Warehouse offers several indexing options including [clustered columnstore indexes](/sql/relational-databases/indexes/columnstore-indexes-overview), [clustered indexes and nonclustered indexes](/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described), and a non-index option also known as [heap](/sql/relational-databases/indexes/heaps-tables-without-clustered-indexes).</span><span class="sxs-lookup"><span data-stu-id="79a29-106">SQL Data Warehouse offers several indexing options including [clustered columnstore indexes](/sql/relational-databases/indexes/columnstore-indexes-overview), [clustered indexes and nonclustered indexes](/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described), and a non-index option also known as [heap](/sql/relational-databases/indexes/heaps-tables-without-clustered-indexes).</span></span>  

<span data-ttu-id="79a29-107">To create a table with an index, see the [CREATE TABLE (Azure SQL Data Warehouse)](/sql/t-sql/statements/create-table-azure-sql-data-warehouse) documentation.</span><span class="sxs-lookup"><span data-stu-id="79a29-107">To create a table with an index, see the [CREATE TABLE (Azure SQL Data Warehouse)](/sql/t-sql/statements/create-table-azure-sql-data-warehouse) documentation.</span></span>

## <a name="clustered-columnstore-indexes"></a><span data-ttu-id="79a29-108">Clustered columnstore indexes</span><span class="sxs-lookup"><span data-stu-id="79a29-108">Clustered columnstore indexes</span></span>
<span data-ttu-id="79a29-109">By default, SQL Data Warehouse creates a clustered columnstore index when no index options are specified on a table.</span><span class="sxs-lookup"><span data-stu-id="79a29-109">By default, SQL Data Warehouse creates a clustered columnstore index when no index options are specified on a table.</span></span> <span data-ttu-id="79a29-110">Clustered columnstore tables offer both the highest level of data compression as well as the best overall query performance.</span><span class="sxs-lookup"><span data-stu-id="79a29-110">Clustered columnstore tables offer both the highest level of data compression as well as the best overall query performance.</span></span>  <span data-ttu-id="79a29-111">Clustered columnstore tables will generally outperform clustered index or heap tables and are usually the best choice for large tables.</span><span class="sxs-lookup"><span data-stu-id="79a29-111">Clustered columnstore tables will generally outperform clustered index or heap tables and are usually the best choice for large tables.</span></span>  <span data-ttu-id="79a29-112">For these reasons, clustered columnstore is the best place to start when you are unsure of how to index your table.</span><span class="sxs-lookup"><span data-stu-id="79a29-112">For these reasons, clustered columnstore is the best place to start when you are unsure of how to index your table.</span></span>  

<span data-ttu-id="79a29-113">To create a clustered columnstore table, simply specify CLUSTERED COLUMNSTORE INDEX in the WITH clause, or leave the WITH clause off:</span><span class="sxs-lookup"><span data-stu-id="79a29-113">To create a clustered columnstore table, simply specify CLUSTERED COLUMNSTORE INDEX in the WITH clause, or leave the WITH clause off:</span></span>

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

<span data-ttu-id="79a29-114">There are a few scenarios where clustered columnstore may not be a good option:</span><span class="sxs-lookup"><span data-stu-id="79a29-114">There are a few scenarios where clustered columnstore may not be a good option:</span></span>

- <span data-ttu-id="79a29-115">Columnstore tables do not support varchar(max), nvarchar(max) and varbinary(max).</span><span class="sxs-lookup"><span data-stu-id="79a29-115">Columnstore tables do not support varchar(max), nvarchar(max) and varbinary(max).</span></span> <span data-ttu-id="79a29-116">Consider heap or clustered index instead.</span><span class="sxs-lookup"><span data-stu-id="79a29-116">Consider heap or clustered index instead.</span></span>
- <span data-ttu-id="79a29-117">Columnstore tables may be less efficient for transient data.</span><span class="sxs-lookup"><span data-stu-id="79a29-117">Columnstore tables may be less efficient for transient data.</span></span> <span data-ttu-id="79a29-118">Consider heap and perhaps even temporary tables.</span><span class="sxs-lookup"><span data-stu-id="79a29-118">Consider heap and perhaps even temporary tables.</span></span>
- <span data-ttu-id="79a29-119">Small tables with less than 100 million rows.</span><span class="sxs-lookup"><span data-stu-id="79a29-119">Small tables with less than 100 million rows.</span></span> <span data-ttu-id="79a29-120">Consider heap tables.</span><span class="sxs-lookup"><span data-stu-id="79a29-120">Consider heap tables.</span></span>

## <a name="heap-tables"></a><span data-ttu-id="79a29-121">Heap tables</span><span class="sxs-lookup"><span data-stu-id="79a29-121">Heap tables</span></span>
<span data-ttu-id="79a29-122">When you are temporarily landing data on SQL Data Warehouse, you may find that using a heap table makes the overall process faster.</span><span class="sxs-lookup"><span data-stu-id="79a29-122">When you are temporarily landing data on SQL Data Warehouse, you may find that using a heap table makes the overall process faster.</span></span> <span data-ttu-id="79a29-123">This is because loads to heaps are faster than to index tables and in some cases the subsequent read can be done from cache.</span><span class="sxs-lookup"><span data-stu-id="79a29-123">This is because loads to heaps are faster than to index tables and in some cases the subsequent read can be done from cache.</span></span>  <span data-ttu-id="79a29-124">If you are loading data only to stage it before running more transformations, loading the table to heap table is much faster than loading the data to a clustered columnstore table.</span><span class="sxs-lookup"><span data-stu-id="79a29-124">If you are loading data only to stage it before running more transformations, loading the table to heap table is much faster than loading the data to a clustered columnstore table.</span></span> <span data-ttu-id="79a29-125">In addition, loading data to a [temporary table](sql-data-warehouse-tables-temporary.md) loads faster than loading a table to permanent storage.</span><span class="sxs-lookup"><span data-stu-id="79a29-125">In addition, loading data to a [temporary table](sql-data-warehouse-tables-temporary.md) loads faster than loading a table to permanent storage.</span></span>  

<span data-ttu-id="79a29-126">For small lookup tables, less than 100 million rows, often heap tables make sense.</span><span class="sxs-lookup"><span data-stu-id="79a29-126">For small lookup tables, less than 100 million rows, often heap tables make sense.</span></span>  <span data-ttu-id="79a29-127">Cluster columnstore tables begin to achieve optimal compression once there is more than 100 million rows.</span><span class="sxs-lookup"><span data-stu-id="79a29-127">Cluster columnstore tables begin to achieve optimal compression once there is more than 100 million rows.</span></span>

<span data-ttu-id="79a29-128">To create a heap table, simply specify HEAP in the WITH clause:</span><span class="sxs-lookup"><span data-stu-id="79a29-128">To create a heap table, simply specify HEAP in the WITH clause:</span></span>

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a><span data-ttu-id="79a29-129">Clustered and nonclustered indexes</span><span class="sxs-lookup"><span data-stu-id="79a29-129">Clustered and nonclustered indexes</span></span>
<span data-ttu-id="79a29-130">Clustered indexes may outperform clustered columnstore tables when a single row needs to be quickly retrieved.</span><span class="sxs-lookup"><span data-stu-id="79a29-130">Clustered indexes may outperform clustered columnstore tables when a single row needs to be quickly retrieved.</span></span> <span data-ttu-id="79a29-131">For queries where a single or very few row lookup is required to performance with extreme speed, consider a cluster index or nonclustered secondary index.</span><span class="sxs-lookup"><span data-stu-id="79a29-131">For queries where a single or very few row lookup is required to performance with extreme speed, consider a cluster index or nonclustered secondary index.</span></span> <span data-ttu-id="79a29-132">The disadvantage to using a clustered index is that only queries that benefit are the ones that use a highly selective filter on the clustered index column.</span><span class="sxs-lookup"><span data-stu-id="79a29-132">The disadvantage to using a clustered index is that only queries that benefit are the ones that use a highly selective filter on the clustered index column.</span></span> <span data-ttu-id="79a29-133">To improve filter on other columns a nonclustered index can be added to other columns.</span><span class="sxs-lookup"><span data-stu-id="79a29-133">To improve filter on other columns a nonclustered index can be added to other columns.</span></span> <span data-ttu-id="79a29-134">However, each index which is added to a table adds both space and processing time to loads.</span><span class="sxs-lookup"><span data-stu-id="79a29-134">However, each index which is added to a table adds both space and processing time to loads.</span></span>

<span data-ttu-id="79a29-135">To create a clustered index table, simply specify CLUSTERED INDEX in the WITH clause:</span><span class="sxs-lookup"><span data-stu-id="79a29-135">To create a clustered index table, simply specify CLUSTERED INDEX in the WITH clause:</span></span>

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

<span data-ttu-id="79a29-136">To add a non-clustered index on a table, simply use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="79a29-136">To add a non-clustered index on a table, simply use the following syntax:</span></span>

```SQL
CREATE INDEX zipCodeIndex ON myTable (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a><span data-ttu-id="79a29-137">Optimizing clustered columnstore indexes</span><span class="sxs-lookup"><span data-stu-id="79a29-137">Optimizing clustered columnstore indexes</span></span>
<span data-ttu-id="79a29-138">Clustered columnstore tables are organized in data into segments.</span><span class="sxs-lookup"><span data-stu-id="79a29-138">Clustered columnstore tables are organized in data into segments.</span></span>  <span data-ttu-id="79a29-139">Having high segment quality is critical to achieving optimal query performance on a columnstore table.</span><span class="sxs-lookup"><span data-stu-id="79a29-139">Having high segment quality is critical to achieving optimal query performance on a columnstore table.</span></span>  <span data-ttu-id="79a29-140">Segment quality can be measured by the number of rows in a compressed row group.</span><span class="sxs-lookup"><span data-stu-id="79a29-140">Segment quality can be measured by the number of rows in a compressed row group.</span></span>  <span data-ttu-id="79a29-141">Segment quality is most optimal where there are at least 100K rows per compressed row group and gain in performance as the number of rows per row group approach 1,048,576 rows, which is the most rows a row group can contain.</span><span class="sxs-lookup"><span data-stu-id="79a29-141">Segment quality is most optimal where there are at least 100K rows per compressed row group and gain in performance as the number of rows per row group approach 1,048,576 rows, which is the most rows a row group can contain.</span></span>

<span data-ttu-id="79a29-142">The below view can be created and used on your system to compute the average rows per row group and identify any sub-optimal cluster columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="79a29-142">The below view can be created and used on your system to compute the average rows per row group and identify any sub-optimal cluster columnstore indexes.</span></span>  <span data-ttu-id="79a29-143">The last column on this view generates a SQL statement which can be used to rebuild your indexes.</span><span class="sxs-lookup"><span data-stu-id="79a29-143">The last column on this view generates a SQL statement which can be used to rebuild your indexes.</span></span>

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

<span data-ttu-id="79a29-144">Now that you have created the view, run this query to identify tables with row groups with less than 100K rows.</span><span class="sxs-lookup"><span data-stu-id="79a29-144">Now that you have created the view, run this query to identify tables with row groups with less than 100K rows.</span></span> <span data-ttu-id="79a29-145">Of course, you may want to increase the threshold of 100K if you are looking for more optimal segment quality.</span><span class="sxs-lookup"><span data-stu-id="79a29-145">Of course, you may want to increase the threshold of 100K if you are looking for more optimal segment quality.</span></span> 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

<span data-ttu-id="79a29-146">Once you have run the query you can begin to look at the data and analyze your results.</span><span class="sxs-lookup"><span data-stu-id="79a29-146">Once you have run the query you can begin to look at the data and analyze your results.</span></span> <span data-ttu-id="79a29-147">This table explains what to look for in your row group analysis.</span><span class="sxs-lookup"><span data-stu-id="79a29-147">This table explains what to look for in your row group analysis.</span></span>

| <span data-ttu-id="79a29-148">Column</span><span class="sxs-lookup"><span data-stu-id="79a29-148">Column</span></span> | <span data-ttu-id="79a29-149">How to use this data</span><span class="sxs-lookup"><span data-stu-id="79a29-149">How to use this data</span></span> |
| --- | --- |
| <span data-ttu-id="79a29-150">[table_partition_count]</span><span class="sxs-lookup"><span data-stu-id="79a29-150">[table_partition_count]</span></span> |<span data-ttu-id="79a29-151">If the table is partitioned, then you may expect to see higher Open row group counts.</span><span class="sxs-lookup"><span data-stu-id="79a29-151">If the table is partitioned, then you may expect to see higher Open row group counts.</span></span> <span data-ttu-id="79a29-152">Each partition in the distribution could in theory have an open row group associated with it.</span><span class="sxs-lookup"><span data-stu-id="79a29-152">Each partition in the distribution could in theory have an open row group associated with it.</span></span> <span data-ttu-id="79a29-153">Factor this into your analysis.</span><span class="sxs-lookup"><span data-stu-id="79a29-153">Factor this into your analysis.</span></span> <span data-ttu-id="79a29-154">A small table that has been partitioned could be optimized by removing the partitioning altogether as this would improve compression.</span><span class="sxs-lookup"><span data-stu-id="79a29-154">A small table that has been partitioned could be optimized by removing the partitioning altogether as this would improve compression.</span></span> |
| <span data-ttu-id="79a29-155">[row_count_total]</span><span class="sxs-lookup"><span data-stu-id="79a29-155">[row_count_total]</span></span> |<span data-ttu-id="79a29-156">Total row count for the table.</span><span class="sxs-lookup"><span data-stu-id="79a29-156">Total row count for the table.</span></span> <span data-ttu-id="79a29-157">For example, you can use this value to calculate percentage of rows in the compressed state.</span><span class="sxs-lookup"><span data-stu-id="79a29-157">For example, you can use this value to calculate percentage of rows in the compressed state.</span></span> |
| <span data-ttu-id="79a29-158">[row_count_per_distribution_MAX]</span><span class="sxs-lookup"><span data-stu-id="79a29-158">[row_count_per_distribution_MAX]</span></span> |<span data-ttu-id="79a29-159">If all rows are evenly distributed this value would be the target number of rows per distribution.</span><span class="sxs-lookup"><span data-stu-id="79a29-159">If all rows are evenly distributed this value would be the target number of rows per distribution.</span></span> <span data-ttu-id="79a29-160">Compare this value with the compressed_rowgroup_count.</span><span class="sxs-lookup"><span data-stu-id="79a29-160">Compare this value with the compressed_rowgroup_count.</span></span> |
| <span data-ttu-id="79a29-161">[COMPRESSED_rowgroup_rows]</span><span class="sxs-lookup"><span data-stu-id="79a29-161">[COMPRESSED_rowgroup_rows]</span></span> |<span data-ttu-id="79a29-162">Total number of rows in columnstore format for the table.</span><span class="sxs-lookup"><span data-stu-id="79a29-162">Total number of rows in columnstore format for the table.</span></span> |
| <span data-ttu-id="79a29-163">[COMPRESSED_rowgroup_rows_AVG]</span><span class="sxs-lookup"><span data-stu-id="79a29-163">[COMPRESSED_rowgroup_rows_AVG]</span></span> |<span data-ttu-id="79a29-164">If the average number of rows is significantly less than the maximum # of rows for a row group, then consider using CTAS or ALTER INDEX REBUILD to recompress the data</span><span class="sxs-lookup"><span data-stu-id="79a29-164">If the average number of rows is significantly less than the maximum # of rows for a row group, then consider using CTAS or ALTER INDEX REBUILD to recompress the data</span></span> |
| <span data-ttu-id="79a29-165">[COMPRESSED_rowgroup_count]</span><span class="sxs-lookup"><span data-stu-id="79a29-165">[COMPRESSED_rowgroup_count]</span></span> |<span data-ttu-id="79a29-166">Number of row groups in columnstore format.</span><span class="sxs-lookup"><span data-stu-id="79a29-166">Number of row groups in columnstore format.</span></span> <span data-ttu-id="79a29-167">If this number is very high in relation to the table it is an indicator that the columnstore density is low.</span><span class="sxs-lookup"><span data-stu-id="79a29-167">If this number is very high in relation to the table it is an indicator that the columnstore density is low.</span></span> |
| <span data-ttu-id="79a29-168">[COMPRESSED_rowgroup_rows_DELETED]</span><span class="sxs-lookup"><span data-stu-id="79a29-168">[COMPRESSED_rowgroup_rows_DELETED]</span></span> |<span data-ttu-id="79a29-169">Rows are logically deleted in columnstore format.</span><span class="sxs-lookup"><span data-stu-id="79a29-169">Rows are logically deleted in columnstore format.</span></span> <span data-ttu-id="79a29-170">If the number is high relative to table size, consider recreating the partition or rebuilding the index as this removes them physically.</span><span class="sxs-lookup"><span data-stu-id="79a29-170">If the number is high relative to table size, consider recreating the partition or rebuilding the index as this removes them physically.</span></span> |
| <span data-ttu-id="79a29-171">[COMPRESSED_rowgroup_rows_MIN]</span><span class="sxs-lookup"><span data-stu-id="79a29-171">[COMPRESSED_rowgroup_rows_MIN]</span></span> |<span data-ttu-id="79a29-172">Use this in conjunction with the AVG and MAX columns to understand the range of values for the row groups in your columnstore.</span><span class="sxs-lookup"><span data-stu-id="79a29-172">Use this in conjunction with the AVG and MAX columns to understand the range of values for the row groups in your columnstore.</span></span> <span data-ttu-id="79a29-173">A low number over the load threshold (102,400 per partition aligned distribution) suggests that optimizations are available in the data load</span><span class="sxs-lookup"><span data-stu-id="79a29-173">A low number over the load threshold (102,400 per partition aligned distribution) suggests that optimizations are available in the data load</span></span> |
| <span data-ttu-id="79a29-174">[COMPRESSED_rowgroup_rows_MAX]</span><span class="sxs-lookup"><span data-stu-id="79a29-174">[COMPRESSED_rowgroup_rows_MAX]</span></span> |<span data-ttu-id="79a29-175">As above</span><span class="sxs-lookup"><span data-stu-id="79a29-175">As above</span></span> |
| <span data-ttu-id="79a29-176">[OPEN_rowgroup_count]</span><span class="sxs-lookup"><span data-stu-id="79a29-176">[OPEN_rowgroup_count]</span></span> |<span data-ttu-id="79a29-177">Open row groups are normal.</span><span class="sxs-lookup"><span data-stu-id="79a29-177">Open row groups are normal.</span></span> <span data-ttu-id="79a29-178">One would reasonably expect one OPEN row group per table distribution (60).</span><span class="sxs-lookup"><span data-stu-id="79a29-178">One would reasonably expect one OPEN row group per table distribution (60).</span></span> <span data-ttu-id="79a29-179">Excessive numbers suggest data loading across partitions.</span><span class="sxs-lookup"><span data-stu-id="79a29-179">Excessive numbers suggest data loading across partitions.</span></span> <span data-ttu-id="79a29-180">Double check the partitioning strategy to make sure it is sound</span><span class="sxs-lookup"><span data-stu-id="79a29-180">Double check the partitioning strategy to make sure it is sound</span></span> |
| <span data-ttu-id="79a29-181">[OPEN_rowgroup_rows]</span><span class="sxs-lookup"><span data-stu-id="79a29-181">[OPEN_rowgroup_rows]</span></span> |<span data-ttu-id="79a29-182">Each row group can have 1,048,576 rows in it as a maximum.</span><span class="sxs-lookup"><span data-stu-id="79a29-182">Each row group can have 1,048,576 rows in it as a maximum.</span></span> <span data-ttu-id="79a29-183">Use this value to see how full the open row groups are currently</span><span class="sxs-lookup"><span data-stu-id="79a29-183">Use this value to see how full the open row groups are currently</span></span> |
| <span data-ttu-id="79a29-184">[OPEN_rowgroup_rows_MIN]</span><span class="sxs-lookup"><span data-stu-id="79a29-184">[OPEN_rowgroup_rows_MIN]</span></span> |<span data-ttu-id="79a29-185">Open groups indicate that data is either being trickle loaded into the table or that the previous load spilled over remaining rows into this row group.</span><span class="sxs-lookup"><span data-stu-id="79a29-185">Open groups indicate that data is either being trickle loaded into the table or that the previous load spilled over remaining rows into this row group.</span></span> <span data-ttu-id="79a29-186">Use the MIN, MAX, AVG columns to see how much data is sat in OPEN row groups.</span><span class="sxs-lookup"><span data-stu-id="79a29-186">Use the MIN, MAX, AVG columns to see how much data is sat in OPEN row groups.</span></span> <span data-ttu-id="79a29-187">For small tables it could be 100% of all the data!</span><span class="sxs-lookup"><span data-stu-id="79a29-187">For small tables it could be 100% of all the data!</span></span> <span data-ttu-id="79a29-188">In which case ALTER INDEX REBUILD to force the data to columnstore.</span><span class="sxs-lookup"><span data-stu-id="79a29-188">In which case ALTER INDEX REBUILD to force the data to columnstore.</span></span> |
| <span data-ttu-id="79a29-189">[OPEN_rowgroup_rows_MAX]</span><span class="sxs-lookup"><span data-stu-id="79a29-189">[OPEN_rowgroup_rows_MAX]</span></span> |<span data-ttu-id="79a29-190">As above</span><span class="sxs-lookup"><span data-stu-id="79a29-190">As above</span></span> |
| <span data-ttu-id="79a29-191">[OPEN_rowgroup_rows_AVG]</span><span class="sxs-lookup"><span data-stu-id="79a29-191">[OPEN_rowgroup_rows_AVG]</span></span> |<span data-ttu-id="79a29-192">As above</span><span class="sxs-lookup"><span data-stu-id="79a29-192">As above</span></span> |
| <span data-ttu-id="79a29-193">[CLOSED_rowgroup_rows]</span><span class="sxs-lookup"><span data-stu-id="79a29-193">[CLOSED_rowgroup_rows]</span></span> |<span data-ttu-id="79a29-194">Look at the closed row group rows as a sanity check.</span><span class="sxs-lookup"><span data-stu-id="79a29-194">Look at the closed row group rows as a sanity check.</span></span> |
| <span data-ttu-id="79a29-195">[CLOSED_rowgroup_count]</span><span class="sxs-lookup"><span data-stu-id="79a29-195">[CLOSED_rowgroup_count]</span></span> |<span data-ttu-id="79a29-196">The number of closed row groups should be low if any are seen at all.</span><span class="sxs-lookup"><span data-stu-id="79a29-196">The number of closed row groups should be low if any are seen at all.</span></span> <span data-ttu-id="79a29-197">Closed row groups can be converted to compressed row groups using the ALTER INDEX ... REORGANIZE command.</span><span class="sxs-lookup"><span data-stu-id="79a29-197">Closed row groups can be converted to compressed row groups using the ALTER INDEX ... REORGANIZE command.</span></span> <span data-ttu-id="79a29-198">However, this is not normally required.</span><span class="sxs-lookup"><span data-stu-id="79a29-198">However, this is not normally required.</span></span> <span data-ttu-id="79a29-199">Closed groups are automatically converted to columnstore row groups by the background "tuple mover" process.</span><span class="sxs-lookup"><span data-stu-id="79a29-199">Closed groups are automatically converted to columnstore row groups by the background "tuple mover" process.</span></span> |
| <span data-ttu-id="79a29-200">[CLOSED_rowgroup_rows_MIN]</span><span class="sxs-lookup"><span data-stu-id="79a29-200">[CLOSED_rowgroup_rows_MIN]</span></span> |<span data-ttu-id="79a29-201">Closed row groups should have a very high fill rate.</span><span class="sxs-lookup"><span data-stu-id="79a29-201">Closed row groups should have a very high fill rate.</span></span> <span data-ttu-id="79a29-202">If the fill rate for a closed row group is low, then further analysis of the columnstore is required.</span><span class="sxs-lookup"><span data-stu-id="79a29-202">If the fill rate for a closed row group is low, then further analysis of the columnstore is required.</span></span> |
| <span data-ttu-id="79a29-203">[CLOSED_rowgroup_rows_MAX]</span><span class="sxs-lookup"><span data-stu-id="79a29-203">[CLOSED_rowgroup_rows_MAX]</span></span> |<span data-ttu-id="79a29-204">As above</span><span class="sxs-lookup"><span data-stu-id="79a29-204">As above</span></span> |
| <span data-ttu-id="79a29-205">[CLOSED_rowgroup_rows_AVG]</span><span class="sxs-lookup"><span data-stu-id="79a29-205">[CLOSED_rowgroup_rows_AVG]</span></span> |<span data-ttu-id="79a29-206">As above</span><span class="sxs-lookup"><span data-stu-id="79a29-206">As above</span></span> |
| <span data-ttu-id="79a29-207">[Rebuild_Index_SQL]</span><span class="sxs-lookup"><span data-stu-id="79a29-207">[Rebuild_Index_SQL]</span></span> |<span data-ttu-id="79a29-208">SQL to rebuild columnstore index for a table</span><span class="sxs-lookup"><span data-stu-id="79a29-208">SQL to rebuild columnstore index for a table</span></span> |

## <a name="causes-of-poor-columnstore-index-quality"></a><span data-ttu-id="79a29-209">Causes of poor columnstore index quality</span><span class="sxs-lookup"><span data-stu-id="79a29-209">Causes of poor columnstore index quality</span></span>
<span data-ttu-id="79a29-210">If you have identified tables with poor segment quality, you want to identify the root cause.</span><span class="sxs-lookup"><span data-stu-id="79a29-210">If you have identified tables with poor segment quality, you want to identify the root cause.</span></span>  <span data-ttu-id="79a29-211">Below are some other common causes of poor segment quality:</span><span class="sxs-lookup"><span data-stu-id="79a29-211">Below are some other common causes of poor segment quality:</span></span>

1. <span data-ttu-id="79a29-212">Memory pressure when index was built</span><span class="sxs-lookup"><span data-stu-id="79a29-212">Memory pressure when index was built</span></span>
2. <span data-ttu-id="79a29-213">High volume of DML operations</span><span class="sxs-lookup"><span data-stu-id="79a29-213">High volume of DML operations</span></span>
3. <span data-ttu-id="79a29-214">Small or trickle load operations</span><span class="sxs-lookup"><span data-stu-id="79a29-214">Small or trickle load operations</span></span>
4. <span data-ttu-id="79a29-215">Too many partitions</span><span class="sxs-lookup"><span data-stu-id="79a29-215">Too many partitions</span></span>

<span data-ttu-id="79a29-216">These factors can cause a columnstore index to have significantly less than the optimal 1 million rows per row group.</span><span class="sxs-lookup"><span data-stu-id="79a29-216">These factors can cause a columnstore index to have significantly less than the optimal 1 million rows per row group.</span></span> <span data-ttu-id="79a29-217">They can also cause rows to go to the delta row group instead of a compressed row group.</span><span class="sxs-lookup"><span data-stu-id="79a29-217">They can also cause rows to go to the delta row group instead of a compressed row group.</span></span> 

### <a name="memory-pressure-when-index-was-built"></a><span data-ttu-id="79a29-218">Memory pressure when index was built</span><span class="sxs-lookup"><span data-stu-id="79a29-218">Memory pressure when index was built</span></span>
<span data-ttu-id="79a29-219">The number of rows per compressed row group are directly related to the width of the row and the amount of memory available to process the row group.</span><span class="sxs-lookup"><span data-stu-id="79a29-219">The number of rows per compressed row group are directly related to the width of the row and the amount of memory available to process the row group.</span></span>  <span data-ttu-id="79a29-220">When rows are written to columnstore tables under memory pressure, columnstore segment quality may suffer.</span><span class="sxs-lookup"><span data-stu-id="79a29-220">When rows are written to columnstore tables under memory pressure, columnstore segment quality may suffer.</span></span>  <span data-ttu-id="79a29-221">Therefore, the best practice is to give the session which is writing to your columnstore index tables access to as much memory as possible.</span><span class="sxs-lookup"><span data-stu-id="79a29-221">Therefore, the best practice is to give the session which is writing to your columnstore index tables access to as much memory as possible.</span></span>  <span data-ttu-id="79a29-222">Since there is a trade-off between memory and concurrency, the guidance on the right memory allocation depends on the data in each row of your table, the data warehouse units allocated to your system, and the number of concurrency slots you can give to the session which is writing data to your table.</span><span class="sxs-lookup"><span data-stu-id="79a29-222">Since there is a trade-off between memory and concurrency, the guidance on the right memory allocation depends on the data in each row of your table, the data warehouse units allocated to your system, and the number of concurrency slots you can give to the session which is writing data to your table.</span></span>  <span data-ttu-id="79a29-223">As a best practice, we recommend starting with xlargerc if you are using DW300 or less, largerc if you are using DW400 to DW600, and mediumrc if you are using DW1000 and above.</span><span class="sxs-lookup"><span data-stu-id="79a29-223">As a best practice, we recommend starting with xlargerc if you are using DW300 or less, largerc if you are using DW400 to DW600, and mediumrc if you are using DW1000 and above.</span></span>

### <a name="high-volume-of-dml-operations"></a><span data-ttu-id="79a29-224">High volume of DML operations</span><span class="sxs-lookup"><span data-stu-id="79a29-224">High volume of DML operations</span></span>
<span data-ttu-id="79a29-225">A high volume of DML operations that update and delete rows can introduce inefficiency into the columnstore.</span><span class="sxs-lookup"><span data-stu-id="79a29-225">A high volume of DML operations that update and delete rows can introduce inefficiency into the columnstore.</span></span> <span data-ttu-id="79a29-226">This is especially true when the majority of the rows in a row group are modified.</span><span class="sxs-lookup"><span data-stu-id="79a29-226">This is especially true when the majority of the rows in a row group are modified.</span></span>

- <span data-ttu-id="79a29-227">Deleting a row from a compressed row group only logically marks the row as deleted.</span><span class="sxs-lookup"><span data-stu-id="79a29-227">Deleting a row from a compressed row group only logically marks the row as deleted.</span></span> <span data-ttu-id="79a29-228">The row remains in the compressed row group until the partition or table is rebuilt.</span><span class="sxs-lookup"><span data-stu-id="79a29-228">The row remains in the compressed row group until the partition or table is rebuilt.</span></span>
- <span data-ttu-id="79a29-229">Inserting a row adds the row to an internal rowstore table called a delta row group.</span><span class="sxs-lookup"><span data-stu-id="79a29-229">Inserting a row adds the row to an internal rowstore table called a delta row group.</span></span> <span data-ttu-id="79a29-230">The inserted row is not converted to columnstore until the delta row group is full and is marked as closed.</span><span class="sxs-lookup"><span data-stu-id="79a29-230">The inserted row is not converted to columnstore until the delta row group is full and is marked as closed.</span></span> <span data-ttu-id="79a29-231">Row groups are closed once they reach the maximum capacity of 1,048,576 rows.</span><span class="sxs-lookup"><span data-stu-id="79a29-231">Row groups are closed once they reach the maximum capacity of 1,048,576 rows.</span></span> 
- <span data-ttu-id="79a29-232">Updating a row in columnstore format is processed as a logical delete and then an insert.</span><span class="sxs-lookup"><span data-stu-id="79a29-232">Updating a row in columnstore format is processed as a logical delete and then an insert.</span></span> <span data-ttu-id="79a29-233">The inserted row may be stored in the delta store.</span><span class="sxs-lookup"><span data-stu-id="79a29-233">The inserted row may be stored in the delta store.</span></span>

<span data-ttu-id="79a29-234">Batched update and insert operations that exceed the bulk threshold of 102,400 rows per partition-aligned distribution go directly to the columnstore format.</span><span class="sxs-lookup"><span data-stu-id="79a29-234">Batched update and insert operations that exceed the bulk threshold of 102,400 rows per partition-aligned distribution go directly to the columnstore format.</span></span> <span data-ttu-id="79a29-235">However, assuming an even distribution, you would need to be modifying more than 6.144 million rows in a single operation for this to occur.</span><span class="sxs-lookup"><span data-stu-id="79a29-235">However, assuming an even distribution, you would need to be modifying more than 6.144 million rows in a single operation for this to occur.</span></span> <span data-ttu-id="79a29-236">If the number of rows for a given partition-aligned distribution is less than 102,400 then the rows go to the delta store andstay there until sufficient rows have been inserted or modified to close the row group or the index has been rebuilt.</span><span class="sxs-lookup"><span data-stu-id="79a29-236">If the number of rows for a given partition-aligned distribution is less than 102,400 then the rows go to the delta store andstay there until sufficient rows have been inserted or modified to close the row group or the index has been rebuilt.</span></span>

### <a name="small-or-trickle-load-operations"></a><span data-ttu-id="79a29-237">Small or trickle load operations</span><span class="sxs-lookup"><span data-stu-id="79a29-237">Small or trickle load operations</span></span>
<span data-ttu-id="79a29-238">Small loads that flow into SQL Data Warehouse are also sometimes known as trickle loads.</span><span class="sxs-lookup"><span data-stu-id="79a29-238">Small loads that flow into SQL Data Warehouse are also sometimes known as trickle loads.</span></span> <span data-ttu-id="79a29-239">They typically represent a near constant stream of data being ingested by the system.</span><span class="sxs-lookup"><span data-stu-id="79a29-239">They typically represent a near constant stream of data being ingested by the system.</span></span> <span data-ttu-id="79a29-240">However, as this stream is near continuous the volume of rows is not particularly large.</span><span class="sxs-lookup"><span data-stu-id="79a29-240">However, as this stream is near continuous the volume of rows is not particularly large.</span></span> <span data-ttu-id="79a29-241">More often than not the data is significantly under the threshold required for a direct load to columnstore format.</span><span class="sxs-lookup"><span data-stu-id="79a29-241">More often than not the data is significantly under the threshold required for a direct load to columnstore format.</span></span>

<span data-ttu-id="79a29-242">In these situations, it is often better to land the data first in Azure blob storage and let it accumulate prior to loading.</span><span class="sxs-lookup"><span data-stu-id="79a29-242">In these situations, it is often better to land the data first in Azure blob storage and let it accumulate prior to loading.</span></span> <span data-ttu-id="79a29-243">This technique is often known as *micro-batching*.</span><span class="sxs-lookup"><span data-stu-id="79a29-243">This technique is often known as *micro-batching*.</span></span>

### <a name="too-many-partitions"></a><span data-ttu-id="79a29-244">Too many partitions</span><span class="sxs-lookup"><span data-stu-id="79a29-244">Too many partitions</span></span>
<span data-ttu-id="79a29-245">Another thing to consider is the impact of partitioning on your clustered columnstore tables.</span><span class="sxs-lookup"><span data-stu-id="79a29-245">Another thing to consider is the impact of partitioning on your clustered columnstore tables.</span></span>  <span data-ttu-id="79a29-246">Before partitioning, SQL Data Warehouse already divides your data into 60 databases.</span><span class="sxs-lookup"><span data-stu-id="79a29-246">Before partitioning, SQL Data Warehouse already divides your data into 60 databases.</span></span>  <span data-ttu-id="79a29-247">Partitioning further divides your data.</span><span class="sxs-lookup"><span data-stu-id="79a29-247">Partitioning further divides your data.</span></span>  <span data-ttu-id="79a29-248">If you partition your data, then consider that **each** partition needs at least 1 million rows to benefit from a clustered columnstore index.</span><span class="sxs-lookup"><span data-stu-id="79a29-248">If you partition your data, then consider that **each** partition needs at least 1 million rows to benefit from a clustered columnstore index.</span></span>  <span data-ttu-id="79a29-249">If you partition your table into 100 partitions, then your table needs at least 6 billion rows to benefit from a clustered columnstore index (60 distributions \* 100 partitions \* 1 million rows).</span><span class="sxs-lookup"><span data-stu-id="79a29-249">If you partition your table into 100 partitions, then your table needs at least 6 billion rows to benefit from a clustered columnstore index (60 distributions \* 100 partitions \* 1 million rows).</span></span> <span data-ttu-id="79a29-250">If your 100-partition table does not have 6 billion rows, either reduce the number of partitions or consider using a heap table instead.</span><span class="sxs-lookup"><span data-stu-id="79a29-250">If your 100-partition table does not have 6 billion rows, either reduce the number of partitions or consider using a heap table instead.</span></span>

<span data-ttu-id="79a29-251">Once your tables have been loaded with some data, follow the below steps to identify and rebuild tables with sub-optimal clustered columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="79a29-251">Once your tables have been loaded with some data, follow the below steps to identify and rebuild tables with sub-optimal clustered columnstore indexes.</span></span>

## <a name="rebuilding-indexes-to-improve-segment-quality"></a><span data-ttu-id="79a29-252">Rebuilding indexes to improve segment quality</span><span class="sxs-lookup"><span data-stu-id="79a29-252">Rebuilding indexes to improve segment quality</span></span>
### <a name="step-1-identify-or-create-user-which-uses-the-right-resource-class"></a><span data-ttu-id="79a29-253">Step 1: Identify or create user which uses the right resource class</span><span class="sxs-lookup"><span data-stu-id="79a29-253">Step 1: Identify or create user which uses the right resource class</span></span>
<span data-ttu-id="79a29-254">One quick way to immediately improve segment quality is to rebuild the index.</span><span class="sxs-lookup"><span data-stu-id="79a29-254">One quick way to immediately improve segment quality is to rebuild the index.</span></span>  <span data-ttu-id="79a29-255">The SQL returned by the above view returns an ALTER INDEX REBUILD statement which can be used to rebuild your indexes.</span><span class="sxs-lookup"><span data-stu-id="79a29-255">The SQL returned by the above view returns an ALTER INDEX REBUILD statement which can be used to rebuild your indexes.</span></span> <span data-ttu-id="79a29-256">When rebuilding your indexes, be sure that you allocate enough memory to the session that rebuilds your index.</span><span class="sxs-lookup"><span data-stu-id="79a29-256">When rebuilding your indexes, be sure that you allocate enough memory to the session that rebuilds your index.</span></span>  <span data-ttu-id="79a29-257">To do this, increase the resource class of a user which has permissions to rebuild the index on this table to the recommended minimum.</span><span class="sxs-lookup"><span data-stu-id="79a29-257">To do this, increase the resource class of a user which has permissions to rebuild the index on this table to the recommended minimum.</span></span> <span data-ttu-id="79a29-258">The resource class of the database owner user cannot be changed, so if you have not created a user on the system, you need to do so first.</span><span class="sxs-lookup"><span data-stu-id="79a29-258">The resource class of the database owner user cannot be changed, so if you have not created a user on the system, you need to do so first.</span></span> <span data-ttu-id="79a29-259">The minimum recommended resource class is xlargerc if you are using DW300 or less, largerc if you are using DW400 to DW600, and mediumrc if you are using DW1000 and above.</span><span class="sxs-lookup"><span data-stu-id="79a29-259">The minimum recommended resource class is xlargerc if you are using DW300 or less, largerc if you are using DW400 to DW600, and mediumrc if you are using DW1000 and above.</span></span>

<span data-ttu-id="79a29-260">Below is an example of how to allocate more memory to a user by increasing their resource class.</span><span class="sxs-lookup"><span data-stu-id="79a29-260">Below is an example of how to allocate more memory to a user by increasing their resource class.</span></span> <span data-ttu-id="79a29-261">To work with resource classes, see [Resource classes for workload management](resource-classes-for-workload-management.md).</span><span class="sxs-lookup"><span data-stu-id="79a29-261">To work with resource classes, see [Resource classes for workload management](resource-classes-for-workload-management.md).</span></span>

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a><span data-ttu-id="79a29-262">Step 2: Rebuild clustered columnstore indexes with higher resource class user</span><span class="sxs-lookup"><span data-stu-id="79a29-262">Step 2: Rebuild clustered columnstore indexes with higher resource class user</span></span>
<span data-ttu-id="79a29-263">Log in as the user from step 1 (e.g. LoadUser), which is now using a higher resource class, and execute the ALTER INDEX statements.</span><span class="sxs-lookup"><span data-stu-id="79a29-263">Log in as the user from step 1 (e.g. LoadUser), which is now using a higher resource class, and execute the ALTER INDEX statements.</span></span> <span data-ttu-id="79a29-264">Be sure that this user has ALTER permission to the tables where the index is being rebuilt.</span><span class="sxs-lookup"><span data-stu-id="79a29-264">Be sure that this user has ALTER permission to the tables where the index is being rebuilt.</span></span> <span data-ttu-id="79a29-265">These examples show how to rebuild the entire columnstore index or how to rebuild a single partition.</span><span class="sxs-lookup"><span data-stu-id="79a29-265">These examples show how to rebuild the entire columnstore index or how to rebuild a single partition.</span></span> <span data-ttu-id="79a29-266">On large tables, it is more practical to rebuild indexes a single partition at a time.</span><span class="sxs-lookup"><span data-stu-id="79a29-266">On large tables, it is more practical to rebuild indexes a single partition at a time.</span></span>

<span data-ttu-id="79a29-267">Alternatively, instead of rebuilding the index, you could copy the table to a new table [using CTAS](sql-data-warehouse-develop-ctas.md).</span><span class="sxs-lookup"><span data-stu-id="79a29-267">Alternatively, instead of rebuilding the index, you could copy the table to a new table [using CTAS](sql-data-warehouse-develop-ctas.md).</span></span> <span data-ttu-id="79a29-268">Which way is best?</span><span class="sxs-lookup"><span data-stu-id="79a29-268">Which way is best?</span></span> <span data-ttu-id="79a29-269">For large volumes of data, CTAS is usually faster than [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="79a29-269">For large volumes of data, CTAS is usually faster than [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql).</span></span> <span data-ttu-id="79a29-270">For smaller volumes of data, ALTER INDEX is easier to use and won't require you to swap out the table.</span><span class="sxs-lookup"><span data-stu-id="79a29-270">For smaller volumes of data, ALTER INDEX is easier to use and won't require you to swap out the table.</span></span> <span data-ttu-id="79a29-271">See **Rebuilding indexes with CTAS and partition switching** below for more details on how to rebuild indexes with CTAS.</span><span class="sxs-lookup"><span data-stu-id="79a29-271">See **Rebuilding indexes with CTAS and partition switching** below for more details on how to rebuild indexes with CTAS.</span></span>

```sql
-- Rebuild the entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

<span data-ttu-id="79a29-272">Rebuilding an index in SQL Data Warehouse is an offline operation.</span><span class="sxs-lookup"><span data-stu-id="79a29-272">Rebuilding an index in SQL Data Warehouse is an offline operation.</span></span>  <span data-ttu-id="79a29-273">For more information about rebuilding indexes, see the ALTER INDEX REBUILD section in [Columnstore Indexes Defragmentation](/sql/relational-databases/indexes/columnstore-indexes-defragmentation), and [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="79a29-273">For more information about rebuilding indexes, see the ALTER INDEX REBUILD section in [Columnstore Indexes Defragmentation](/sql/relational-databases/indexes/columnstore-indexes-defragmentation), and [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql).</span></span>

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a><span data-ttu-id="79a29-274">Step 3: Verify clustered columnstore segment quality has improved</span><span class="sxs-lookup"><span data-stu-id="79a29-274">Step 3: Verify clustered columnstore segment quality has improved</span></span>
<span data-ttu-id="79a29-275">Rerun the query which identified table with poor segment quality and verify segment quality has improved.</span><span class="sxs-lookup"><span data-stu-id="79a29-275">Rerun the query which identified table with poor segment quality and verify segment quality has improved.</span></span>  <span data-ttu-id="79a29-276">If segment quality did not improve, it could be that the rows in your table are extra wide.</span><span class="sxs-lookup"><span data-stu-id="79a29-276">If segment quality did not improve, it could be that the rows in your table are extra wide.</span></span>  <span data-ttu-id="79a29-277">Consider using a higher resource class or DWU when rebuilding your indexes.</span><span class="sxs-lookup"><span data-stu-id="79a29-277">Consider using a higher resource class or DWU when rebuilding your indexes.</span></span>

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a><span data-ttu-id="79a29-278">Rebuilding indexes with CTAS and partition switching</span><span class="sxs-lookup"><span data-stu-id="79a29-278">Rebuilding indexes with CTAS and partition switching</span></span>
<span data-ttu-id="79a29-279">This example uses the [CREATE TABLE AS SELECT (CTAS)](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) statement and partition switching to rebuild a table partition.</span><span class="sxs-lookup"><span data-stu-id="79a29-279">This example uses the [CREATE TABLE AS SELECT (CTAS)](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) statement and partition switching to rebuild a table partition.</span></span> 

```sql
-- Step 1: Select the partition of data and write it out to a new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT the data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 TO  [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN the rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 TO  [dbo].[FactInternetSales] PARTITION 2;
```

<span data-ttu-id="79a29-280">For more details about re-creating partitions using CTAS, see [Using partitions in SQL Data Warehouse](sql-data-warehouse-tables-partition.md).</span><span class="sxs-lookup"><span data-stu-id="79a29-280">For more details about re-creating partitions using CTAS, see [Using partitions in SQL Data Warehouse](sql-data-warehouse-tables-partition.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="79a29-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="79a29-281">Next steps</span></span>
<span data-ttu-id="79a29-282">For more information about developing tables, see [Developing tables](sql-data-warehouse-tables-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79a29-282">For more information about developing tables, see [Developing tables](sql-data-warehouse-tables-overview.md).</span></span>

