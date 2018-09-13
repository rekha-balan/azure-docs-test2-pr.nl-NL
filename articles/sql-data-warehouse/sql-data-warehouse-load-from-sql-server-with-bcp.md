---
title: Load data from SQL Server into Azure SQL Data Warehouse (bcp) | Microsoft Docs
description: For a small data size, uses bcp to export data from SQL Server to flat files and import the data directly into Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 702be4f48d08d1c69e61e7c2c4fdaf3ddbab2045
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553777"
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="ce45b-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span><span class="sxs-lookup"><span data-stu-id="ce45b-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="ce45b-107">For small data sets, you can use the bcp command-line utility to export data from SQL Server and then load it directly to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ce45b-107">For small data sets, you can use the bcp command-line utility to export data from SQL Server and then load it directly to Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="ce45b-108">In this tutorial, you will use bcp to:</span><span class="sxs-lookup"><span data-stu-id="ce45b-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="ce45b-109">Export a table from from SQL Server by using the bcp out command (or create a simple sample file)</span><span class="sxs-lookup"><span data-stu-id="ce45b-109">Export a table from from SQL Server by using the bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="ce45b-110">Import the table from a flat file to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ce45b-110">Import the table from a flat file to SQL Data Warehouse.</span></span>
* <span data-ttu-id="ce45b-111">Create statistics on the loaded data.</span><span class="sxs-lookup"><span data-stu-id="ce45b-111">Create statistics on the loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="ce45b-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ce45b-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="ce45b-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ce45b-113">Prerequisites</span></span>
<span data-ttu-id="ce45b-114">To step through this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="ce45b-114">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="ce45b-115">A SQL Data Warehouse database</span><span class="sxs-lookup"><span data-stu-id="ce45b-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="ce45b-116">The bcp command-line utility installed</span><span class="sxs-lookup"><span data-stu-id="ce45b-116">The bcp command-line utility installed</span></span>
* <span data-ttu-id="ce45b-117">The sqlcmd command-line utility installed</span><span class="sxs-lookup"><span data-stu-id="ce45b-117">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="ce45b-118">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="ce45b-118">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="ce45b-119">Data in ASCII or UTF-16 format</span><span class="sxs-lookup"><span data-stu-id="ce45b-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="ce45b-120">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ce45b-120">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="ce45b-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span><span class="sxs-lookup"><span data-stu-id="ce45b-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="ce45b-122">Note that if you want to combine bcp with PolyBase you will need to transform the data to UTF-8 after it is exported from SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ce45b-122">Note that if you want to combine bcp with PolyBase you will need to transform the data to UTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="ce45b-123">1. Create a destination table</span><span class="sxs-lookup"><span data-stu-id="ce45b-123">1. Create a destination table</span></span>
<span data-ttu-id="ce45b-124">Define a table in SQL Data Warehouse that will be the destination table for the load.</span><span class="sxs-lookup"><span data-stu-id="ce45b-124">Define a table in SQL Data Warehouse that will be the destination table for the load.</span></span> <span data-ttu-id="ce45b-125">The columns in the table must correspond to the data in each row of your data file.</span><span class="sxs-lookup"><span data-stu-id="ce45b-125">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="ce45b-126">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span><span class="sxs-lookup"><span data-stu-id="ce45b-126">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="ce45b-127">2. Create a source data file</span><span class="sxs-lookup"><span data-stu-id="ce45b-127">2. Create a source data file</span></span>
<span data-ttu-id="ce45b-128">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="ce45b-128">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="ce45b-129">This data is in ASCII format.</span><span class="sxs-lookup"><span data-stu-id="ce45b-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="ce45b-130">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span><span class="sxs-lookup"><span data-stu-id="ce45b-130">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="ce45b-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span><span class="sxs-lookup"><span data-stu-id="ce45b-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-the-data"></a><span data-ttu-id="ce45b-132">3. Load the data</span><span class="sxs-lookup"><span data-stu-id="ce45b-132">3. Load the data</span></span>
<span data-ttu-id="ce45b-133">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span><span class="sxs-lookup"><span data-stu-id="ce45b-133">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="ce45b-134">Use this command to verify the data was loaded properly</span><span class="sxs-lookup"><span data-stu-id="ce45b-134">Use this command to verify the data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="ce45b-135">The results should look like this:</span><span class="sxs-lookup"><span data-stu-id="ce45b-135">The results should look like this:</span></span>

