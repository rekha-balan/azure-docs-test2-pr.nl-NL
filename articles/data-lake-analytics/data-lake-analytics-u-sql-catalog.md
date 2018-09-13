---
title: Get started with the U-SQL catalog in Azure Data Lake Analytics
description: Learn how to use the U-SQL catalog to share code and data.
services: data-lake-analytics
ms.service: data-lake-analytics
author: saveenr
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.topic: conceptual
ms.date: 05/09/2017
ms.openlocfilehash: 62f43fc082969bf04b7177725478585ce41aa347
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868777"
---
# <a name="get-started-with-the-u-sql-catalog-in-azure-data-lake-analytics"></a><span data-ttu-id="0b0b2-103">Get started with the U-SQL Catalog in Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0b0b2-103">Get started with the U-SQL Catalog in Azure Data Lake Analytics</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="0b0b2-104">Create a TVF</span><span class="sxs-lookup"><span data-stu-id="0b0b2-104">Create a TVF</span></span>

<span data-ttu-id="0b0b2-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="0b0b2-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="0b0b2-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

<span data-ttu-id="0b0b2-108">The following script shows you how to use the TVF that was defined in the previous script:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="0b0b2-109">Create views</span><span class="sxs-lookup"><span data-stu-id="0b0b2-109">Create views</span></span>

<span data-ttu-id="0b0b2-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="0b0b2-111">The following script creates a view called `SearchlogView` in the default database and schema:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

<span data-ttu-id="0b0b2-112">The following script demonstrates the use of the defined view:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="0b0b2-113">Create tables</span><span class="sxs-lookup"><span data-stu-id="0b0b2-113">Create tables</span></span>
<span data-ttu-id="0b0b2-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="0b0b2-115">Create a database and two tables by using the following script:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-115">Create a database and two tables by using the following script:</span></span>

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a><span data-ttu-id="0b0b2-116">Query tables</span><span class="sxs-lookup"><span data-stu-id="0b0b2-116">Query tables</span></span>
<span data-ttu-id="0b0b2-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="0b0b2-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="0b0b2-119">To read from the tables, modify the transform script that you used previously:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-119">To read from the tables, modify the transform script that you used previously:</span></span>

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="0b0b2-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b0b2-121">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0b0b2-121">Next Steps</span></span>
* [<span data-ttu-id="0b0b2-122">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0b0b2-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="0b0b2-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b0b2-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="0b0b2-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="0b0b2-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
