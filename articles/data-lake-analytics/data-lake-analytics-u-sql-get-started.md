---
title: 'Tutorial: Get started with Azure Data Lake Analytics U-SQL language | Microsoft Docs'
description: Use this tutorial to learn about the Azure Data Lake Analytics U-SQL language.
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: dc8c7beaf5b8e8d4f5467ffe22390c41f446d787
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562818"
---
# <a name="tutorial-get-started-with-azure-data-lake-analytics-u-sql-language"></a><span data-ttu-id="6cc6b-103">Tutorial: Get started with Azure Data Lake Analytics U-SQL language</span><span class="sxs-lookup"><span data-stu-id="6cc6b-103">Tutorial: Get started with Azure Data Lake Analytics U-SQL language</span></span>
<span data-ttu-id="6cc6b-104">U-SQL is a language that combines the benefits of SQL with the expressive power of your own code to process data at any scale.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-104">U-SQL is a language that combines the benefits of SQL with the expressive power of your own code to process data at any scale.</span></span> <span data-ttu-id="6cc6b-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="6cc6b-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="6cc6b-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> <span data-ttu-id="6cc6b-108">To learn more about the design philosophy behind U-SQL, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-108">To learn more about the design philosophy behind U-SQL, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="6cc6b-109">U-SQL differs in some ways from ANSI SQL or T-SQL.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-109">U-SQL differs in some ways from ANSI SQL or T-SQL.</span></span> <span data-ttu-id="6cc6b-110">For example, keywords such as SELECT must be in all-uppercase letters.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-110">For example, keywords such as SELECT must be in all-uppercase letters.</span></span>

 <span data-ttu-id="6cc6b-111">Its type system and expression language, inside SELECT clauses and WHERE predicates, are C#.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-111">Its type system and expression language, inside SELECT clauses and WHERE predicates, are C#.</span></span> <span data-ttu-id="6cc6b-112">This means that the data types are the C# types, they use C# NULL semantics, and the comparison operations inside a predicate follow C# syntax (for example, a == "foo").</span><span class="sxs-lookup"><span data-stu-id="6cc6b-112">This means that the data types are the C# types, they use C# NULL semantics, and the comparison operations inside a predicate follow C# syntax (for example, a == "foo").</span></span> <span data-ttu-id="6cc6b-113">It also means that the values are full .NET objects, so you can easily use any method to operate on the object (for example, "f o o o".Split(' ')).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-113">It also means that the values are full .NET objects, so you can easily use any method to operate on the object (for example, "f o o o".Split(' ')).</span></span>

<span data-ttu-id="6cc6b-114">For more information about U-SQL, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-114">For more information about U-SQL, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6cc6b-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6cc6b-115">Prerequisites</span></span>
<span data-ttu-id="6cc6b-116">If you have not already done so, please read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-116">If you have not already done so, please read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="6cc6b-117">After you have completed the tutorial, return to this article.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-117">After you have completed the tutorial, return to this article.</span></span>

<span data-ttu-id="6cc6b-118">In the tutorial, you ran an Azure Data Lake Analytics job with the following U-SQL script:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-118">In the tutorial, you ran an Azure Data Lake Analytics job with the following U-SQL script:</span></span>

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

<span data-ttu-id="6cc6b-119">This script doesn't have any transformation steps.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-119">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="6cc6b-120">It reads from the source file called SearchLog.tsv, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-120">It reads from the source file called SearchLog.tsv, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="6cc6b-121">Notice the question mark next to the data type in the **Duration** field.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-121">Notice the question mark next to the data type in the **Duration** field.</span></span> <span data-ttu-id="6cc6b-122">It means that the **Duration** field could be null.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-122">It means that the **Duration** field could be null.</span></span>

<span data-ttu-id="6cc6b-123">In the script, you'll find the following concepts and keywords:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-123">In the script, you'll find the following concepts and keywords:</span></span>

* <span data-ttu-id="6cc6b-124">Rowset variables: Each query expression that produces a rowset can be assigned to a variable.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-124">Rowset variables: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="6cc6b-125">U-SQL follows the T-SQL variable naming pattern (@searchlog, for example) in the script.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-125">U-SQL follows the T-SQL variable naming pattern (@searchlog, for example) in the script.</span></span>

 >[!NOTE]
 ><span data-ttu-id="6cc6b-126">The assignment does not force execution.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-126">The assignment does not force execution.</span></span> <span data-ttu-id="6cc6b-127">It merely names the expression so that you can build up more complex expressions.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-127">It merely names the expression so that you can build up more complex expressions.</span></span>
