---
title: Data types for tables in SQL Data Warehouse | Microsoft Docs
description: Getting started with data types for Azure SQL Data Warehouse tables.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: ''
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c85f0d8d0975add3b9554eb0f6fbc6d7830eb4db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553772"
---
# <a name="data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="f0f36-103">Data types for tables in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f0f36-103">Data types for tables in SQL Data Warehouse</span></span>
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

<span data-ttu-id="f0f36-111">SQL Data Warehouse supports the most commonly used data types.</span><span class="sxs-lookup"><span data-stu-id="f0f36-111">SQL Data Warehouse supports the most commonly used data types.</span></span>  <span data-ttu-id="f0f36-112">Below is a list of the data types supported by SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f0f36-112">Below is a list of the data types supported by SQL Data Warehouse.</span></span>  <span data-ttu-id="f0f36-113">For additional details on data type support, see [create table][create table].</span><span class="sxs-lookup"><span data-stu-id="f0f36-113">For additional details on data type support, see [create table][create table].</span></span>

| <span data-ttu-id="f0f36-114">**Supported Data Types**</span><span class="sxs-lookup"><span data-stu-id="f0f36-114">**Supported Data Types**</span></span> |  |  |
| --- | --- | --- |
| <span data-ttu-id="f0f36-115">[bigint][bigint]</span><span class="sxs-lookup"><span data-stu-id="f0f36-115">[bigint][bigint]</span></span> |<span data-ttu-id="f0f36-116">[decimal][decimal]</span><span class="sxs-lookup"><span data-stu-id="f0f36-116">[decimal][decimal]</span></span> |<span data-ttu-id="f0f36-117">[smallint][smallint]</span><span class="sxs-lookup"><span data-stu-id="f0f36-117">[smallint][smallint]</span></span> |
| <span data-ttu-id="f0f36-118">[binary][binary]</span><span class="sxs-lookup"><span data-stu-id="f0f36-118">[binary][binary]</span></span> |<span data-ttu-id="f0f36-119">[float][float]</span><span class="sxs-lookup"><span data-stu-id="f0f36-119">[float][float]</span></span> |<span data-ttu-id="f0f36-120">[smallmoney][smallmoney]</span><span class="sxs-lookup"><span data-stu-id="f0f36-120">[smallmoney][smallmoney]</span></span> |
| <span data-ttu-id="f0f36-121">[bit][bit]</span><span class="sxs-lookup"><span data-stu-id="f0f36-121">[bit][bit]</span></span> |<span data-ttu-id="f0f36-122">[int][int]</span><span class="sxs-lookup"><span data-stu-id="f0f36-122">[int][int]</span></span> |<span data-ttu-id="f0f36-123">[sysname][sysname]</span><span class="sxs-lookup"><span data-stu-id="f0f36-123">[sysname][sysname]</span></span> |
| <span data-ttu-id="f0f36-124">[char][char]</span><span class="sxs-lookup"><span data-stu-id="f0f36-124">[char][char]</span></span> |<span data-ttu-id="f0f36-125">[money][money]</span><span class="sxs-lookup"><span data-stu-id="f0f36-125">[money][money]</span></span> |<span data-ttu-id="f0f36-126">[time][time]</span><span class="sxs-lookup"><span data-stu-id="f0f36-126">[time][time]</span></span> |
| <span data-ttu-id="f0f36-127">[date][date]</span><span class="sxs-lookup"><span data-stu-id="f0f36-127">[date][date]</span></span> |<span data-ttu-id="f0f36-128">[nchar][nchar]</span><span class="sxs-lookup"><span data-stu-id="f0f36-128">[nchar][nchar]</span></span> |<span data-ttu-id="f0f36-129">[tinyint][tinyint]</span><span class="sxs-lookup"><span data-stu-id="f0f36-129">[tinyint][tinyint]</span></span> |
| <span data-ttu-id="f0f36-130">[datetime][datetime]</span><span class="sxs-lookup"><span data-stu-id="f0f36-130">[datetime][datetime]</span></span> |<span data-ttu-id="f0f36-131">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="f0f36-131">[nvarchar][nvarchar]</span></span> |<span data-ttu-id="f0f36-132">[uniqueidentifier][uniqueidentifier]</span><span class="sxs-lookup"><span data-stu-id="f0f36-132">[uniqueidentifier][uniqueidentifier]</span></span> |
| <span data-ttu-id="f0f36-133">[datetime2][datetime2]</span><span class="sxs-lookup"><span data-stu-id="f0f36-133">[datetime2][datetime2]</span></span> |<span data-ttu-id="f0f36-134">[real][real]</span><span class="sxs-lookup"><span data-stu-id="f0f36-134">[real][real]</span></span> |<span data-ttu-id="f0f36-135">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="f0f36-135">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="f0f36-136">[datetimeoffset][datetimeoffset]</span><span class="sxs-lookup"><span data-stu-id="f0f36-136">[datetimeoffset][datetimeoffset]</span></span> |<span data-ttu-id="f0f36-137">[smalldatetime][smalldatetime]</span><span class="sxs-lookup"><span data-stu-id="f0f36-137">[smalldatetime][smalldatetime]</span></span> |<span data-ttu-id="f0f36-138">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="f0f36-138">[varchar][varchar]</span></span> |

