---
title: Load data from SQL Server into Azure SQL Data Warehouse (PolyBase) | Microsoft Docs
description: Uses bcp to export data from SQL Server to flat files, AZCopy to import data to Azure blob storage, and PolyBase to ingest the data into Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: ''
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 08f94bc26d8b1e1f5a56dfccd41e394dbd721024
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549473"
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="db9d9-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="db9d9-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="db9d9-104">Use bcp and AZCopy command-line utilities to load data from SQL Server to Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="db9d9-104">Use bcp and AZCopy command-line utilities to load data from SQL Server to Azure blob storage.</span></span> <span data-ttu-id="db9d9-105">Then use PolyBase or Azure Data Factory to load the data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="db9d9-105">Then use PolyBase or Azure Data Factory to load the data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db9d9-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="db9d9-106">Prerequisites</span></span>
<span data-ttu-id="db9d9-107">To step through this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="db9d9-107">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="db9d9-108">A SQL Data Warehouse database</span><span class="sxs-lookup"><span data-stu-id="db9d9-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="db9d9-109">The bcp command line utility installed</span><span class="sxs-lookup"><span data-stu-id="db9d9-109">The bcp command line utility installed</span></span>
* <span data-ttu-id="db9d9-110">The SQLCMD command line utility installed</span><span class="sxs-lookup"><span data-stu-id="db9d9-110">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="db9d9-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="db9d9-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="db9d9-112">Import data into SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="db9d9-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="db9d9-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span><span class="sxs-lookup"><span data-stu-id="db9d9-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="db9d9-114">Step 1: Create a table in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="db9d9-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="db9d9-115">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span><span class="sxs-lookup"><span data-stu-id="db9d9-115">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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
> <span data-ttu-id="db9d9-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span><span class="sxs-lookup"><span data-stu-id="db9d9-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="db9d9-117">Step 2: Create a source data file</span><span class="sxs-lookup"><span data-stu-id="db9d9-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="db9d9-118">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="db9d9-118">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="db9d9-119">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span><span class="sxs-lookup"><span data-stu-id="db9d9-119">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="db9d9-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="db9d9-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="db9d9-121">Step 3: Connect and import the data</span><span class="sxs-lookup"><span data-stu-id="db9d9-121">Step 3: Connect and import the data</span></span>
<span data-ttu-id="db9d9-122">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span><span class="sxs-lookup"><span data-stu-id="db9d9-122">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="db9d9-123">You can verify the data was loaded by running the following query using sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="db9d9-123">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="db9d9-124">This should return the following results:</span><span class="sxs-lookup"><span data-stu-id="db9d9-124">This should return the following results:</span></span>

