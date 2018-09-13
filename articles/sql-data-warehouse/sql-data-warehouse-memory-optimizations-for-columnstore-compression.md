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
# <a name="memory-optimizations-for-columnstore-compression"></a>Memory optimizations for columnstore compression

Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.  Use these methods to improve compression rates and query performance for columnstore indexes.

## <a name="why-the-rowgroup-size-matters"></a>Why the rowgroup size matters
Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance. When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.

For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Target size for rowgroups
For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index. A rowgroup can have a maximum of 1,048,576 rows. It's okay to not have the maximum number of rows per rowgroup. Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Rowgroups can get trimmed during compression

During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup. When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.

When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.

For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-to-estimate-memory-requirements"></a>How to estimate memory requirements

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

The maximum required memory to compress one rowgroup is approximately

- 72 MB +
- \#rows \* \#columns \* 8 bytes +
- \#rows \* \#short-string-columns \* 32 bytes +
- \#long-string-columns \* 16 MB for compression dictionary

where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.

Long strings are compressed with a compression method designed for compressing text. This compression method uses a *dictionary* to store text patterns. The maximum size of a dictionary is 16 MB. There is only one dictionary for each long string column in the rowgroup.

For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).

## <a name="ways-to-reduce-memory-requirements"></a>Ways to reduce memory requirements

Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.

### <a name="use-fewer-columns"></a>Use fewer columns
If possible, design the table with fewer columns. When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately. Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.


### <a name="use-fewer-string-columns"></a>Use fewer string columns
Columns of string data types require more memory than numeric and date data types. To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.

Additional memory requirements for string compression:

- String data types up to 32 characters can require 32 additional bytes per value.
- String data types with more than 32 characters are compressed using dictionary methods.  Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.

### <a name="avoid-over-partitioning"></a>Avoid over-partitioning

Columnstore indexes create one or more rowgroups per partition. In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned. If the table has too many partitions, there might not be enough rows to fill the rowgroups. The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.

Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table. During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed. Having too many partitions creates additional memory pressure.

### <a name="simplify-the-load-query"></a>Simplify the load query

The database shares the memory grant for a query among all the operators in the query. When a load query has complex sorts and joins, the memory available for compression is reduced.

Design the load query to focus only on loading the query. If you need to run transformations on the data, run them separate from the load query. For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index. You can also load the data first and then use the MPP system to transform the data.

### <a name="adjust-maxdop"></a>Adjust MAXDOP

Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution. The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.

To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a>Ways to allocate more memory

DWU size and the user resource class together determine how much memory is available for a user query. To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.

- To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#change-a-user-resource-class-example).

For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution. For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).

Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes. These examples show how you can run the load query with enough memory.

- Using DWU 1000 and mediumrc, your memory grant is 800 MB
- Using DWU 600 and largerc, your memory grant is 800 MB.


## <a name="next-steps"></a>Next steps

To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
