---
title: Improve columnstore index performance in Azure SQL | Microsoft Docs
description: Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: ''
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 11/18/2016
ms.author: shigu;barbkess
ms.openlocfilehash: f8943c6419b0c2dc13aeb342a5200bbab02b6233
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564311"
---
# <a name="memory-optimizations-for-columnstore-compression"></a><span data-ttu-id="5b7f9-103">Memory optimizations for columnstore compression</span><span class="sxs-lookup"><span data-stu-id="5b7f9-103">Memory optimizations for columnstore compression</span></span>

<span data-ttu-id="5b7f9-104">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-104">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="5b7f9-105">Use these methods to improve compression rates and query performance for columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-105">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="5b7f9-106">Why the rowgroup size matters</span><span class="sxs-lookup"><span data-stu-id="5b7f9-106">Why the rowgroup size matters</span></span>
<span data-ttu-id="5b7f9-107">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-107">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="5b7f9-108">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-108">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="5b7f9-109">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b7f9-109">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="5b7f9-110">Target size for rowgroups</span><span class="sxs-lookup"><span data-stu-id="5b7f9-110">Target size for rowgroups</span></span>
<span data-ttu-id="5b7f9-111">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-111">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="5b7f9-112">A rowgroup can have a maximum of 1,048,576 rows.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-112">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="5b7f9-113">It's okay to not have the maximum number of rows per rowgroup.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-113">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="5b7f9-114">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-114">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="5b7f9-115">Rowgroups can get trimmed during compression</span><span class="sxs-lookup"><span data-stu-id="5b7f9-115">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="5b7f9-116">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-116">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="5b7f9-117">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-117">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span>

<span data-ttu-id="5b7f9-118">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-118">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="5b7f9-119">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="5b7f9-119">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="5b7f9-120">How to estimate memory requirements</span><span class="sxs-lookup"><span data-stu-id="5b7f9-120">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="5b7f9-121">The maximum required memory to compress one rowgroup is approximately</span><span class="sxs-lookup"><span data-stu-id="5b7f9-121">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="5b7f9-122">72 MB +</span><span class="sxs-lookup"><span data-stu-id="5b7f9-122">72 MB +</span></span>
- <span data-ttu-id="5b7f9-123">\#rows \* \#columns \* 8 bytes +</span><span class="sxs-lookup"><span data-stu-id="5b7f9-123">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="5b7f9-124">\#rows \* \#short-string-columns \* 32 bytes +</span><span class="sxs-lookup"><span data-stu-id="5b7f9-124">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="5b7f9-125">\#long-string-columns \* 16 MB for compression dictionary</span><span class="sxs-lookup"><span data-stu-id="5b7f9-125">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="5b7f9-126">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-126">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="5b7f9-127">Long strings are compressed with a compression method designed for compressing text.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-127">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="5b7f9-128">This compression method uses a *dictionary* to store text patterns.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-128">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="5b7f9-129">The maximum size of a dictionary is 16 MB.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-129">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="5b7f9-130">There is only one dictionary for each long string column in the rowgroup.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-130">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="5b7f9-131">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="5b7f9-131">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="5b7f9-132">Ways to reduce memory requirements</span><span class="sxs-lookup"><span data-stu-id="5b7f9-132">Ways to reduce memory requirements</span></span>

<span data-ttu-id="5b7f9-133">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-133">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="5b7f9-134">Use fewer columns</span><span class="sxs-lookup"><span data-stu-id="5b7f9-134">Use fewer columns</span></span>
<span data-ttu-id="5b7f9-135">If possible, design the table with fewer columns.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-135">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="5b7f9-136">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-136">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="5b7f9-137">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-137">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="5b7f9-138">Use fewer string columns</span><span class="sxs-lookup"><span data-stu-id="5b7f9-138">Use fewer string columns</span></span>
<span data-ttu-id="5b7f9-139">Columns of string data types require more memory than numeric and date data types.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-139">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="5b7f9-140">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-140">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="5b7f9-141">Additional memory requirements for string compression:</span><span class="sxs-lookup"><span data-stu-id="5b7f9-141">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="5b7f9-142">String data types up to 32 characters can require 32 additional bytes per value.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-142">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="5b7f9-143">String data types with more than 32 characters are compressed using dictionary methods.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-143">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="5b7f9-144">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-144">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="5b7f9-145">Avoid over-partitioning</span><span class="sxs-lookup"><span data-stu-id="5b7f9-145">Avoid over-partitioning</span></span>

<span data-ttu-id="5b7f9-146">Columnstore indexes create one or more rowgroups per partition.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-146">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="5b7f9-147">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-147">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="5b7f9-148">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-148">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="5b7f9-149">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-149">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="5b7f9-150">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-150">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="5b7f9-151">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-151">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="5b7f9-152">Having too many partitions creates additional memory pressure.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-152">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="5b7f9-153">Simplify the load query</span><span class="sxs-lookup"><span data-stu-id="5b7f9-153">Simplify the load query</span></span>

<span data-ttu-id="5b7f9-154">The database shares the memory grant for a query among all the operators in the query.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-154">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="5b7f9-155">When a load query has complex sorts and joins, the memory available for compression is reduced.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-155">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="5b7f9-156">Design the load query to focus only on loading the query.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-156">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="5b7f9-157">If you need to run transformations on the data, run them separate from the load query.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-157">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="5b7f9-158">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-158">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="5b7f9-159">You can also load the data first and then use the MPP system to transform the data.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-159">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="5b7f9-160">Adjust MAXDOP</span><span class="sxs-lookup"><span data-stu-id="5b7f9-160">Adjust MAXDOP</span></span>

<span data-ttu-id="5b7f9-161">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-161">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="5b7f9-162">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-162">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="5b7f9-163">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-163">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="5b7f9-164">Ways to allocate more memory</span><span class="sxs-lookup"><span data-stu-id="5b7f9-164">Ways to allocate more memory</span></span>

<span data-ttu-id="5b7f9-165">DWU size and the user resource class together determine how much memory is available for a user query.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-165">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="5b7f9-166">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-166">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="5b7f9-167">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="5b7f9-167">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="5b7f9-168">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#change-a-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="5b7f9-168">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#change-a-user-resource-class-example).</span></span>

<span data-ttu-id="5b7f9-169">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-169">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="5b7f9-170">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="5b7f9-170">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="5b7f9-171">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-171">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="5b7f9-172">These examples show how you can run the load query with enough memory.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-172">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="5b7f9-173">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span><span class="sxs-lookup"><span data-stu-id="5b7f9-173">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="5b7f9-174">Using DWU 600 and largerc, your memory grant is 800 MB.</span><span class="sxs-lookup"><span data-stu-id="5b7f9-174">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5b7f9-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b7f9-175">Next steps</span></span>

<span data-ttu-id="5b7f9-176">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="5b7f9-176">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