## <a name="data-type-best-practices"></a><span data-ttu-id="f0f36-139">Data type best practices</span><span class="sxs-lookup"><span data-stu-id="f0f36-139">Data type best practices</span></span>
 <span data-ttu-id="f0f36-140">When defining your column types, using the smallest data type which will support your data will improve query performance.</span><span class="sxs-lookup"><span data-stu-id="f0f36-140">When defining your column types, using the smallest data type which will support your data will improve query performance.</span></span> <span data-ttu-id="f0f36-141">This is especially important for CHAR and VARCHAR columns.</span><span class="sxs-lookup"><span data-stu-id="f0f36-141">This is especially important for CHAR and VARCHAR columns.</span></span> <span data-ttu-id="f0f36-142">If the longest value in a column is 25 characters, then define your column as VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="f0f36-142">If the longest value in a column is 25 characters, then define your column as VARCHAR(25).</span></span> <span data-ttu-id="f0f36-143">Avoid defining all character columns to a large default length.</span><span class="sxs-lookup"><span data-stu-id="f0f36-143">Avoid defining all character columns to a large default length.</span></span> <span data-ttu-id="f0f36-144">In addition, define columns as VARCHAR when that is all that is needed rather than use [NVARCHAR][NVARCHAR].</span><span class="sxs-lookup"><span data-stu-id="f0f36-144">In addition, define columns as VARCHAR when that is all that is needed rather than use [NVARCHAR][NVARCHAR].</span></span>  <span data-ttu-id="f0f36-145">Use NVARCHAR(4000) or VARCHAR(8000) when possible instead of NVARCHAR(MAX) or VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="f0f36-145">Use NVARCHAR(4000) or VARCHAR(8000) when possible instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

## <a name="polybase-limitation"></a><span data-ttu-id="f0f36-146">Polybase limitation</span><span class="sxs-lookup"><span data-stu-id="f0f36-146">Polybase limitation</span></span>
<span data-ttu-id="f0f36-147">If you are using Polybase to load your tables, ensure that the length of the data does not exceed 1 MB.</span><span class="sxs-lookup"><span data-stu-id="f0f36-147">If you are using Polybase to load your tables, ensure that the length of the data does not exceed 1 MB.</span></span>  <span data-ttu-id="f0f36-148">While you can define a row with variable length data that can exceed this width and load rows with BCP, you will not be able to use Polybase to load this data.</span><span class="sxs-lookup"><span data-stu-id="f0f36-148">While you can define a row with variable length data that can exceed this width and load rows with BCP, you will not be able to use Polybase to load this data.</span></span>  

## <a name="unsupported-data-types"></a><span data-ttu-id="f0f36-149">Unsupported data types</span><span class="sxs-lookup"><span data-stu-id="f0f36-149">Unsupported data types</span></span>
<span data-ttu-id="f0f36-150">If you are migrating your database from another SQL platform like Azure SQL Database, as you migrate, you may encounter some data types that are not supported on SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f0f36-150">If you are migrating your database from another SQL platform like Azure SQL Database, as you migrate, you may encounter some data types that are not supported on SQL Data Warehouse.</span></span>  <span data-ttu-id="f0f36-151">Below are unsupported data types as well as some alternatives you can use in place of unsupported data types.</span><span class="sxs-lookup"><span data-stu-id="f0f36-151">Below are unsupported data types as well as some alternatives you can use in place of unsupported data types.</span></span>

