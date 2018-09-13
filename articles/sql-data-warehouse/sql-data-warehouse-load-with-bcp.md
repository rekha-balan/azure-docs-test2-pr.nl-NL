---
title: Use bcp to load data into SQL Data Warehouse | Microsoft Docs
description: Learn what bcp is and how to use it for data warehousing scenarios.
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: barbkess
editor: ''
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.openlocfilehash: a22e9acfadc29109b1f9b6272bab800b823904da
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661918"
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="803a0-103">Load data with bcp</span><span class="sxs-lookup"><span data-stu-id="803a0-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="803a0-108">**[bcp][bcp]** is a command-line bulk load utility that allows you to copy data between SQL Server, data files, and SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="803a0-108">**[bcp][bcp]** is a command-line bulk load utility that allows you to copy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="803a0-109">Use bcp to import large numbers of rows into SQL Data Warehouse tables or to export data from SQL Server tables into data files.</span><span class="sxs-lookup"><span data-stu-id="803a0-109">Use bcp to import large numbers of rows into SQL Data Warehouse tables or to export data from SQL Server tables into data files.</span></span> <span data-ttu-id="803a0-110">Except when used with the queryout option, bcp requires no knowledge of Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="803a0-110">Except when used with the queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="803a0-111">bcp is a quick and easy way to move smaller data sets into and out of a SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="803a0-111">bcp is a quick and easy way to move smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="803a0-112">The exact amount of data that is recommended to load/extract via bcp will depend on you network connection to the Azure data center.</span><span class="sxs-lookup"><span data-stu-id="803a0-112">The exact amount of data that is recommended to load/extract via bcp will depend on you network connection to the Azure data center.</span></span>  <span data-ttu-id="803a0-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span><span class="sxs-lookup"><span data-stu-id="803a0-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="803a0-114">Polybase is the recommended tool for loading and extracting large volumes of data as it does a better job leveraging the massively parallel processing architecture of SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="803a0-114">Polybase is the recommended tool for loading and extracting large volumes of data as it does a better job leveraging the massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="803a0-115">With bcp you can:</span><span class="sxs-lookup"><span data-stu-id="803a0-115">With bcp you can:</span></span>

* <span data-ttu-id="803a0-116">Use a simple command-line utility to load data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="803a0-116">Use a simple command-line utility to load data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="803a0-117">Use a simple command-line utility to extract data from SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="803a0-117">Use a simple command-line utility to extract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="803a0-118">This tutorial will show you how to:</span><span class="sxs-lookup"><span data-stu-id="803a0-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="803a0-119">Import data into a table using the bcp in command</span><span class="sxs-lookup"><span data-stu-id="803a0-119">Import data into a table using the bcp in command</span></span>
* <span data-ttu-id="803a0-120">Export data from a table uisng the bcp out command</span><span class="sxs-lookup"><span data-stu-id="803a0-120">Export data from a table uisng the bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="803a0-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="803a0-121">Prerequisites</span></span>
<span data-ttu-id="803a0-122">To step through this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="803a0-122">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="803a0-123">A SQL Data Warehouse database</span><span class="sxs-lookup"><span data-stu-id="803a0-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="803a0-124">The bcp command line utility installed</span><span class="sxs-lookup"><span data-stu-id="803a0-124">The bcp command line utility installed</span></span>
* <span data-ttu-id="803a0-125">The SQLCMD command line utility installed</span><span class="sxs-lookup"><span data-stu-id="803a0-125">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="803a0-127">Import data into SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="803a0-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="803a0-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span><span class="sxs-lookup"><span data-stu-id="803a0-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="803a0-129">Step 1: Create a table in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="803a0-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="803a0-130">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span><span class="sxs-lookup"><span data-stu-id="803a0-130">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="803a0-132">Step 2: Create a source data file</span><span class="sxs-lookup"><span data-stu-id="803a0-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="803a0-133">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="803a0-133">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> It is important to remember that bcp.exe does not support the UTF-8 file encoding. Please use ASCII files or UTF-16 encoded files when using bcp.exe.
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="803a0-136">Step 3: Connect and import the data</span><span class="sxs-lookup"><span data-stu-id="803a0-136">Step 3: Connect and import the data</span></span>
<span data-ttu-id="803a0-137">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span><span class="sxs-lookup"><span data-stu-id="803a0-137">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="803a0-138">You can verify the data was loaded by running the following query using sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="803a0-138">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="803a0-139">This should return the following results:</span><span class="sxs-lookup"><span data-stu-id="803a0-139">This should return the following results:</span></span>

