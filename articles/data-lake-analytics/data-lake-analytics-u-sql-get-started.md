---
title: Get started with U-SQL language in Azure Data Lake Analytics
description: Learn the basics of the U-SQL language in Azure Data Lake Analytics.
services: data-lake-analytics
author: saveenr
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.topic: conceptual
ms.date: 06/23/2017
ms.openlocfilehash: 1822ac9b539aa196601c6c07ccc8d0544fd5f3dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827502"
---
# <a name="get-started-with-u-sql-in-azure-data-lake-analytics"></a><span data-ttu-id="593d5-103">Get started with U-SQL in Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="593d5-103">Get started with U-SQL in Azure Data Lake Analytics</span></span>
<span data-ttu-id="593d5-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span><span class="sxs-lookup"><span data-stu-id="593d5-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span></span> <span data-ttu-id="593d5-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="593d5-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="593d5-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span><span class="sxs-lookup"><span data-stu-id="593d5-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="593d5-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span><span class="sxs-lookup"><span data-stu-id="593d5-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="593d5-108">Learning resources</span><span class="sxs-lookup"><span data-stu-id="593d5-108">Learning resources</span></span>

* <span data-ttu-id="593d5-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span><span class="sxs-lookup"><span data-stu-id="593d5-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span></span> <span data-ttu-id="593d5-110">This document is recommended reading for all developers wanting to learn U-SQL.</span><span class="sxs-lookup"><span data-stu-id="593d5-110">This document is recommended reading for all developers wanting to learn U-SQL.</span></span>
* <span data-ttu-id="593d5-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="593d5-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="593d5-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="593d5-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="593d5-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="593d5-113">Prerequisites</span></span>

<span data-ttu-id="593d5-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="593d5-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="593d5-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="593d5-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="593d5-116">Your first U-SQL script</span><span class="sxs-lookup"><span data-stu-id="593d5-116">Your first U-SQL script</span></span>

<span data-ttu-id="593d5-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span><span class="sxs-lookup"><span data-stu-id="593d5-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span></span>

```
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

OUTPUT @searchlog   
    TO "/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="593d5-118">This script doesn't have any transformation steps.</span><span class="sxs-lookup"><span data-stu-id="593d5-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="593d5-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="593d5-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="593d5-120">Notice the question mark next to the data type in the `Duration` field.</span><span class="sxs-lookup"><span data-stu-id="593d5-120">Notice the question mark next to the data type in the `Duration` field.</span></span> <span data-ttu-id="593d5-121">It means that the `Duration` field could be null.</span><span class="sxs-lookup"><span data-stu-id="593d5-121">It means that the `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="593d5-122">Key concepts</span><span class="sxs-lookup"><span data-stu-id="593d5-122">Key concepts</span></span>
* <span data-ttu-id="593d5-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span><span class="sxs-lookup"><span data-stu-id="593d5-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="593d5-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span><span class="sxs-lookup"><span data-stu-id="593d5-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span></span>
* <span data-ttu-id="593d5-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span><span class="sxs-lookup"><span data-stu-id="593d5-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span></span> <span data-ttu-id="593d5-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span><span class="sxs-lookup"><span data-stu-id="593d5-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="593d5-127">You can develop custom extractors.</span><span class="sxs-lookup"><span data-stu-id="593d5-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="593d5-128">The **OUTPUT** writes data from a rowset to a file.</span><span class="sxs-lookup"><span data-stu-id="593d5-128">The **OUTPUT** writes data from a rowset to a file.</span></span> <span data-ttu-id="593d5-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span><span class="sxs-lookup"><span data-stu-id="593d5-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span></span> <span data-ttu-id="593d5-130">You can develop custom outputters.</span><span class="sxs-lookup"><span data-stu-id="593d5-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="593d5-131">File paths</span><span class="sxs-lookup"><span data-stu-id="593d5-131">File paths</span></span>

<span data-ttu-id="593d5-132">The EXTRACT and OUTPUT statements use file paths.</span><span class="sxs-lookup"><span data-stu-id="593d5-132">The EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="593d5-133">File paths can be absolute or relative:</span><span class="sxs-lookup"><span data-stu-id="593d5-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="593d5-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span><span class="sxs-lookup"><span data-stu-id="593d5-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="593d5-135">This following file path starts with `"/"`.</span><span class="sxs-lookup"><span data-stu-id="593d5-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="593d5-136">It refers to a file in the default Data Lake Store account:</span><span class="sxs-lookup"><span data-stu-id="593d5-136">It refers to a file in the default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="593d5-137">Use scalar variables</span><span class="sxs-lookup"><span data-stu-id="593d5-137">Use scalar variables</span></span>

<span data-ttu-id="593d5-138">You can use scalar variables as well to make your script maintenance easier.</span><span class="sxs-lookup"><span data-stu-id="593d5-138">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="593d5-139">The previous U-SQL script can also be written as:</span><span class="sxs-lookup"><span data-stu-id="593d5-139">The previous U-SQL script can also be written as:</span></span>

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO @out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="593d5-140">Transform rowsets</span><span class="sxs-lookup"><span data-stu-id="593d5-140">Transform rowsets</span></span>

<span data-ttu-id="593d5-141">Use **SELECT** to transform rowsets:</span><span class="sxs-lookup"><span data-stu-id="593d5-141">Use **SELECT** to transform rowsets:</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="593d5-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="593d5-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="593d5-143">You can use the C# expression language to do your own expressions and functions.</span><span class="sxs-lookup"><span data-stu-id="593d5-143">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="593d5-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span><span class="sxs-lookup"><span data-stu-id="593d5-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="593d5-145">The following script uses the DateTime.Parse() method and a conjunction.</span><span class="sxs-lookup"><span data-stu-id="593d5-145">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="593d5-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span><span class="sxs-lookup"><span data-stu-id="593d5-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="593d5-147">You can also reuse a variable name, and the names are scoped lexically.</span><span class="sxs-lookup"><span data-stu-id="593d5-147">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="593d5-148">Aggregate rowsets</span><span class="sxs-lookup"><span data-stu-id="593d5-148">Aggregate rowsets</span></span>
<span data-ttu-id="593d5-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span><span class="sxs-lookup"><span data-stu-id="593d5-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="593d5-150">The following query finds the total duration per region, and then displays the top five durations in order.</span><span class="sxs-lookup"><span data-stu-id="593d5-150">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="593d5-151">U-SQL rowsets do not preserve their order for the next query.</span><span class="sxs-lookup"><span data-stu-id="593d5-151">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="593d5-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span><span class="sxs-lookup"><span data-stu-id="593d5-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

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

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        TO @out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        TO @out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="593d5-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span><span class="sxs-lookup"><span data-stu-id="593d5-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="593d5-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span><span class="sxs-lookup"><span data-stu-id="593d5-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

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

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        TO "/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="593d5-155">For advanced aggregation scenarios, see the U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="593d5-155">For advanced aggregation scenarios, see the U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="593d5-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="593d5-156">Next steps</span></span>
* [<span data-ttu-id="593d5-157">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="593d5-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="593d5-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="593d5-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
