---
title: Create table as select (CTAS) in SQL Data Warehouse | Microsoft Docs
description: Tips for coding with the create table as select (CTAS) statement in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 2619fd57efbbac090842d1dd665db3235b291c1a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555403"
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="a7da1-103">Create Table As Select (CTAS) in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a7da1-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="a7da1-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span><span class="sxs-lookup"><span data-stu-id="a7da1-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span></span> <span data-ttu-id="a7da1-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span><span class="sxs-lookup"><span data-stu-id="a7da1-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="a7da1-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span><span class="sxs-lookup"><span data-stu-id="a7da1-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span></span> <span data-ttu-id="a7da1-107">This document provides both examples and best practices for `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="a7da1-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="a7da1-108">SELECT..INTO vs. CTAS</span><span class="sxs-lookup"><span data-stu-id="a7da1-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="a7da1-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="a7da1-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="a7da1-110">Below is an example of a simple `SELECT..INTO` statement:</span><span class="sxs-lookup"><span data-stu-id="a7da1-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="a7da1-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a7da1-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="a7da1-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span><span class="sxs-lookup"><span data-stu-id="a7da1-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="a7da1-113">This is where `CTAS` comes in.</span><span class="sxs-lookup"><span data-stu-id="a7da1-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="a7da1-114">To convert the above to `CTAS` is quite straight-forward:</span><span class="sxs-lookup"><span data-stu-id="a7da1-114">To convert the above to `CTAS` is quite straight-forward:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<span data-ttu-id="a7da1-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span><span class="sxs-lookup"><span data-stu-id="a7da1-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="a7da1-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span><span class="sxs-lookup"><span data-stu-id="a7da1-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="a7da1-117">This will avoid cross distribution data movement during the operation which is more efficient.</span><span class="sxs-lookup"><span data-stu-id="a7da1-117">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="a7da1-118">Using CTAS to copy a table</span><span class="sxs-lookup"><span data-stu-id="a7da1-118">Using CTAS to copy a table</span></span>
<span data-ttu-id="a7da1-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span><span class="sxs-lookup"><span data-stu-id="a7da1-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="a7da1-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span><span class="sxs-lookup"><span data-stu-id="a7da1-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="a7da1-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span><span class="sxs-lookup"><span data-stu-id="a7da1-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="a7da1-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="a7da1-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

<span data-ttu-id="a7da1-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span><span class="sxs-lookup"><span data-stu-id="a7da1-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="a7da1-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span><span class="sxs-lookup"><span data-stu-id="a7da1-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="a7da1-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span><span class="sxs-lookup"><span data-stu-id="a7da1-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="a7da1-126">Here is the CTAS statement which would copy your old table into a new table.</span><span class="sxs-lookup"><span data-stu-id="a7da1-126">Here is the CTAS statement which would copy your old table into a new table.</span></span>

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

<span data-ttu-id="a7da1-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span><span class="sxs-lookup"><span data-stu-id="a7da1-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="a7da1-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span><span class="sxs-lookup"><span data-stu-id="a7da1-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="a7da1-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span><span class="sxs-lookup"><span data-stu-id="a7da1-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="a7da1-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span><span class="sxs-lookup"><span data-stu-id="a7da1-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="a7da1-131">Using CTAS to work around unsupported features</span><span class="sxs-lookup"><span data-stu-id="a7da1-131">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="a7da1-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span><span class="sxs-lookup"><span data-stu-id="a7da1-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="a7da1-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a7da1-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="a7da1-134">This is as a result of its fully parallelized design.</span><span class="sxs-lookup"><span data-stu-id="a7da1-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="a7da1-135">Scenarios that can be worked around with CTAS include:</span><span class="sxs-lookup"><span data-stu-id="a7da1-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="a7da1-136">ANSI JOINS on UPDATEs</span><span class="sxs-lookup"><span data-stu-id="a7da1-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="a7da1-137">ANSI JOINs on DELETEs</span><span class="sxs-lookup"><span data-stu-id="a7da1-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="a7da1-138">MERGE statement</span><span class="sxs-lookup"><span data-stu-id="a7da1-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="a7da1-139">Try to think "CTAS first".</span><span class="sxs-lookup"><span data-stu-id="a7da1-139">Try to think "CTAS first".</span></span> <span data-ttu-id="a7da1-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span><span class="sxs-lookup"><span data-stu-id="a7da1-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="a7da1-141">ANSI join replacement for update statements</span><span class="sxs-lookup"><span data-stu-id="a7da1-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="a7da1-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span><span class="sxs-lookup"><span data-stu-id="a7da1-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="a7da1-143">Imagine you had to update this table:</span><span class="sxs-lookup"><span data-stu-id="a7da1-143">Imagine you had to update this table:</span></span>

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

<span data-ttu-id="a7da1-144">The original query might have looked something like this:</span><span class="sxs-lookup"><span data-stu-id="a7da1-144">The original query might have looked something like this:</span></span>

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

<span data-ttu-id="a7da1-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span><span class="sxs-lookup"><span data-stu-id="a7da1-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="a7da1-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span><span class="sxs-lookup"><span data-stu-id="a7da1-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="a7da1-147">ANSI join replacement for delete statements</span><span class="sxs-lookup"><span data-stu-id="a7da1-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="a7da1-148">Sometimes the best approach for deleting data is to use `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="a7da1-148">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="a7da1-149">Rather than deleting the data simply select the data you want to keep.</span><span class="sxs-lookup"><span data-stu-id="a7da1-149">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="a7da1-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span><span class="sxs-lookup"><span data-stu-id="a7da1-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="a7da1-151">An example of a converted DELETE statement is available below:</span><span class="sxs-lookup"><span data-stu-id="a7da1-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="a7da1-152">Replace merge statements</span><span class="sxs-lookup"><span data-stu-id="a7da1-152">Replace merge statements</span></span>
<span data-ttu-id="a7da1-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="a7da1-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="a7da1-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span><span class="sxs-lookup"><span data-stu-id="a7da1-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span></span> <span data-ttu-id="a7da1-155">Any deleted records would need to be closed off in a second statement.</span><span class="sxs-lookup"><span data-stu-id="a7da1-155">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="a7da1-156">An example of an `UPSERT` is available below:</span><span class="sxs-lookup"><span data-stu-id="a7da1-156">An example of an `UPSERT` is available below:</span></span>

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="a7da1-157">CTAS recommendation: Explicitly state data type and nullability of output</span><span class="sxs-lookup"><span data-stu-id="a7da1-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="a7da1-158">When migrating code you might find you run across this type of coding pattern:</span><span class="sxs-lookup"><span data-stu-id="a7da1-158">When migrating code you might find you run across this type of coding pattern:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

