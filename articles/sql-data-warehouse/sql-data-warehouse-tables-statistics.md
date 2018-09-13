---
title: Managing statistics on tables in SQL Data Warehouse | Microsoft Docs
description: Getting started with statistics on tables in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 03265f4f1f9d7cddbfde0c4e69fd3a0145611798
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549953"
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="054b2-103">Managing statistics on tables in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="054b2-103">Managing statistics on tables in SQL Data Warehouse</span></span>
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

<span data-ttu-id="054b2-111">The more SQL Data Warehouse knows about your data, the faster it can execute queries against your data.</span><span class="sxs-lookup"><span data-stu-id="054b2-111">The more SQL Data Warehouse knows about your data, the faster it can execute queries against your data.</span></span>  <span data-ttu-id="054b2-112">The way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span><span class="sxs-lookup"><span data-stu-id="054b2-112">The way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="054b2-113">Having statistics on your data is one of the most important things you can do to optimize your queries.</span><span class="sxs-lookup"><span data-stu-id="054b2-113">Having statistics on your data is one of the most important things you can do to optimize your queries.</span></span>  <span data-ttu-id="054b2-114">Statistics help SQL Data Warehouse create the most optimal plan for your queries.</span><span class="sxs-lookup"><span data-stu-id="054b2-114">Statistics help SQL Data Warehouse create the most optimal plan for your queries.</span></span>  <span data-ttu-id="054b2-115">This is because the SQL Data Warehouse query optimizer is a cost based optimizer.</span><span class="sxs-lookup"><span data-stu-id="054b2-115">This is because the SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="054b2-116">That is, it compares the cost of various query plans and then chooses the plan with the lowest cost, which should also be the plan that will execute the fastest.</span><span class="sxs-lookup"><span data-stu-id="054b2-116">That is, it compares the cost of various query plans and then chooses the plan with the lowest cost, which should also be the plan that will execute the fastest.</span></span>

<span data-ttu-id="054b2-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span><span class="sxs-lookup"><span data-stu-id="054b2-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="054b2-118">Statistics are stored in a histogram which captures the range and selectivity of values.</span><span class="sxs-lookup"><span data-stu-id="054b2-118">Statistics are stored in a histogram which captures the range and selectivity of values.</span></span>  <span data-ttu-id="054b2-119">This is of particular interest when the optimizer needs to evaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span><span class="sxs-lookup"><span data-stu-id="054b2-119">This is of particular interest when the optimizer needs to evaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="054b2-120">For example, if the optimizer estimates that the date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span><span class="sxs-lookup"><span data-stu-id="054b2-120">For example, if the optimizer estimates that the date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="054b2-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect the current state of the table.</span><span class="sxs-lookup"><span data-stu-id="054b2-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect the current state of the table.</span></span>  <span data-ttu-id="054b2-122">Having up-to-date statistics ensures that a good plan is selected by the optimizer.</span><span class="sxs-lookup"><span data-stu-id="054b2-122">Having up-to-date statistics ensures that a good plan is selected by the optimizer.</span></span>  <span data-ttu-id="054b2-123">The plans created by the optimizer are only as good as the statistics on your data.</span><span class="sxs-lookup"><span data-stu-id="054b2-123">The plans created by the optimizer are only as good as the statistics on your data.</span></span>