* <span data-ttu-id="6cc6b-128">EXTRACT: By using this keyword, you can define a schema on read.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-128">EXTRACT: By using this keyword, you can define a schema on read.</span></span> <span data-ttu-id="6cc6b-129">The schema is specified by a column name and C# type name pair per column.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-129">The schema is specified by a column name and C# type name pair per column.</span></span> <span data-ttu-id="6cc6b-130">The schema uses a so-called extractor (Extractors.Tsv(), for example) to extract .tsv files.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-130">The schema uses a so-called extractor (Extractors.Tsv(), for example) to extract .tsv files.</span></span> <span data-ttu-id="6cc6b-131">You can develop custom extractors.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-131">You can develop custom extractors.</span></span>
* <span data-ttu-id="6cc6b-132">OUTPUT: This keyword takes a rowset and serializes it.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-132">OUTPUT: This keyword takes a rowset and serializes it.</span></span> <span data-ttu-id="6cc6b-133">Outputters.Csv() writes a comma-separated file into the specified location.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-133">Outputters.Csv() writes a comma-separated file into the specified location.</span></span> <span data-ttu-id="6cc6b-134">You can also develop custom outputters.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-134">You can also develop custom outputters.</span></span>

 >[!NOTE]
 ><span data-ttu-id="6cc6b-135">The two paths are relative paths.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-135">The two paths are relative paths.</span></span> <span data-ttu-id="6cc6b-136">You can also use absolute paths.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-136">You can also use absolute paths.</span></span> <span data-ttu-id="6cc6b-137">For example:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-137">For example:</span></span>    
 >     <span data-ttu-id="6cc6b-138">adl://\<ADLStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv</span><span class="sxs-lookup"><span data-stu-id="6cc6b-138">adl://\<ADLStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv</span></span>
 >
 ><span data-ttu-id="6cc6b-139">You must use an absolute path to access the files in the linked storage accounts.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-139">You must use an absolute path to access the files in the linked storage accounts.</span></span>  <span data-ttu-id="6cc6b-140">The syntax for files stored in linked Azure storage account is: wasb://\<BlobContainerName>@\<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv</span><span class="sxs-lookup"><span data-stu-id="6cc6b-140">The syntax for files stored in linked Azure storage account is: wasb://\<BlobContainerName>@\<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv</span></span>

 >[!NOTE]
 ><span data-ttu-id="6cc6b-141">Azure Blob storage containers with public blobs or public containers access permissions are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-141">Azure Blob storage containers with public blobs or public containers access permissions are not currently supported.</span></span>

## <a name="use-scalar-variables"></a><span data-ttu-id="6cc6b-142">Use scalar variables</span><span class="sxs-lookup"><span data-stu-id="6cc6b-142">Use scalar variables</span></span>
<span data-ttu-id="6cc6b-143">You can use scalar variables as well to make your script maintenance easier.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-143">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="6cc6b-144">The previous U-SQL script can also be written as:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-144">The previous U-SQL script can also be written as:</span></span>

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

## <a name="transform-rowsets"></a><span data-ttu-id="6cc6b-145">Transform rowsets</span><span class="sxs-lookup"><span data-stu-id="6cc6b-145">Transform rowsets</span></span>
<span data-ttu-id="6cc6b-146">Use **SELECT** to transform rowsets:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-146">Use **SELECT** to transform rowsets:</span></span>

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

<span data-ttu-id="6cc6b-147">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-147">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="6cc6b-148">You can use the C# expression language to do your own expressions and functions.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-148">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="6cc6b-149">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-149">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="6cc6b-150">The following script uses the DateTime.Parse() method and a conjunction.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-150">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

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
        TO "/output/SearchLog-transform-datatime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="6cc6b-151">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-151">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="6cc6b-152">You can also reuse a variable name, and the names are scoped lexically.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-152">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="6cc6b-153">Aggregate rowsets</span><span class="sxs-lookup"><span data-stu-id="6cc6b-153">Aggregate rowsets</span></span>
<span data-ttu-id="6cc6b-154">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-154">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="6cc6b-155">The following query finds the total duration per region, and then displays the top five durations in order.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-155">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="6cc6b-156">U-SQL rowsets do not preserve their order for the next query.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-156">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="6cc6b-157">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-157">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

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

<span data-ttu-id="6cc6b-158">The U-SQL ORDER BY clause has to be combined with the FETCH clause in a SELECT expression.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-158">The U-SQL ORDER BY clause has to be combined with the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="6cc6b-159">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-159">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

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

