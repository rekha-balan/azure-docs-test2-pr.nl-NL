---
title: Overview of tables in SQL Data Warehouse | Microsoft Docs
description: Getting started with Azure SQL Data Warehouse Tables.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: barbkess;jrj
ms.openlocfilehash: 914d85267e82ce6a2e60f3841889935046f17c87
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555789"
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="28423-103">Overview of tables in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="28423-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [Overview][Overview]
> * [Data Types][Data Types]
> * [Distribute][Distribute]
> * [Index][Index]
> * [Partition][Partition]
> * [Statistics][Statistics]
> * [Temporary][Temporary]
> 
> 

<span data-ttu-id="28423-111">Getting started with creating tables in SQL Data Warehouse is simple.</span><span class="sxs-lookup"><span data-stu-id="28423-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="28423-112">The basic [CREATE TABLE][CREATE TABLE] syntax follows the common syntax you are most likely already familiar with from working with other databases.</span><span class="sxs-lookup"><span data-stu-id="28423-112">The basic [CREATE TABLE][CREATE TABLE] syntax follows the common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="28423-113">To create a table, you simply need to name your table, name your columns and define data types for each column.</span><span class="sxs-lookup"><span data-stu-id="28423-113">To create a table, you simply need to name your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="28423-114">If you've create tables in other databases, this should look very familiar to you.</span><span class="sxs-lookup"><span data-stu-id="28423-114">If you've create tables in other databases, this should look very familiar to you.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="28423-115">The above example creates a table named Customers with two columns, FirstName and LastName.</span><span class="sxs-lookup"><span data-stu-id="28423-115">The above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="28423-116">Each column is defined with a data type of VARCHAR(25), which limits the data to 25 characters.</span><span class="sxs-lookup"><span data-stu-id="28423-116">Each column is defined with a data type of VARCHAR(25), which limits the data to 25 characters.</span></span>  <span data-ttu-id="28423-117">These fundamental attributes of a table, as well as others, are mostly the same as other databases.</span><span class="sxs-lookup"><span data-stu-id="28423-117">These fundamental attributes of a table, as well as others, are mostly the same as other databases.</span></span>  <span data-ttu-id="28423-118">Data types are defined for each column and ensure the integrity of your data.</span><span class="sxs-lookup"><span data-stu-id="28423-118">Data types are defined for each column and ensure the integrity of your data.</span></span>  <span data-ttu-id="28423-119">Indexes can be added to improve performance by reducing I/O.</span><span class="sxs-lookup"><span data-stu-id="28423-119">Indexes can be added to improve performance by reducing I/O.</span></span>  <span data-ttu-id="28423-120">Partitioning can be added to improve performance when you need to modify data.</span><span class="sxs-lookup"><span data-stu-id="28423-120">Partitioning can be added to improve performance when you need to modify data.</span></span>