<span data-ttu-id="054b2-124">The process of creating and updating statistics is currently a manual process, but is very simple to do.</span><span class="sxs-lookup"><span data-stu-id="054b2-124">The process of creating and updating statistics is currently a manual process, but is very simple to do.</span></span>  <span data-ttu-id="054b2-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span><span class="sxs-lookup"><span data-stu-id="054b2-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="054b2-126">By using the information below, you can greatly automate the management of the statistics on your data.</span><span class="sxs-lookup"><span data-stu-id="054b2-126">By using the information below, you can greatly automate the management of the statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="054b2-127">Getting started with statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-127">Getting started with statistics</span></span>
 <span data-ttu-id="054b2-128">Creating sampled statistics on every column is an easy way to get started with statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-128">Creating sampled statistics on every column is an easy way to get started with statistics.</span></span>  <span data-ttu-id="054b2-129">Since it is equally important to keep statistics up-to-date, a conservative approach may be to update your statistics daily or after each load.</span><span class="sxs-lookup"><span data-stu-id="054b2-129">Since it is equally important to keep statistics up-to-date, a conservative approach may be to update your statistics daily or after each load.</span></span> <span data-ttu-id="054b2-130">There are always trade-offs between performance and the cost to create and update statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-130">There are always trade-offs between performance and the cost to create and update statistics.</span></span>  <span data-ttu-id="054b2-131">If you find it is taking too long to maintain all of your statistics, you may want to try to be more selective about which columns have statistics or which columns need frequent updating.</span><span class="sxs-lookup"><span data-stu-id="054b2-131">If you find it is taking too long to maintain all of your statistics, you may want to try to be more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="054b2-132">For example, you might want to update date columns daily, as new values may be added rather than after every load.</span><span class="sxs-lookup"><span data-stu-id="054b2-132">For example, you might want to update date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="054b2-133">Again, you will gain the most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span><span class="sxs-lookup"><span data-stu-id="054b2-133">Again, you will gain the most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="054b2-134">If you have a table with a lot of columns which are only used in the SELECT clause, statistics on these columns may not help, and spending a little more effort to identify only the columns where statistics will help, can reduce the time to maintain your statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-134">If you have a table with a lot of columns which are only used in the SELECT clause, statistics on these columns may not help, and spending a little more effort to identify only the columns where statistics will help, can reduce the time to maintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="054b2-135">Multi-column statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-135">Multi-column statistics</span></span>
<span data-ttu-id="054b2-136">In addition to creating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-136">In addition to creating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="054b2-137">Multi-column statistics are statistics created on a list of columns.</span><span class="sxs-lookup"><span data-stu-id="054b2-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="054b2-138">They include single column statistics on the first column in the list, plus some cross-column correlation information called densities.</span><span class="sxs-lookup"><span data-stu-id="054b2-138">They include single column statistics on the first column in the list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="054b2-139">For example, if you have a table that joins to another on two columns, you may find that SQL Data Warehouse can better optimize the plan if it understands the relationship between two columns.</span><span class="sxs-lookup"><span data-stu-id="054b2-139">For example, if you have a table that joins to another on two columns, you may find that SQL Data Warehouse can better optimize the plan if it understands the relationship between two columns.</span></span>   <span data-ttu-id="054b2-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span><span class="sxs-lookup"><span data-stu-id="054b2-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="054b2-141">Updating statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-141">Updating statistics</span></span>
<span data-ttu-id="054b2-142">Updating statistics is an important part of your database management routine.</span><span class="sxs-lookup"><span data-stu-id="054b2-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="054b2-143">When the distribution of data in the database changes, statistics need to be updated.</span><span class="sxs-lookup"><span data-stu-id="054b2-143">When the distribution of data in the database changes, statistics need to be updated.</span></span>  <span data-ttu-id="054b2-144">Out-of-date statistics will lead to sub-optimal query performance.</span><span class="sxs-lookup"><span data-stu-id="054b2-144">Out-of-date statistics will lead to sub-optimal query performance.</span></span>

<span data-ttu-id="054b2-145">One best practice is to update statistics on date columns each day as new dates are added.</span><span class="sxs-lookup"><span data-stu-id="054b2-145">One best practice is to update statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="054b2-146">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span><span class="sxs-lookup"><span data-stu-id="054b2-146">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="054b2-147">These change the data distribution and make the statistics out-of-date.</span><span class="sxs-lookup"><span data-stu-id="054b2-147">These change the data distribution and make the statistics out-of-date.</span></span> <span data-ttu-id="054b2-148">Conversely, statistics on a country column in a customer table might never need to be updated, as the distribution of values doesn’t generally change.</span><span class="sxs-lookup"><span data-stu-id="054b2-148">Conversely, statistics on a country column in a customer table might never need to be updated, as the distribution of values doesn’t generally change.</span></span> <span data-ttu-id="054b2-149">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span><span class="sxs-lookup"><span data-stu-id="054b2-149">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="054b2-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need to update statistics on the country column.</span><span class="sxs-lookup"><span data-stu-id="054b2-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need to update statistics on the country column.</span></span>

<span data-ttu-id="054b2-151">One of the first questions to ask when troubleshooting a query is, "Are the statistics up-to-date?"</span><span class="sxs-lookup"><span data-stu-id="054b2-151">One of the first questions to ask when troubleshooting a query is, "Are the statistics up-to-date?"</span></span>

