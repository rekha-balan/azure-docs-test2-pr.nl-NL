---
title: Load sample data into SQL Data Warehouse | Microsoft Docs
description: Load sample data into SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: cddbc2c2968d1fb6cb934ca3f217f88e1da82935
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555895"
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="0783a-103">Load sample data into SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0783a-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="0783a-104">Follow these simple steps to load and query the Adventure Works Sample database.</span><span class="sxs-lookup"><span data-stu-id="0783a-104">Follow these simple steps to load and query the Adventure Works Sample database.</span></span> <span data-ttu-id="0783a-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span><span class="sxs-lookup"><span data-stu-id="0783a-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span></span> <span data-ttu-id="0783a-106">Once tables have been created, the scripts will use bcp to load data.</span><span class="sxs-lookup"><span data-stu-id="0783a-106">Once tables have been created, the scripts will use bcp to load data.</span></span>  <span data-ttu-id="0783a-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="0783a-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="0783a-108">Load sample data</span><span class="sxs-lookup"><span data-stu-id="0783a-108">Load sample data</span></span>
1. <span data-ttu-id="0783a-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span><span class="sxs-lookup"><span data-stu-id="0783a-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="0783a-110">Extract the files from downloaded zip to a directory on your local machine.</span><span class="sxs-lookup"><span data-stu-id="0783a-110">Extract the files from downloaded zip to a directory on your local machine.</span></span>
3. <span data-ttu-id="0783a-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span><span class="sxs-lookup"><span data-stu-id="0783a-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span></span>  <span data-ttu-id="0783a-112">Be sure to leave no whitespace between the "=" and the parameter.</span><span class="sxs-lookup"><span data-stu-id="0783a-112">Be sure to leave no whitespace between the "=" and the parameter.</span></span>  <span data-ttu-id="0783a-113">Below are examples of how your edits might look.</span><span class="sxs-lookup"><span data-stu-id="0783a-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="0783a-114">From a Windows cmd prompt, run the edited aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="0783a-114">From a Windows cmd prompt, run the edited aw_create.bat.</span></span>  <span data-ttu-id="0783a-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="0783a-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="0783a-116">This script will...</span><span class="sxs-lookup"><span data-stu-id="0783a-116">This script will...</span></span>
   
   * <span data-ttu-id="0783a-117">Drop any Adventure Works tables or views that already exist in your database</span><span class="sxs-lookup"><span data-stu-id="0783a-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="0783a-118">Create the Adventure Works tables and views</span><span class="sxs-lookup"><span data-stu-id="0783a-118">Create the Adventure Works tables and views</span></span>
   * <span data-ttu-id="0783a-119">Load each Adventure Works table using bcp</span><span class="sxs-lookup"><span data-stu-id="0783a-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="0783a-120">Validate the row counts for each Adventure Works table</span><span class="sxs-lookup"><span data-stu-id="0783a-120">Validate the row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="0783a-121">Collect statistics on every column for each Adventure Works table</span><span class="sxs-lookup"><span data-stu-id="0783a-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="0783a-122">Query sample data</span><span class="sxs-lookup"><span data-stu-id="0783a-122">Query sample data</span></span>
<span data-ttu-id="0783a-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span><span class="sxs-lookup"><span data-stu-id="0783a-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="0783a-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span><span class="sxs-lookup"><span data-stu-id="0783a-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="0783a-125">Example of simple select statement to get all the info of the employees:</span><span class="sxs-lookup"><span data-stu-id="0783a-125">Example of simple select statement to get all the info of the employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="0783a-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span><span class="sxs-lookup"><span data-stu-id="0783a-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="0783a-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span><span class="sxs-lookup"><span data-stu-id="0783a-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="0783a-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span><span class="sxs-lookup"><span data-stu-id="0783a-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="0783a-129">Any differences are documented in our [migrate code][migrate code] documentation.</span><span class="sxs-lookup"><span data-stu-id="0783a-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0783a-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="0783a-130">Next steps</span></span>
<span data-ttu-id="0783a-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0783a-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