| <span data-ttu-id="803a0-140">DateId</span><span class="sxs-lookup"><span data-stu-id="803a0-140">DateId</span></span> | <span data-ttu-id="803a0-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="803a0-141">CalendarQuarter</span></span> | <span data-ttu-id="803a0-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="803a0-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="803a0-143">20150101</span><span class="sxs-lookup"><span data-stu-id="803a0-143">20150101</span></span> |<span data-ttu-id="803a0-144">1</span><span class="sxs-lookup"><span data-stu-id="803a0-144">1</span></span> |<span data-ttu-id="803a0-145">3</span><span class="sxs-lookup"><span data-stu-id="803a0-145">3</span></span> |
| <span data-ttu-id="803a0-146">20150201</span><span class="sxs-lookup"><span data-stu-id="803a0-146">20150201</span></span> |<span data-ttu-id="803a0-147">1</span><span class="sxs-lookup"><span data-stu-id="803a0-147">1</span></span> |<span data-ttu-id="803a0-148">3</span><span class="sxs-lookup"><span data-stu-id="803a0-148">3</span></span> |
| <span data-ttu-id="803a0-149">20150301</span><span class="sxs-lookup"><span data-stu-id="803a0-149">20150301</span></span> |<span data-ttu-id="803a0-150">1</span><span class="sxs-lookup"><span data-stu-id="803a0-150">1</span></span> |<span data-ttu-id="803a0-151">3</span><span class="sxs-lookup"><span data-stu-id="803a0-151">3</span></span> |
| <span data-ttu-id="803a0-152">20150401</span><span class="sxs-lookup"><span data-stu-id="803a0-152">20150401</span></span> |<span data-ttu-id="803a0-153">2</span><span class="sxs-lookup"><span data-stu-id="803a0-153">2</span></span> |<span data-ttu-id="803a0-154">4</span><span class="sxs-lookup"><span data-stu-id="803a0-154">4</span></span> |
| <span data-ttu-id="803a0-155">20150501</span><span class="sxs-lookup"><span data-stu-id="803a0-155">20150501</span></span> |<span data-ttu-id="803a0-156">2</span><span class="sxs-lookup"><span data-stu-id="803a0-156">2</span></span> |<span data-ttu-id="803a0-157">4</span><span class="sxs-lookup"><span data-stu-id="803a0-157">4</span></span> |
| <span data-ttu-id="803a0-158">20150601</span><span class="sxs-lookup"><span data-stu-id="803a0-158">20150601</span></span> |<span data-ttu-id="803a0-159">2</span><span class="sxs-lookup"><span data-stu-id="803a0-159">2</span></span> |<span data-ttu-id="803a0-160">4</span><span class="sxs-lookup"><span data-stu-id="803a0-160">4</span></span> |
| <span data-ttu-id="803a0-161">20150701</span><span class="sxs-lookup"><span data-stu-id="803a0-161">20150701</span></span> |<span data-ttu-id="803a0-162">3</span><span class="sxs-lookup"><span data-stu-id="803a0-162">3</span></span> |<span data-ttu-id="803a0-163">1</span><span class="sxs-lookup"><span data-stu-id="803a0-163">1</span></span> |
| <span data-ttu-id="803a0-164">20150801</span><span class="sxs-lookup"><span data-stu-id="803a0-164">20150801</span></span> |<span data-ttu-id="803a0-165">3</span><span class="sxs-lookup"><span data-stu-id="803a0-165">3</span></span> |<span data-ttu-id="803a0-166">1</span><span class="sxs-lookup"><span data-stu-id="803a0-166">1</span></span> |
| <span data-ttu-id="803a0-167">20150801</span><span class="sxs-lookup"><span data-stu-id="803a0-167">20150801</span></span> |<span data-ttu-id="803a0-168">3</span><span class="sxs-lookup"><span data-stu-id="803a0-168">3</span></span> |<span data-ttu-id="803a0-169">1</span><span class="sxs-lookup"><span data-stu-id="803a0-169">1</span></span> |
| <span data-ttu-id="803a0-170">20151001</span><span class="sxs-lookup"><span data-stu-id="803a0-170">20151001</span></span> |<span data-ttu-id="803a0-171">4</span><span class="sxs-lookup"><span data-stu-id="803a0-171">4</span></span> |<span data-ttu-id="803a0-172">2</span><span class="sxs-lookup"><span data-stu-id="803a0-172">2</span></span> |
| <span data-ttu-id="803a0-173">20151101</span><span class="sxs-lookup"><span data-stu-id="803a0-173">20151101</span></span> |<span data-ttu-id="803a0-174">4</span><span class="sxs-lookup"><span data-stu-id="803a0-174">4</span></span> |<span data-ttu-id="803a0-175">2</span><span class="sxs-lookup"><span data-stu-id="803a0-175">2</span></span> |
| <span data-ttu-id="803a0-176">20151201</span><span class="sxs-lookup"><span data-stu-id="803a0-176">20151201</span></span> |<span data-ttu-id="803a0-177">4</span><span class="sxs-lookup"><span data-stu-id="803a0-177">4</span></span> |<span data-ttu-id="803a0-178">2</span><span class="sxs-lookup"><span data-stu-id="803a0-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="803a0-179">Step 4: Create Statistics on your newly loaded data</span><span class="sxs-lookup"><span data-stu-id="803a0-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="803a0-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span><span class="sxs-lookup"><span data-stu-id="803a0-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="803a0-181">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span><span class="sxs-lookup"><span data-stu-id="803a0-181">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="803a0-182">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span><span class="sxs-lookup"><span data-stu-id="803a0-182">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="803a0-183">Below is a quick example of how to create statistics on the tabled loaded in this example</span><span class="sxs-lookup"><span data-stu-id="803a0-183">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="803a0-184">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span><span class="sxs-lookup"><span data-stu-id="803a0-184">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="803a0-185">Export data from SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="803a0-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="803a0-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="803a0-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="803a0-187">We will export the data we created above to a new data file called DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="803a0-187">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="803a0-188">Step 1: Export the data</span><span class="sxs-lookup"><span data-stu-id="803a0-188">Step 1: Export the data</span></span>
<span data-ttu-id="803a0-189">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span><span class="sxs-lookup"><span data-stu-id="803a0-189">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="803a0-190">You can verify the data was exported correctly by opening the new file.</span><span class="sxs-lookup"><span data-stu-id="803a0-190">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="803a0-191">The data in the file should match the text below:</span><span class="sxs-lookup"><span data-stu-id="803a0-191">The data in the file should match the text below:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases. Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.
> 
> 

## <a name="next-steps"></a><span data-ttu-id="803a0-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="803a0-194">Next steps</span></span>
<span data-ttu-id="803a0-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="803a0-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="803a0-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="803a0-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