<span data-ttu-id="054b2-152">This question is not one that can be answered by the age of the data.</span><span class="sxs-lookup"><span data-stu-id="054b2-152">This question is not one that can be answered by the age of the data.</span></span> <span data-ttu-id="054b2-153">An up to date statistics object could be very old if there's been no material change to the underlying data.</span><span class="sxs-lookup"><span data-stu-id="054b2-153">An up to date statistics object could be very old if there's been no material change to the underlying data.</span></span> <span data-ttu-id="054b2-154">When the number of rows has changed substantially or there is a material change in the distribution of values for a given column *then* it's time to update statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-154">When the number of rows has changed substantially or there is a material change in the distribution of values for a given column *then* it's time to update statistics.</span></span>  

<span data-ttu-id="054b2-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span><span class="sxs-lookup"><span data-stu-id="054b2-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="054b2-156">If you have zero rows in the table, when you add rows, you’ll get an automatic update of statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-156">If you have zero rows in the table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="054b2-157">When you add more than 500 rows to a table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows to a total of 999 rows), you’ll get an automatic update</span><span class="sxs-lookup"><span data-stu-id="054b2-157">When you add more than 500 rows to a table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows to a total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="054b2-158">Once you’re over 500 rows you will have to add 500 additional rows + 20% of the size of the table before you’ll see an automatic update on the stats</span><span class="sxs-lookup"><span data-stu-id="054b2-158">Once you’re over 500 rows you will have to add 500 additional rows + 20% of the size of the table before you’ll see an automatic update on the stats</span></span>

<span data-ttu-id="054b2-159">Since there is no DMV to determine if data within the table has changed since the last time statistics were updated, knowing the age of your statistics can provide you with part of the picture.</span><span class="sxs-lookup"><span data-stu-id="054b2-159">Since there is no DMV to determine if data within the table has changed since the last time statistics were updated, knowing the age of your statistics can provide you with part of the picture.</span></span>  <span data-ttu-id="054b2-160">You can use the following query to determine the last time your statistics where updated on each table.</span><span class="sxs-lookup"><span data-stu-id="054b2-160">You can use the following query to determine the last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> Remember if there is a material change in the distribution of values for a given column, you should update statistics regardless of the last time they were updated.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

<span data-ttu-id="054b2-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span><span class="sxs-lookup"><span data-stu-id="054b2-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="054b2-163">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span><span class="sxs-lookup"><span data-stu-id="054b2-163">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="054b2-164">These change the data distribution and make the statistics out-of-date.</span><span class="sxs-lookup"><span data-stu-id="054b2-164">These change the data distribution and make the statistics out-of-date.</span></span>  <span data-ttu-id="054b2-165">Conversely, statistics on a gender column on a customer table might never need to be updated.</span><span class="sxs-lookup"><span data-stu-id="054b2-165">Conversely, statistics on a gender column on a customer table might never need to be updated.</span></span> <span data-ttu-id="054b2-166">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span><span class="sxs-lookup"><span data-stu-id="054b2-166">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="054b2-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need to update statistics on the gender column.</span><span class="sxs-lookup"><span data-stu-id="054b2-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need to update statistics on the gender column.</span></span>

<span data-ttu-id="054b2-168">For further explanation, see [Statistics][Statistics] on MSDN.</span><span class="sxs-lookup"><span data-stu-id="054b2-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="054b2-169">Implementing statistics management</span><span class="sxs-lookup"><span data-stu-id="054b2-169">Implementing statistics management</span></span>
<span data-ttu-id="054b2-170">It is often a good idea to extend your data loading process to ensure that statistics are updated at the end of the load.</span><span class="sxs-lookup"><span data-stu-id="054b2-170">It is often a good idea to extend your data loading process to ensure that statistics are updated at the end of the load.</span></span> <span data-ttu-id="054b2-171">The data load is when tables most frequently change their size and/or their distribution of values.</span><span class="sxs-lookup"><span data-stu-id="054b2-171">The data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="054b2-172">Therefore, this is a logical place to implement some management processes.</span><span class="sxs-lookup"><span data-stu-id="054b2-172">Therefore, this is a logical place to implement some management processes.</span></span>