<span data-ttu-id="a7da1-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span><span class="sxs-lookup"><span data-stu-id="a7da1-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="a7da1-160">However, there is a hidden issue here.</span><span class="sxs-lookup"><span data-stu-id="a7da1-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="a7da1-161">The following code does NOT yield the same result:</span><span class="sxs-lookup"><span data-stu-id="a7da1-161">The following code does NOT yield the same result:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

<span data-ttu-id="a7da1-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span><span class="sxs-lookup"><span data-stu-id="a7da1-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="a7da1-163">This can lead to subtle variances in values if you aren't careful.</span><span class="sxs-lookup"><span data-stu-id="a7da1-163">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="a7da1-164">Try the following as an example:</span><span class="sxs-lookup"><span data-stu-id="a7da1-164">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="a7da1-165">The value stored for result is different.</span><span class="sxs-lookup"><span data-stu-id="a7da1-165">The value stored for result is different.</span></span> <span data-ttu-id="a7da1-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span><span class="sxs-lookup"><span data-stu-id="a7da1-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="a7da1-167">This is particularly important for data migrations.</span><span class="sxs-lookup"><span data-stu-id="a7da1-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="a7da1-168">Even though the second query is arguably more accurate there is a problem.</span><span class="sxs-lookup"><span data-stu-id="a7da1-168">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="a7da1-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span><span class="sxs-lookup"><span data-stu-id="a7da1-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="a7da1-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span><span class="sxs-lookup"><span data-stu-id="a7da1-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="a7da1-171">The reason we see this disparity between the two results is down to implicit type casting.</span><span class="sxs-lookup"><span data-stu-id="a7da1-171">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="a7da1-172">In the first example the table defines the column definition.</span><span class="sxs-lookup"><span data-stu-id="a7da1-172">In the first example the table defines the column definition.</span></span> <span data-ttu-id="a7da1-173">When the row is inserted an implicit type conversion occurs.</span><span class="sxs-lookup"><span data-stu-id="a7da1-173">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="a7da1-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span><span class="sxs-lookup"><span data-stu-id="a7da1-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="a7da1-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span><span class="sxs-lookup"><span data-stu-id="a7da1-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="a7da1-176">When the table was created in the first example column nullability was explicitly defined.</span><span class="sxs-lookup"><span data-stu-id="a7da1-176">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="a7da1-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span><span class="sxs-lookup"><span data-stu-id="a7da1-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="a7da1-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span><span class="sxs-lookup"><span data-stu-id="a7da1-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span></span> <span data-ttu-id="a7da1-179">You cannot set these properties in the create table part.</span><span class="sxs-lookup"><span data-stu-id="a7da1-179">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="a7da1-180">The example below demonstrates how to fix the code:</span><span class="sxs-lookup"><span data-stu-id="a7da1-180">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="a7da1-181">Note the following:</span><span class="sxs-lookup"><span data-stu-id="a7da1-181">Note the following:</span></span>

