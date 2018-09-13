---
title: Group by options in SQL Data Warehouse | Microsoft Docs
description: Tips for implementing group by options in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: ce1eecdd10c260074f4fe5560d07106e31e6ca80
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555529"
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="a2937-103">Group by options in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a2937-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="a2937-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span><span class="sxs-lookup"><span data-stu-id="a2937-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="a2937-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a2937-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="a2937-106">These options are</span><span class="sxs-lookup"><span data-stu-id="a2937-106">These options are</span></span>

* <span data-ttu-id="a2937-107">GROUP BY with ROLLUP</span><span class="sxs-lookup"><span data-stu-id="a2937-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="a2937-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="a2937-108">GROUPING SETS</span></span>
* <span data-ttu-id="a2937-109">GROUP BY with CUBE</span><span class="sxs-lookup"><span data-stu-id="a2937-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="a2937-110">Rollup and grouping sets options</span><span class="sxs-lookup"><span data-stu-id="a2937-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="a2937-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span><span class="sxs-lookup"><span data-stu-id="a2937-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="a2937-112">The result is exactly the same</span><span class="sxs-lookup"><span data-stu-id="a2937-112">The result is exactly the same</span></span>

<span data-ttu-id="a2937-113">Below is an example of a group by statement using the `ROLLUP` option:</span><span class="sxs-lookup"><span data-stu-id="a2937-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="a2937-114">By using ROLLUP we have requested the following aggregations:</span><span class="sxs-lookup"><span data-stu-id="a2937-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="a2937-115">Country and Region</span><span class="sxs-lookup"><span data-stu-id="a2937-115">Country and Region</span></span>
* <span data-ttu-id="a2937-116">Country</span><span class="sxs-lookup"><span data-stu-id="a2937-116">Country</span></span>
* <span data-ttu-id="a2937-117">Grand Total</span><span class="sxs-lookup"><span data-stu-id="a2937-117">Grand Total</span></span>

<span data-ttu-id="a2937-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span><span class="sxs-lookup"><span data-stu-id="a2937-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="a2937-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span><span class="sxs-lookup"><span data-stu-id="a2937-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="a2937-120">Cube options</span><span class="sxs-lookup"><span data-stu-id="a2937-120">Cube options</span></span>
<span data-ttu-id="a2937-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span><span class="sxs-lookup"><span data-stu-id="a2937-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="a2937-122">The problem is that the code can quickly become cumbersome and unwieldy.</span><span class="sxs-lookup"><span data-stu-id="a2937-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="a2937-123">To mitigate this you can use this more advanced approach.</span><span class="sxs-lookup"><span data-stu-id="a2937-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="a2937-124">Let's use the example above.</span><span class="sxs-lookup"><span data-stu-id="a2937-124">Let's use the example above.</span></span>

<span data-ttu-id="a2937-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span><span class="sxs-lookup"><span data-stu-id="a2937-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="a2937-126">It is important to take note of the CROSS JOIN of the two derived tables.</span><span class="sxs-lookup"><span data-stu-id="a2937-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="a2937-127">This generates all the levels for us.</span><span class="sxs-lookup"><span data-stu-id="a2937-127">This generates all the levels for us.</span></span> <span data-ttu-id="a2937-128">The rest of the code is really there for formatting.</span><span class="sxs-lookup"><span data-stu-id="a2937-128">The rest of the code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="a2937-129">The results of the CTAS can be seen below:</span><span class="sxs-lookup"><span data-stu-id="a2937-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="a2937-130">The second step is to specify a target table to store interim results:</span><span class="sxs-lookup"><span data-stu-id="a2937-130">The second step is to specify a target table to store interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="a2937-131">The third step is to loop over our cube of columns performing the aggregation.</span><span class="sxs-lookup"><span data-stu-id="a2937-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="a2937-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span><span class="sxs-lookup"><span data-stu-id="a2937-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="a2937-133">Lastly we can return the results by simply reading from the #Results temporary table</span><span class="sxs-lookup"><span data-stu-id="a2937-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="a2937-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span><span class="sxs-lookup"><span data-stu-id="a2937-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2937-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2937-135">Next steps</span></span>
<span data-ttu-id="a2937-136">For more development tips, see [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="a2937-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->