<span data-ttu-id="054b2-173">Some guiding principles are provided below for updating your statistics during the load process:</span><span class="sxs-lookup"><span data-stu-id="054b2-173">Some guiding principles are provided below for updating your statistics during the load process:</span></span>

* <span data-ttu-id="054b2-174">Ensure that each loaded table has at least one statistics object updated.</span><span class="sxs-lookup"><span data-stu-id="054b2-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="054b2-175">This updates the tables size (row count and page count) information as part of the stats update.</span><span class="sxs-lookup"><span data-stu-id="054b2-175">This updates the tables size (row count and page count) information as part of the stats update.</span></span>
* <span data-ttu-id="054b2-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span><span class="sxs-lookup"><span data-stu-id="054b2-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="054b2-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in the statistics histogram.</span><span class="sxs-lookup"><span data-stu-id="054b2-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in the statistics histogram.</span></span>
* <span data-ttu-id="054b2-178">Consider updating static distribution columns less frequently.</span><span class="sxs-lookup"><span data-stu-id="054b2-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="054b2-179">Remember each statistic object is updated in series.</span><span class="sxs-lookup"><span data-stu-id="054b2-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="054b2-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span><span class="sxs-lookup"><span data-stu-id="054b2-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> For more details on [ascending key] please refer to the SQL Server 2014 cardinality estimation model whitepaper.
> 
> 

<span data-ttu-id="054b2-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span><span class="sxs-lookup"><span data-stu-id="054b2-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="054b2-183">Examples: Create statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-183">Examples: Create statistics</span></span>
<span data-ttu-id="054b2-184">These examples show how to use various options for creating statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-184">These examples show how to use various options for creating statistics.</span></span> <span data-ttu-id="054b2-185">The options that you use for each column depend on the characteristics of your data and how the column will be used in queries.</span><span class="sxs-lookup"><span data-stu-id="054b2-185">The options that you use for each column depend on the characteristics of your data and how the column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="054b2-186">A.</span><span class="sxs-lookup"><span data-stu-id="054b2-186">A.</span></span> <span data-ttu-id="054b2-187">Create single-column statistics with default options</span><span class="sxs-lookup"><span data-stu-id="054b2-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="054b2-188">To create statistics on a column, simply provide a name for the statistics object and the name of the column.</span><span class="sxs-lookup"><span data-stu-id="054b2-188">To create statistics on a column, simply provide a name for the statistics object and the name of the column.</span></span>

<span data-ttu-id="054b2-189">This syntax uses all of the default options.</span><span class="sxs-lookup"><span data-stu-id="054b2-189">This syntax uses all of the default options.</span></span> <span data-ttu-id="054b2-190">By default, SQL Data Warehouse samples 20 percent of the table when it creates statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-190">By default, SQL Data Warehouse samples 20 percent of the table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="054b2-191">For example:</span><span class="sxs-lookup"><span data-stu-id="054b2-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="054b2-192">B.</span><span class="sxs-lookup"><span data-stu-id="054b2-192">B.</span></span> <span data-ttu-id="054b2-193">Create single-column statistics by examining every row</span><span class="sxs-lookup"><span data-stu-id="054b2-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="054b2-194">The default sampling rate of 20 percent is sufficient for most situations.</span><span class="sxs-lookup"><span data-stu-id="054b2-194">The default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="054b2-195">However, you can adjust the sampling rate.</span><span class="sxs-lookup"><span data-stu-id="054b2-195">However, you can adjust the sampling rate.</span></span>