<span data-ttu-id="28423-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span><span class="sxs-lookup"><span data-stu-id="28423-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer TO CustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="28423-122">Distributed tables</span><span class="sxs-lookup"><span data-stu-id="28423-122">Distributed tables</span></span>
<span data-ttu-id="28423-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is the **distribution column**.</span><span class="sxs-lookup"><span data-stu-id="28423-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is the **distribution column**.</span></span>  <span data-ttu-id="28423-124">The distribution column is very much what it sounds like.</span><span class="sxs-lookup"><span data-stu-id="28423-124">The distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="28423-125">It is the column that determines how to distribute, or divide, your data behind the scenes.</span><span class="sxs-lookup"><span data-stu-id="28423-125">It is the column that determines how to distribute, or divide, your data behind the scenes.</span></span>  <span data-ttu-id="28423-126">When you create a table without specifying the distribution column, the table is automatically distributed using **round robin**.</span><span class="sxs-lookup"><span data-stu-id="28423-126">When you create a table without specifying the distribution column, the table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="28423-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span><span class="sxs-lookup"><span data-stu-id="28423-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="28423-128">See [Distributing a Table][Distribute] to learn more about how to select a distribution column.</span><span class="sxs-lookup"><span data-stu-id="28423-128">See [Distributing a Table][Distribute] to learn more about how to select a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="28423-129">Indexing and partitioning tables</span><span class="sxs-lookup"><span data-stu-id="28423-129">Indexing and partitioning tables</span></span>
<span data-ttu-id="28423-130">As you become more advanced in using SQL Data Warehouse and want to optimize performance, you'll want to learn more about Table Design.</span><span class="sxs-lookup"><span data-stu-id="28423-130">As you become more advanced in using SQL Data Warehouse and want to optimize performance, you'll want to learn more about Table Design.</span></span>  <span data-ttu-id="28423-131">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span><span class="sxs-lookup"><span data-stu-id="28423-131">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="28423-132">Table statistics</span><span class="sxs-lookup"><span data-stu-id="28423-132">Table statistics</span></span>
<span data-ttu-id="28423-133">Statistics are an extremely important to getting the best performance out of your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="28423-133">Statistics are an extremely important to getting the best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="28423-134">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come to expect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of the most important articles you read to ensure that you get the best performance from your queries.</span><span class="sxs-lookup"><span data-stu-id="28423-134">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come to expect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of the most important articles you read to ensure that you get the best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="28423-135">Temporary tables</span><span class="sxs-lookup"><span data-stu-id="28423-135">Temporary tables</span></span>
<span data-ttu-id="28423-136">Temporary tables are tables which only exist for the duration of your logon and cannot be seen by other users.</span><span class="sxs-lookup"><span data-stu-id="28423-136">Temporary tables are tables which only exist for the duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="28423-137">Temporary tables can be a good way to prevent others from seeing temporary results and also reduce the need for cleanup.</span><span class="sxs-lookup"><span data-stu-id="28423-137">Temporary tables can be a good way to prevent others from seeing temporary results and also reduce the need for cleanup.</span></span>  <span data-ttu-id="28423-138">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span><span class="sxs-lookup"><span data-stu-id="28423-138">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="28423-139">See the [Temporary Table][Temporary] articles for more details about temporary tables.</span><span class="sxs-lookup"><span data-stu-id="28423-139">See the [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="28423-140">External tables</span><span class="sxs-lookup"><span data-stu-id="28423-140">External tables</span></span>
<span data-ttu-id="28423-141">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point to data external from SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="28423-141">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point to data external from SQL Data Warehouse.</span></span>  <span data-ttu-id="28423-142">For example, you can create an external table which points to files on Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="28423-142">For example, you can create an external table which points to files on Azure Blob Storage.</span></span>  <span data-ttu-id="28423-143">For more details on how to create and query an external table, see [Load data with Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="28423-143">For more details on how to create and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="28423-144">Unsupported table features</span><span class="sxs-lookup"><span data-stu-id="28423-144">Unsupported table features</span></span>
<span data-ttu-id="28423-145">While SQL Data Warehouse contains many of the same table features offered by other databases, there are some features which are not yet supported.</span><span class="sxs-lookup"><span data-stu-id="28423-145">While SQL Data Warehouse contains many of the same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="28423-146">Below is a list of some of the table features which are not yet supported.</span><span class="sxs-lookup"><span data-stu-id="28423-146">Below is a list of some of the table features which are not yet supported.</span></span>

| <span data-ttu-id="28423-147">Unsupported features</span><span class="sxs-lookup"><span data-stu-id="28423-147">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="28423-148">[Identity Property][Identity Property] (see [Assigning Surrogate Key Workaround][Assigning Surrogate Key Workaround])</span><span class="sxs-lookup"><span data-stu-id="28423-148">[Identity Property][Identity Property] (see [Assigning Surrogate Key Workaround][Assigning Surrogate Key Workaround])</span></span> |
| <span data-ttu-id="28423-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="28423-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="28423-150">[Unique Indexes][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="28423-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="28423-151">[Computed Columns][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="28423-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="28423-152">[Sparse Columns][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="28423-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="28423-153">[User-Defined Types][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="28423-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="28423-154">[Sequence][Sequence]</span><span class="sxs-lookup"><span data-stu-id="28423-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="28423-155">[Triggers][Triggers]</span><span class="sxs-lookup"><span data-stu-id="28423-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="28423-156">[Indexed Views][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="28423-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="28423-157">[Synonyms][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="28423-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="28423-158">Table size queries</span><span class="sxs-lookup"><span data-stu-id="28423-158">Table size queries</span></span>
<span data-ttu-id="28423-159">One simple way to identify space and rows consumed by a table in each of the 60 distributions, is to use [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="28423-159">One simple way to identify space and rows consumed by a table in each of the 60 distributions, is to use [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="28423-160">However, using DBCC commands can be quite limiting.</span><span class="sxs-lookup"><span data-stu-id="28423-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="28423-161">Dynamic management views (DMVs) will allow you to see much more detail as well as give you much greater control over the query results.</span><span class="sxs-lookup"><span data-stu-id="28423-161">Dynamic management views (DMVs) will allow you to see much more detail as well as give you much greater control over the query results.</span></span>  <span data-ttu-id="28423-162">Start by creating this view, which will be referred to by many of our examples in this and other articles.</span><span class="sxs-lookup"><span data-stu-id="28423-162">Start by creating this view, which will be referred to by many of our examples in this and other articles.</span></span>

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a><span data-ttu-id="28423-163">Table space summary</span><span class="sxs-lookup"><span data-stu-id="28423-163">Table space summary</span></span>
<span data-ttu-id="28423-164">This query returns the rows and space by table.</span><span class="sxs-lookup"><span data-stu-id="28423-164">This query returns the rows and space by table.</span></span>  <span data-ttu-id="28423-165">It is a great query to see which tables are your largest tables and whether they are round robin or hash distributed.</span><span class="sxs-lookup"><span data-stu-id="28423-165">It is a great query to see which tables are your largest tables and whether they are round robin or hash distributed.</span></span>  <span data-ttu-id="28423-166">For hash distributed tables it also shows the distribution column.</span><span class="sxs-lookup"><span data-stu-id="28423-166">For hash distributed tables it also shows the distribution column.</span></span>  <span data-ttu-id="28423-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span><span class="sxs-lookup"><span data-stu-id="28423-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="28423-168">Table space by distribution type</span><span class="sxs-lookup"><span data-stu-id="28423-168">Table space by distribution type</span></span>
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a><span data-ttu-id="28423-169">Table space by index type</span><span class="sxs-lookup"><span data-stu-id="28423-169">Table space by index type</span></span>
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a><span data-ttu-id="28423-170">Distribution space summary</span><span class="sxs-lookup"><span data-stu-id="28423-170">Distribution space summary</span></span>
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a><span data-ttu-id="28423-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="28423-171">Next steps</span></span>
<span data-ttu-id="28423-172">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span><span class="sxs-lookup"><span data-stu-id="28423-172">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="28423-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="28423-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Identity Property]: https://msdn.microsoft.com/library/ms186775.aspx
[Assigning Surrogate Key Workaround]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/18/assigning-surrogate-key-to-dimension-tables-in-sql-dw-and-aps/
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
