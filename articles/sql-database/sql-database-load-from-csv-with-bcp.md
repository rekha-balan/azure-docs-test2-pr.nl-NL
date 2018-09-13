---
title: Load data from CSV file into Azure SQL Databaase (bcp) | Microsoft Docs
description: For a small data size, uses bcp to import data into Azure SQL Database.
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: ee7172712546af28dcb80a11951bdcfe4b2803b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670697"
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="ff913-103">Load data from CSV into Azure SQL Database (flat files)</span><span class="sxs-lookup"><span data-stu-id="ff913-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="ff913-104">You can use the bcp command-line utility to import data from a CSV file into Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ff913-104">You can use the bcp command-line utility to import data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ff913-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ff913-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="ff913-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff913-106">Prerequisites</span></span>
<span data-ttu-id="ff913-107">To step through this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="ff913-107">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="ff913-108">An Azure SQL Database logical server and database</span><span class="sxs-lookup"><span data-stu-id="ff913-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="ff913-109">The bcp command-line utility installed</span><span class="sxs-lookup"><span data-stu-id="ff913-109">The bcp command-line utility installed</span></span>
* <span data-ttu-id="ff913-110">The sqlcmd command-line utility installed</span><span class="sxs-lookup"><span data-stu-id="ff913-110">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="ff913-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="ff913-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="ff913-112">Data in ASCII or UTF-16 format</span><span class="sxs-lookup"><span data-stu-id="ff913-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="ff913-113">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ff913-113">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="ff913-114">1. Create a destination table</span><span class="sxs-lookup"><span data-stu-id="ff913-114">1. Create a destination table</span></span>
<span data-ttu-id="ff913-115">Define a table in SQL Database as the destination table.</span><span class="sxs-lookup"><span data-stu-id="ff913-115">Define a table in SQL Database as the destination table.</span></span> <span data-ttu-id="ff913-116">The columns in the table must correspond to the data in each row of your data file.</span><span class="sxs-lookup"><span data-stu-id="ff913-116">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="ff913-117">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span><span class="sxs-lookup"><span data-stu-id="ff913-117">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="ff913-118">2. Create a source data file</span><span class="sxs-lookup"><span data-stu-id="ff913-118">2. Create a source data file</span></span>
<span data-ttu-id="ff913-119">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="ff913-119">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="ff913-120">This data is in ASCII format.</span><span class="sxs-lookup"><span data-stu-id="ff913-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="ff913-121">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span><span class="sxs-lookup"><span data-stu-id="ff913-121">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="ff913-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span><span class="sxs-lookup"><span data-stu-id="ff913-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```

## <a name="3-load-the-data"></a><span data-ttu-id="ff913-123">3. Load the data</span><span class="sxs-lookup"><span data-stu-id="ff913-123">3. Load the data</span></span>
<span data-ttu-id="ff913-124">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span><span class="sxs-lookup"><span data-stu-id="ff913-124">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="ff913-125">Use this command to verify the data was loaded properly</span><span class="sxs-lookup"><span data-stu-id="ff913-125">Use this command to verify the data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="ff913-126">The results should look like this:</span><span class="sxs-lookup"><span data-stu-id="ff913-126">The results should look like this:</span></span>