<span data-ttu-id="054b2-196">To sample the full table, use this syntax:</span><span class="sxs-lookup"><span data-stu-id="054b2-196">To sample the full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="054b2-197">For example:</span><span class="sxs-lookup"><span data-stu-id="054b2-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-the-sample-size"></a><span data-ttu-id="054b2-198">C.</span><span class="sxs-lookup"><span data-stu-id="054b2-198">C.</span></span> <span data-ttu-id="054b2-199">Create single-column statistics by specifying the sample size</span><span class="sxs-lookup"><span data-stu-id="054b2-199">Create single-column statistics by specifying the sample size</span></span>
<span data-ttu-id="054b2-200">Alternatively, you can specify the sample size as a percent:</span><span class="sxs-lookup"><span data-stu-id="054b2-200">Alternatively, you can specify the sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-the-rows"></a><span data-ttu-id="054b2-201">D.</span><span class="sxs-lookup"><span data-stu-id="054b2-201">D.</span></span> <span data-ttu-id="054b2-202">Create single-column statistics on only some of the rows</span><span class="sxs-lookup"><span data-stu-id="054b2-202">Create single-column statistics on only some of the rows</span></span>
<span data-ttu-id="054b2-203">Another option, you can create statistics on a portion of the rows in your table.</span><span class="sxs-lookup"><span data-stu-id="054b2-203">Another option, you can create statistics on a portion of the rows in your table.</span></span> <span data-ttu-id="054b2-204">This is called a filtered statistic.</span><span class="sxs-lookup"><span data-stu-id="054b2-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="054b2-205">For example, you could use filtered statistics when you plan to query a specific partition of a large partitioned table.</span><span class="sxs-lookup"><span data-stu-id="054b2-205">For example, you could use filtered statistics when you plan to query a specific partition of a large partitioned table.</span></span> <span data-ttu-id="054b2-206">By creating statistics on only the partition values, the accuracy of the statistics will improve, and therefore improve query performance.</span><span class="sxs-lookup"><span data-stu-id="054b2-206">By creating statistics on only the partition values, the accuracy of the statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="054b2-207">This example creates statistics on a range of values.</span><span class="sxs-lookup"><span data-stu-id="054b2-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="054b2-208">The values could easily be defined to match the range of values in a partition.</span><span class="sxs-lookup"><span data-stu-id="054b2-208">The values could easily be defined to match the range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> For the query optimizer to consider using filtered statistics when it chooses the distributed query plan, the query must fit inside the definition of the statistics object. Using the previous example, the query's where clause needs to specify col1 values between 2000101 and 20001231.
> 
> 

### <a name="e-create-single-column-statistics-with-all-the-options"></a><span data-ttu-id="054b2-211">E.</span><span class="sxs-lookup"><span data-stu-id="054b2-211">E.</span></span> <span data-ttu-id="054b2-212">Create single-column statistics with all the options</span><span class="sxs-lookup"><span data-stu-id="054b2-212">Create single-column statistics with all the options</span></span>
<span data-ttu-id="054b2-213">You can, of course, combine the options together.</span><span class="sxs-lookup"><span data-stu-id="054b2-213">You can, of course, combine the options together.</span></span> <span data-ttu-id="054b2-214">The example below creates a filtered statistics object with a custom sample size:</span><span class="sxs-lookup"><span data-stu-id="054b2-214">The example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="054b2-215">For the full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span><span class="sxs-lookup"><span data-stu-id="054b2-215">For the full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="054b2-216">F.</span><span class="sxs-lookup"><span data-stu-id="054b2-216">F.</span></span> <span data-ttu-id="054b2-217">Create multi-column statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-217">Create multi-column statistics</span></span>
<span data-ttu-id="054b2-218">To create a multi-column statistics, simply use the previous examples, but specify more columns.</span><span class="sxs-lookup"><span data-stu-id="054b2-218">To create a multi-column statistics, simply use the previous examples, but specify more columns.</span></span>

> [!NOTE]
> The histogram, which is used to estimate number of rows in the query result, is only available for the first column listed in the statistics object definition.
> 
> 

<span data-ttu-id="054b2-220">In this example, the histogram is on *product\_category*.</span><span class="sxs-lookup"><span data-stu-id="054b2-220">In this example, the histogram is on *product\_category*.</span></span> <span data-ttu-id="054b2-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="054b2-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="054b2-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at the same time.</span><span class="sxs-lookup"><span data-stu-id="054b2-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at the same time.</span></span>