| <span data-ttu-id="f0f36-152">Data Type</span><span class="sxs-lookup"><span data-stu-id="f0f36-152">Data Type</span></span> | <span data-ttu-id="f0f36-153">Workaround</span><span class="sxs-lookup"><span data-stu-id="f0f36-153">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="f0f36-154">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="f0f36-154">[geometry][geometry]</span></span> |<span data-ttu-id="f0f36-155">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="f0f36-155">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="f0f36-156">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="f0f36-156">[geography][geography]</span></span> |<span data-ttu-id="f0f36-157">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="f0f36-157">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="f0f36-158">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="f0f36-158">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="f0f36-159">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="f0f36-159">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="f0f36-160">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="f0f36-160">[image][ntext,text,image]</span></span> |<span data-ttu-id="f0f36-161">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="f0f36-161">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="f0f36-162">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="f0f36-162">[text][ntext,text,image]</span></span> |<span data-ttu-id="f0f36-163">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="f0f36-163">[varchar][varchar]</span></span> |
| <span data-ttu-id="f0f36-164">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="f0f36-164">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="f0f36-165">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="f0f36-165">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="f0f36-166">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="f0f36-166">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="f0f36-167">Split column into several strongly typed columns.</span><span class="sxs-lookup"><span data-stu-id="f0f36-167">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="f0f36-168">[table][table]</span><span class="sxs-lookup"><span data-stu-id="f0f36-168">[table][table]</span></span> |<span data-ttu-id="f0f36-169">Convert to temporary tables.</span><span class="sxs-lookup"><span data-stu-id="f0f36-169">Convert to temporary tables.</span></span> |
| <span data-ttu-id="f0f36-170">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="f0f36-170">[timestamp][timestamp]</span></span> |<span data-ttu-id="f0f36-171">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span><span class="sxs-lookup"><span data-stu-id="f0f36-171">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="f0f36-172">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span><span class="sxs-lookup"><span data-stu-id="f0f36-172">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="f0f36-173">If you need to migrate row version values from a timestamp typed column then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span><span class="sxs-lookup"><span data-stu-id="f0f36-173">If you need to migrate row version values from a timestamp typed column then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="f0f36-174">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="f0f36-174">[xml][xml]</span></span> |<span data-ttu-id="f0f36-175">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="f0f36-175">[varchar][varchar]</span></span> |
| <span data-ttu-id="f0f36-176">[user defined types][user defined types]</span><span class="sxs-lookup"><span data-stu-id="f0f36-176">[user defined types][user defined types]</span></span> |<span data-ttu-id="f0f36-177">convert back to their native types where possible</span><span class="sxs-lookup"><span data-stu-id="f0f36-177">convert back to their native types where possible</span></span> |
| <span data-ttu-id="f0f36-178">default values</span><span class="sxs-lookup"><span data-stu-id="f0f36-178">default values</span></span> |<span data-ttu-id="f0f36-179">default values support literals and constants only.</span><span class="sxs-lookup"><span data-stu-id="f0f36-179">default values support literals and constants only.</span></span>  <span data-ttu-id="f0f36-180">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span><span class="sxs-lookup"><span data-stu-id="f0f36-180">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |

<span data-ttu-id="f0f36-181">The below SQL can be run on your current SQL database to identify columns which are not be supported by Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="f0f36-181">The below SQL can be run on your current SQL database to identify columns which are not be supported by Azure SQL Data Warehouse:</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```

## <a name="next-steps"></a><span data-ttu-id="f0f36-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="f0f36-182">Next steps</span></span>
<span data-ttu-id="f0f36-183">To learn more, see the articles on [Table Overview][Overview], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span><span class="sxs-lookup"><span data-stu-id="f0f36-183">To learn more, see the articles on [Table Overview][Overview], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="f0f36-184">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="f0f36-184">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
