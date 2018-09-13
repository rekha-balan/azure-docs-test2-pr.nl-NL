---
title: Guide for using PolyBase in SQL Data Warehouse | Microsoft Docs
description: Guidelines and recommendations for using PolyBase in SQL Data Warehouse scenarios.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: ''
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: 43ca5562d690e6f52b15acba4cf1cd6a549d64ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564274"
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="756a9-103">Guide for using PolyBase in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="756a9-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="756a9-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="756a9-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="756a9-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span><span class="sxs-lookup"><span data-stu-id="756a9-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="756a9-106">Rotating storage keys</span><span class="sxs-lookup"><span data-stu-id="756a9-106">Rotating storage keys</span></span>
<span data-ttu-id="756a9-107">From time to time you will want to change the access key to your blob storage for security reasons.</span><span class="sxs-lookup"><span data-stu-id="756a9-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="756a9-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span><span class="sxs-lookup"><span data-stu-id="756a9-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="756a9-109">You may have noticed that you have two storage keys for your blob storage account.</span><span class="sxs-lookup"><span data-stu-id="756a9-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="756a9-110">This is so that you can transition</span><span class="sxs-lookup"><span data-stu-id="756a9-110">This is so that you can transition</span></span>

<span data-ttu-id="756a9-111">Rotating your Azure storage account keys is a simple three step process</span><span class="sxs-lookup"><span data-stu-id="756a9-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="756a9-112">Create second database scoped credential based on the secondary storage access key</span><span class="sxs-lookup"><span data-stu-id="756a9-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="756a9-113">Create second external data source based off this new credential</span><span class="sxs-lookup"><span data-stu-id="756a9-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="756a9-114">Drop and create the external table(s) pointing to the new external data source</span><span class="sxs-lookup"><span data-stu-id="756a9-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="756a9-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span><span class="sxs-lookup"><span data-stu-id="756a9-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="756a9-116">Drop first external data source</span><span class="sxs-lookup"><span data-stu-id="756a9-116">Drop first external data source</span></span>
2. <span data-ttu-id="756a9-117">Drop first database scoped credential based on the primary storage access key</span><span class="sxs-lookup"><span data-stu-id="756a9-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="756a9-118">Log into Azure and regenerate the primary access key ready for the next time</span><span class="sxs-lookup"><span data-stu-id="756a9-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="756a9-119">Query Azure blob storage data</span><span class="sxs-lookup"><span data-stu-id="756a9-119">Query Azure blob storage data</span></span>
<span data-ttu-id="756a9-120">Queries against external tables simply use the table name as though it was a relational table.</span><span class="sxs-lookup"><span data-stu-id="756a9-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="756a9-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span><span class="sxs-lookup"><span data-stu-id="756a9-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="756a9-122">This indicates that your external data contains *dirty* records.</span><span class="sxs-lookup"><span data-stu-id="756a9-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="756a9-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span><span class="sxs-lookup"><span data-stu-id="756a9-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="756a9-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span><span class="sxs-lookup"><span data-stu-id="756a9-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="756a9-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span><span class="sxs-lookup"><span data-stu-id="756a9-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="756a9-126">Load data from Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="756a9-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="756a9-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="756a9-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="756a9-128">Storing data directly removes the data transfer time for queries.</span><span class="sxs-lookup"><span data-stu-id="756a9-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="756a9-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span><span class="sxs-lookup"><span data-stu-id="756a9-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="756a9-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span><span class="sxs-lookup"><span data-stu-id="756a9-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="756a9-131">The new table inherits the columns named in the query.</span><span class="sxs-lookup"><span data-stu-id="756a9-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="756a9-132">It inherits the data types of those columns from the external table definition.</span><span class="sxs-lookup"><span data-stu-id="756a9-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="756a9-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="756a9-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="756a9-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="756a9-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="756a9-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="756a9-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="756a9-136">Create Statistics on newly loaded data</span><span class="sxs-lookup"><span data-stu-id="756a9-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="756a9-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span><span class="sxs-lookup"><span data-stu-id="756a9-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="756a9-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span><span class="sxs-lookup"><span data-stu-id="756a9-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="756a9-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span><span class="sxs-lookup"><span data-stu-id="756a9-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="756a9-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span><span class="sxs-lookup"><span data-stu-id="756a9-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="756a9-141">Export data to Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="756a9-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="756a9-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="756a9-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="756a9-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="756a9-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="756a9-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span><span class="sxs-lookup"><span data-stu-id="756a9-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="756a9-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span><span class="sxs-lookup"><span data-stu-id="756a9-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="756a9-146">The data is exported in the specified text file format.</span><span class="sxs-lookup"><span data-stu-id="756a9-146">The data is exported in the specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```


## <a name="working-around-the-polybase-utf-8-requirement"></a><span data-ttu-id="756a9-147">Working around the PolyBase UTF-8 requirement</span><span class="sxs-lookup"><span data-stu-id="756a9-147">Working around the PolyBase UTF-8 requirement</span></span>
<span data-ttu-id="756a9-148">At present PolyBase supports loading data files that have been UTF-8 encoded.</span><span class="sxs-lookup"><span data-stu-id="756a9-148">At present PolyBase supports loading data files that have been UTF-8 encoded.</span></span> <span data-ttu-id="756a9-149">As UTF-8 uses the same character encoding as ASCII PolyBase will also support loading data that is ASCII encoded.</span><span class="sxs-lookup"><span data-stu-id="756a9-149">As UTF-8 uses the same character encoding as ASCII PolyBase will also support loading data that is ASCII encoded.</span></span> <span data-ttu-id="756a9-150">However, PolyBase does not support other character encoding such as UTF-16 / Unicode or extended ASCII characters.</span><span class="sxs-lookup"><span data-stu-id="756a9-150">However, PolyBase does not support other character encoding such as UTF-16 / Unicode or extended ASCII characters.</span></span> <span data-ttu-id="756a9-151">Extended ASCII includes characters with accents such as the umlaut which is common in German.</span><span class="sxs-lookup"><span data-stu-id="756a9-151">Extended ASCII includes characters with accents such as the umlaut which is common in German.</span></span>

<span data-ttu-id="756a9-152">To work around this requirement the best answer is to re-write to UTF-8 encoding.</span><span class="sxs-lookup"><span data-stu-id="756a9-152">To work around this requirement the best answer is to re-write to UTF-8 encoding.</span></span>

<span data-ttu-id="756a9-153">There are several ways to do this.</span><span class="sxs-lookup"><span data-stu-id="756a9-153">There are several ways to do this.</span></span> <span data-ttu-id="756a9-154">Below are two approaches using Powershell:</span><span class="sxs-lookup"><span data-stu-id="756a9-154">Below are two approaches using Powershell:</span></span>

### <a name="simple-example-for-small-files"></a><span data-ttu-id="756a9-155">Simple example for small files</span><span class="sxs-lookup"><span data-stu-id="756a9-155">Simple example for small files</span></span>
<span data-ttu-id="756a9-156">Below is a simple one line Powershell script that creates the file.</span><span class="sxs-lookup"><span data-stu-id="756a9-156">Below is a simple one line Powershell script that creates the file.</span></span>

```PowerShell
Get-Content <input_file_name> -Encoding Unicode | Set-Content <output_file_name> -Encoding utf8
```

<span data-ttu-id="756a9-157">However, whilst this is a simple way to re-encode the data it is by no means the most efficient.</span><span class="sxs-lookup"><span data-stu-id="756a9-157">However, whilst this is a simple way to re-encode the data it is by no means the most efficient.</span></span> <span data-ttu-id="756a9-158">The io streaming example below is much, much faster and achieves the same result.</span><span class="sxs-lookup"><span data-stu-id="756a9-158">The io streaming example below is much, much faster and achieves the same result.</span></span>

### <a name="io-streaming-example-for-larger-files"></a><span data-ttu-id="756a9-159">IO Streaming example for larger files</span><span class="sxs-lookup"><span data-stu-id="756a9-159">IO Streaming example for larger files</span></span>
<span data-ttu-id="756a9-160">The code sample below is more complex but as it streams the rows of data from source to target it is much more efficient.</span><span class="sxs-lookup"><span data-stu-id="756a9-160">The code sample below is more complex but as it streams the rows of data from source to target it is much more efficient.</span></span> <span data-ttu-id="756a9-161">Use this approach for larger files.</span><span class="sxs-lookup"><span data-stu-id="756a9-161">Use this approach for larger files.</span></span>

```PowerShell
#Static variables
$ascii = [System.Text.Encoding]::ASCII
$utf16le = [System.Text.Encoding]::Unicode
$utf8 = [System.Text.Encoding]::UTF8
$ansi = [System.Text.Encoding]::Default
$append = $False

#Set source file path and file name
$src = [System.IO.Path]::Combine("C:\input_file_path\","input_file_name.txt")

#Set source file encoding (using list above)
$src_enc = $ansi

#Set target file path and file name
$tgt = [System.IO.Path]::Combine("C:\output_file_path\","output_file_name.txt")

#Set target file encoding (using list above)
$tgt_enc = $utf8

$read = New-Object System.IO.StreamReader($src,$src_enc)
$write = New-Object System.IO.StreamWriter($tgt,$append,$tgt_enc)

while ($read.Peek() -ne -1)
{
    $line = $read.ReadLine();
    $write.WriteLine($line);
}
$read.Close()
$read.Dispose()
$write.Close()
$write.Dispose()
```

## <a name="next-steps"></a><span data-ttu-id="756a9-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="756a9-162">Next steps</span></span>
<span data-ttu-id="756a9-163">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="756a9-163">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
