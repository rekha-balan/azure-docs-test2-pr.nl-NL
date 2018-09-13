---
title: Distributing tables in SQL Data Warehouse | Microsoft Docs
description: Getting started with distributing tables in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: ''
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: fe47cc1e5489d094f08b771cc8ec89de84509972
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661915"
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="d99d5-103">Distributing tables in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d99d5-103">Distributing tables in SQL Data Warehouse</span></span>
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

<span data-ttu-id="d99d5-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span><span class="sxs-lookup"><span data-stu-id="d99d5-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="d99d5-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span><span class="sxs-lookup"><span data-stu-id="d99d5-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="d99d5-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span><span class="sxs-lookup"><span data-stu-id="d99d5-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="d99d5-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span><span class="sxs-lookup"><span data-stu-id="d99d5-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="d99d5-115">Understanding data movement</span><span class="sxs-lookup"><span data-stu-id="d99d5-115">Understanding data movement</span></span>
<span data-ttu-id="d99d5-116">In an MPP system, the data from each table is divided across several underlying databases.</span><span class="sxs-lookup"><span data-stu-id="d99d5-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="d99d5-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span><span class="sxs-lookup"><span data-stu-id="d99d5-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="d99d5-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span><span class="sxs-lookup"><span data-stu-id="d99d5-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="d99d5-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span><span class="sxs-lookup"><span data-stu-id="d99d5-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="d99d5-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span><span class="sxs-lookup"><span data-stu-id="d99d5-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="d99d5-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span><span class="sxs-lookup"><span data-stu-id="d99d5-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="d99d5-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span><span class="sxs-lookup"><span data-stu-id="d99d5-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="d99d5-123">But when this extra step can be avoided, naturally your query will run faster.</span><span class="sxs-lookup"><span data-stu-id="d99d5-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="d99d5-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span><span class="sxs-lookup"><span data-stu-id="d99d5-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="d99d5-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span><span class="sxs-lookup"><span data-stu-id="d99d5-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="d99d5-126">The trick is figuring out which is less work.</span><span class="sxs-lookup"><span data-stu-id="d99d5-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="d99d5-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span><span class="sxs-lookup"><span data-stu-id="d99d5-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="d99d5-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span><span class="sxs-lookup"><span data-stu-id="d99d5-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="d99d5-129">Select distribution method</span><span class="sxs-lookup"><span data-stu-id="d99d5-129">Select distribution method</span></span>
<span data-ttu-id="d99d5-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span><span class="sxs-lookup"><span data-stu-id="d99d5-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="d99d5-131">Each individual database is referred to as a **distribution**.</span><span class="sxs-lookup"><span data-stu-id="d99d5-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="d99d5-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="d99d5-133">The distribution method is defined at the table level and currently there are two choices:</span><span class="sxs-lookup"><span data-stu-id="d99d5-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="d99d5-134">**Round robin** which distribute data evenly but randomly.</span><span class="sxs-lookup"><span data-stu-id="d99d5-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="d99d5-135">**Hash Distributed** which distributes data based on hashing values from a single column</span><span class="sxs-lookup"><span data-stu-id="d99d5-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="d99d5-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span><span class="sxs-lookup"><span data-stu-id="d99d5-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="d99d5-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span><span class="sxs-lookup"><span data-stu-id="d99d5-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="d99d5-138">Round Robin Tables</span><span class="sxs-lookup"><span data-stu-id="d99d5-138">Round Robin Tables</span></span>
<span data-ttu-id="d99d5-139">Using the Round Robin method of distributing data is very much how it sounds.</span><span class="sxs-lookup"><span data-stu-id="d99d5-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="d99d5-140">As your data is loaded, each row is simply sent to the next distribution.</span><span class="sxs-lookup"><span data-stu-id="d99d5-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="d99d5-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="d99d5-142">That is, there is no sorting done during the round robin process which places your data.</span><span class="sxs-lookup"><span data-stu-id="d99d5-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="d99d5-143">A round robin distribution is sometimes called a random hash for this reason.</span><span class="sxs-lookup"><span data-stu-id="d99d5-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="d99d5-144">With a round-robin distributed table there is no need to understand the data.</span><span class="sxs-lookup"><span data-stu-id="d99d5-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="d99d5-145">For this reason, Round-Robin tables often make good loading targets.</span><span class="sxs-lookup"><span data-stu-id="d99d5-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="d99d5-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span><span class="sxs-lookup"><span data-stu-id="d99d5-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="d99d5-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span><span class="sxs-lookup"><span data-stu-id="d99d5-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="d99d5-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span><span class="sxs-lookup"><span data-stu-id="d99d5-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="d99d5-149">This extra step can slow down your queries.</span><span class="sxs-lookup"><span data-stu-id="d99d5-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="d99d5-150">Consider using Round Robin distribution for your table in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="d99d5-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="d99d5-151">When getting started as a simple starting point</span><span class="sxs-lookup"><span data-stu-id="d99d5-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="d99d5-152">If there is no obvious joining key</span><span class="sxs-lookup"><span data-stu-id="d99d5-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="d99d5-153">If there is not good candidate column for hash distributing the table</span><span class="sxs-lookup"><span data-stu-id="d99d5-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="d99d5-154">If the table does not share a common join key with other tables</span><span class="sxs-lookup"><span data-stu-id="d99d5-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="d99d5-155">If the join is less significant than other joins in the query</span><span class="sxs-lookup"><span data-stu-id="d99d5-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="d99d5-156">When the table is a temporary staging table</span><span class="sxs-lookup"><span data-stu-id="d99d5-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="d99d5-157">Both of these examples will create a Round Robin Table:</span><span class="sxs-lookup"><span data-stu-id="d99d5-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
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
;

