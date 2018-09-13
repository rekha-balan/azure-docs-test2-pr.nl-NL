---
title: CREATE TABLE AS SELECT (CTAS) in Azure SQL Data Warehouse | Microsoft Docs
description: Tips for coding with the CREATE TABLE AS SELECT (CTAS) statement in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
author: ckarst
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: cakarst
ms.reviewer: igorstan
ms.openlocfilehash: dad0b1570f54cde1b1d474d8ebfc78f793724ef4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818836"
---
# <a name="using-create-table-as-select-ctas-in-azure-sql-data-warehouse"></a><span data-ttu-id="231ca-103">Using CREATE TABLE AS SELECT (CTAS) in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="231ca-103">Using CREATE TABLE AS SELECT (CTAS) in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="231ca-104">Tips for coding with the CREATE TABLE AS SELECT (CTAS) T-SQL statement in Azure SQL Data Warehouse for developing solutions.</span><span class="sxs-lookup"><span data-stu-id="231ca-104">Tips for coding with the CREATE TABLE AS SELECT (CTAS) T-SQL statement in Azure SQL Data Warehouse for developing solutions.</span></span>

## <a name="what-is-create-table-as-select-ctas"></a><span data-ttu-id="231ca-105">What is CREATE TABLE AS SELECT (CTAS)?</span><span class="sxs-lookup"><span data-stu-id="231ca-105">What is CREATE TABLE AS SELECT (CTAS)?</span></span>

<span data-ttu-id="231ca-106">The [CREATE TABLE AS SELECT](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) or CTAS statement is one of the most important T-SQL features available.</span><span class="sxs-lookup"><span data-stu-id="231ca-106">The [CREATE TABLE AS SELECT](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) or CTAS statement is one of the most important T-SQL features available.</span></span> <span data-ttu-id="231ca-107">It is a parallel operation that creates a new table based on the output of a SELECT statement.</span><span class="sxs-lookup"><span data-stu-id="231ca-107">It is a parallel operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="231ca-108">CTASD is the simplest and fastest way to create a copy of a table.</span><span class="sxs-lookup"><span data-stu-id="231ca-108">CTASD is the simplest and fastest way to create a copy of a table.</span></span> 

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="231ca-109">SELECT..INTO vs. CTAS</span><span class="sxs-lookup"><span data-stu-id="231ca-109">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="231ca-110">You can consider CTAS as a super-charged version of the [SELECT...INTO](/sql/t-sql/queries/select-into-clause-transact-sql) statement.</span><span class="sxs-lookup"><span data-stu-id="231ca-110">You can consider CTAS as a super-charged version of the [SELECT...INTO](/sql/t-sql/queries/select-into-clause-transact-sql) statement.</span></span>

<span data-ttu-id="231ca-111">Below is an example of a simple SELECT..INTO:</span><span class="sxs-lookup"><span data-stu-id="231ca-111">Below is an example of a simple SELECT..INTO:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="231ca-112">In the preceding example, `[dbo].[FactInternetSales_new]` is be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX since these are the table defaults in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="231ca-112">In the preceding example, `[dbo].[FactInternetSales_new]` is be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX since these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="231ca-113">SELECT..INTO, however, does not allow you to change either the distribution method or the index type as part of the operation.</span><span class="sxs-lookup"><span data-stu-id="231ca-113">SELECT..INTO, however, does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="231ca-114">This is where CTAS comes in.</span><span class="sxs-lookup"><span data-stu-id="231ca-114">This is where CTAS comes in.</span></span>

<span data-ttu-id="231ca-115">To convert the previous example to CTAS is quite straight-forward:</span><span class="sxs-lookup"><span data-stu-id="231ca-115">To convert the previous example to CTAS is quite straight-forward:</span></span>

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

<span data-ttu-id="231ca-116">With CTAS you are able to change both the distribution of the table data as well as the table type.</span><span class="sxs-lookup"><span data-stu-id="231ca-116">With CTAS you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="231ca-117">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span><span class="sxs-lookup"><span data-stu-id="231ca-117">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="231ca-118">This will avoid cross distribution data movement during the operation which is more efficient.</span><span class="sxs-lookup"><span data-stu-id="231ca-118">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="231ca-119">Using CTAS to copy a table</span><span class="sxs-lookup"><span data-stu-id="231ca-119">Using CTAS to copy a table</span></span>
<span data-ttu-id="231ca-120">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span><span class="sxs-lookup"><span data-stu-id="231ca-120">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="231ca-121">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span><span class="sxs-lookup"><span data-stu-id="231ca-121">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="231ca-122">`CTAS` can also be used to change partitioning, indexing, or column types.</span><span class="sxs-lookup"><span data-stu-id="231ca-122">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="231ca-123">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="231ca-123">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

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