| <span data-ttu-id="ce45b-136">DateId</span><span class="sxs-lookup"><span data-stu-id="ce45b-136">DateId</span></span> | <span data-ttu-id="ce45b-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="ce45b-137">CalendarQuarter</span></span> | <span data-ttu-id="ce45b-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="ce45b-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce45b-139">20150101</span><span class="sxs-lookup"><span data-stu-id="ce45b-139">20150101</span></span> |<span data-ttu-id="ce45b-140">1</span><span class="sxs-lookup"><span data-stu-id="ce45b-140">1</span></span> |<span data-ttu-id="ce45b-141">3</span><span class="sxs-lookup"><span data-stu-id="ce45b-141">3</span></span> |
| <span data-ttu-id="ce45b-142">20150201</span><span class="sxs-lookup"><span data-stu-id="ce45b-142">20150201</span></span> |<span data-ttu-id="ce45b-143">1</span><span class="sxs-lookup"><span data-stu-id="ce45b-143">1</span></span> |<span data-ttu-id="ce45b-144">3</span><span class="sxs-lookup"><span data-stu-id="ce45b-144">3</span></span> |
| <span data-ttu-id="ce45b-145">20150301</span><span class="sxs-lookup"><span data-stu-id="ce45b-145">20150301</span></span> |<span data-ttu-id="ce45b-146">1</span><span class="sxs-lookup"><span data-stu-id="ce45b-146">1</span></span> |<span data-ttu-id="ce45b-147">3</span><span class="sxs-lookup"><span data-stu-id="ce45b-147">3</span></span> |
| <span data-ttu-id="ce45b-148">20150401</span><span class="sxs-lookup"><span data-stu-id="ce45b-148">20150401</span></span> |<span data-ttu-id="ce45b-149">2</span><span class="sxs-lookup"><span data-stu-id="ce45b-149">2</span></span> |<span data-ttu-id="ce45b-150">4</span><span class="sxs-lookup"><span data-stu-id="ce45b-150">4</span></span> |
| <span data-ttu-id="ce45b-151">20150501</span><span class="sxs-lookup"><span data-stu-id="ce45b-151">20150501</span></span> |<span data-ttu-id="ce45b-152">2</span><span class="sxs-lookup"><span data-stu-id="ce45b-152">2</span></span> |<span data-ttu-id="ce45b-153">4</span><span class="sxs-lookup"><span data-stu-id="ce45b-153">4</span></span> |
| <span data-ttu-id="ce45b-154">20150601</span><span class="sxs-lookup"><span data-stu-id="ce45b-154">20150601</span></span> |<span data-ttu-id="ce45b-155">2</span><span class="sxs-lookup"><span data-stu-id="ce45b-155">2</span></span> |<span data-ttu-id="ce45b-156">4</span><span class="sxs-lookup"><span data-stu-id="ce45b-156">4</span></span> |
| <span data-ttu-id="ce45b-157">20150701</span><span class="sxs-lookup"><span data-stu-id="ce45b-157">20150701</span></span> |<span data-ttu-id="ce45b-158">3</span><span class="sxs-lookup"><span data-stu-id="ce45b-158">3</span></span> |<span data-ttu-id="ce45b-159">1</span><span class="sxs-lookup"><span data-stu-id="ce45b-159">1</span></span> |
| <span data-ttu-id="ce45b-160">20150801</span><span class="sxs-lookup"><span data-stu-id="ce45b-160">20150801</span></span> |<span data-ttu-id="ce45b-161">3</span><span class="sxs-lookup"><span data-stu-id="ce45b-161">3</span></span> |<span data-ttu-id="ce45b-162">1</span><span class="sxs-lookup"><span data-stu-id="ce45b-162">1</span></span> |
| <span data-ttu-id="ce45b-163">20150801</span><span class="sxs-lookup"><span data-stu-id="ce45b-163">20150801</span></span> |<span data-ttu-id="ce45b-164">3</span><span class="sxs-lookup"><span data-stu-id="ce45b-164">3</span></span> |<span data-ttu-id="ce45b-165">1</span><span class="sxs-lookup"><span data-stu-id="ce45b-165">1</span></span> |
| <span data-ttu-id="ce45b-166">20151001</span><span class="sxs-lookup"><span data-stu-id="ce45b-166">20151001</span></span> |<span data-ttu-id="ce45b-167">4</span><span class="sxs-lookup"><span data-stu-id="ce45b-167">4</span></span> |<span data-ttu-id="ce45b-168">2</span><span class="sxs-lookup"><span data-stu-id="ce45b-168">2</span></span> |
| <span data-ttu-id="ce45b-169">20151101</span><span class="sxs-lookup"><span data-stu-id="ce45b-169">20151101</span></span> |<span data-ttu-id="ce45b-170">4</span><span class="sxs-lookup"><span data-stu-id="ce45b-170">4</span></span> |<span data-ttu-id="ce45b-171">2</span><span class="sxs-lookup"><span data-stu-id="ce45b-171">2</span></span> |
| <span data-ttu-id="ce45b-172">20151201</span><span class="sxs-lookup"><span data-stu-id="ce45b-172">20151201</span></span> |<span data-ttu-id="ce45b-173">4</span><span class="sxs-lookup"><span data-stu-id="ce45b-173">4</span></span> |<span data-ttu-id="ce45b-174">2</span><span class="sxs-lookup"><span data-stu-id="ce45b-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="ce45b-175">4. Create statistics</span><span class="sxs-lookup"><span data-stu-id="ce45b-175">4. Create statistics</span></span>
<span data-ttu-id="ce45b-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span><span class="sxs-lookup"><span data-stu-id="ce45b-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="ce45b-177">To get the best query performance, it's important to create statistics on all columns of all tables after the first load or after any substantial changes occur in the data.</span><span class="sxs-lookup"><span data-stu-id="ce45b-177">To get the best query performance, it's important to create statistics on all columns of all tables after the first load or after any substantial changes occur in the data.</span></span> <span data-ttu-id="ce45b-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span><span class="sxs-lookup"><span data-stu-id="ce45b-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="ce45b-179">Run the following command to create statistics on your newly loaded table.</span><span class="sxs-lookup"><span data-stu-id="ce45b-179">Run the following command to create statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="ce45b-180">5. Export data from SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ce45b-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="ce45b-181">For fun, you can export the data that you just loaded back out of SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ce45b-181">For fun, you can export the data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="ce45b-182">The command to export is exactly the same as exporting from SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ce45b-182">The command to export is exactly the same as exporting from SQL Server.</span></span>