## <a name="join-data"></a><span data-ttu-id="6cc6b-160">Join data</span><span class="sxs-lookup"><span data-stu-id="6cc6b-160">Join data</span></span>
<span data-ttu-id="6cc6b-161">U-SQL provides common join operators such as INNER JOIN, LEFT/RIGHT/FULL OUTER JOIN, SEMI JOIN, to join not only tables but any rowsets (even those produced from files).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-161">U-SQL provides common join operators such as INNER JOIN, LEFT/RIGHT/FULL OUTER JOIN, SEMI JOIN, to join not only tables but any rowsets (even those produced from files).</span></span>

<span data-ttu-id="6cc6b-162">The following script joins the searchlog with an advertisement impression log and gives us the advertisements for the query string for a given date.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-162">The following script joins the searchlog with an advertisement impression log and gives us the advertisements for the query string for a given date.</span></span>

    @adlog =
        EXTRACT UserId int,
                Ad string,
                Clicked int
        FROM "/Samples/Data/AdsLog.tsv"
        USING Extractors.Tsv();

    @join =
        SELECT a.Ad, s.Query, s.Start AS Date
        FROM @adlog AS a JOIN <insert your DB name>.dbo.SearchLog1 AS s
                        ON a.UserId == s.UserId
        WHERE a.Clicked == 1;

    OUTPUT @join   
        TO "/output/Searchlog-join.csv"
        USING Outputters.Csv();


<span data-ttu-id="6cc6b-163">U-SQL supports only the ANSI-compliant join syntax: Rowset1 JOIN Rowset2 ON predicate.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-163">U-SQL supports only the ANSI-compliant join syntax: Rowset1 JOIN Rowset2 ON predicate.</span></span> <span data-ttu-id="6cc6b-164">The old syntax of FROM Rowset1, Rowset2 WHERE predicate is _not_ supported.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-164">The old syntax of FROM Rowset1, Rowset2 WHERE predicate is _not_ supported.</span></span>
<span data-ttu-id="6cc6b-165">The predicate in a JOIN has to be an equality join and no expression.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-165">The predicate in a JOIN has to be an equality join and no expression.</span></span> <span data-ttu-id="6cc6b-166">If you want to use an expression, add it to a previous rowset's select clause.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-166">If you want to use an expression, add it to a previous rowset's select clause.</span></span> <span data-ttu-id="6cc6b-167">If you want to do a different comparison, you can move it into the WHERE clause.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-167">If you want to do a different comparison, you can move it into the WHERE clause.</span></span>

## <a name="create-databases-table-valued-functions-views-and-tables"></a><span data-ttu-id="6cc6b-168">Create databases, table-valued functions, views, and tables</span><span class="sxs-lookup"><span data-stu-id="6cc6b-168">Create databases, table-valued functions, views, and tables</span></span>
<span data-ttu-id="6cc6b-169">In U-SQL, you can use data in the context of a database and schema, and you don't always have to read from or write to files.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-169">In U-SQL, you can use data in the context of a database and schema, and you don't always have to read from or write to files.</span></span>

<span data-ttu-id="6cc6b-170">Every U-SQL script runs with a default database (master) and default schema (DBO) as its default context.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-170">Every U-SQL script runs with a default database (master) and default schema (DBO) as its default context.</span></span> <span data-ttu-id="6cc6b-171">You can create your own database or schema.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-171">You can create your own database or schema.</span></span> <span data-ttu-id="6cc6b-172">To change the context, use the USE statement.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-172">To change the context, use the USE statement.</span></span>

### <a name="create-a-tvf"></a><span data-ttu-id="6cc6b-173">Create a TVF</span><span class="sxs-lookup"><span data-stu-id="6cc6b-173">Create a TVF</span></span>
<span data-ttu-id="6cc6b-174">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-174">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="6cc6b-175">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-175">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="6cc6b-176">The following script creates a TVF called *Searchlog()* in the default database and schema:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-176">The following script creates a TVF called *Searchlog()* in the default database and schema:</span></span>

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

<span data-ttu-id="6cc6b-177">The following script shows you how to use the TVF that was defined in the previous script:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-177">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

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

### <a name="create-views"></a><span data-ttu-id="6cc6b-178">Create views</span><span class="sxs-lookup"><span data-stu-id="6cc6b-178">Create views</span></span>
<span data-ttu-id="6cc6b-179">If you have only one query expression that you want to abstract and do not want to create a parameter from it, you can create a view instead of a table-valued function.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-179">If you have only one query expression that you want to abstract and do not want to create a parameter from it, you can create a view instead of a table-valued function.</span></span>

<span data-ttu-id="6cc6b-180">The following script creates a view called *SearchlogView* in the default database and schema:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-180">The following script creates a view called *SearchlogView* in the default database and schema:</span></span>

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