<span data-ttu-id="231ca-124">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span><span class="sxs-lookup"><span data-stu-id="231ca-124">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="231ca-125">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span><span class="sxs-lookup"><span data-stu-id="231ca-125">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="231ca-126">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span><span class="sxs-lookup"><span data-stu-id="231ca-126">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="231ca-127">Here is the CTAS statement which would copy your old table into a new table.</span><span class="sxs-lookup"><span data-stu-id="231ca-127">Here is the CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="231ca-128">Finally you can rename your tables to swap in your new table and then drop your old table.</span><span class="sxs-lookup"><span data-stu-id="231ca-128">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="231ca-129">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span><span class="sxs-lookup"><span data-stu-id="231ca-129">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="231ca-130">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span><span class="sxs-lookup"><span data-stu-id="231ca-130">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="231ca-131">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span><span class="sxs-lookup"><span data-stu-id="231ca-131">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="231ca-132">Using CTAS to work around unsupported features</span><span class="sxs-lookup"><span data-stu-id="231ca-132">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="231ca-133">CTAS can also be used to work around a number of the unsupported features listed below.</span><span class="sxs-lookup"><span data-stu-id="231ca-133">CTAS can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="231ca-134">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="231ca-134">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="231ca-135">This is as a result of its fully parallelized design.</span><span class="sxs-lookup"><span data-stu-id="231ca-135">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="231ca-136">Scenarios that can be worked around with CTAS include:</span><span class="sxs-lookup"><span data-stu-id="231ca-136">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="231ca-137">ANSI JOINS on UPDATEs</span><span class="sxs-lookup"><span data-stu-id="231ca-137">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="231ca-138">ANSI JOINs on DELETEs</span><span class="sxs-lookup"><span data-stu-id="231ca-138">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="231ca-139">MERGE statement</span><span class="sxs-lookup"><span data-stu-id="231ca-139">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="231ca-140">Try to think "CTAS first".</span><span class="sxs-lookup"><span data-stu-id="231ca-140">Try to think "CTAS first".</span></span> <span data-ttu-id="231ca-141">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span><span class="sxs-lookup"><span data-stu-id="231ca-141">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="231ca-142">ANSI join replacement for update statements</span><span class="sxs-lookup"><span data-stu-id="231ca-142">ANSI join replacement for update statements</span></span>
<span data-ttu-id="231ca-143">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span><span class="sxs-lookup"><span data-stu-id="231ca-143">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="231ca-144">Imagine you had to update this table:</span><span class="sxs-lookup"><span data-stu-id="231ca-144">Imagine you had to update this table:</span></span>

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

<span data-ttu-id="231ca-145">The original query might have looked something like this:</span><span class="sxs-lookup"><span data-stu-id="231ca-145">The original query might have looked something like this:</span></span>

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