### <a name="g-create-statistics-on-all-the-columns-in-a-table"></a><span data-ttu-id="054b2-223">G.</span><span class="sxs-lookup"><span data-stu-id="054b2-223">G.</span></span> <span data-ttu-id="054b2-224">Create statistics on all the columns in a table</span><span class="sxs-lookup"><span data-stu-id="054b2-224">Create statistics on all the columns in a table</span></span>
<span data-ttu-id="054b2-225">One way to create statistics is to issues CREATE STATISTICS commands after creating the table.</span><span class="sxs-lookup"><span data-stu-id="054b2-225">One way to create statistics is to issues CREATE STATISTICS commands after creating the table.</span></span>

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-to-create-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="054b2-226">H.</span><span class="sxs-lookup"><span data-stu-id="054b2-226">H.</span></span> <span data-ttu-id="054b2-227">Use a stored procedure to create statistics on all columns in a database</span><span class="sxs-lookup"><span data-stu-id="054b2-227">Use a stored procedure to create statistics on all columns in a database</span></span>
<span data-ttu-id="054b2-228">SQL Data Warehouse does not have a system stored procedure equivalent to [sp_create_stats][] in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="054b2-228">SQL Data Warehouse does not have a system stored procedure equivalent to [sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="054b2-229">This stored procedure creates a single column statistics object on every column of the database that doesn't already have statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-229">This stored procedure creates a single column statistics object on every column of the database that doesn't already have statistics.</span></span>

<span data-ttu-id="054b2-230">This will help you get started with your database design.</span><span class="sxs-lookup"><span data-stu-id="054b2-230">This will help you get started with your database design.</span></span> <span data-ttu-id="054b2-231">Feel free to adapt it to your needs.</span><span class="sxs-lookup"><span data-stu-id="054b2-231">Feel free to adapt it to your needs.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

<span data-ttu-id="054b2-232">To create statistics on all columns in the table with this procedure, simply call the procedure.</span><span class="sxs-lookup"><span data-stu-id="054b2-232">To create statistics on all columns in the table with this procedure, simply call the procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="054b2-233">Examples: update statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-233">Examples: update statistics</span></span>
<span data-ttu-id="054b2-234">To update statistics, you can:</span><span class="sxs-lookup"><span data-stu-id="054b2-234">To update statistics, you can:</span></span>

1. <span data-ttu-id="054b2-235">Update one statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-235">Update one statistics object.</span></span> <span data-ttu-id="054b2-236">Specify the name of the statistics object you wish to update.</span><span class="sxs-lookup"><span data-stu-id="054b2-236">Specify the name of the statistics object you wish to update.</span></span>
2. <span data-ttu-id="054b2-237">Update all statistics objects on a table.</span><span class="sxs-lookup"><span data-stu-id="054b2-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="054b2-238">Specify the name of the table instead of one specific statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-238">Specify the name of the table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="054b2-239">A.</span><span class="sxs-lookup"><span data-stu-id="054b2-239">A.</span></span> <span data-ttu-id="054b2-240">Update one specific statistics object</span><span class="sxs-lookup"><span data-stu-id="054b2-240">Update one specific statistics object</span></span>
<span data-ttu-id="054b2-241">Use the following syntax to update a specific statistics object:</span><span class="sxs-lookup"><span data-stu-id="054b2-241">Use the following syntax to update a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="054b2-242">For example:</span><span class="sxs-lookup"><span data-stu-id="054b2-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="054b2-243">By updating specific statistics objects, you can minimize the time and resources required to manage statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-243">By updating specific statistics objects, you can minimize the time and resources required to manage statistics.</span></span> <span data-ttu-id="054b2-244">This requires some thought, though, to choose the best statistics objects to update.</span><span class="sxs-lookup"><span data-stu-id="054b2-244">This requires some thought, though, to choose the best statistics objects to update.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="054b2-245">B.</span><span class="sxs-lookup"><span data-stu-id="054b2-245">B.</span></span> <span data-ttu-id="054b2-246">Update all statistics on a table</span><span class="sxs-lookup"><span data-stu-id="054b2-246">Update all statistics on a table</span></span>
<span data-ttu-id="054b2-247">This shows a simple method for updating all the statistics objects on a table.</span><span class="sxs-lookup"><span data-stu-id="054b2-247">This shows a simple method for updating all the statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="054b2-248">For example:</span><span class="sxs-lookup"><span data-stu-id="054b2-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="054b2-249">This statement is easy to use.</span><span class="sxs-lookup"><span data-stu-id="054b2-249">This statement is easy to use.</span></span> <span data-ttu-id="054b2-250">Just remember this updates all statistics on the table, and therefore might perform more work than is necessary.</span><span class="sxs-lookup"><span data-stu-id="054b2-250">Just remember this updates all statistics on the table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="054b2-251">If the performance is not an issue, this is definitely the easiest and most complete way to guarantee statistics are up-to-date.</span><span class="sxs-lookup"><span data-stu-id="054b2-251">If the performance is not an issue, this is definitely the easiest and most complete way to guarantee statistics are up-to-date.</span></span>

> [!NOTE]
> When updating all statistics on a table, SQL Data Warehouse does a scan to sample the table for each statistics. If the table is large, has many columns, and many statistics, it might be more efficient to update individual statistics based on need.
> 
> 

<span data-ttu-id="054b2-254">For an implementation of an `UPDATE STATISTICS` procedure please see the [Temporary Tables][Temporary] article.</span><span class="sxs-lookup"><span data-stu-id="054b2-254">For an implementation of an `UPDATE STATISTICS` procedure please see the [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="054b2-255">The implementation method is slightly different to the `CREATE STATISTICS` procedure above but the end result is the same.</span><span class="sxs-lookup"><span data-stu-id="054b2-255">The implementation method is slightly different to the `CREATE STATISTICS` procedure above but the end result is the same.</span></span>

<span data-ttu-id="054b2-256">For the full syntax, see [Update Statistics][Update Statistics] on MSDN.</span><span class="sxs-lookup"><span data-stu-id="054b2-256">For the full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="054b2-257">Statistics metadata</span><span class="sxs-lookup"><span data-stu-id="054b2-257">Statistics metadata</span></span>
<span data-ttu-id="054b2-258">There are several system view and functions that you can use to find information about statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-258">There are several system view and functions that you can use to find information about statistics.</span></span> <span data-ttu-id="054b2-259">For example, you can see if a statistics object might be out-of-date by using the stats-date function to see when statistics were last created or updated.</span><span class="sxs-lookup"><span data-stu-id="054b2-259">For example, you can see if a statistics object might be out-of-date by using the stats-date function to see when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="054b2-260">Catalog views for statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-260">Catalog views for statistics</span></span>
<span data-ttu-id="054b2-261">These system views provide information about statistics:</span><span class="sxs-lookup"><span data-stu-id="054b2-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="054b2-262">Catalog View</span><span class="sxs-lookup"><span data-stu-id="054b2-262">Catalog View</span></span> | <span data-ttu-id="054b2-263">Description</span><span class="sxs-lookup"><span data-stu-id="054b2-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="054b2-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="054b2-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="054b2-265">One row for each column.</span><span class="sxs-lookup"><span data-stu-id="054b2-265">One row for each column.</span></span> |
| <span data-ttu-id="054b2-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="054b2-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="054b2-267">One row for each object in the database.</span><span class="sxs-lookup"><span data-stu-id="054b2-267">One row for each object in the database.</span></span> |
| <span data-ttu-id="054b2-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="054b2-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="054b2-269">One row for each schema in the database.</span><span class="sxs-lookup"><span data-stu-id="054b2-269">One row for each schema in the database.</span></span> |
| <span data-ttu-id="054b2-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="054b2-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="054b2-271">One row for each statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="054b2-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="054b2-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="054b2-273">One row for each column in the statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-273">One row for each column in the statistics object.</span></span> <span data-ttu-id="054b2-274">Links back to sys.columns.</span><span class="sxs-lookup"><span data-stu-id="054b2-274">Links back to sys.columns.</span></span> |
| <span data-ttu-id="054b2-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="054b2-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="054b2-276">One row for each table (includes external tables).</span><span class="sxs-lookup"><span data-stu-id="054b2-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="054b2-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="054b2-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="054b2-278">One row for each data type.</span><span class="sxs-lookup"><span data-stu-id="054b2-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="054b2-279">System functions for statistics</span><span class="sxs-lookup"><span data-stu-id="054b2-279">System functions for statistics</span></span>
<span data-ttu-id="054b2-280">These system functions are useful for working with statistics:</span><span class="sxs-lookup"><span data-stu-id="054b2-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="054b2-281">System Function</span><span class="sxs-lookup"><span data-stu-id="054b2-281">System Function</span></span> | <span data-ttu-id="054b2-282">Description</span><span class="sxs-lookup"><span data-stu-id="054b2-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="054b2-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="054b2-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="054b2-284">Date the statistics object was last updated.</span><span class="sxs-lookup"><span data-stu-id="054b2-284">Date the statistics object was last updated.</span></span> |
| <span data-ttu-id="054b2-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="054b2-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="054b2-286">Provides summary level and detailed information about the distribution of values as understood by the statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-286">Provides summary level and detailed information about the distribution of values as understood by the statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="054b2-287">Combine statistics columns and functions into one view</span><span class="sxs-lookup"><span data-stu-id="054b2-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="054b2-288">This view brings columns that relate to statistics, and results from the [STATS_DATE()][]function together.</span><span class="sxs-lookup"><span data-stu-id="054b2-288">This view brings columns that relate to statistics, and results from the [STATS_DATE()][]function together.</span></span>

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="054b2-289">DBCC SHOW_STATISTICS() examples</span><span class="sxs-lookup"><span data-stu-id="054b2-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="054b2-290">DBCC SHOW_STATISTICS() shows the data held within a statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-290">DBCC SHOW_STATISTICS() shows the data held within a statistics object.</span></span> <span data-ttu-id="054b2-291">This data comes in three parts.</span><span class="sxs-lookup"><span data-stu-id="054b2-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="054b2-292">Header</span><span class="sxs-lookup"><span data-stu-id="054b2-292">Header</span></span>
2. <span data-ttu-id="054b2-293">Density Vector</span><span class="sxs-lookup"><span data-stu-id="054b2-293">Density Vector</span></span>
3. <span data-ttu-id="054b2-294">Histogram</span><span class="sxs-lookup"><span data-stu-id="054b2-294">Histogram</span></span>

<span data-ttu-id="054b2-295">The header metadata about the statistics.</span><span class="sxs-lookup"><span data-stu-id="054b2-295">The header metadata about the statistics.</span></span> <span data-ttu-id="054b2-296">The histogram displays the distribution of values in the first key column of the statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-296">The histogram displays the distribution of values in the first key column of the statistics object.</span></span> <span data-ttu-id="054b2-297">The density vector measures cross-column correlation.</span><span class="sxs-lookup"><span data-stu-id="054b2-297">The density vector measures cross-column correlation.</span></span> <span data-ttu-id="054b2-298">SQLDW computes cardinality estimates with any of the data in the statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-298">SQLDW computes cardinality estimates with any of the data in the statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="054b2-299">Show header, density, and histogram</span><span class="sxs-lookup"><span data-stu-id="054b2-299">Show header, density, and histogram</span></span>
<span data-ttu-id="054b2-300">This simple example shows all three parts of a statistics object.</span><span class="sxs-lookup"><span data-stu-id="054b2-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="054b2-301">For example:</span><span class="sxs-lookup"><span data-stu-id="054b2-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="054b2-302">Show one or more parts of DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="054b2-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="054b2-303">If you are only interested in viewing specific parts, use the `WITH` clause and specify which parts you want to see:</span><span class="sxs-lookup"><span data-stu-id="054b2-303">If you are only interested in viewing specific parts, use the `WITH` clause and specify which parts you want to see:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="054b2-304">For example:</span><span class="sxs-lookup"><span data-stu-id="054b2-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="054b2-305">DBCC SHOW_STATISTICS() differences</span><span class="sxs-lookup"><span data-stu-id="054b2-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="054b2-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="054b2-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared to SQL Server.</span></span>

1. <span data-ttu-id="054b2-307">Undocumented features are not supported</span><span class="sxs-lookup"><span data-stu-id="054b2-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="054b2-308">Cannot use Stats_stream</span><span class="sxs-lookup"><span data-stu-id="054b2-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="054b2-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="054b2-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="054b2-310">NO_INFOMSGS cannot be set for message suppression</span><span class="sxs-lookup"><span data-stu-id="054b2-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="054b2-311">Square brackets around statistics names cannot be used</span><span class="sxs-lookup"><span data-stu-id="054b2-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="054b2-312">Cannot use column names to identify statistics objects</span><span class="sxs-lookup"><span data-stu-id="054b2-312">Cannot use column names to identify statistics objects</span></span>
7. <span data-ttu-id="054b2-313">Custom error 2767 is not supported</span><span class="sxs-lookup"><span data-stu-id="054b2-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="054b2-314">Next steps</span><span class="sxs-lookup"><span data-stu-id="054b2-314">Next steps</span></span>
<span data-ttu-id="054b2-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span><span class="sxs-lookup"><span data-stu-id="054b2-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="054b2-316">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span><span class="sxs-lookup"><span data-stu-id="054b2-316">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="054b2-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="054b2-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