-- Explicitly Created Round Robin Table
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
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="d99d5-159">Hash Distributed Tables</span><span class="sxs-lookup"><span data-stu-id="d99d5-159">Hash Distributed Tables</span></span>
<span data-ttu-id="d99d5-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span><span class="sxs-lookup"><span data-stu-id="d99d5-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="d99d5-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span><span class="sxs-lookup"><span data-stu-id="d99d5-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="d99d5-162">The distribution column is what determines how the data is divided across your distributed databases.</span><span class="sxs-lookup"><span data-stu-id="d99d5-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="d99d5-163">The hash function uses the distribution column to assign rows to distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="d99d5-164">The hashing algorithm and resulting distribution is deterministic.</span><span class="sxs-lookup"><span data-stu-id="d99d5-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="d99d5-165">That is the same value with the same data type will always has to the same distribution.</span><span class="sxs-lookup"><span data-stu-id="d99d5-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="d99d5-166">This example will create a table distributed on id:</span><span class="sxs-lookup"><span data-stu-id="d99d5-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="d99d5-167">Select distribution column</span><span class="sxs-lookup"><span data-stu-id="d99d5-167">Select distribution column</span></span>
<span data-ttu-id="d99d5-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span><span class="sxs-lookup"><span data-stu-id="d99d5-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="d99d5-169">When selecting a distribution column, there are three major factors to consider.</span><span class="sxs-lookup"><span data-stu-id="d99d5-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="d99d5-170">Select a single column which will:</span><span class="sxs-lookup"><span data-stu-id="d99d5-170">Select a single column which will:</span></span>