<span data-ttu-id="ce45b-183">However, there is a difference in the results.</span><span class="sxs-lookup"><span data-stu-id="ce45b-183">However, there is a difference in the results.</span></span> <span data-ttu-id="ce45b-184">Since the data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data to the output file.</span><span class="sxs-lookup"><span data-stu-id="ce45b-184">Since the data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data to the output file.</span></span> <span data-ttu-id="ce45b-185">The order of the data in the output file is likely to be different than the order of the data in the input file.</span><span class="sxs-lookup"><span data-stu-id="ce45b-185">The order of the data in the output file is likely to be different than the order of the data in the input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="ce45b-186">Export a table and compare exported results</span><span class="sxs-lookup"><span data-stu-id="ce45b-186">Export a table and compare exported results</span></span>
<span data-ttu-id="ce45b-187">To see the exported data, open a command prompt and run this command using your own parameters.</span><span class="sxs-lookup"><span data-stu-id="ce45b-187">To see the exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="ce45b-188">ServerName is the name of your Azure logical SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ce45b-188">ServerName is the name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="ce45b-189">You can verify the data was exported correctly by opening the new file.</span><span class="sxs-lookup"><span data-stu-id="ce45b-189">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="ce45b-190">The data in the file should match the text below, but will likely be sorted in a different order:</span><span class="sxs-lookup"><span data-stu-id="ce45b-190">The data in the file should match the text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-the-results-of-a-query"></a><span data-ttu-id="ce45b-191">Export the results of a query</span><span class="sxs-lookup"><span data-stu-id="ce45b-191">Export the results of a query</span></span>
<span data-ttu-id="ce45b-192">You can use the **queryout** function of bcp to export the results of a query instead of exporting the entire table.</span><span class="sxs-lookup"><span data-stu-id="ce45b-192">You can use the **queryout** function of bcp to export the results of a query instead of exporting the entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ce45b-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="ce45b-193">Next steps</span></span>
<span data-ttu-id="ce45b-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="ce45b-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="ce45b-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="ce45b-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="ce45b-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ce45b-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