* <span data-ttu-id="a7da1-182">CAST or CONVERT could have been used</span><span class="sxs-lookup"><span data-stu-id="a7da1-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="a7da1-183">ISNULL is used to force NULLability not COALESCE</span><span class="sxs-lookup"><span data-stu-id="a7da1-183">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="a7da1-184">ISNULL is the outermost function</span><span class="sxs-lookup"><span data-stu-id="a7da1-184">ISNULL is the outermost function</span></span>
* <span data-ttu-id="a7da1-185">The second part of the ISNULL is a constant i.e. 0</span><span class="sxs-lookup"><span data-stu-id="a7da1-185">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="a7da1-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="a7da1-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="a7da1-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span><span class="sxs-lookup"><span data-stu-id="a7da1-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="a7da1-188">`ISNULL` is different.</span><span class="sxs-lookup"><span data-stu-id="a7da1-188">`ISNULL` is different.</span></span> <span data-ttu-id="a7da1-189">It is deterministic.</span><span class="sxs-lookup"><span data-stu-id="a7da1-189">It is deterministic.</span></span> <span data-ttu-id="a7da1-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="a7da1-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="a7da1-191">This tip is not just useful for ensuring the integrity of your calculations.</span><span class="sxs-lookup"><span data-stu-id="a7da1-191">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="a7da1-192">It is also important for table partition switching.</span><span class="sxs-lookup"><span data-stu-id="a7da1-192">It is also important for table partition switching.</span></span> <span data-ttu-id="a7da1-193">Imagine you have this table defined as your fact:</span><span class="sxs-lookup"><span data-stu-id="a7da1-193">Imagine you have this table defined as your fact:</span></span>

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

<span data-ttu-id="a7da1-194">However, the value field is a calculated expression it is not part of the source data.</span><span class="sxs-lookup"><span data-stu-id="a7da1-194">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="a7da1-195">To create your partitioned dataset you might want to do this:</span><span class="sxs-lookup"><span data-stu-id="a7da1-195">To create your partitioned dataset you might want to do this:</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

<span data-ttu-id="a7da1-196">The query would run perfectly fine.</span><span class="sxs-lookup"><span data-stu-id="a7da1-196">The query would run perfectly fine.</span></span> <span data-ttu-id="a7da1-197">The problem comes when you try to perform the partition switch.</span><span class="sxs-lookup"><span data-stu-id="a7da1-197">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="a7da1-198">The table definitions do not match.</span><span class="sxs-lookup"><span data-stu-id="a7da1-198">The table definitions do not match.</span></span> <span data-ttu-id="a7da1-199">To make the table definitions match the CTAS needs to be modified.</span><span class="sxs-lookup"><span data-stu-id="a7da1-199">To make the table definitions match the CTAS needs to be modified.</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

<span data-ttu-id="a7da1-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span><span class="sxs-lookup"><span data-stu-id="a7da1-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="a7da1-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span><span class="sxs-lookup"><span data-stu-id="a7da1-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="a7da1-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="a7da1-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="a7da1-203">It is one of the most important statements in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a7da1-203">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a7da1-204">Make sure you thoroughly understand it.</span><span class="sxs-lookup"><span data-stu-id="a7da1-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7da1-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7da1-205">Next steps</span></span>
<span data-ttu-id="a7da1-206">For more development tips, see [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="a7da1-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->