1. <span data-ttu-id="d99d5-171">Not be updated</span><span class="sxs-lookup"><span data-stu-id="d99d5-171">Not be updated</span></span>
2. <span data-ttu-id="d99d5-172">Distribute data evenly, avoiding data skew</span><span class="sxs-lookup"><span data-stu-id="d99d5-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="d99d5-173">Minimize data movement</span><span class="sxs-lookup"><span data-stu-id="d99d5-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="d99d5-174">Select distribution column which will not be updated</span><span class="sxs-lookup"><span data-stu-id="d99d5-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="d99d5-175">Distribution columns are not updatable, therefore, select a column with static values.</span><span class="sxs-lookup"><span data-stu-id="d99d5-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="d99d5-176">If a column will need to be updated, it is generally not a good distribution candidate.</span><span class="sxs-lookup"><span data-stu-id="d99d5-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="d99d5-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span><span class="sxs-lookup"><span data-stu-id="d99d5-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="d99d5-178">Select distribution column which will distribute data evenly</span><span class="sxs-lookup"><span data-stu-id="d99d5-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="d99d5-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span><span class="sxs-lookup"><span data-stu-id="d99d5-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="d99d5-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span><span class="sxs-lookup"><span data-stu-id="d99d5-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="d99d5-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span><span class="sxs-lookup"><span data-stu-id="d99d5-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="d99d5-182">When work is well divided across the system, the data is balanced across the distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="d99d5-183">When data is not evenly balanced, we call this **data skew**.</span><span class="sxs-lookup"><span data-stu-id="d99d5-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="d99d5-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span><span class="sxs-lookup"><span data-stu-id="d99d5-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="d99d5-185">Select a column which contains a significant number of distinct values.</span><span class="sxs-lookup"><span data-stu-id="d99d5-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="d99d5-186">Avoid distributing data on columns with a few distinct values.</span><span class="sxs-lookup"><span data-stu-id="d99d5-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="d99d5-187">Avoid distributing data on columns with a high frequency of nulls.</span><span class="sxs-lookup"><span data-stu-id="d99d5-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="d99d5-188">Avoid distributing data on date columns.</span><span class="sxs-lookup"><span data-stu-id="d99d5-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="d99d5-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span><span class="sxs-lookup"><span data-stu-id="d99d5-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="d99d5-190">To illustrate, consider a case where a column only has 40 unique values.</span><span class="sxs-lookup"><span data-stu-id="d99d5-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="d99d5-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span><span class="sxs-lookup"><span data-stu-id="d99d5-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="d99d5-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="d99d5-193">This scenario is an example of data skew.</span><span class="sxs-lookup"><span data-stu-id="d99d5-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="d99d5-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span><span class="sxs-lookup"><span data-stu-id="d99d5-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="d99d5-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span><span class="sxs-lookup"><span data-stu-id="d99d5-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="d99d5-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span><span class="sxs-lookup"><span data-stu-id="d99d5-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="d99d5-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="d99d5-198">Data skew will lead to processing skew.</span><span class="sxs-lookup"><span data-stu-id="d99d5-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="d99d5-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span><span class="sxs-lookup"><span data-stu-id="d99d5-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="d99d5-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span><span class="sxs-lookup"><span data-stu-id="d99d5-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="d99d5-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span><span class="sxs-lookup"><span data-stu-id="d99d5-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="d99d5-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="d99d5-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span><span class="sxs-lookup"><span data-stu-id="d99d5-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="d99d5-204">Select distribution column which will minimize data movement</span><span class="sxs-lookup"><span data-stu-id="d99d5-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="d99d5-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d99d5-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="d99d5-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span><span class="sxs-lookup"><span data-stu-id="d99d5-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="d99d5-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span><span class="sxs-lookup"><span data-stu-id="d99d5-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="d99d5-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span><span class="sxs-lookup"><span data-stu-id="d99d5-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="d99d5-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span><span class="sxs-lookup"><span data-stu-id="d99d5-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="d99d5-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span><span class="sxs-lookup"><span data-stu-id="d99d5-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="d99d5-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span><span class="sxs-lookup"><span data-stu-id="d99d5-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="d99d5-212">There are a few key criteria which must be met to avoid data movement during a join:</span><span class="sxs-lookup"><span data-stu-id="d99d5-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="d99d5-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span><span class="sxs-lookup"><span data-stu-id="d99d5-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="d99d5-214">The data types of the join columns must match between both tables.</span><span class="sxs-lookup"><span data-stu-id="d99d5-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="d99d5-215">The columns must be joined with an equals operator.</span><span class="sxs-lookup"><span data-stu-id="d99d5-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="d99d5-216">The join type may not be a `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="d99d5-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="d99d5-217">Troubleshooting data skew</span><span class="sxs-lookup"><span data-stu-id="d99d5-217">Troubleshooting data skew</span></span>
<span data-ttu-id="d99d5-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span><span class="sxs-lookup"><span data-stu-id="d99d5-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="d99d5-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span><span class="sxs-lookup"><span data-stu-id="d99d5-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="d99d5-220">Depending on the degree of the data skew you might need to address it.</span><span class="sxs-lookup"><span data-stu-id="d99d5-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="d99d5-221">Identifying skew</span><span class="sxs-lookup"><span data-stu-id="d99d5-221">Identifying skew</span></span>
<span data-ttu-id="d99d5-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="d99d5-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="d99d5-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span><span class="sxs-lookup"><span data-stu-id="d99d5-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="d99d5-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="d99d5-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span><span class="sxs-lookup"><span data-stu-id="d99d5-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="d99d5-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span><span class="sxs-lookup"><span data-stu-id="d99d5-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="d99d5-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span><span class="sxs-lookup"><span data-stu-id="d99d5-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="d99d5-228">Resolving data skew</span><span class="sxs-lookup"><span data-stu-id="d99d5-228">Resolving data skew</span></span>
<span data-ttu-id="d99d5-229">Not all skew is enough to warrant a fix.</span><span class="sxs-lookup"><span data-stu-id="d99d5-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="d99d5-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span><span class="sxs-lookup"><span data-stu-id="d99d5-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="d99d5-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span><span class="sxs-lookup"><span data-stu-id="d99d5-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="d99d5-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span><span class="sxs-lookup"><span data-stu-id="d99d5-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="d99d5-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span><span class="sxs-lookup"><span data-stu-id="d99d5-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="d99d5-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span><span class="sxs-lookup"><span data-stu-id="d99d5-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="d99d5-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span><span class="sxs-lookup"><span data-stu-id="d99d5-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="d99d5-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span><span class="sxs-lookup"><span data-stu-id="d99d5-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="d99d5-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span><span class="sxs-lookup"><span data-stu-id="d99d5-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="d99d5-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span><span class="sxs-lookup"><span data-stu-id="d99d5-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="d99d5-239">Here are two examples of how resolve data skew:</span><span class="sxs-lookup"><span data-stu-id="d99d5-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="d99d5-240">Example 1: Re-create the table with a new distribution column</span><span class="sxs-lookup"><span data-stu-id="d99d5-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="d99d5-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span><span class="sxs-lookup"><span data-stu-id="d99d5-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

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

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="d99d5-242">Example 2: Re-create the table using round robin distribution</span><span class="sxs-lookup"><span data-stu-id="d99d5-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="d99d5-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span><span class="sxs-lookup"><span data-stu-id="d99d5-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="d99d5-244">This change will produce even data distribution at the cost of increased data movement.</span><span class="sxs-lookup"><span data-stu-id="d99d5-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
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
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="d99d5-245">Next steps</span><span class="sxs-lookup"><span data-stu-id="d99d5-245">Next steps</span></span>
<span data-ttu-id="d99d5-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span><span class="sxs-lookup"><span data-stu-id="d99d5-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="d99d5-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="d99d5-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