<span data-ttu-id="231ca-146">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span><span class="sxs-lookup"><span data-stu-id="231ca-146">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="231ca-147">You can use a combination of a `CTAS` and an implicit join to replace this code:</span><span class="sxs-lookup"><span data-stu-id="231ca-147">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

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

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="231ca-148">ANSI join replacement for delete statements</span><span class="sxs-lookup"><span data-stu-id="231ca-148">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="231ca-149">Sometimes the best approach for deleting data is to use `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="231ca-149">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="231ca-150">Rather than deleting the data simply select the data you want to keep.</span><span class="sxs-lookup"><span data-stu-id="231ca-150">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="231ca-151">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span><span class="sxs-lookup"><span data-stu-id="231ca-151">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="231ca-152">An example of a converted DELETE statement is available below:</span><span class="sxs-lookup"><span data-stu-id="231ca-152">An example of a converted DELETE statement is available below:</span></span>

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

## <a name="replace-merge-statements"></a><span data-ttu-id="231ca-153">Replace merge statements</span><span class="sxs-lookup"><span data-stu-id="231ca-153">Replace merge statements</span></span>
<span data-ttu-id="231ca-154">Merge statements can be replaced, at least in part, by using CTAS.</span><span class="sxs-lookup"><span data-stu-id="231ca-154">Merge statements can be replaced, at least in part, by using CTAS.</span></span> <span data-ttu-id="231ca-155">You can consolidate the INSERT and the UPDATE into a single statement.</span><span class="sxs-lookup"><span data-stu-id="231ca-155">You can consolidate the INSERT and the UPDATE into a single statement.</span></span> <span data-ttu-id="231ca-156">Any deleted records would need to be closed off in a second statement.</span><span class="sxs-lookup"><span data-stu-id="231ca-156">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="231ca-157">The following is an example of an UPSERT:</span><span class="sxs-lookup"><span data-stu-id="231ca-157">The following is an example of an UPSERT:</span></span>

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="231ca-158">CTAS recommendation: Explicitly state data type and nullability of output</span><span class="sxs-lookup"><span data-stu-id="231ca-158">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="231ca-159">When migrating code you might find you run across this type of coding pattern:</span><span class="sxs-lookup"><span data-stu-id="231ca-159">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="231ca-160">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span><span class="sxs-lookup"><span data-stu-id="231ca-160">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="231ca-161">However, there is a hidden issue here.</span><span class="sxs-lookup"><span data-stu-id="231ca-161">However, there is a hidden issue here.</span></span>

<span data-ttu-id="231ca-162">The following code does NOT yield the same result:</span><span class="sxs-lookup"><span data-stu-id="231ca-162">The following code does NOT yield the same result:</span></span>

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

<span data-ttu-id="231ca-163">Notice that the column "result" carries forward the data type and nullability values of the expression.</span><span class="sxs-lookup"><span data-stu-id="231ca-163">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="231ca-164">This can lead to subtle variances in values if you aren't careful.</span><span class="sxs-lookup"><span data-stu-id="231ca-164">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="231ca-165">Try the following as an example:</span><span class="sxs-lookup"><span data-stu-id="231ca-165">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="231ca-166">The value stored for result is different.</span><span class="sxs-lookup"><span data-stu-id="231ca-166">The value stored for result is different.</span></span> <span data-ttu-id="231ca-167">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span><span class="sxs-lookup"><span data-stu-id="231ca-167">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![CTAS results](media/sql-data-warehouse-develop-ctas/ctas-results.png)

<span data-ttu-id="231ca-169">This is particularly important for data migrations.</span><span class="sxs-lookup"><span data-stu-id="231ca-169">This is particularly important for data migrations.</span></span> <span data-ttu-id="231ca-170">Even though the second query is arguably more accurate there is a problem.</span><span class="sxs-lookup"><span data-stu-id="231ca-170">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="231ca-171">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span><span class="sxs-lookup"><span data-stu-id="231ca-171">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="231ca-172">This is one of those rare cases where the "wrong" answer is actually the right one!</span><span class="sxs-lookup"><span data-stu-id="231ca-172">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="231ca-173">The reason we see this disparity between the two results is down to implicit type casting.</span><span class="sxs-lookup"><span data-stu-id="231ca-173">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="231ca-174">In the first example the table defines the column definition.</span><span class="sxs-lookup"><span data-stu-id="231ca-174">In the first example the table defines the column definition.</span></span> <span data-ttu-id="231ca-175">When the row is inserted an implicit type conversion occurs.</span><span class="sxs-lookup"><span data-stu-id="231ca-175">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="231ca-176">In the second example there is no implicit type conversion as the expression defines data type of the column.</span><span class="sxs-lookup"><span data-stu-id="231ca-176">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="231ca-177">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span><span class="sxs-lookup"><span data-stu-id="231ca-177">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="231ca-178">When the table was created in the first example column nullability was explicitly defined.</span><span class="sxs-lookup"><span data-stu-id="231ca-178">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="231ca-179">In the second example it was just left to the expression and by default this would result in a NULL definition.</span><span class="sxs-lookup"><span data-stu-id="231ca-179">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="231ca-180">To resolve these issues you must explicitly set the type conversion and nullability in the SELECT portion of the CTAS statement.</span><span class="sxs-lookup"><span data-stu-id="231ca-180">To resolve these issues you must explicitly set the type conversion and nullability in the SELECT portion of the CTAS statement.</span></span> <span data-ttu-id="231ca-181">You cannot set these properties in the create table part.</span><span class="sxs-lookup"><span data-stu-id="231ca-181">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="231ca-182">The example below demonstrates how to fix the code:</span><span class="sxs-lookup"><span data-stu-id="231ca-182">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="231ca-183">Note the following:</span><span class="sxs-lookup"><span data-stu-id="231ca-183">Note the following:</span></span>

* <span data-ttu-id="231ca-184">CAST or CONVERT could have been used</span><span class="sxs-lookup"><span data-stu-id="231ca-184">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="231ca-185">ISNULL is used to force NULLability not COALESCE</span><span class="sxs-lookup"><span data-stu-id="231ca-185">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="231ca-186">ISNULL is the outermost function</span><span class="sxs-lookup"><span data-stu-id="231ca-186">ISNULL is the outermost function</span></span>
* <span data-ttu-id="231ca-187">The second part of the ISNULL is a constant i.e. 0</span><span class="sxs-lookup"><span data-stu-id="231ca-187">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="231ca-188">For the nullability to be correctly set it is vital to use ISNULL and not COALESCE.</span><span class="sxs-lookup"><span data-stu-id="231ca-188">For the nullability to be correctly set it is vital to use ISNULL and not COALESCE.</span></span> <span data-ttu-id="231ca-189">COALESCE is not a deterministic function and so the result of the expression will always be NULLable.</span><span class="sxs-lookup"><span data-stu-id="231ca-189">COALESCE is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="231ca-190">ISNULL is different.</span><span class="sxs-lookup"><span data-stu-id="231ca-190">ISNULL is different.</span></span> <span data-ttu-id="231ca-191">It is deterministic.</span><span class="sxs-lookup"><span data-stu-id="231ca-191">It is deterministic.</span></span> <span data-ttu-id="231ca-192">Therefore when the second part of the ISNULL function is a constant or a literal then the resulting value will be NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="231ca-192">Therefore when the second part of the ISNULL function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="231ca-193">This tip is not just useful for ensuring the integrity of your calculations.</span><span class="sxs-lookup"><span data-stu-id="231ca-193">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="231ca-194">It is also important for table partition switching.</span><span class="sxs-lookup"><span data-stu-id="231ca-194">It is also important for table partition switching.</span></span> <span data-ttu-id="231ca-195">Imagine you have this table defined as your fact:</span><span class="sxs-lookup"><span data-stu-id="231ca-195">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="231ca-196">However, the value field is a calculated expression it is not part of the source data.</span><span class="sxs-lookup"><span data-stu-id="231ca-196">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="231ca-197">To create your partitioned dataset you might want to do this:</span><span class="sxs-lookup"><span data-stu-id="231ca-197">To create your partitioned dataset you might want to do this:</span></span>

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

<span data-ttu-id="231ca-198">The query would run perfectly fine.</span><span class="sxs-lookup"><span data-stu-id="231ca-198">The query would run perfectly fine.</span></span> <span data-ttu-id="231ca-199">The problem comes when you try to perform the partition switch.</span><span class="sxs-lookup"><span data-stu-id="231ca-199">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="231ca-200">The table definitions do not match.</span><span class="sxs-lookup"><span data-stu-id="231ca-200">The table definitions do not match.</span></span> <span data-ttu-id="231ca-201">To make the table definitions match the CTAS needs to be modified.</span><span class="sxs-lookup"><span data-stu-id="231ca-201">To make the table definitions match the CTAS needs to be modified.</span></span>

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

<span data-ttu-id="231ca-202">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span><span class="sxs-lookup"><span data-stu-id="231ca-202">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="231ca-203">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span><span class="sxs-lookup"><span data-stu-id="231ca-203">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="231ca-204">Please refer to the [CTAS](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) documentation.</span><span class="sxs-lookup"><span data-stu-id="231ca-204">Please refer to the [CTAS](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) documentation.</span></span> <span data-ttu-id="231ca-205">It is one of the most important statements in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="231ca-205">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="231ca-206">Make sure you thoroughly understand it.</span><span class="sxs-lookup"><span data-stu-id="231ca-206">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="231ca-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="231ca-207">Next steps</span></span>
<span data-ttu-id="231ca-208">For more development tips, see [development overview](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="231ca-208">For more development tips, see [development overview](sql-data-warehouse-overview-develop.md).</span></span>