<span data-ttu-id="6cc6b-181">The following script demonstrates the use of the defined view:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-181">The following script demonstrates the use of the defined view:</span></span>

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

### <a name="create-tables"></a><span data-ttu-id="6cc6b-182">Create tables</span><span class="sxs-lookup"><span data-stu-id="6cc6b-182">Create tables</span></span>
<span data-ttu-id="6cc6b-183">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-183">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="6cc6b-184">Create a database and two tables by using the following script:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-184">Create a database and two tables by using the following script:</span></span>

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


### <a name="query-tables"></a><span data-ttu-id="6cc6b-185">Query tables</span><span class="sxs-lookup"><span data-stu-id="6cc6b-185">Query tables</span></span>
<span data-ttu-id="6cc6b-186">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-186">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="6cc6b-187">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-187">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="6cc6b-188">To read from the tables, modify the transform script that you used previously:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-188">To read from the tables, modify the transform script that you used previously:</span></span>

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

 >[!NOTE]
 ><span data-ttu-id="6cc6b-189">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-189">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="conclusion"></a><span data-ttu-id="6cc6b-190">Conclusion</span><span class="sxs-lookup"><span data-stu-id="6cc6b-190">Conclusion</span></span>
<span data-ttu-id="6cc6b-191">This tutorial covers only a small part of U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-191">This tutorial covers only a small part of U-SQL.</span></span> <span data-ttu-id="6cc6b-192">Because of its limited scope, the tutorial has not discussed many other benefits of U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-192">Because of its limited scope, the tutorial has not discussed many other benefits of U-SQL.</span></span> <span data-ttu-id="6cc6b-193">For example, you can:</span><span class="sxs-lookup"><span data-stu-id="6cc6b-193">For example, you can:</span></span>

* <span data-ttu-id="6cc6b-194">Use CROSS APPLY to unpack parts of strings, arrays, and maps into rows.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-194">Use CROSS APPLY to unpack parts of strings, arrays, and maps into rows.</span></span>
* <span data-ttu-id="6cc6b-195">Operate partitioned sets of data (file sets and partitioned tables).</span><span class="sxs-lookup"><span data-stu-id="6cc6b-195">Operate partitioned sets of data (file sets and partitioned tables).</span></span>
* <span data-ttu-id="6cc6b-196">Develop user-defined operators such as extractors, outputters, processors, and user-defined aggregators in C#.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-196">Develop user-defined operators such as extractors, outputters, processors, and user-defined aggregators in C#.</span></span>
* <span data-ttu-id="6cc6b-197">Use U-SQL windowing functions.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-197">Use U-SQL windowing functions.</span></span>
* <span data-ttu-id="6cc6b-198">Manage U-SQL code with views, table-valued functions, and stored procedures.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-198">Manage U-SQL code with views, table-valued functions, and stored procedures.</span></span>
* <span data-ttu-id="6cc6b-199">Run arbitrary custom code on your processing nodes.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-199">Run arbitrary custom code on your processing nodes.</span></span>
* <span data-ttu-id="6cc6b-200">Connect to SQL databases and federate queries across them and your U-SQL and Azure Data Lake data.</span><span class="sxs-lookup"><span data-stu-id="6cc6b-200">Connect to SQL databases and federate queries across them and your U-SQL and Azure Data Lake data.</span></span>

## <a name="see-also"></a><span data-ttu-id="6cc6b-201">See also</span><span class="sxs-lookup"><span data-stu-id="6cc6b-201">See also</span></span>
* [<span data-ttu-id="6cc6b-202">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6cc6b-202">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="6cc6b-203">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6cc6b-203">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="6cc6b-204">Using U-SQL window functions for Azure Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="6cc6b-204">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
* [<span data-ttu-id="6cc6b-205">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="6cc6b-205">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

## <a name="let-us-know-what-you-think"></a><span data-ttu-id="6cc6b-206">Let us know what you think</span><span class="sxs-lookup"><span data-stu-id="6cc6b-206">Let us know what you think</span></span>
* [<span data-ttu-id="6cc6b-207">Submit a feature request</span><span class="sxs-lookup"><span data-stu-id="6cc6b-207">Submit a feature request</span></span>](http://aka.ms/adlafeedback)
* [<span data-ttu-id="6cc6b-208">Get help in the forums</span><span class="sxs-lookup"><span data-stu-id="6cc6b-208">Get help in the forums</span></span>](http://aka.ms/adlaforums)
* [<span data-ttu-id="6cc6b-209">Provide feedback on U-SQL</span><span class="sxs-lookup"><span data-stu-id="6cc6b-209">Provide feedback on U-SQL</span></span>](http://aka.ms/usqldiscuss)