| <span data-ttu-id="ff913-127">DateId</span><span class="sxs-lookup"><span data-stu-id="ff913-127">DateId</span></span> | <span data-ttu-id="ff913-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="ff913-128">CalendarQuarter</span></span> | <span data-ttu-id="ff913-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="ff913-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff913-130">20150101</span><span class="sxs-lookup"><span data-stu-id="ff913-130">20150101</span></span> |<span data-ttu-id="ff913-131">1</span><span class="sxs-lookup"><span data-stu-id="ff913-131">1</span></span> |<span data-ttu-id="ff913-132">3</span><span class="sxs-lookup"><span data-stu-id="ff913-132">3</span></span> |
| <span data-ttu-id="ff913-133">20150201</span><span class="sxs-lookup"><span data-stu-id="ff913-133">20150201</span></span> |<span data-ttu-id="ff913-134">1</span><span class="sxs-lookup"><span data-stu-id="ff913-134">1</span></span> |<span data-ttu-id="ff913-135">3</span><span class="sxs-lookup"><span data-stu-id="ff913-135">3</span></span> |
| <span data-ttu-id="ff913-136">20150301</span><span class="sxs-lookup"><span data-stu-id="ff913-136">20150301</span></span> |<span data-ttu-id="ff913-137">1</span><span class="sxs-lookup"><span data-stu-id="ff913-137">1</span></span> |<span data-ttu-id="ff913-138">3</span><span class="sxs-lookup"><span data-stu-id="ff913-138">3</span></span> |
| <span data-ttu-id="ff913-139">20150401</span><span class="sxs-lookup"><span data-stu-id="ff913-139">20150401</span></span> |<span data-ttu-id="ff913-140">2</span><span class="sxs-lookup"><span data-stu-id="ff913-140">2</span></span> |<span data-ttu-id="ff913-141">4</span><span class="sxs-lookup"><span data-stu-id="ff913-141">4</span></span> |
| <span data-ttu-id="ff913-142">20150501</span><span class="sxs-lookup"><span data-stu-id="ff913-142">20150501</span></span> |<span data-ttu-id="ff913-143">2</span><span class="sxs-lookup"><span data-stu-id="ff913-143">2</span></span> |<span data-ttu-id="ff913-144">4</span><span class="sxs-lookup"><span data-stu-id="ff913-144">4</span></span> |
| <span data-ttu-id="ff913-145">20150601</span><span class="sxs-lookup"><span data-stu-id="ff913-145">20150601</span></span> |<span data-ttu-id="ff913-146">2</span><span class="sxs-lookup"><span data-stu-id="ff913-146">2</span></span> |<span data-ttu-id="ff913-147">4</span><span class="sxs-lookup"><span data-stu-id="ff913-147">4</span></span> |
| <span data-ttu-id="ff913-148">20150701</span><span class="sxs-lookup"><span data-stu-id="ff913-148">20150701</span></span> |<span data-ttu-id="ff913-149">3</span><span class="sxs-lookup"><span data-stu-id="ff913-149">3</span></span> |<span data-ttu-id="ff913-150">1</span><span class="sxs-lookup"><span data-stu-id="ff913-150">1</span></span> |
| <span data-ttu-id="ff913-151">20150801</span><span class="sxs-lookup"><span data-stu-id="ff913-151">20150801</span></span> |<span data-ttu-id="ff913-152">3</span><span class="sxs-lookup"><span data-stu-id="ff913-152">3</span></span> |<span data-ttu-id="ff913-153">1</span><span class="sxs-lookup"><span data-stu-id="ff913-153">1</span></span> |
| <span data-ttu-id="ff913-154">20150801</span><span class="sxs-lookup"><span data-stu-id="ff913-154">20150801</span></span> |<span data-ttu-id="ff913-155">3</span><span class="sxs-lookup"><span data-stu-id="ff913-155">3</span></span> |<span data-ttu-id="ff913-156">1</span><span class="sxs-lookup"><span data-stu-id="ff913-156">1</span></span> |
| <span data-ttu-id="ff913-157">20151001</span><span class="sxs-lookup"><span data-stu-id="ff913-157">20151001</span></span> |<span data-ttu-id="ff913-158">4</span><span class="sxs-lookup"><span data-stu-id="ff913-158">4</span></span> |<span data-ttu-id="ff913-159">2</span><span class="sxs-lookup"><span data-stu-id="ff913-159">2</span></span> |
| <span data-ttu-id="ff913-160">20151101</span><span class="sxs-lookup"><span data-stu-id="ff913-160">20151101</span></span> |<span data-ttu-id="ff913-161">4</span><span class="sxs-lookup"><span data-stu-id="ff913-161">4</span></span> |<span data-ttu-id="ff913-162">2</span><span class="sxs-lookup"><span data-stu-id="ff913-162">2</span></span> |
| <span data-ttu-id="ff913-163">20151201</span><span class="sxs-lookup"><span data-stu-id="ff913-163">20151201</span></span> |<span data-ttu-id="ff913-164">4</span><span class="sxs-lookup"><span data-stu-id="ff913-164">4</span></span> |<span data-ttu-id="ff913-165">2</span><span class="sxs-lookup"><span data-stu-id="ff913-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff913-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff913-166">Next steps</span></span>
<span data-ttu-id="ff913-167">To migrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="ff913-167">To migrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