| <span data-ttu-id="db9d9-125">DateId</span><span class="sxs-lookup"><span data-stu-id="db9d9-125">DateId</span></span> | <span data-ttu-id="db9d9-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="db9d9-126">CalendarQuarter</span></span> | <span data-ttu-id="db9d9-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="db9d9-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db9d9-128">20150101</span><span class="sxs-lookup"><span data-stu-id="db9d9-128">20150101</span></span> |<span data-ttu-id="db9d9-129">1</span><span class="sxs-lookup"><span data-stu-id="db9d9-129">1</span></span> |<span data-ttu-id="db9d9-130">3</span><span class="sxs-lookup"><span data-stu-id="db9d9-130">3</span></span> |
| <span data-ttu-id="db9d9-131">20150201</span><span class="sxs-lookup"><span data-stu-id="db9d9-131">20150201</span></span> |<span data-ttu-id="db9d9-132">1</span><span class="sxs-lookup"><span data-stu-id="db9d9-132">1</span></span> |<span data-ttu-id="db9d9-133">3</span><span class="sxs-lookup"><span data-stu-id="db9d9-133">3</span></span> |
| <span data-ttu-id="db9d9-134">20150301</span><span class="sxs-lookup"><span data-stu-id="db9d9-134">20150301</span></span> |<span data-ttu-id="db9d9-135">1</span><span class="sxs-lookup"><span data-stu-id="db9d9-135">1</span></span> |<span data-ttu-id="db9d9-136">3</span><span class="sxs-lookup"><span data-stu-id="db9d9-136">3</span></span> |
| <span data-ttu-id="db9d9-137">20150401</span><span class="sxs-lookup"><span data-stu-id="db9d9-137">20150401</span></span> |<span data-ttu-id="db9d9-138">2</span><span class="sxs-lookup"><span data-stu-id="db9d9-138">2</span></span> |<span data-ttu-id="db9d9-139">4</span><span class="sxs-lookup"><span data-stu-id="db9d9-139">4</span></span> |
| <span data-ttu-id="db9d9-140">20150501</span><span class="sxs-lookup"><span data-stu-id="db9d9-140">20150501</span></span> |<span data-ttu-id="db9d9-141">2</span><span class="sxs-lookup"><span data-stu-id="db9d9-141">2</span></span> |<span data-ttu-id="db9d9-142">4</span><span class="sxs-lookup"><span data-stu-id="db9d9-142">4</span></span> |
| <span data-ttu-id="db9d9-143">20150601</span><span class="sxs-lookup"><span data-stu-id="db9d9-143">20150601</span></span> |<span data-ttu-id="db9d9-144">2</span><span class="sxs-lookup"><span data-stu-id="db9d9-144">2</span></span> |<span data-ttu-id="db9d9-145">4</span><span class="sxs-lookup"><span data-stu-id="db9d9-145">4</span></span> |
| <span data-ttu-id="db9d9-146">20150701</span><span class="sxs-lookup"><span data-stu-id="db9d9-146">20150701</span></span> |<span data-ttu-id="db9d9-147">3</span><span class="sxs-lookup"><span data-stu-id="db9d9-147">3</span></span> |<span data-ttu-id="db9d9-148">1</span><span class="sxs-lookup"><span data-stu-id="db9d9-148">1</span></span> |
| <span data-ttu-id="db9d9-149">20150801</span><span class="sxs-lookup"><span data-stu-id="db9d9-149">20150801</span></span> |<span data-ttu-id="db9d9-150">3</span><span class="sxs-lookup"><span data-stu-id="db9d9-150">3</span></span> |<span data-ttu-id="db9d9-151">1</span><span class="sxs-lookup"><span data-stu-id="db9d9-151">1</span></span> |
| <span data-ttu-id="db9d9-152">20150801</span><span class="sxs-lookup"><span data-stu-id="db9d9-152">20150801</span></span> |<span data-ttu-id="db9d9-153">3</span><span class="sxs-lookup"><span data-stu-id="db9d9-153">3</span></span> |<span data-ttu-id="db9d9-154">1</span><span class="sxs-lookup"><span data-stu-id="db9d9-154">1</span></span> |
| <span data-ttu-id="db9d9-155">20151001</span><span class="sxs-lookup"><span data-stu-id="db9d9-155">20151001</span></span> |<span data-ttu-id="db9d9-156">4</span><span class="sxs-lookup"><span data-stu-id="db9d9-156">4</span></span> |<span data-ttu-id="db9d9-157">2</span><span class="sxs-lookup"><span data-stu-id="db9d9-157">2</span></span> |
| <span data-ttu-id="db9d9-158">20151101</span><span class="sxs-lookup"><span data-stu-id="db9d9-158">20151101</span></span> |<span data-ttu-id="db9d9-159">4</span><span class="sxs-lookup"><span data-stu-id="db9d9-159">4</span></span> |<span data-ttu-id="db9d9-160">2</span><span class="sxs-lookup"><span data-stu-id="db9d9-160">2</span></span> |
| <span data-ttu-id="db9d9-161">20151201</span><span class="sxs-lookup"><span data-stu-id="db9d9-161">20151201</span></span> |<span data-ttu-id="db9d9-162">4</span><span class="sxs-lookup"><span data-stu-id="db9d9-162">4</span></span> |<span data-ttu-id="db9d9-163">2</span><span class="sxs-lookup"><span data-stu-id="db9d9-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="db9d9-164">Step 4: Create Statistics on your newly loaded data</span><span class="sxs-lookup"><span data-stu-id="db9d9-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="db9d9-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span><span class="sxs-lookup"><span data-stu-id="db9d9-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="db9d9-166">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span><span class="sxs-lookup"><span data-stu-id="db9d9-166">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="db9d9-167">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span><span class="sxs-lookup"><span data-stu-id="db9d9-167">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="db9d9-168">Below is a quick example of how to create statistics on the tabled loaded in this example</span><span class="sxs-lookup"><span data-stu-id="db9d9-168">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="db9d9-169">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span><span class="sxs-lookup"><span data-stu-id="db9d9-169">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="db9d9-170">Export data from SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="db9d9-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="db9d9-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="db9d9-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="db9d9-172">We will export the data we created above to a new data file called DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="db9d9-172">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="db9d9-173">Step 1: Export the data</span><span class="sxs-lookup"><span data-stu-id="db9d9-173">Step 1: Export the data</span></span>
<span data-ttu-id="db9d9-174">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span><span class="sxs-lookup"><span data-stu-id="db9d9-174">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="db9d9-175">You can verify the data was exported correctly by opening the new file.</span><span class="sxs-lookup"><span data-stu-id="db9d9-175">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="db9d9-176">The data in the file should match the text below:</span><span class="sxs-lookup"><span data-stu-id="db9d9-176">The data in the file should match the text below:</span></span>

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
> <span data-ttu-id="db9d9-177">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span><span class="sxs-lookup"><span data-stu-id="db9d9-177">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="db9d9-178">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span><span class="sxs-lookup"><span data-stu-id="db9d9-178">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="db9d9-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="db9d9-179">Next steps</span></span>
<span data-ttu-id="db9d9-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="db9d9-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="db9d9-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="db9d9-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
