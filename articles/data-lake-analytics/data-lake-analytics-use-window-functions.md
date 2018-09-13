---
title: Using U-SQL window functions for Azure Data Lake Analytics jobs | Microsoft Docs
description: 'Learn how to use U-SQL window functions. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: a5e14b32-d5eb-4f4b-9258-e257359f9988
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data`
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 61878145660e24e44093199499b5f21aa6f2dbd7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556504"
---
# <a name="using-u-sql-window-functions-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="f017f-103">Using U-SQL window functions for Azure Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="f017f-103">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="f017f-104">Window functions were introduced to the ISO/ANSI SQL Standard in 2003.</span><span class="sxs-lookup"><span data-stu-id="f017f-104">Window functions were introduced to the ISO/ANSI SQL Standard in 2003.</span></span> <span data-ttu-id="f017f-105">U-SQL adopts a subset of window functions as defined by the ANSI SQL Standard.</span><span class="sxs-lookup"><span data-stu-id="f017f-105">U-SQL adopts a subset of window functions as defined by the ANSI SQL Standard.</span></span>

<span data-ttu-id="f017f-106">Window functions are used to do computation within sets of rows called *windows*.</span><span class="sxs-lookup"><span data-stu-id="f017f-106">Window functions are used to do computation within sets of rows called *windows*.</span></span> <span data-ttu-id="f017f-107">Windows are defined by the OVER clause.</span><span class="sxs-lookup"><span data-stu-id="f017f-107">Windows are defined by the OVER clause.</span></span> <span data-ttu-id="f017f-108">Window functions solve some key scenarios in a highly efficient manner.</span><span class="sxs-lookup"><span data-stu-id="f017f-108">Window functions solve some key scenarios in a highly efficient manner.</span></span>

<span data-ttu-id="f017f-109">This learning guide uses two sample datasets to walk you through some sample scenario where you can apply window functions.</span><span class="sxs-lookup"><span data-stu-id="f017f-109">This learning guide uses two sample datasets to walk you through some sample scenario where you can apply window functions.</span></span> <span data-ttu-id="f017f-110">For more information, see [U-SQL reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="f017f-110">For more information, see [U-SQL reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>

<span data-ttu-id="f017f-111">The window functions are categorized into:</span><span class="sxs-lookup"><span data-stu-id="f017f-111">The window functions are categorized into:</span></span> 

* <span data-ttu-id="f017f-112">[Reporting aggregation functions](#reporting-aggregation-functions), such as SUM or AVG</span><span class="sxs-lookup"><span data-stu-id="f017f-112">[Reporting aggregation functions](#reporting-aggregation-functions), such as SUM or AVG</span></span>
* <span data-ttu-id="f017f-113">[Ranking functions](#ranking-functions), such as DENSE_RANK, ROW_NUMBER, NTILE, and RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-113">[Ranking functions](#ranking-functions), such as DENSE_RANK, ROW_NUMBER, NTILE, and RANK</span></span>
* <span data-ttu-id="f017f-114">[Analytic functions](#analytic-functions), such as cumulative distribution or percentiles, access data from a previous row (in the same result set) without using a self-join</span><span class="sxs-lookup"><span data-stu-id="f017f-114">[Analytic functions](#analytic-functions), such as cumulative distribution or percentiles, access data from a previous row (in the same result set) without using a self-join</span></span>

<span data-ttu-id="f017f-115">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="f017f-115">**Prerequisites:**</span></span>

* <span data-ttu-id="f017f-116">Go through the following two tutorials:</span><span class="sxs-lookup"><span data-stu-id="f017f-116">Go through the following two tutorials:</span></span>
  
  * <span data-ttu-id="f017f-117">[Get started using Azure Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f017f-117">[Get started using Azure Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
  * <span data-ttu-id="f017f-118">[Get started using U-SQL for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f017f-118">[Get started using U-SQL for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="f017f-119">Create a Data Lake Analytic account as instructed in [Get started using Azure Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f017f-119">Create a Data Lake Analytic account as instructed in [Get started using Azure Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="f017f-120">Create a Visual Studio U-SQL project as instructed in [Get started using U-SQL for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f017f-120">Create a Visual Studio U-SQL project as instructed in [Get started using U-SQL for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-get-started.md).</span></span>

## <a name="sample-datasets"></a><span data-ttu-id="f017f-121">Sample datasets</span><span class="sxs-lookup"><span data-stu-id="f017f-121">Sample datasets</span></span>
<span data-ttu-id="f017f-122">This tutorial uses two datasets:</span><span class="sxs-lookup"><span data-stu-id="f017f-122">This tutorial uses two datasets:</span></span>

* <span data-ttu-id="f017f-123">QueryLog</span><span class="sxs-lookup"><span data-stu-id="f017f-123">QueryLog</span></span> 
  
    <span data-ttu-id="f017f-124">QueryLog represents a list of what people searched for in search engine.</span><span class="sxs-lookup"><span data-stu-id="f017f-124">QueryLog represents a list of what people searched for in search engine.</span></span> <span data-ttu-id="f017f-125">Each query log includes:</span><span class="sxs-lookup"><span data-stu-id="f017f-125">Each query log includes:</span></span>
  
    - <span data-ttu-id="f017f-126">Query - What the user was searching for.</span><span class="sxs-lookup"><span data-stu-id="f017f-126">Query - What the user was searching for.</span></span>
    - <span data-ttu-id="f017f-127">Latency - How fast the query came back to the user in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="f017f-127">Latency - How fast the query came back to the user in milliseconds.</span></span>
    - <span data-ttu-id="f017f-128">Vertical - What kind of content the user was interested in (Web links, Images, Videos).</span><span class="sxs-lookup"><span data-stu-id="f017f-128">Vertical - What kind of content the user was interested in (Web links, Images, Videos).</span></span>
  
    <span data-ttu-id="f017f-129">Copy and paste the following script into your U-SQL project for constructing the QueryLog rowset:</span><span class="sxs-lookup"><span data-stu-id="f017f-129">Copy and paste the following script into your U-SQL project for constructing the QueryLog rowset:</span></span>
  
    ```
    @querylog = 
        SELECT * FROM ( VALUES
            ("Banana"  , 300, "Image" ),
            ("Cherry"  , 300, "Image" ),
            ("Durian"  , 500, "Image" ),
            ("Apple"   , 100, "Web"   ),
            ("Fig"     , 200, "Web"   ),
            ("Papaya"  , 200, "Web"   ),
            ("Avocado" , 300, "Web"   ),
            ("Cherry"  , 400, "Web"   ),
            ("Durian"  , 500, "Web"   ) )
        AS T(Query,Latency,Vertical);
    ```

    <span data-ttu-id="f017f-130">In practice, the data is usually stored in a file.</span><span class="sxs-lookup"><span data-stu-id="f017f-130">In practice, the data is usually stored in a file.</span></span> <span data-ttu-id="f017f-131">You would access the data in a tab-delimited file with the following code:</span><span class="sxs-lookup"><span data-stu-id="f017f-131">You would access the data in a tab-delimited file with the following code:</span></span> 
  
    ```
    @querylog = 
    EXTRACT 
        Query    string, 
        Latency  int, 
        Vertical string
    FROM "/Samples/QueryLog.tsv"
    USING Extractors.Tsv();
    ```
* <span data-ttu-id="f017f-132">Employees</span><span class="sxs-lookup"><span data-stu-id="f017f-132">Employees</span></span>
  
    <span data-ttu-id="f017f-133">The Employee dataset includes the following fields:</span><span class="sxs-lookup"><span data-stu-id="f017f-133">The Employee dataset includes the following fields:</span></span>
  
        - EmpID - Employee ID.
        - EmpName  Employee name.
        - DeptName - Department name. 
        - DeptID - Deparment ID.
        - Salary - Employee salary.
  
    <span data-ttu-id="f017f-134">Copy and paste the following script into your U-SQL project to construct the Employees rowset:</span><span class="sxs-lookup"><span data-stu-id="f017f-134">Copy and paste the following script into your U-SQL project to construct the Employees rowset:</span></span>
  
        @employees = 
            SELECT * FROM ( VALUES
                (1, "Noah",   "Engineering", 100, 10000),
                (2, "Sophia", "Engineering", 100, 20000),
                (3, "Liam",   "Engineering", 100, 30000),
                (4, "Emma",   "HR",          200, 10000),
                (5, "Jacob",  "HR",          200, 10000),
                (6, "Olivia", "HR",          200, 10000),
                (7, "Mason",  "Executive",   300, 50000),
                (8, "Ava",    "Marketing",   400, 15000),
                (9, "Ethan",  "Marketing",   400, 10000) )
            AS T(EmpID, EmpName, DeptName, DeptID, Salary);
  
    <span data-ttu-id="f017f-135">The following statement demonstrates creating the rowset by extracting it from a data file.</span><span class="sxs-lookup"><span data-stu-id="f017f-135">The following statement demonstrates creating the rowset by extracting it from a data file.</span></span>
  
        @employees = 
        EXTRACT 
            EmpID    int, 
            EmpName  string, 
            DeptName string, 
            DeptID   int, 
            Salary   int
        FROM "/Samples/Employees.tsv"
        USING Extractors.Tsv();

<span data-ttu-id="f017f-136">When you test the samples in tutorial, you must include the rowset definitions.</span><span class="sxs-lookup"><span data-stu-id="f017f-136">When you test the samples in tutorial, you must include the rowset definitions.</span></span> <span data-ttu-id="f017f-137">U-SQL requires you to define only the rowsets that are used.</span><span class="sxs-lookup"><span data-stu-id="f017f-137">U-SQL requires you to define only the rowsets that are used.</span></span> <span data-ttu-id="f017f-138">Some samples only need one rowset.</span><span class="sxs-lookup"><span data-stu-id="f017f-138">Some samples only need one rowset.</span></span>

<span data-ttu-id="f017f-139">Add the following statement to output the result rowset to a data file:</span><span class="sxs-lookup"><span data-stu-id="f017f-139">Add the following statement to output the result rowset to a data file:</span></span>

    OUTPUT @result TO "/wfresult.csv" 
        USING Outputters.Csv();

 <span data-ttu-id="f017f-140">Most of the samples use the variable called **@result** for the results.</span><span class="sxs-lookup"><span data-stu-id="f017f-140">Most of the samples use the variable called **@result** for the results.</span></span>

## <a name="compare-window-functions-to-grouping"></a><span data-ttu-id="f017f-141">Compare window functions to Grouping</span><span class="sxs-lookup"><span data-stu-id="f017f-141">Compare window functions to Grouping</span></span>
<span data-ttu-id="f017f-142">Windowing and Grouping are conceptually related by also different.</span><span class="sxs-lookup"><span data-stu-id="f017f-142">Windowing and Grouping are conceptually related by also different.</span></span> <span data-ttu-id="f017f-143">It is helpful to understand this relationship.</span><span class="sxs-lookup"><span data-stu-id="f017f-143">It is helpful to understand this relationship.</span></span>

### <a name="use-aggregation-and-grouping"></a><span data-ttu-id="f017f-144">Use aggregation and Grouping</span><span class="sxs-lookup"><span data-stu-id="f017f-144">Use aggregation and Grouping</span></span>
<span data-ttu-id="f017f-145">The following query uses an aggregation to calculate the total salary for all employees:</span><span class="sxs-lookup"><span data-stu-id="f017f-145">The following query uses an aggregation to calculate the total salary for all employees:</span></span>

    @result = 
        SELECT 
            SUM(Salary) AS TotalSalary
        FROM @employees;

> [!NOTE]
> <span data-ttu-id="f017f-146">For instructions for testing and checking the output, see [Get started using U-SQL for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f017f-146">For instructions for testing and checking the output, see [Get started using U-SQL for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-get-started.md).</span></span>
> 
> 

<span data-ttu-id="f017f-147">The result is a single row with a single column.</span><span class="sxs-lookup"><span data-stu-id="f017f-147">The result is a single row with a single column.</span></span> <span data-ttu-id="f017f-148">The $165000 is the sum of the Salary value from the whole table.</span><span class="sxs-lookup"><span data-stu-id="f017f-148">The $165000 is the sum of the Salary value from the whole table.</span></span> 

| <span data-ttu-id="f017f-149">TotalSalary</span><span class="sxs-lookup"><span data-stu-id="f017f-149">TotalSalary</span></span> |
| --- |
| <span data-ttu-id="f017f-150">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-150">165000</span></span> |

> [!NOTE]
> <span data-ttu-id="f017f-151">If you are new to windows functions, it is helpful to remember the numbers in the outputs.</span><span class="sxs-lookup"><span data-stu-id="f017f-151">If you are new to windows functions, it is helpful to remember the numbers in the outputs.</span></span>  
> 
> 

<span data-ttu-id="f017f-152">The following statement uses the GROUP BY clause to calculate the total salary for each department:</span><span class="sxs-lookup"><span data-stu-id="f017f-152">The following statement uses the GROUP BY clause to calculate the total salary for each department:</span></span>

    @result=
        SELECT DeptName, SUM(Salary) AS SalaryByDept
        FROM @employees
        GROUP BY DeptName;

<span data-ttu-id="f017f-153">The results are:</span><span class="sxs-lookup"><span data-stu-id="f017f-153">The results are:</span></span>

| <span data-ttu-id="f017f-154">DeptName</span><span class="sxs-lookup"><span data-stu-id="f017f-154">DeptName</span></span> | <span data-ttu-id="f017f-155">SalaryByDept</span><span class="sxs-lookup"><span data-stu-id="f017f-155">SalaryByDept</span></span> |
| --- | --- |
| <span data-ttu-id="f017f-156">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-156">Engineering</span></span> |<span data-ttu-id="f017f-157">60000</span><span class="sxs-lookup"><span data-stu-id="f017f-157">60000</span></span> |
| <span data-ttu-id="f017f-158">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-158">HR</span></span> |<span data-ttu-id="f017f-159">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-159">30000</span></span> |
| <span data-ttu-id="f017f-160">Executive</span><span class="sxs-lookup"><span data-stu-id="f017f-160">Executive</span></span> |<span data-ttu-id="f017f-161">50000</span><span class="sxs-lookup"><span data-stu-id="f017f-161">50000</span></span> |
| <span data-ttu-id="f017f-162">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-162">Marketing</span></span> |<span data-ttu-id="f017f-163">25000</span><span class="sxs-lookup"><span data-stu-id="f017f-163">25000</span></span> |

<span data-ttu-id="f017f-164">The sum of the SalaryByDept column is $165000, which matches the amount in the last script.</span><span class="sxs-lookup"><span data-stu-id="f017f-164">The sum of the SalaryByDept column is $165000, which matches the amount in the last script.</span></span>

<span data-ttu-id="f017f-165">In both these cases the number of there are fewer output rows than input rows:</span><span class="sxs-lookup"><span data-stu-id="f017f-165">In both these cases the number of there are fewer output rows than input rows:</span></span>

* <span data-ttu-id="f017f-166">Without GROUP BY, the aggregation collapses all the rows into a single row.</span><span class="sxs-lookup"><span data-stu-id="f017f-166">Without GROUP BY, the aggregation collapses all the rows into a single row.</span></span> 
* <span data-ttu-id="f017f-167">With GROUP BY, there are N output rows where N is the number of distinct values that appear in the data.</span><span class="sxs-lookup"><span data-stu-id="f017f-167">With GROUP BY, there are N output rows where N is the number of distinct values that appear in the data.</span></span>  <span data-ttu-id="f017f-168">In this case, four rows are output.</span><span class="sxs-lookup"><span data-stu-id="f017f-168">In this case, four rows are output.</span></span>

### <a name="use-a-window-function"></a><span data-ttu-id="f017f-169">Use a window function</span><span class="sxs-lookup"><span data-stu-id="f017f-169">Use a window function</span></span>
<span data-ttu-id="f017f-170">The OVER clause in the following sample is empty, so the window includes all rows.</span><span class="sxs-lookup"><span data-stu-id="f017f-170">The OVER clause in the following sample is empty, so the window includes all rows.</span></span> <span data-ttu-id="f017f-171">The SUM in this example is applied to the OVER clause that it precedes.</span><span class="sxs-lookup"><span data-stu-id="f017f-171">The SUM in this example is applied to the OVER clause that it precedes.</span></span>

<span data-ttu-id="f017f-172">You could read this query as: “The sum of Salary over a window of all rows.”</span><span class="sxs-lookup"><span data-stu-id="f017f-172">You could read this query as: “The sum of Salary over a window of all rows.”</span></span>

    @result=
        SELECT
            EmpName,
            SUM(Salary) OVER( ) AS SalaryAllDepts
        FROM @employees;

<span data-ttu-id="f017f-173">Unlike GROUP BY, there are as many output rows as input rows:</span><span class="sxs-lookup"><span data-stu-id="f017f-173">Unlike GROUP BY, there are as many output rows as input rows:</span></span> 

| <span data-ttu-id="f017f-174">EmpName</span><span class="sxs-lookup"><span data-stu-id="f017f-174">EmpName</span></span> | <span data-ttu-id="f017f-175">TotalAllDepts</span><span class="sxs-lookup"><span data-stu-id="f017f-175">TotalAllDepts</span></span> |
| --- | --- |
| <span data-ttu-id="f017f-176">Noah</span><span class="sxs-lookup"><span data-stu-id="f017f-176">Noah</span></span> |<span data-ttu-id="f017f-177">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-177">165000</span></span> |
| <span data-ttu-id="f017f-178">Sophia</span><span class="sxs-lookup"><span data-stu-id="f017f-178">Sophia</span></span> |<span data-ttu-id="f017f-179">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-179">165000</span></span> |
| <span data-ttu-id="f017f-180">Liam</span><span class="sxs-lookup"><span data-stu-id="f017f-180">Liam</span></span> |<span data-ttu-id="f017f-181">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-181">165000</span></span> |
| <span data-ttu-id="f017f-182">Emma</span><span class="sxs-lookup"><span data-stu-id="f017f-182">Emma</span></span> |<span data-ttu-id="f017f-183">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-183">165000</span></span> |
| <span data-ttu-id="f017f-184">Jacob</span><span class="sxs-lookup"><span data-stu-id="f017f-184">Jacob</span></span> |<span data-ttu-id="f017f-185">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-185">165000</span></span> |
| <span data-ttu-id="f017f-186">Olivia</span><span class="sxs-lookup"><span data-stu-id="f017f-186">Olivia</span></span> |<span data-ttu-id="f017f-187">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-187">165000</span></span> |
| <span data-ttu-id="f017f-188">Mason</span><span class="sxs-lookup"><span data-stu-id="f017f-188">Mason</span></span> |<span data-ttu-id="f017f-189">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-189">165000</span></span> |
| <span data-ttu-id="f017f-190">Ava</span><span class="sxs-lookup"><span data-stu-id="f017f-190">Ava</span></span> |<span data-ttu-id="f017f-191">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-191">165000</span></span> |
| <span data-ttu-id="f017f-192">Ethan</span><span class="sxs-lookup"><span data-stu-id="f017f-192">Ethan</span></span> |<span data-ttu-id="f017f-193">165000</span><span class="sxs-lookup"><span data-stu-id="f017f-193">165000</span></span> |

<span data-ttu-id="f017f-194">The value of 165000 (the total of all salaries) is placed in each output row.</span><span class="sxs-lookup"><span data-stu-id="f017f-194">The value of 165000 (the total of all salaries) is placed in each output row.</span></span> <span data-ttu-id="f017f-195">That total comes from the "window" of all rows, so it includes all the salaries.</span><span class="sxs-lookup"><span data-stu-id="f017f-195">That total comes from the "window" of all rows, so it includes all the salaries.</span></span> 

<span data-ttu-id="f017f-196">The next example demonstrates how to refine the "window" to list all the employees, the department, and the total salary for the department.</span><span class="sxs-lookup"><span data-stu-id="f017f-196">The next example demonstrates how to refine the "window" to list all the employees, the department, and the total salary for the department.</span></span> <span data-ttu-id="f017f-197">PARTITION BY is added to the OVER clause.</span><span class="sxs-lookup"><span data-stu-id="f017f-197">PARTITION BY is added to the OVER clause.</span></span>

    @result=
    SELECT
        EmpName, DeptName,
        SUM(Salary) OVER( PARTITION BY DeptName ) AS SalaryByDept
    FROM @employees;

<span data-ttu-id="f017f-198">The results are:</span><span class="sxs-lookup"><span data-stu-id="f017f-198">The results are:</span></span>

| <span data-ttu-id="f017f-199">EmpName</span><span class="sxs-lookup"><span data-stu-id="f017f-199">EmpName</span></span> | <span data-ttu-id="f017f-200">DeptName</span><span class="sxs-lookup"><span data-stu-id="f017f-200">DeptName</span></span> | <span data-ttu-id="f017f-201">SalaryByDep</span><span class="sxs-lookup"><span data-stu-id="f017f-201">SalaryByDep</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f017f-202">Noah</span><span class="sxs-lookup"><span data-stu-id="f017f-202">Noah</span></span> |<span data-ttu-id="f017f-203">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-203">Engineering</span></span> |<span data-ttu-id="f017f-204">60000</span><span class="sxs-lookup"><span data-stu-id="f017f-204">60000</span></span> |
| <span data-ttu-id="f017f-205">Sophia</span><span class="sxs-lookup"><span data-stu-id="f017f-205">Sophia</span></span> |<span data-ttu-id="f017f-206">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-206">Engineering</span></span> |<span data-ttu-id="f017f-207">60000</span><span class="sxs-lookup"><span data-stu-id="f017f-207">60000</span></span> |
| <span data-ttu-id="f017f-208">Liam</span><span class="sxs-lookup"><span data-stu-id="f017f-208">Liam</span></span> |<span data-ttu-id="f017f-209">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-209">Engineering</span></span> |<span data-ttu-id="f017f-210">60000</span><span class="sxs-lookup"><span data-stu-id="f017f-210">60000</span></span> |
| <span data-ttu-id="f017f-211">Mason</span><span class="sxs-lookup"><span data-stu-id="f017f-211">Mason</span></span> |<span data-ttu-id="f017f-212">Executive</span><span class="sxs-lookup"><span data-stu-id="f017f-212">Executive</span></span> |<span data-ttu-id="f017f-213">50000</span><span class="sxs-lookup"><span data-stu-id="f017f-213">50000</span></span> |
| <span data-ttu-id="f017f-214">Emma</span><span class="sxs-lookup"><span data-stu-id="f017f-214">Emma</span></span> |<span data-ttu-id="f017f-215">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-215">HR</span></span> |<span data-ttu-id="f017f-216">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-216">30000</span></span> |
| <span data-ttu-id="f017f-217">Jacob</span><span class="sxs-lookup"><span data-stu-id="f017f-217">Jacob</span></span> |<span data-ttu-id="f017f-218">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-218">HR</span></span> |<span data-ttu-id="f017f-219">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-219">30000</span></span> |
| <span data-ttu-id="f017f-220">Olivia</span><span class="sxs-lookup"><span data-stu-id="f017f-220">Olivia</span></span> |<span data-ttu-id="f017f-221">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-221">HR</span></span> |<span data-ttu-id="f017f-222">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-222">30000</span></span> |
| <span data-ttu-id="f017f-223">Ava</span><span class="sxs-lookup"><span data-stu-id="f017f-223">Ava</span></span> |<span data-ttu-id="f017f-224">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-224">Marketing</span></span> |<span data-ttu-id="f017f-225">25000</span><span class="sxs-lookup"><span data-stu-id="f017f-225">25000</span></span> |
| <span data-ttu-id="f017f-226">Ethan</span><span class="sxs-lookup"><span data-stu-id="f017f-226">Ethan</span></span> |<span data-ttu-id="f017f-227">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-227">Marketing</span></span> |<span data-ttu-id="f017f-228">25000</span><span class="sxs-lookup"><span data-stu-id="f017f-228">25000</span></span> |

<span data-ttu-id="f017f-229">Again, there are the same number of input rows as output rows.</span><span class="sxs-lookup"><span data-stu-id="f017f-229">Again, there are the same number of input rows as output rows.</span></span> <span data-ttu-id="f017f-230">However each row has a total salary for the corresponding department.</span><span class="sxs-lookup"><span data-stu-id="f017f-230">However each row has a total salary for the corresponding department.</span></span>

## <a name="reporting-aggregation-functions"></a><span data-ttu-id="f017f-231">Reporting aggregation functions</span><span class="sxs-lookup"><span data-stu-id="f017f-231">Reporting aggregation functions</span></span>
<span data-ttu-id="f017f-232">Window functions also support the following aggregates:</span><span class="sxs-lookup"><span data-stu-id="f017f-232">Window functions also support the following aggregates:</span></span>

* <span data-ttu-id="f017f-233">COUNT</span><span class="sxs-lookup"><span data-stu-id="f017f-233">COUNT</span></span>
* <span data-ttu-id="f017f-234">SUM</span><span class="sxs-lookup"><span data-stu-id="f017f-234">SUM</span></span>
* <span data-ttu-id="f017f-235">MIN</span><span class="sxs-lookup"><span data-stu-id="f017f-235">MIN</span></span>
* <span data-ttu-id="f017f-236">MAX</span><span class="sxs-lookup"><span data-stu-id="f017f-236">MAX</span></span>
* <span data-ttu-id="f017f-237">AVG</span><span class="sxs-lookup"><span data-stu-id="f017f-237">AVG</span></span>
* <span data-ttu-id="f017f-238">STDEV</span><span class="sxs-lookup"><span data-stu-id="f017f-238">STDEV</span></span>
* <span data-ttu-id="f017f-239">VAR</span><span class="sxs-lookup"><span data-stu-id="f017f-239">VAR</span></span>

<span data-ttu-id="f017f-240">The syntax:</span><span class="sxs-lookup"><span data-stu-id="f017f-240">The syntax:</span></span>

    <AggregateFunction>( [DISTINCT] <expression>) [<OVER_clause>]

<span data-ttu-id="f017f-241">Note:</span><span class="sxs-lookup"><span data-stu-id="f017f-241">Note:</span></span> 

* <span data-ttu-id="f017f-242">By default, aggregate functions, except COUNT, ignore null values.</span><span class="sxs-lookup"><span data-stu-id="f017f-242">By default, aggregate functions, except COUNT, ignore null values.</span></span>
* <span data-ttu-id="f017f-243">When aggregate functions are specified along with the OVER clause, the ORDER BY clause is not allowed in the OVER clause.</span><span class="sxs-lookup"><span data-stu-id="f017f-243">When aggregate functions are specified along with the OVER clause, the ORDER BY clause is not allowed in the OVER clause.</span></span>

### <a name="use-sum"></a><span data-ttu-id="f017f-244">Use SUM</span><span class="sxs-lookup"><span data-stu-id="f017f-244">Use SUM</span></span>
<span data-ttu-id="f017f-245">The following example adds a total salary by department to each input row:</span><span class="sxs-lookup"><span data-stu-id="f017f-245">The following example adds a total salary by department to each input row:</span></span>

    @result=
        SELECT 
            *,
            SUM(Salary) OVER( PARTITION BY DeptName ) AS TotalByDept
        FROM @employees;

<span data-ttu-id="f017f-246">Here is the output:</span><span class="sxs-lookup"><span data-stu-id="f017f-246">Here is the output:</span></span>

| <span data-ttu-id="f017f-247">EmpID</span><span class="sxs-lookup"><span data-stu-id="f017f-247">EmpID</span></span> | <span data-ttu-id="f017f-248">EmpName</span><span class="sxs-lookup"><span data-stu-id="f017f-248">EmpName</span></span> | <span data-ttu-id="f017f-249">DeptName</span><span class="sxs-lookup"><span data-stu-id="f017f-249">DeptName</span></span> | <span data-ttu-id="f017f-250">DeptID</span><span class="sxs-lookup"><span data-stu-id="f017f-250">DeptID</span></span> | <span data-ttu-id="f017f-251">Salary</span><span class="sxs-lookup"><span data-stu-id="f017f-251">Salary</span></span> | <span data-ttu-id="f017f-252">TotalByDept</span><span class="sxs-lookup"><span data-stu-id="f017f-252">TotalByDept</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f017f-253">1</span><span class="sxs-lookup"><span data-stu-id="f017f-253">1</span></span> |<span data-ttu-id="f017f-254">Noah</span><span class="sxs-lookup"><span data-stu-id="f017f-254">Noah</span></span> |<span data-ttu-id="f017f-255">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-255">Engineering</span></span> |<span data-ttu-id="f017f-256">100</span><span class="sxs-lookup"><span data-stu-id="f017f-256">100</span></span> |<span data-ttu-id="f017f-257">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-257">10000</span></span> |<span data-ttu-id="f017f-258">60000</span><span class="sxs-lookup"><span data-stu-id="f017f-258">60000</span></span> |
| <span data-ttu-id="f017f-259">2</span><span class="sxs-lookup"><span data-stu-id="f017f-259">2</span></span> |<span data-ttu-id="f017f-260">Sophia</span><span class="sxs-lookup"><span data-stu-id="f017f-260">Sophia</span></span> |<span data-ttu-id="f017f-261">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-261">Engineering</span></span> |<span data-ttu-id="f017f-262">100</span><span class="sxs-lookup"><span data-stu-id="f017f-262">100</span></span> |<span data-ttu-id="f017f-263">20000</span><span class="sxs-lookup"><span data-stu-id="f017f-263">20000</span></span> |<span data-ttu-id="f017f-264">60000</span><span class="sxs-lookup"><span data-stu-id="f017f-264">60000</span></span> |
| <span data-ttu-id="f017f-265">3</span><span class="sxs-lookup"><span data-stu-id="f017f-265">3</span></span> |<span data-ttu-id="f017f-266">Liam</span><span class="sxs-lookup"><span data-stu-id="f017f-266">Liam</span></span> |<span data-ttu-id="f017f-267">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-267">Engineering</span></span> |<span data-ttu-id="f017f-268">100</span><span class="sxs-lookup"><span data-stu-id="f017f-268">100</span></span> |<span data-ttu-id="f017f-269">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-269">30000</span></span> |<span data-ttu-id="f017f-270">60000</span><span class="sxs-lookup"><span data-stu-id="f017f-270">60000</span></span> |
| <span data-ttu-id="f017f-271">7</span><span class="sxs-lookup"><span data-stu-id="f017f-271">7</span></span> |<span data-ttu-id="f017f-272">Mason</span><span class="sxs-lookup"><span data-stu-id="f017f-272">Mason</span></span> |<span data-ttu-id="f017f-273">Executive</span><span class="sxs-lookup"><span data-stu-id="f017f-273">Executive</span></span> |<span data-ttu-id="f017f-274">300</span><span class="sxs-lookup"><span data-stu-id="f017f-274">300</span></span> |<span data-ttu-id="f017f-275">50000</span><span class="sxs-lookup"><span data-stu-id="f017f-275">50000</span></span> |<span data-ttu-id="f017f-276">50000</span><span class="sxs-lookup"><span data-stu-id="f017f-276">50000</span></span> |
| <span data-ttu-id="f017f-277">4</span><span class="sxs-lookup"><span data-stu-id="f017f-277">4</span></span> |<span data-ttu-id="f017f-278">Emma</span><span class="sxs-lookup"><span data-stu-id="f017f-278">Emma</span></span> |<span data-ttu-id="f017f-279">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-279">HR</span></span> |<span data-ttu-id="f017f-280">200</span><span class="sxs-lookup"><span data-stu-id="f017f-280">200</span></span> |<span data-ttu-id="f017f-281">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-281">10000</span></span> |<span data-ttu-id="f017f-282">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-282">30000</span></span> |
| <span data-ttu-id="f017f-283">5</span><span class="sxs-lookup"><span data-stu-id="f017f-283">5</span></span> |<span data-ttu-id="f017f-284">Jacob</span><span class="sxs-lookup"><span data-stu-id="f017f-284">Jacob</span></span> |<span data-ttu-id="f017f-285">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-285">HR</span></span> |<span data-ttu-id="f017f-286">200</span><span class="sxs-lookup"><span data-stu-id="f017f-286">200</span></span> |<span data-ttu-id="f017f-287">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-287">10000</span></span> |<span data-ttu-id="f017f-288">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-288">30000</span></span> |
| <span data-ttu-id="f017f-289">6</span><span class="sxs-lookup"><span data-stu-id="f017f-289">6</span></span> |<span data-ttu-id="f017f-290">Olivia</span><span class="sxs-lookup"><span data-stu-id="f017f-290">Olivia</span></span> |<span data-ttu-id="f017f-291">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-291">HR</span></span> |<span data-ttu-id="f017f-292">200</span><span class="sxs-lookup"><span data-stu-id="f017f-292">200</span></span> |<span data-ttu-id="f017f-293">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-293">10000</span></span> |<span data-ttu-id="f017f-294">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-294">30000</span></span> |
| <span data-ttu-id="f017f-295">8</span><span class="sxs-lookup"><span data-stu-id="f017f-295">8</span></span> |<span data-ttu-id="f017f-296">Ava</span><span class="sxs-lookup"><span data-stu-id="f017f-296">Ava</span></span> |<span data-ttu-id="f017f-297">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-297">Marketing</span></span> |<span data-ttu-id="f017f-298">400</span><span class="sxs-lookup"><span data-stu-id="f017f-298">400</span></span> |<span data-ttu-id="f017f-299">15000</span><span class="sxs-lookup"><span data-stu-id="f017f-299">15000</span></span> |<span data-ttu-id="f017f-300">25000</span><span class="sxs-lookup"><span data-stu-id="f017f-300">25000</span></span> |
| <span data-ttu-id="f017f-301">9</span><span class="sxs-lookup"><span data-stu-id="f017f-301">9</span></span> |<span data-ttu-id="f017f-302">Ethan</span><span class="sxs-lookup"><span data-stu-id="f017f-302">Ethan</span></span> |<span data-ttu-id="f017f-303">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-303">Marketing</span></span> |<span data-ttu-id="f017f-304">400</span><span class="sxs-lookup"><span data-stu-id="f017f-304">400</span></span> |<span data-ttu-id="f017f-305">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-305">10000</span></span> |<span data-ttu-id="f017f-306">25000</span><span class="sxs-lookup"><span data-stu-id="f017f-306">25000</span></span> |

### <a name="use-count"></a><span data-ttu-id="f017f-307">Use COUNT</span><span class="sxs-lookup"><span data-stu-id="f017f-307">Use COUNT</span></span>
<span data-ttu-id="f017f-308">The following example adds an extra field to each row to show the total number employees in each department.</span><span class="sxs-lookup"><span data-stu-id="f017f-308">The following example adds an extra field to each row to show the total number employees in each department.</span></span>

    @result =
        SELECT *, 
            COUNT(*) OVER(PARTITION BY DeptName) AS CountByDept 
        FROM @employees;

<span data-ttu-id="f017f-309">The result:</span><span class="sxs-lookup"><span data-stu-id="f017f-309">The result:</span></span>

| <span data-ttu-id="f017f-310">EmpID</span><span class="sxs-lookup"><span data-stu-id="f017f-310">EmpID</span></span> | <span data-ttu-id="f017f-311">EmpName</span><span class="sxs-lookup"><span data-stu-id="f017f-311">EmpName</span></span> | <span data-ttu-id="f017f-312">DeptName</span><span class="sxs-lookup"><span data-stu-id="f017f-312">DeptName</span></span> | <span data-ttu-id="f017f-313">DeptID</span><span class="sxs-lookup"><span data-stu-id="f017f-313">DeptID</span></span> | <span data-ttu-id="f017f-314">Salary</span><span class="sxs-lookup"><span data-stu-id="f017f-314">Salary</span></span> | <span data-ttu-id="f017f-315">CountByDept</span><span class="sxs-lookup"><span data-stu-id="f017f-315">CountByDept</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f017f-316">1</span><span class="sxs-lookup"><span data-stu-id="f017f-316">1</span></span> |<span data-ttu-id="f017f-317">Noah</span><span class="sxs-lookup"><span data-stu-id="f017f-317">Noah</span></span> |<span data-ttu-id="f017f-318">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-318">Engineering</span></span> |<span data-ttu-id="f017f-319">100</span><span class="sxs-lookup"><span data-stu-id="f017f-319">100</span></span> |<span data-ttu-id="f017f-320">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-320">10000</span></span> |<span data-ttu-id="f017f-321">3</span><span class="sxs-lookup"><span data-stu-id="f017f-321">3</span></span> |
| <span data-ttu-id="f017f-322">2</span><span class="sxs-lookup"><span data-stu-id="f017f-322">2</span></span> |<span data-ttu-id="f017f-323">Sophia</span><span class="sxs-lookup"><span data-stu-id="f017f-323">Sophia</span></span> |<span data-ttu-id="f017f-324">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-324">Engineering</span></span> |<span data-ttu-id="f017f-325">100</span><span class="sxs-lookup"><span data-stu-id="f017f-325">100</span></span> |<span data-ttu-id="f017f-326">20000</span><span class="sxs-lookup"><span data-stu-id="f017f-326">20000</span></span> |<span data-ttu-id="f017f-327">3</span><span class="sxs-lookup"><span data-stu-id="f017f-327">3</span></span> |
| <span data-ttu-id="f017f-328">3</span><span class="sxs-lookup"><span data-stu-id="f017f-328">3</span></span> |<span data-ttu-id="f017f-329">Liam</span><span class="sxs-lookup"><span data-stu-id="f017f-329">Liam</span></span> |<span data-ttu-id="f017f-330">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-330">Engineering</span></span> |<span data-ttu-id="f017f-331">100</span><span class="sxs-lookup"><span data-stu-id="f017f-331">100</span></span> |<span data-ttu-id="f017f-332">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-332">30000</span></span> |<span data-ttu-id="f017f-333">3</span><span class="sxs-lookup"><span data-stu-id="f017f-333">3</span></span> |
| <span data-ttu-id="f017f-334">7</span><span class="sxs-lookup"><span data-stu-id="f017f-334">7</span></span> |<span data-ttu-id="f017f-335">Mason</span><span class="sxs-lookup"><span data-stu-id="f017f-335">Mason</span></span> |<span data-ttu-id="f017f-336">Executive</span><span class="sxs-lookup"><span data-stu-id="f017f-336">Executive</span></span> |<span data-ttu-id="f017f-337">300</span><span class="sxs-lookup"><span data-stu-id="f017f-337">300</span></span> |<span data-ttu-id="f017f-338">50000</span><span class="sxs-lookup"><span data-stu-id="f017f-338">50000</span></span> |<span data-ttu-id="f017f-339">1</span><span class="sxs-lookup"><span data-stu-id="f017f-339">1</span></span> |
| <span data-ttu-id="f017f-340">4</span><span class="sxs-lookup"><span data-stu-id="f017f-340">4</span></span> |<span data-ttu-id="f017f-341">Emma</span><span class="sxs-lookup"><span data-stu-id="f017f-341">Emma</span></span> |<span data-ttu-id="f017f-342">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-342">HR</span></span> |<span data-ttu-id="f017f-343">200</span><span class="sxs-lookup"><span data-stu-id="f017f-343">200</span></span> |<span data-ttu-id="f017f-344">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-344">10000</span></span> |<span data-ttu-id="f017f-345">3</span><span class="sxs-lookup"><span data-stu-id="f017f-345">3</span></span> |
| <span data-ttu-id="f017f-346">5</span><span class="sxs-lookup"><span data-stu-id="f017f-346">5</span></span> |<span data-ttu-id="f017f-347">Jacob</span><span class="sxs-lookup"><span data-stu-id="f017f-347">Jacob</span></span> |<span data-ttu-id="f017f-348">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-348">HR</span></span> |<span data-ttu-id="f017f-349">200</span><span class="sxs-lookup"><span data-stu-id="f017f-349">200</span></span> |<span data-ttu-id="f017f-350">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-350">10000</span></span> |<span data-ttu-id="f017f-351">3</span><span class="sxs-lookup"><span data-stu-id="f017f-351">3</span></span> |
| <span data-ttu-id="f017f-352">6</span><span class="sxs-lookup"><span data-stu-id="f017f-352">6</span></span> |<span data-ttu-id="f017f-353">Olivia</span><span class="sxs-lookup"><span data-stu-id="f017f-353">Olivia</span></span> |<span data-ttu-id="f017f-354">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-354">HR</span></span> |<span data-ttu-id="f017f-355">200</span><span class="sxs-lookup"><span data-stu-id="f017f-355">200</span></span> |<span data-ttu-id="f017f-356">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-356">10000</span></span> |<span data-ttu-id="f017f-357">3</span><span class="sxs-lookup"><span data-stu-id="f017f-357">3</span></span> |
| <span data-ttu-id="f017f-358">8</span><span class="sxs-lookup"><span data-stu-id="f017f-358">8</span></span> |<span data-ttu-id="f017f-359">Ava</span><span class="sxs-lookup"><span data-stu-id="f017f-359">Ava</span></span> |<span data-ttu-id="f017f-360">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-360">Marketing</span></span> |<span data-ttu-id="f017f-361">400</span><span class="sxs-lookup"><span data-stu-id="f017f-361">400</span></span> |<span data-ttu-id="f017f-362">15000</span><span class="sxs-lookup"><span data-stu-id="f017f-362">15000</span></span> |<span data-ttu-id="f017f-363">2</span><span class="sxs-lookup"><span data-stu-id="f017f-363">2</span></span> |
| <span data-ttu-id="f017f-364">9</span><span class="sxs-lookup"><span data-stu-id="f017f-364">9</span></span> |<span data-ttu-id="f017f-365">Ethan</span><span class="sxs-lookup"><span data-stu-id="f017f-365">Ethan</span></span> |<span data-ttu-id="f017f-366">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-366">Marketing</span></span> |<span data-ttu-id="f017f-367">400</span><span class="sxs-lookup"><span data-stu-id="f017f-367">400</span></span> |<span data-ttu-id="f017f-368">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-368">10000</span></span> |<span data-ttu-id="f017f-369">2</span><span class="sxs-lookup"><span data-stu-id="f017f-369">2</span></span> |

### <a name="use-min-and-max"></a><span data-ttu-id="f017f-370">Use MIN and MAX</span><span class="sxs-lookup"><span data-stu-id="f017f-370">Use MIN and MAX</span></span>
<span data-ttu-id="f017f-371">The following example adds an extra field to each row to show the lowest salary of each department:</span><span class="sxs-lookup"><span data-stu-id="f017f-371">The following example adds an extra field to each row to show the lowest salary of each department:</span></span>

    @result =
        SELECT 
            *,
            MIN(Salary) OVER( PARTITION BY DeptName ) AS MinSalary
        FROM @employees;

<span data-ttu-id="f017f-372">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-372">The results:</span></span>

| <span data-ttu-id="f017f-373">EmpID</span><span class="sxs-lookup"><span data-stu-id="f017f-373">EmpID</span></span> | <span data-ttu-id="f017f-374">EmpName</span><span class="sxs-lookup"><span data-stu-id="f017f-374">EmpName</span></span> | <span data-ttu-id="f017f-375">DeptName</span><span class="sxs-lookup"><span data-stu-id="f017f-375">DeptName</span></span> | <span data-ttu-id="f017f-376">DeptID</span><span class="sxs-lookup"><span data-stu-id="f017f-376">DeptID</span></span> | <span data-ttu-id="f017f-377">Salary</span><span class="sxs-lookup"><span data-stu-id="f017f-377">Salary</span></span> | <span data-ttu-id="f017f-378">MinSalary</span><span class="sxs-lookup"><span data-stu-id="f017f-378">MinSalary</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f017f-379">1</span><span class="sxs-lookup"><span data-stu-id="f017f-379">1</span></span> |<span data-ttu-id="f017f-380">Noah</span><span class="sxs-lookup"><span data-stu-id="f017f-380">Noah</span></span> |<span data-ttu-id="f017f-381">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-381">Engineering</span></span> |<span data-ttu-id="f017f-382">100</span><span class="sxs-lookup"><span data-stu-id="f017f-382">100</span></span> |<span data-ttu-id="f017f-383">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-383">10000</span></span> |<span data-ttu-id="f017f-384">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-384">10000</span></span> |
| <span data-ttu-id="f017f-385">2</span><span class="sxs-lookup"><span data-stu-id="f017f-385">2</span></span> |<span data-ttu-id="f017f-386">Sophia</span><span class="sxs-lookup"><span data-stu-id="f017f-386">Sophia</span></span> |<span data-ttu-id="f017f-387">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-387">Engineering</span></span> |<span data-ttu-id="f017f-388">100</span><span class="sxs-lookup"><span data-stu-id="f017f-388">100</span></span> |<span data-ttu-id="f017f-389">20000</span><span class="sxs-lookup"><span data-stu-id="f017f-389">20000</span></span> |<span data-ttu-id="f017f-390">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-390">10000</span></span> |
| <span data-ttu-id="f017f-391">3</span><span class="sxs-lookup"><span data-stu-id="f017f-391">3</span></span> |<span data-ttu-id="f017f-392">Liam</span><span class="sxs-lookup"><span data-stu-id="f017f-392">Liam</span></span> |<span data-ttu-id="f017f-393">Engineering</span><span class="sxs-lookup"><span data-stu-id="f017f-393">Engineering</span></span> |<span data-ttu-id="f017f-394">100</span><span class="sxs-lookup"><span data-stu-id="f017f-394">100</span></span> |<span data-ttu-id="f017f-395">30000</span><span class="sxs-lookup"><span data-stu-id="f017f-395">30000</span></span> |<span data-ttu-id="f017f-396">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-396">10000</span></span> |
| <span data-ttu-id="f017f-397">7</span><span class="sxs-lookup"><span data-stu-id="f017f-397">7</span></span> |<span data-ttu-id="f017f-398">Mason</span><span class="sxs-lookup"><span data-stu-id="f017f-398">Mason</span></span> |<span data-ttu-id="f017f-399">Executive</span><span class="sxs-lookup"><span data-stu-id="f017f-399">Executive</span></span> |<span data-ttu-id="f017f-400">300</span><span class="sxs-lookup"><span data-stu-id="f017f-400">300</span></span> |<span data-ttu-id="f017f-401">50000</span><span class="sxs-lookup"><span data-stu-id="f017f-401">50000</span></span> |<span data-ttu-id="f017f-402">50000</span><span class="sxs-lookup"><span data-stu-id="f017f-402">50000</span></span> |
| <span data-ttu-id="f017f-403">4</span><span class="sxs-lookup"><span data-stu-id="f017f-403">4</span></span> |<span data-ttu-id="f017f-404">Emma</span><span class="sxs-lookup"><span data-stu-id="f017f-404">Emma</span></span> |<span data-ttu-id="f017f-405">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-405">HR</span></span> |<span data-ttu-id="f017f-406">200</span><span class="sxs-lookup"><span data-stu-id="f017f-406">200</span></span> |<span data-ttu-id="f017f-407">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-407">10000</span></span> |<span data-ttu-id="f017f-408">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-408">10000</span></span> |
| <span data-ttu-id="f017f-409">5</span><span class="sxs-lookup"><span data-stu-id="f017f-409">5</span></span> |<span data-ttu-id="f017f-410">Jacob</span><span class="sxs-lookup"><span data-stu-id="f017f-410">Jacob</span></span> |<span data-ttu-id="f017f-411">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-411">HR</span></span> |<span data-ttu-id="f017f-412">200</span><span class="sxs-lookup"><span data-stu-id="f017f-412">200</span></span> |<span data-ttu-id="f017f-413">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-413">10000</span></span> |<span data-ttu-id="f017f-414">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-414">10000</span></span> |
| <span data-ttu-id="f017f-415">6</span><span class="sxs-lookup"><span data-stu-id="f017f-415">6</span></span> |<span data-ttu-id="f017f-416">Olivia</span><span class="sxs-lookup"><span data-stu-id="f017f-416">Olivia</span></span> |<span data-ttu-id="f017f-417">HR</span><span class="sxs-lookup"><span data-stu-id="f017f-417">HR</span></span> |<span data-ttu-id="f017f-418">200</span><span class="sxs-lookup"><span data-stu-id="f017f-418">200</span></span> |<span data-ttu-id="f017f-419">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-419">10000</span></span> |<span data-ttu-id="f017f-420">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-420">10000</span></span> |
| <span data-ttu-id="f017f-421">8</span><span class="sxs-lookup"><span data-stu-id="f017f-421">8</span></span> |<span data-ttu-id="f017f-422">Ava</span><span class="sxs-lookup"><span data-stu-id="f017f-422">Ava</span></span> |<span data-ttu-id="f017f-423">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-423">Marketing</span></span> |<span data-ttu-id="f017f-424">400</span><span class="sxs-lookup"><span data-stu-id="f017f-424">400</span></span> |<span data-ttu-id="f017f-425">15000</span><span class="sxs-lookup"><span data-stu-id="f017f-425">15000</span></span> |<span data-ttu-id="f017f-426">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-426">10000</span></span> |
| <span data-ttu-id="f017f-427">9</span><span class="sxs-lookup"><span data-stu-id="f017f-427">9</span></span> |<span data-ttu-id="f017f-428">Ethan</span><span class="sxs-lookup"><span data-stu-id="f017f-428">Ethan</span></span> |<span data-ttu-id="f017f-429">Marketing</span><span class="sxs-lookup"><span data-stu-id="f017f-429">Marketing</span></span> |<span data-ttu-id="f017f-430">400</span><span class="sxs-lookup"><span data-stu-id="f017f-430">400</span></span> |<span data-ttu-id="f017f-431">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-431">10000</span></span> |<span data-ttu-id="f017f-432">10000</span><span class="sxs-lookup"><span data-stu-id="f017f-432">10000</span></span> |

<span data-ttu-id="f017f-433">To see the highest salary of each department, replace MIN with MAX and re-run the query.</span><span class="sxs-lookup"><span data-stu-id="f017f-433">To see the highest salary of each department, replace MIN with MAX and re-run the query.</span></span>

## <a name="ranking-functions"></a><span data-ttu-id="f017f-434">Ranking Functions</span><span class="sxs-lookup"><span data-stu-id="f017f-434">Ranking Functions</span></span>
<span data-ttu-id="f017f-435">Ranking functions return a ranking value (a LONG) for each row in each partition as defined by the PARTITION BY and OVER clauses.</span><span class="sxs-lookup"><span data-stu-id="f017f-435">Ranking functions return a ranking value (a LONG) for each row in each partition as defined by the PARTITION BY and OVER clauses.</span></span> <span data-ttu-id="f017f-436">The ordering of the rank is controlled by the ORDER BY in the OVER clause.</span><span class="sxs-lookup"><span data-stu-id="f017f-436">The ordering of the rank is controlled by the ORDER BY in the OVER clause.</span></span>

<span data-ttu-id="f017f-437">The following are supported ranking functions:</span><span class="sxs-lookup"><span data-stu-id="f017f-437">The following are supported ranking functions:</span></span>

* <span data-ttu-id="f017f-438">RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-438">RANK</span></span>
* <span data-ttu-id="f017f-439">DENSE_RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-439">DENSE_RANK</span></span> 
* <span data-ttu-id="f017f-440">NTILE</span><span class="sxs-lookup"><span data-stu-id="f017f-440">NTILE</span></span>
* <span data-ttu-id="f017f-441">ROW_NUMBER</span><span class="sxs-lookup"><span data-stu-id="f017f-441">ROW_NUMBER</span></span>

<span data-ttu-id="f017f-442">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="f017f-442">**Syntax:**</span></span>

    [ RANK() | DENSE_RANK() | ROW_NUMBER() | NTILE(<numgroups>) ]
        OVER (
            [PARTITION BY <identifier, > …[n]]
            [ORDER BY <identifier, > …[n] [ASC|DESC]] 
    ) AS <alias>

* <span data-ttu-id="f017f-443">The ORDER BY clause is optional for ranking functions.</span><span class="sxs-lookup"><span data-stu-id="f017f-443">The ORDER BY clause is optional for ranking functions.</span></span> <span data-ttu-id="f017f-444">If the ORDER BY is not specified, then U-SQL assigns values based on the order it reads record, resulting in non-deterministic values for ROW_NUMBER, RANK, or DENSE_RANK.</span><span class="sxs-lookup"><span data-stu-id="f017f-444">If the ORDER BY is not specified, then U-SQL assigns values based on the order it reads record, resulting in non-deterministic values for ROW_NUMBER, RANK, or DENSE_RANK.</span></span>
* <span data-ttu-id="f017f-445">NTILE requires an expression that evaluates to a positive integer.</span><span class="sxs-lookup"><span data-stu-id="f017f-445">NTILE requires an expression that evaluates to a positive integer.</span></span> <span data-ttu-id="f017f-446">This number specifies the number of groups into which each partition must be divided.</span><span class="sxs-lookup"><span data-stu-id="f017f-446">This number specifies the number of groups into which each partition must be divided.</span></span> <span data-ttu-id="f017f-447">This identifier is used only with the NTILE ranking function.</span><span class="sxs-lookup"><span data-stu-id="f017f-447">This identifier is used only with the NTILE ranking function.</span></span> 

<span data-ttu-id="f017f-448">For more information on the OVER clause, see [U-SQL reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="f017f-448">For more information on the OVER clause, see [U-SQL reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>

<span data-ttu-id="f017f-449">ROW_NUMBER, RANK, and DENSE_RANK all assign numbers to rows in a window.</span><span class="sxs-lookup"><span data-stu-id="f017f-449">ROW_NUMBER, RANK, and DENSE_RANK all assign numbers to rows in a window.</span></span> <span data-ttu-id="f017f-450">Rather than cover them separately, it’s more intuitive to see how They respond to the same input.</span><span class="sxs-lookup"><span data-stu-id="f017f-450">Rather than cover them separately, it’s more intuitive to see how They respond to the same input.</span></span>

    @result =
    SELECT 
        *,
        ROW_NUMBER() OVER (PARTITION BY Vertical ORDER BY Latency) AS RowNumber,
        RANK() OVER (PARTITION BY Vertical ORDER BY Latency) AS Rank, 
        DENSE_RANK() OVER (PARTITION BY Vertical ORDER BY Latency) AS DenseRank 
    FROM @querylog;

<span data-ttu-id="f017f-451">Note the OVER clauses are identical.</span><span class="sxs-lookup"><span data-stu-id="f017f-451">Note the OVER clauses are identical.</span></span> <span data-ttu-id="f017f-452">The result:</span><span class="sxs-lookup"><span data-stu-id="f017f-452">The result:</span></span>

| <span data-ttu-id="f017f-453">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-453">Query</span></span> | <span data-ttu-id="f017f-454">Latency: INT</span><span class="sxs-lookup"><span data-stu-id="f017f-454">Latency: INT</span></span> | <span data-ttu-id="f017f-455">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-455">Vertical</span></span> | <span data-ttu-id="f017f-456">RowNumber</span><span class="sxs-lookup"><span data-stu-id="f017f-456">RowNumber</span></span> | <span data-ttu-id="f017f-457">Rank</span><span class="sxs-lookup"><span data-stu-id="f017f-457">Rank</span></span> | <span data-ttu-id="f017f-458">DenseRank</span><span class="sxs-lookup"><span data-stu-id="f017f-458">DenseRank</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f017f-459">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-459">Banana</span></span> |<span data-ttu-id="f017f-460">300</span><span class="sxs-lookup"><span data-stu-id="f017f-460">300</span></span> |<span data-ttu-id="f017f-461">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-461">Image</span></span> |<span data-ttu-id="f017f-462">1</span><span class="sxs-lookup"><span data-stu-id="f017f-462">1</span></span> |<span data-ttu-id="f017f-463">1</span><span class="sxs-lookup"><span data-stu-id="f017f-463">1</span></span> |<span data-ttu-id="f017f-464">1</span><span class="sxs-lookup"><span data-stu-id="f017f-464">1</span></span> |
| <span data-ttu-id="f017f-465">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-465">Cherry</span></span> |<span data-ttu-id="f017f-466">300</span><span class="sxs-lookup"><span data-stu-id="f017f-466">300</span></span> |<span data-ttu-id="f017f-467">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-467">Image</span></span> |<span data-ttu-id="f017f-468">2</span><span class="sxs-lookup"><span data-stu-id="f017f-468">2</span></span> |<span data-ttu-id="f017f-469">1</span><span class="sxs-lookup"><span data-stu-id="f017f-469">1</span></span> |<span data-ttu-id="f017f-470">1</span><span class="sxs-lookup"><span data-stu-id="f017f-470">1</span></span> |
| <span data-ttu-id="f017f-471">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-471">Durian</span></span> |<span data-ttu-id="f017f-472">500</span><span class="sxs-lookup"><span data-stu-id="f017f-472">500</span></span> |<span data-ttu-id="f017f-473">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-473">Image</span></span> |<span data-ttu-id="f017f-474">3</span><span class="sxs-lookup"><span data-stu-id="f017f-474">3</span></span> |<span data-ttu-id="f017f-475">3</span><span class="sxs-lookup"><span data-stu-id="f017f-475">3</span></span> |<span data-ttu-id="f017f-476">2</span><span class="sxs-lookup"><span data-stu-id="f017f-476">2</span></span> |
| <span data-ttu-id="f017f-477">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-477">Apple</span></span> |<span data-ttu-id="f017f-478">100</span><span class="sxs-lookup"><span data-stu-id="f017f-478">100</span></span> |<span data-ttu-id="f017f-479">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-479">Web</span></span> |<span data-ttu-id="f017f-480">1</span><span class="sxs-lookup"><span data-stu-id="f017f-480">1</span></span> |<span data-ttu-id="f017f-481">1</span><span class="sxs-lookup"><span data-stu-id="f017f-481">1</span></span> |<span data-ttu-id="f017f-482">1</span><span class="sxs-lookup"><span data-stu-id="f017f-482">1</span></span> |
| <span data-ttu-id="f017f-483">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-483">Fig</span></span> |<span data-ttu-id="f017f-484">200</span><span class="sxs-lookup"><span data-stu-id="f017f-484">200</span></span> |<span data-ttu-id="f017f-485">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-485">Web</span></span> |<span data-ttu-id="f017f-486">2</span><span class="sxs-lookup"><span data-stu-id="f017f-486">2</span></span> |<span data-ttu-id="f017f-487">2</span><span class="sxs-lookup"><span data-stu-id="f017f-487">2</span></span> |<span data-ttu-id="f017f-488">2</span><span class="sxs-lookup"><span data-stu-id="f017f-488">2</span></span> |
| <span data-ttu-id="f017f-489">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-489">Papaya</span></span> |<span data-ttu-id="f017f-490">200</span><span class="sxs-lookup"><span data-stu-id="f017f-490">200</span></span> |<span data-ttu-id="f017f-491">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-491">Web</span></span> |<span data-ttu-id="f017f-492">3</span><span class="sxs-lookup"><span data-stu-id="f017f-492">3</span></span> |<span data-ttu-id="f017f-493">2</span><span class="sxs-lookup"><span data-stu-id="f017f-493">2</span></span> |<span data-ttu-id="f017f-494">2</span><span class="sxs-lookup"><span data-stu-id="f017f-494">2</span></span> |
| <span data-ttu-id="f017f-495">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-495">Fig</span></span> |<span data-ttu-id="f017f-496">300</span><span class="sxs-lookup"><span data-stu-id="f017f-496">300</span></span> |<span data-ttu-id="f017f-497">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-497">Web</span></span> |<span data-ttu-id="f017f-498">4</span><span class="sxs-lookup"><span data-stu-id="f017f-498">4</span></span> |<span data-ttu-id="f017f-499">4</span><span class="sxs-lookup"><span data-stu-id="f017f-499">4</span></span> |<span data-ttu-id="f017f-500">3</span><span class="sxs-lookup"><span data-stu-id="f017f-500">3</span></span> |
| <span data-ttu-id="f017f-501">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-501">Cherry</span></span> |<span data-ttu-id="f017f-502">400</span><span class="sxs-lookup"><span data-stu-id="f017f-502">400</span></span> |<span data-ttu-id="f017f-503">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-503">Web</span></span> |<span data-ttu-id="f017f-504">5</span><span class="sxs-lookup"><span data-stu-id="f017f-504">5</span></span> |<span data-ttu-id="f017f-505">5</span><span class="sxs-lookup"><span data-stu-id="f017f-505">5</span></span> |<span data-ttu-id="f017f-506">4</span><span class="sxs-lookup"><span data-stu-id="f017f-506">4</span></span> |
| <span data-ttu-id="f017f-507">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-507">Durian</span></span> |<span data-ttu-id="f017f-508">500</span><span class="sxs-lookup"><span data-stu-id="f017f-508">500</span></span> |<span data-ttu-id="f017f-509">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-509">Web</span></span> |<span data-ttu-id="f017f-510">6</span><span class="sxs-lookup"><span data-stu-id="f017f-510">6</span></span> |<span data-ttu-id="f017f-511">6</span><span class="sxs-lookup"><span data-stu-id="f017f-511">6</span></span> |<span data-ttu-id="f017f-512">5</span><span class="sxs-lookup"><span data-stu-id="f017f-512">5</span></span> |

### <a name="rownumber"></a><span data-ttu-id="f017f-513">ROW_NUMBER</span><span class="sxs-lookup"><span data-stu-id="f017f-513">ROW_NUMBER</span></span>
<span data-ttu-id="f017f-514">Within each Window (Vertical, either Image or Web), the row number increases by 1 ordered by Latency.</span><span class="sxs-lookup"><span data-stu-id="f017f-514">Within each Window (Vertical, either Image or Web), the row number increases by 1 ordered by Latency.</span></span>  

![U-SQL window function ROW_NUMBER](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-use-windowing-functions/u-sql-windowing-function-row-number-result.png)

### <a name="rank"></a><span data-ttu-id="f017f-516">RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-516">RANK</span></span>
<span data-ttu-id="f017f-517">Different from ROW_NUMBER(), RANK() uses the value of the latency, which is specified in the ORDER BY clause for the window.</span><span class="sxs-lookup"><span data-stu-id="f017f-517">Different from ROW_NUMBER(), RANK() uses the value of the latency, which is specified in the ORDER BY clause for the window.</span></span>

<span data-ttu-id="f017f-518">RANK starts with (1, 1, 3) because the first two values for Latency are the same.</span><span class="sxs-lookup"><span data-stu-id="f017f-518">RANK starts with (1, 1, 3) because the first two values for Latency are the same.</span></span> <span data-ttu-id="f017f-519">Then the next value is 3 because the Latency value has moved on to 500.</span><span class="sxs-lookup"><span data-stu-id="f017f-519">Then the next value is 3 because the Latency value has moved on to 500.</span></span> <span data-ttu-id="f017f-520">The key point being that even though duplicate values are given the same rank, the RANK number will skip to the next ROW_NUMBER value.</span><span class="sxs-lookup"><span data-stu-id="f017f-520">The key point being that even though duplicate values are given the same rank, the RANK number will skip to the next ROW_NUMBER value.</span></span> <span data-ttu-id="f017f-521">You can see this pattern repeat with the sequence (2, 2, 4) in the Web vertical.</span><span class="sxs-lookup"><span data-stu-id="f017f-521">You can see this pattern repeat with the sequence (2, 2, 4) in the Web vertical.</span></span>

![U-SQL window function RANK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-use-windowing-functions/u-sql-windowing-function-rank-result.png)

### <a name="denserank"></a><span data-ttu-id="f017f-523">DENSE_RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-523">DENSE_RANK</span></span>
<span data-ttu-id="f017f-524">DENSE_RANK is just like RANK except it doesn’t skip to the next ROW_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="f017f-524">DENSE_RANK is just like RANK except it doesn’t skip to the next ROW_NUMBER.</span></span> <span data-ttu-id="f017f-525">DENSE_RANK goes to the next number in the sequence.</span><span class="sxs-lookup"><span data-stu-id="f017f-525">DENSE_RANK goes to the next number in the sequence.</span></span> <span data-ttu-id="f017f-526">Notice the sequences (1, 1, 2) and (2, 2, 3) in the sample.</span><span class="sxs-lookup"><span data-stu-id="f017f-526">Notice the sequences (1, 1, 2) and (2, 2, 3) in the sample.</span></span>

![U-SQL window function DENSE_RANK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-use-windowing-functions/u-sql-windowing-function-dense-rank-result.png)

### <a name="remarks"></a><span data-ttu-id="f017f-528">Remarks</span><span class="sxs-lookup"><span data-stu-id="f017f-528">Remarks</span></span>
* <span data-ttu-id="f017f-529">If ORDER BY is not specified, the ranking function is applied to the rowset without any ordering, resulting in non-deterministic behavior.</span><span class="sxs-lookup"><span data-stu-id="f017f-529">If ORDER BY is not specified, the ranking function is applied to the rowset without any ordering, resulting in non-deterministic behavior.</span></span>
* <span data-ttu-id="f017f-530">The following conditions must be true to guarantee that rows returned by a query using ROW_NUMBER are ordered the same with each execution.</span><span class="sxs-lookup"><span data-stu-id="f017f-530">The following conditions must be true to guarantee that rows returned by a query using ROW_NUMBER are ordered the same with each execution.</span></span>
  
  * <span data-ttu-id="f017f-531">Values of the partitioned column are unique.</span><span class="sxs-lookup"><span data-stu-id="f017f-531">Values of the partitioned column are unique.</span></span>
  * <span data-ttu-id="f017f-532">Values of the ORDER BY columns are unique.</span><span class="sxs-lookup"><span data-stu-id="f017f-532">Values of the ORDER BY columns are unique.</span></span>
  * <span data-ttu-id="f017f-533">Combinations of values of the partition column and ORDER BY columns are unique.</span><span class="sxs-lookup"><span data-stu-id="f017f-533">Combinations of values of the partition column and ORDER BY columns are unique.</span></span>

### <a name="ntile"></a><span data-ttu-id="f017f-534">NTILE</span><span class="sxs-lookup"><span data-stu-id="f017f-534">NTILE</span></span>
<span data-ttu-id="f017f-535">NTILE distributes the rows in an ordered partition into a specified number of groups.</span><span class="sxs-lookup"><span data-stu-id="f017f-535">NTILE distributes the rows in an ordered partition into a specified number of groups.</span></span> <span data-ttu-id="f017f-536">The groups are numbered, starting at one.</span><span class="sxs-lookup"><span data-stu-id="f017f-536">The groups are numbered, starting at one.</span></span> 

<span data-ttu-id="f017f-537">The following example splits the set of rows in each partition (vertical) into four groups, ordered by latency, and returns the group number for each row.</span><span class="sxs-lookup"><span data-stu-id="f017f-537">The following example splits the set of rows in each partition (vertical) into four groups, ordered by latency, and returns the group number for each row.</span></span> 

<span data-ttu-id="f017f-538">The Image vertical has three rows, so it has three groups.</span><span class="sxs-lookup"><span data-stu-id="f017f-538">The Image vertical has three rows, so it has three groups.</span></span> 

<span data-ttu-id="f017f-539">The Web vertical has six rows.</span><span class="sxs-lookup"><span data-stu-id="f017f-539">The Web vertical has six rows.</span></span>  <span data-ttu-id="f017f-540">The two extra rows are distributed to the first two groups.</span><span class="sxs-lookup"><span data-stu-id="f017f-540">The two extra rows are distributed to the first two groups.</span></span> <span data-ttu-id="f017f-541">That's why there are two rows in group 1 and group 2, and only one row in group 3 and group 4.</span><span class="sxs-lookup"><span data-stu-id="f017f-541">That's why there are two rows in group 1 and group 2, and only one row in group 3 and group 4.</span></span>  

    @result =
        SELECT 
            *,
            NTILE(4) OVER(PARTITION BY Vertical ORDER BY Latency) AS Quartile   
        FROM @querylog;

<span data-ttu-id="f017f-542">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-542">The results:</span></span>

| <span data-ttu-id="f017f-543">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-543">Query</span></span> | <span data-ttu-id="f017f-544">Latency</span><span class="sxs-lookup"><span data-stu-id="f017f-544">Latency</span></span> | <span data-ttu-id="f017f-545">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-545">Vertical</span></span> | <span data-ttu-id="f017f-546">Quartile</span><span class="sxs-lookup"><span data-stu-id="f017f-546">Quartile</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f017f-547">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-547">Banana</span></span> |<span data-ttu-id="f017f-548">300</span><span class="sxs-lookup"><span data-stu-id="f017f-548">300</span></span> |<span data-ttu-id="f017f-549">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-549">Image</span></span> |<span data-ttu-id="f017f-550">1</span><span class="sxs-lookup"><span data-stu-id="f017f-550">1</span></span> |
| <span data-ttu-id="f017f-551">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-551">Cherry</span></span> |<span data-ttu-id="f017f-552">300</span><span class="sxs-lookup"><span data-stu-id="f017f-552">300</span></span> |<span data-ttu-id="f017f-553">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-553">Image</span></span> |<span data-ttu-id="f017f-554">2</span><span class="sxs-lookup"><span data-stu-id="f017f-554">2</span></span> |
| <span data-ttu-id="f017f-555">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-555">Durian</span></span> |<span data-ttu-id="f017f-556">500</span><span class="sxs-lookup"><span data-stu-id="f017f-556">500</span></span> |<span data-ttu-id="f017f-557">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-557">Image</span></span> |<span data-ttu-id="f017f-558">3</span><span class="sxs-lookup"><span data-stu-id="f017f-558">3</span></span> |
| <span data-ttu-id="f017f-559">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-559">Apple</span></span> |<span data-ttu-id="f017f-560">100</span><span class="sxs-lookup"><span data-stu-id="f017f-560">100</span></span> |<span data-ttu-id="f017f-561">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-561">Web</span></span> |<span data-ttu-id="f017f-562">1</span><span class="sxs-lookup"><span data-stu-id="f017f-562">1</span></span> |
| <span data-ttu-id="f017f-563">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-563">Fig</span></span> |<span data-ttu-id="f017f-564">200</span><span class="sxs-lookup"><span data-stu-id="f017f-564">200</span></span> |<span data-ttu-id="f017f-565">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-565">Web</span></span> |<span data-ttu-id="f017f-566">1</span><span class="sxs-lookup"><span data-stu-id="f017f-566">1</span></span> |
| <span data-ttu-id="f017f-567">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-567">Papaya</span></span> |<span data-ttu-id="f017f-568">200</span><span class="sxs-lookup"><span data-stu-id="f017f-568">200</span></span> |<span data-ttu-id="f017f-569">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-569">Web</span></span> |<span data-ttu-id="f017f-570">2</span><span class="sxs-lookup"><span data-stu-id="f017f-570">2</span></span> |
| <span data-ttu-id="f017f-571">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-571">Fig</span></span> |<span data-ttu-id="f017f-572">300</span><span class="sxs-lookup"><span data-stu-id="f017f-572">300</span></span> |<span data-ttu-id="f017f-573">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-573">Web</span></span> |<span data-ttu-id="f017f-574">2</span><span class="sxs-lookup"><span data-stu-id="f017f-574">2</span></span> |
| <span data-ttu-id="f017f-575">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-575">Cherry</span></span> |<span data-ttu-id="f017f-576">400</span><span class="sxs-lookup"><span data-stu-id="f017f-576">400</span></span> |<span data-ttu-id="f017f-577">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-577">Web</span></span> |<span data-ttu-id="f017f-578">3</span><span class="sxs-lookup"><span data-stu-id="f017f-578">3</span></span> |
| <span data-ttu-id="f017f-579">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-579">Durian</span></span> |<span data-ttu-id="f017f-580">500</span><span class="sxs-lookup"><span data-stu-id="f017f-580">500</span></span> |<span data-ttu-id="f017f-581">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-581">Web</span></span> |<span data-ttu-id="f017f-582">4</span><span class="sxs-lookup"><span data-stu-id="f017f-582">4</span></span> |

<span data-ttu-id="f017f-583">NTILE takes a parameter ("numgroups").</span><span class="sxs-lookup"><span data-stu-id="f017f-583">NTILE takes a parameter ("numgroups").</span></span> <span data-ttu-id="f017f-584">Numgroups is a positive int or long constant expression that specifies the number of groups into which each partition must be divided.</span><span class="sxs-lookup"><span data-stu-id="f017f-584">Numgroups is a positive int or long constant expression that specifies the number of groups into which each partition must be divided.</span></span> 

* <span data-ttu-id="f017f-585">If the number of rows in the partition is evenly divisible by numgroups, then the groups will have equal size.</span><span class="sxs-lookup"><span data-stu-id="f017f-585">If the number of rows in the partition is evenly divisible by numgroups, then the groups will have equal size.</span></span> 
* <span data-ttu-id="f017f-586">If the number of rows in a partition is not divisible by numgroups, this causes groups of two sizes that differ by one member.</span><span class="sxs-lookup"><span data-stu-id="f017f-586">If the number of rows in a partition is not divisible by numgroups, this causes groups of two sizes that differ by one member.</span></span> <span data-ttu-id="f017f-587">Larger groups come before smaller groups in the order specified by the OVER clause.</span><span class="sxs-lookup"><span data-stu-id="f017f-587">Larger groups come before smaller groups in the order specified by the OVER clause.</span></span> 

<span data-ttu-id="f017f-588">For example:</span><span class="sxs-lookup"><span data-stu-id="f017f-588">For example:</span></span>

* <span data-ttu-id="f017f-589">100 rows divided into 4 groups: [ 25, 25, 25, 25 ]</span><span class="sxs-lookup"><span data-stu-id="f017f-589">100 rows divided into 4 groups: [ 25, 25, 25, 25 ]</span></span>
* <span data-ttu-id="f017f-590">102 rows divided into 4 groups: [ 26, 26, 25, 25 ]</span><span class="sxs-lookup"><span data-stu-id="f017f-590">102 rows divided into 4 groups: [ 26, 26, 25, 25 ]</span></span>

### <a name="top-n-records-per-partition-via-rank-denserank-or-rownumber"></a><span data-ttu-id="f017f-591">Top N Records per Partition via RANK, DENSE_RANK or ROW_NUMBER</span><span class="sxs-lookup"><span data-stu-id="f017f-591">Top N Records per Partition via RANK, DENSE_RANK or ROW_NUMBER</span></span>
<span data-ttu-id="f017f-592">Many users want to select only TOP n rows per group, which can't be done with the traditional GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="f017f-592">Many users want to select only TOP n rows per group, which can't be done with the traditional GROUP BY.</span></span> 

<span data-ttu-id="f017f-593">You have seen the following example at the beginning of the Ranking functions section.</span><span class="sxs-lookup"><span data-stu-id="f017f-593">You have seen the following example at the beginning of the Ranking functions section.</span></span> <span data-ttu-id="f017f-594">It doesn't show top N records for each partition:</span><span class="sxs-lookup"><span data-stu-id="f017f-594">It doesn't show top N records for each partition:</span></span>

    @result =
    SELECT 
        *,
        ROW_NUMBER() OVER (PARTITION BY Vertical ORDER BY Latency) AS RowNumber,
        RANK() OVER (PARTITION BY Vertical ORDER BY Latency) AS Rank,
        DENSE_RANK() OVER (PARTITION BY Vertical ORDER BY Latency) AS DenseRank
    FROM @querylog;

<span data-ttu-id="f017f-595">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-595">The results:</span></span>

| <span data-ttu-id="f017f-596">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-596">Query</span></span> | <span data-ttu-id="f017f-597">Latency</span><span class="sxs-lookup"><span data-stu-id="f017f-597">Latency</span></span> | <span data-ttu-id="f017f-598">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-598">Vertical</span></span> | <span data-ttu-id="f017f-599">Rank</span><span class="sxs-lookup"><span data-stu-id="f017f-599">Rank</span></span> | <span data-ttu-id="f017f-600">DenseRank</span><span class="sxs-lookup"><span data-stu-id="f017f-600">DenseRank</span></span> | <span data-ttu-id="f017f-601">RowNumber</span><span class="sxs-lookup"><span data-stu-id="f017f-601">RowNumber</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f017f-602">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-602">Banana</span></span> |<span data-ttu-id="f017f-603">300</span><span class="sxs-lookup"><span data-stu-id="f017f-603">300</span></span> |<span data-ttu-id="f017f-604">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-604">Image</span></span> |<span data-ttu-id="f017f-605">1</span><span class="sxs-lookup"><span data-stu-id="f017f-605">1</span></span> |<span data-ttu-id="f017f-606">1</span><span class="sxs-lookup"><span data-stu-id="f017f-606">1</span></span> |<span data-ttu-id="f017f-607">1</span><span class="sxs-lookup"><span data-stu-id="f017f-607">1</span></span> |
| <span data-ttu-id="f017f-608">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-608">Cherry</span></span> |<span data-ttu-id="f017f-609">300</span><span class="sxs-lookup"><span data-stu-id="f017f-609">300</span></span> |<span data-ttu-id="f017f-610">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-610">Image</span></span> |<span data-ttu-id="f017f-611">1</span><span class="sxs-lookup"><span data-stu-id="f017f-611">1</span></span> |<span data-ttu-id="f017f-612">1</span><span class="sxs-lookup"><span data-stu-id="f017f-612">1</span></span> |<span data-ttu-id="f017f-613">2</span><span class="sxs-lookup"><span data-stu-id="f017f-613">2</span></span> |
| <span data-ttu-id="f017f-614">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-614">Durian</span></span> |<span data-ttu-id="f017f-615">500</span><span class="sxs-lookup"><span data-stu-id="f017f-615">500</span></span> |<span data-ttu-id="f017f-616">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-616">Image</span></span> |<span data-ttu-id="f017f-617">3</span><span class="sxs-lookup"><span data-stu-id="f017f-617">3</span></span> |<span data-ttu-id="f017f-618">2</span><span class="sxs-lookup"><span data-stu-id="f017f-618">2</span></span> |<span data-ttu-id="f017f-619">3</span><span class="sxs-lookup"><span data-stu-id="f017f-619">3</span></span> |
| <span data-ttu-id="f017f-620">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-620">Apple</span></span> |<span data-ttu-id="f017f-621">100</span><span class="sxs-lookup"><span data-stu-id="f017f-621">100</span></span> |<span data-ttu-id="f017f-622">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-622">Web</span></span> |<span data-ttu-id="f017f-623">1</span><span class="sxs-lookup"><span data-stu-id="f017f-623">1</span></span> |<span data-ttu-id="f017f-624">1</span><span class="sxs-lookup"><span data-stu-id="f017f-624">1</span></span> |<span data-ttu-id="f017f-625">1</span><span class="sxs-lookup"><span data-stu-id="f017f-625">1</span></span> |
| <span data-ttu-id="f017f-626">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-626">Fig</span></span> |<span data-ttu-id="f017f-627">200</span><span class="sxs-lookup"><span data-stu-id="f017f-627">200</span></span> |<span data-ttu-id="f017f-628">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-628">Web</span></span> |<span data-ttu-id="f017f-629">2</span><span class="sxs-lookup"><span data-stu-id="f017f-629">2</span></span> |<span data-ttu-id="f017f-630">2</span><span class="sxs-lookup"><span data-stu-id="f017f-630">2</span></span> |<span data-ttu-id="f017f-631">2</span><span class="sxs-lookup"><span data-stu-id="f017f-631">2</span></span> |
| <span data-ttu-id="f017f-632">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-632">Papaya</span></span> |<span data-ttu-id="f017f-633">200</span><span class="sxs-lookup"><span data-stu-id="f017f-633">200</span></span> |<span data-ttu-id="f017f-634">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-634">Web</span></span> |<span data-ttu-id="f017f-635">2</span><span class="sxs-lookup"><span data-stu-id="f017f-635">2</span></span> |<span data-ttu-id="f017f-636">2</span><span class="sxs-lookup"><span data-stu-id="f017f-636">2</span></span> |<span data-ttu-id="f017f-637">3</span><span class="sxs-lookup"><span data-stu-id="f017f-637">3</span></span> |
| <span data-ttu-id="f017f-638">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-638">Fig</span></span> |<span data-ttu-id="f017f-639">300</span><span class="sxs-lookup"><span data-stu-id="f017f-639">300</span></span> |<span data-ttu-id="f017f-640">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-640">Web</span></span> |<span data-ttu-id="f017f-641">4</span><span class="sxs-lookup"><span data-stu-id="f017f-641">4</span></span> |<span data-ttu-id="f017f-642">3</span><span class="sxs-lookup"><span data-stu-id="f017f-642">3</span></span> |<span data-ttu-id="f017f-643">4</span><span class="sxs-lookup"><span data-stu-id="f017f-643">4</span></span> |
| <span data-ttu-id="f017f-644">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-644">Cherry</span></span> |<span data-ttu-id="f017f-645">400</span><span class="sxs-lookup"><span data-stu-id="f017f-645">400</span></span> |<span data-ttu-id="f017f-646">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-646">Web</span></span> |<span data-ttu-id="f017f-647">5</span><span class="sxs-lookup"><span data-stu-id="f017f-647">5</span></span> |<span data-ttu-id="f017f-648">4</span><span class="sxs-lookup"><span data-stu-id="f017f-648">4</span></span> |<span data-ttu-id="f017f-649">5</span><span class="sxs-lookup"><span data-stu-id="f017f-649">5</span></span> |
| <span data-ttu-id="f017f-650">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-650">Durian</span></span> |<span data-ttu-id="f017f-651">500</span><span class="sxs-lookup"><span data-stu-id="f017f-651">500</span></span> |<span data-ttu-id="f017f-652">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-652">Web</span></span> |<span data-ttu-id="f017f-653">6</span><span class="sxs-lookup"><span data-stu-id="f017f-653">6</span></span> |<span data-ttu-id="f017f-654">5</span><span class="sxs-lookup"><span data-stu-id="f017f-654">5</span></span> |<span data-ttu-id="f017f-655">6</span><span class="sxs-lookup"><span data-stu-id="f017f-655">6</span></span> |

### <a name="top-n-with-dense-rank"></a><span data-ttu-id="f017f-656">TOP N with DENSE RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-656">TOP N with DENSE RANK</span></span>
<span data-ttu-id="f017f-657">The following example returns the top three records from each group, with no gaps in the sequential rank numbering of rows in each partition.</span><span class="sxs-lookup"><span data-stu-id="f017f-657">The following example returns the top three records from each group, with no gaps in the sequential rank numbering of rows in each partition.</span></span>

    @result =
    SELECT 
        *,
        DENSE_RANK() OVER (PARTITION BY Vertical ORDER BY Latency) AS DenseRank
    FROM @querylog;

    @result = 
        SELECT *
        FROM @result
        WHERE DenseRank <= 3;

<span data-ttu-id="f017f-658">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-658">The results:</span></span>

| <span data-ttu-id="f017f-659">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-659">Query</span></span> | <span data-ttu-id="f017f-660">Latency</span><span class="sxs-lookup"><span data-stu-id="f017f-660">Latency</span></span> | <span data-ttu-id="f017f-661">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-661">Vertical</span></span> | <span data-ttu-id="f017f-662">DenseRank</span><span class="sxs-lookup"><span data-stu-id="f017f-662">DenseRank</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f017f-663">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-663">Banana</span></span> |<span data-ttu-id="f017f-664">300</span><span class="sxs-lookup"><span data-stu-id="f017f-664">300</span></span> |<span data-ttu-id="f017f-665">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-665">Image</span></span> |<span data-ttu-id="f017f-666">1</span><span class="sxs-lookup"><span data-stu-id="f017f-666">1</span></span> |
| <span data-ttu-id="f017f-667">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-667">Cherry</span></span> |<span data-ttu-id="f017f-668">300</span><span class="sxs-lookup"><span data-stu-id="f017f-668">300</span></span> |<span data-ttu-id="f017f-669">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-669">Image</span></span> |<span data-ttu-id="f017f-670">1</span><span class="sxs-lookup"><span data-stu-id="f017f-670">1</span></span> |
| <span data-ttu-id="f017f-671">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-671">Durian</span></span> |<span data-ttu-id="f017f-672">500</span><span class="sxs-lookup"><span data-stu-id="f017f-672">500</span></span> |<span data-ttu-id="f017f-673">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-673">Image</span></span> |<span data-ttu-id="f017f-674">2</span><span class="sxs-lookup"><span data-stu-id="f017f-674">2</span></span> |
| <span data-ttu-id="f017f-675">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-675">Apple</span></span> |<span data-ttu-id="f017f-676">100</span><span class="sxs-lookup"><span data-stu-id="f017f-676">100</span></span> |<span data-ttu-id="f017f-677">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-677">Web</span></span> |<span data-ttu-id="f017f-678">1</span><span class="sxs-lookup"><span data-stu-id="f017f-678">1</span></span> |
| <span data-ttu-id="f017f-679">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-679">Fig</span></span> |<span data-ttu-id="f017f-680">200</span><span class="sxs-lookup"><span data-stu-id="f017f-680">200</span></span> |<span data-ttu-id="f017f-681">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-681">Web</span></span> |<span data-ttu-id="f017f-682">2</span><span class="sxs-lookup"><span data-stu-id="f017f-682">2</span></span> |
| <span data-ttu-id="f017f-683">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-683">Papaya</span></span> |<span data-ttu-id="f017f-684">200</span><span class="sxs-lookup"><span data-stu-id="f017f-684">200</span></span> |<span data-ttu-id="f017f-685">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-685">Web</span></span> |<span data-ttu-id="f017f-686">2</span><span class="sxs-lookup"><span data-stu-id="f017f-686">2</span></span> |
| <span data-ttu-id="f017f-687">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-687">Fig</span></span> |<span data-ttu-id="f017f-688">300</span><span class="sxs-lookup"><span data-stu-id="f017f-688">300</span></span> |<span data-ttu-id="f017f-689">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-689">Web</span></span> |<span data-ttu-id="f017f-690">3</span><span class="sxs-lookup"><span data-stu-id="f017f-690">3</span></span> |

### <a name="top-n-with-rank"></a><span data-ttu-id="f017f-691">TOP N with RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-691">TOP N with RANK</span></span>
    @result =
        SELECT 
            *,
            RANK() OVER (PARTITION BY Vertical ORDER BY Latency) AS Rank
        FROM @querylog;

    @result = 
        SELECT *
        FROM @result
        WHERE Rank <= 3;

<span data-ttu-id="f017f-692">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-692">The results:</span></span>    

| <span data-ttu-id="f017f-693">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-693">Query</span></span> | <span data-ttu-id="f017f-694">Latency</span><span class="sxs-lookup"><span data-stu-id="f017f-694">Latency</span></span> | <span data-ttu-id="f017f-695">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-695">Vertical</span></span> | <span data-ttu-id="f017f-696">Rank</span><span class="sxs-lookup"><span data-stu-id="f017f-696">Rank</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f017f-697">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-697">Banana</span></span> |<span data-ttu-id="f017f-698">300</span><span class="sxs-lookup"><span data-stu-id="f017f-698">300</span></span> |<span data-ttu-id="f017f-699">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-699">Image</span></span> |<span data-ttu-id="f017f-700">1</span><span class="sxs-lookup"><span data-stu-id="f017f-700">1</span></span> |
| <span data-ttu-id="f017f-701">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-701">Cherry</span></span> |<span data-ttu-id="f017f-702">300</span><span class="sxs-lookup"><span data-stu-id="f017f-702">300</span></span> |<span data-ttu-id="f017f-703">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-703">Image</span></span> |<span data-ttu-id="f017f-704">1</span><span class="sxs-lookup"><span data-stu-id="f017f-704">1</span></span> |
| <span data-ttu-id="f017f-705">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-705">Durian</span></span> |<span data-ttu-id="f017f-706">500</span><span class="sxs-lookup"><span data-stu-id="f017f-706">500</span></span> |<span data-ttu-id="f017f-707">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-707">Image</span></span> |<span data-ttu-id="f017f-708">3</span><span class="sxs-lookup"><span data-stu-id="f017f-708">3</span></span> |
| <span data-ttu-id="f017f-709">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-709">Apple</span></span> |<span data-ttu-id="f017f-710">100</span><span class="sxs-lookup"><span data-stu-id="f017f-710">100</span></span> |<span data-ttu-id="f017f-711">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-711">Web</span></span> |<span data-ttu-id="f017f-712">1</span><span class="sxs-lookup"><span data-stu-id="f017f-712">1</span></span> |
| <span data-ttu-id="f017f-713">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-713">Fig</span></span> |<span data-ttu-id="f017f-714">200</span><span class="sxs-lookup"><span data-stu-id="f017f-714">200</span></span> |<span data-ttu-id="f017f-715">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-715">Web</span></span> |<span data-ttu-id="f017f-716">2</span><span class="sxs-lookup"><span data-stu-id="f017f-716">2</span></span> |
| <span data-ttu-id="f017f-717">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-717">Papaya</span></span> |<span data-ttu-id="f017f-718">200</span><span class="sxs-lookup"><span data-stu-id="f017f-718">200</span></span> |<span data-ttu-id="f017f-719">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-719">Web</span></span> |<span data-ttu-id="f017f-720">2</span><span class="sxs-lookup"><span data-stu-id="f017f-720">2</span></span> |

### <a name="top-n-with-rownumber"></a><span data-ttu-id="f017f-721">TOP N with ROW_NUMBER</span><span class="sxs-lookup"><span data-stu-id="f017f-721">TOP N with ROW_NUMBER</span></span>
    @result =
        SELECT 
            *,
            ROW_NUMBER() OVER (PARTITION BY Vertical ORDER BY Latency) AS RowNumber
        FROM @querylog;

    @result = 
        SELECT *
        FROM @result
        WHERE RowNumber <= 3;

<span data-ttu-id="f017f-722">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-722">The results:</span></span>   

| <span data-ttu-id="f017f-723">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-723">Query</span></span> | <span data-ttu-id="f017f-724">Latency</span><span class="sxs-lookup"><span data-stu-id="f017f-724">Latency</span></span> | <span data-ttu-id="f017f-725">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-725">Vertical</span></span> | <span data-ttu-id="f017f-726">RowNumber</span><span class="sxs-lookup"><span data-stu-id="f017f-726">RowNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f017f-727">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-727">Banana</span></span> |<span data-ttu-id="f017f-728">300</span><span class="sxs-lookup"><span data-stu-id="f017f-728">300</span></span> |<span data-ttu-id="f017f-729">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-729">Image</span></span> |<span data-ttu-id="f017f-730">1</span><span class="sxs-lookup"><span data-stu-id="f017f-730">1</span></span> |
| <span data-ttu-id="f017f-731">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-731">Cherry</span></span> |<span data-ttu-id="f017f-732">300</span><span class="sxs-lookup"><span data-stu-id="f017f-732">300</span></span> |<span data-ttu-id="f017f-733">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-733">Image</span></span> |<span data-ttu-id="f017f-734">2</span><span class="sxs-lookup"><span data-stu-id="f017f-734">2</span></span> |
| <span data-ttu-id="f017f-735">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-735">Durian</span></span> |<span data-ttu-id="f017f-736">500</span><span class="sxs-lookup"><span data-stu-id="f017f-736">500</span></span> |<span data-ttu-id="f017f-737">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-737">Image</span></span> |<span data-ttu-id="f017f-738">3</span><span class="sxs-lookup"><span data-stu-id="f017f-738">3</span></span> |
| <span data-ttu-id="f017f-739">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-739">Apple</span></span> |<span data-ttu-id="f017f-740">100</span><span class="sxs-lookup"><span data-stu-id="f017f-740">100</span></span> |<span data-ttu-id="f017f-741">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-741">Web</span></span> |<span data-ttu-id="f017f-742">1</span><span class="sxs-lookup"><span data-stu-id="f017f-742">1</span></span> |
| <span data-ttu-id="f017f-743">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-743">Fig</span></span> |<span data-ttu-id="f017f-744">200</span><span class="sxs-lookup"><span data-stu-id="f017f-744">200</span></span> |<span data-ttu-id="f017f-745">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-745">Web</span></span> |<span data-ttu-id="f017f-746">2</span><span class="sxs-lookup"><span data-stu-id="f017f-746">2</span></span> |
| <span data-ttu-id="f017f-747">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-747">Papaya</span></span> |<span data-ttu-id="f017f-748">200</span><span class="sxs-lookup"><span data-stu-id="f017f-748">200</span></span> |<span data-ttu-id="f017f-749">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-749">Web</span></span> |<span data-ttu-id="f017f-750">3</span><span class="sxs-lookup"><span data-stu-id="f017f-750">3</span></span> |

### <a name="assign-globally-unique-row-number"></a><span data-ttu-id="f017f-751">Assign Globally Unique Row Number</span><span class="sxs-lookup"><span data-stu-id="f017f-751">Assign Globally Unique Row Number</span></span>
<span data-ttu-id="f017f-752">It’s often useful to assign a globally unique number to each row.</span><span class="sxs-lookup"><span data-stu-id="f017f-752">It’s often useful to assign a globally unique number to each row.</span></span> <span data-ttu-id="f017f-753">Ranking functions are easier and more efficient than using a reducer.</span><span class="sxs-lookup"><span data-stu-id="f017f-753">Ranking functions are easier and more efficient than using a reducer.</span></span>

    @result =
        SELECT 
            *,
            ROW_NUMBER() OVER () AS RowNumber
        FROM @querylog;

<!-- ################################################### -->
## <a name="analytic-functions"></a><span data-ttu-id="f017f-754">Analytic functions</span><span class="sxs-lookup"><span data-stu-id="f017f-754">Analytic functions</span></span>
<span data-ttu-id="f017f-755">Analytic functions are used to understand the distributions of values in windows.</span><span class="sxs-lookup"><span data-stu-id="f017f-755">Analytic functions are used to understand the distributions of values in windows.</span></span> <span data-ttu-id="f017f-756">The most common scenario for using analytic functions is the computation of percentiles.</span><span class="sxs-lookup"><span data-stu-id="f017f-756">The most common scenario for using analytic functions is the computation of percentiles.</span></span>

<span data-ttu-id="f017f-757">**Supported analytic window functions**</span><span class="sxs-lookup"><span data-stu-id="f017f-757">**Supported analytic window functions**</span></span>

* <span data-ttu-id="f017f-758">CUME_DIST</span><span class="sxs-lookup"><span data-stu-id="f017f-758">CUME_DIST</span></span> 
* <span data-ttu-id="f017f-759">PERCENT_RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-759">PERCENT_RANK</span></span>
* <span data-ttu-id="f017f-760">PERCENTILE_CONT</span><span class="sxs-lookup"><span data-stu-id="f017f-760">PERCENTILE_CONT</span></span>
* <span data-ttu-id="f017f-761">PERCENTILE_DISC</span><span class="sxs-lookup"><span data-stu-id="f017f-761">PERCENTILE_DISC</span></span>

### <a name="cumedist"></a><span data-ttu-id="f017f-762">CUME_DIST</span><span class="sxs-lookup"><span data-stu-id="f017f-762">CUME_DIST</span></span>
<span data-ttu-id="f017f-763">CUME_DIST computes the relative position of a specified value in a group of values.</span><span class="sxs-lookup"><span data-stu-id="f017f-763">CUME_DIST computes the relative position of a specified value in a group of values.</span></span> <span data-ttu-id="f017f-764">It calculates the percent of queries that have a latency less than or equal to the current query latency in the same vertical.</span><span class="sxs-lookup"><span data-stu-id="f017f-764">It calculates the percent of queries that have a latency less than or equal to the current query latency in the same vertical.</span></span> <span data-ttu-id="f017f-765">The CUME_DIST for a row R, assuming ascending ordering, is the number of rows with values lower than or equal to the value of R, divided by the number of rows evaluated in the partition.</span><span class="sxs-lookup"><span data-stu-id="f017f-765">The CUME_DIST for a row R, assuming ascending ordering, is the number of rows with values lower than or equal to the value of R, divided by the number of rows evaluated in the partition.</span></span> <span data-ttu-id="f017f-766">CUME_DIST returns numbers in the range 0 < x <= 1.</span><span class="sxs-lookup"><span data-stu-id="f017f-766">CUME_DIST returns numbers in the range 0 < x <= 1.</span></span>

<span data-ttu-id="f017f-767">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="f017f-767">**Syntax:**</span></span>

    CUME_DIST() 
        OVER (
            [PARTITION BY <identifier, > …[n]]
            ORDER BY <identifier, > …[n] [ASC|DESC] 
    ) AS <alias>

<span data-ttu-id="f017f-768">The following example uses the CUME_DIST function to compute the latency percentile for each query within a vertical.</span><span class="sxs-lookup"><span data-stu-id="f017f-768">The following example uses the CUME_DIST function to compute the latency percentile for each query within a vertical.</span></span> 

    @result=
        SELECT 
            *,
            CUME_DIST() OVER(PARTITION BY Vertical ORDER BY Latency) AS CumeDist
        FROM @querylog;

<span data-ttu-id="f017f-769">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-769">The results:</span></span>

| <span data-ttu-id="f017f-770">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-770">Query</span></span> | <span data-ttu-id="f017f-771">Latency</span><span class="sxs-lookup"><span data-stu-id="f017f-771">Latency</span></span> | <span data-ttu-id="f017f-772">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-772">Vertical</span></span> | <span data-ttu-id="f017f-773">CumeDist</span><span class="sxs-lookup"><span data-stu-id="f017f-773">CumeDist</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f017f-774">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-774">Durian</span></span> |<span data-ttu-id="f017f-775">500</span><span class="sxs-lookup"><span data-stu-id="f017f-775">500</span></span> |<span data-ttu-id="f017f-776">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-776">Image</span></span> |<span data-ttu-id="f017f-777">1</span><span class="sxs-lookup"><span data-stu-id="f017f-777">1</span></span> |
| <span data-ttu-id="f017f-778">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-778">Banana</span></span> |<span data-ttu-id="f017f-779">300</span><span class="sxs-lookup"><span data-stu-id="f017f-779">300</span></span> |<span data-ttu-id="f017f-780">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-780">Image</span></span> |<span data-ttu-id="f017f-781">0.666666666666667</span><span class="sxs-lookup"><span data-stu-id="f017f-781">0.666666666666667</span></span> |
| <span data-ttu-id="f017f-782">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-782">Cherry</span></span> |<span data-ttu-id="f017f-783">300</span><span class="sxs-lookup"><span data-stu-id="f017f-783">300</span></span> |<span data-ttu-id="f017f-784">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-784">Image</span></span> |<span data-ttu-id="f017f-785">0.666666666666667</span><span class="sxs-lookup"><span data-stu-id="f017f-785">0.666666666666667</span></span> |
| <span data-ttu-id="f017f-786">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-786">Durian</span></span> |<span data-ttu-id="f017f-787">500</span><span class="sxs-lookup"><span data-stu-id="f017f-787">500</span></span> |<span data-ttu-id="f017f-788">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-788">Web</span></span> |<span data-ttu-id="f017f-789">1</span><span class="sxs-lookup"><span data-stu-id="f017f-789">1</span></span> |
| <span data-ttu-id="f017f-790">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-790">Cherry</span></span> |<span data-ttu-id="f017f-791">400</span><span class="sxs-lookup"><span data-stu-id="f017f-791">400</span></span> |<span data-ttu-id="f017f-792">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-792">Web</span></span> |<span data-ttu-id="f017f-793">0.833333333333333</span><span class="sxs-lookup"><span data-stu-id="f017f-793">0.833333333333333</span></span> |
| <span data-ttu-id="f017f-794">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-794">Fig</span></span> |<span data-ttu-id="f017f-795">300</span><span class="sxs-lookup"><span data-stu-id="f017f-795">300</span></span> |<span data-ttu-id="f017f-796">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-796">Web</span></span> |<span data-ttu-id="f017f-797">0.666666666666667</span><span class="sxs-lookup"><span data-stu-id="f017f-797">0.666666666666667</span></span> |
| <span data-ttu-id="f017f-798">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-798">Fig</span></span> |<span data-ttu-id="f017f-799">200</span><span class="sxs-lookup"><span data-stu-id="f017f-799">200</span></span> |<span data-ttu-id="f017f-800">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-800">Web</span></span> |<span data-ttu-id="f017f-801">0.5</span><span class="sxs-lookup"><span data-stu-id="f017f-801">0.5</span></span> |
| <span data-ttu-id="f017f-802">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-802">Papaya</span></span> |<span data-ttu-id="f017f-803">200</span><span class="sxs-lookup"><span data-stu-id="f017f-803">200</span></span> |<span data-ttu-id="f017f-804">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-804">Web</span></span> |<span data-ttu-id="f017f-805">0.5</span><span class="sxs-lookup"><span data-stu-id="f017f-805">0.5</span></span> |
| <span data-ttu-id="f017f-806">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-806">Apple</span></span> |<span data-ttu-id="f017f-807">100</span><span class="sxs-lookup"><span data-stu-id="f017f-807">100</span></span> |<span data-ttu-id="f017f-808">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-808">Web</span></span> |<span data-ttu-id="f017f-809">0.166666666666667</span><span class="sxs-lookup"><span data-stu-id="f017f-809">0.166666666666667</span></span> |

<span data-ttu-id="f017f-810">There are six rows in the partition where partition key is “Web” (4th row and down):</span><span class="sxs-lookup"><span data-stu-id="f017f-810">There are six rows in the partition where partition key is “Web” (4th row and down):</span></span>

* <span data-ttu-id="f017f-811">There are six rows with the value equal or lower than 500, so the CUME_DIST equals to 6/6=1</span><span class="sxs-lookup"><span data-stu-id="f017f-811">There are six rows with the value equal or lower than 500, so the CUME_DIST equals to 6/6=1</span></span>
* <span data-ttu-id="f017f-812">There are five rows with the value equal or lower than 400, so the CUME_DIST equals to 5/6=0.83</span><span class="sxs-lookup"><span data-stu-id="f017f-812">There are five rows with the value equal or lower than 400, so the CUME_DIST equals to 5/6=0.83</span></span>
* <span data-ttu-id="f017f-813">There are four rows with the value equal or lower than 300, so the CUME_DIST equals to 4/6=0.66</span><span class="sxs-lookup"><span data-stu-id="f017f-813">There are four rows with the value equal or lower than 300, so the CUME_DIST equals to 4/6=0.66</span></span>
* <span data-ttu-id="f017f-814">There are three rows with the value equal or lower than 200, so the CUME_DIST equals to 3/6=0.5.</span><span class="sxs-lookup"><span data-stu-id="f017f-814">There are three rows with the value equal or lower than 200, so the CUME_DIST equals to 3/6=0.5.</span></span> <span data-ttu-id="f017f-815">There are two rows with the same latency value.</span><span class="sxs-lookup"><span data-stu-id="f017f-815">There are two rows with the same latency value.</span></span>
* <span data-ttu-id="f017f-816">There is one row with the value equal or lower than 100, so the CUME_DIST equals to 1/6=0.16.</span><span class="sxs-lookup"><span data-stu-id="f017f-816">There is one row with the value equal or lower than 100, so the CUME_DIST equals to 1/6=0.16.</span></span> 

<span data-ttu-id="f017f-817">**Usage notes:**</span><span class="sxs-lookup"><span data-stu-id="f017f-817">**Usage notes:**</span></span>

* <span data-ttu-id="f017f-818">Tie values always evaluate to the same cumulative distribution value.</span><span class="sxs-lookup"><span data-stu-id="f017f-818">Tie values always evaluate to the same cumulative distribution value.</span></span>
* <span data-ttu-id="f017f-819">NULL values are treated as the lowest possible values.</span><span class="sxs-lookup"><span data-stu-id="f017f-819">NULL values are treated as the lowest possible values.</span></span>
* <span data-ttu-id="f017f-820">An ORDER BY clause is required to calculate CUME_DIST.</span><span class="sxs-lookup"><span data-stu-id="f017f-820">An ORDER BY clause is required to calculate CUME_DIST.</span></span>
* <span data-ttu-id="f017f-821">CUME_DIST is similar to the PERCENT_RANK function</span><span class="sxs-lookup"><span data-stu-id="f017f-821">CUME_DIST is similar to the PERCENT_RANK function</span></span>

<span data-ttu-id="f017f-822">Note: If the SELECT statement is not followed by OUTPUT, the ORDER BY clause is not allowed.</span><span class="sxs-lookup"><span data-stu-id="f017f-822">Note: If the SELECT statement is not followed by OUTPUT, the ORDER BY clause is not allowed.</span></span>

### <a name="percentrank"></a><span data-ttu-id="f017f-823">PERCENT_RANK</span><span class="sxs-lookup"><span data-stu-id="f017f-823">PERCENT_RANK</span></span>
<span data-ttu-id="f017f-824">PERCENT_RANK calculates the relative rank of a row within a group of rows.</span><span class="sxs-lookup"><span data-stu-id="f017f-824">PERCENT_RANK calculates the relative rank of a row within a group of rows.</span></span> <span data-ttu-id="f017f-825">PERCENT_RANK is used to evaluate the relative standing of a value within a rowset or partition.</span><span class="sxs-lookup"><span data-stu-id="f017f-825">PERCENT_RANK is used to evaluate the relative standing of a value within a rowset or partition.</span></span> <span data-ttu-id="f017f-826">The range of values returned by PERCENT_RANK is greater than 0 and less than or equal to 1.</span><span class="sxs-lookup"><span data-stu-id="f017f-826">The range of values returned by PERCENT_RANK is greater than 0 and less than or equal to 1.</span></span> <span data-ttu-id="f017f-827">Unlike CUME_DIST, PERCENT_RANK is always 0 for the first row.</span><span class="sxs-lookup"><span data-stu-id="f017f-827">Unlike CUME_DIST, PERCENT_RANK is always 0 for the first row.</span></span>

<span data-ttu-id="f017f-828">\*\* Syntax:\*\*</span><span class="sxs-lookup"><span data-stu-id="f017f-828">\*\* Syntax:\*\*</span></span>

    PERCENT_RANK() 
        OVER (
            [PARTITION BY <identifier, > …[n]]
            ORDER BY <identifier, > …[n] [ASC|DESC] 
        ) AS <alias>

<span data-ttu-id="f017f-829">**Notes**</span><span class="sxs-lookup"><span data-stu-id="f017f-829">**Notes**</span></span>

* <span data-ttu-id="f017f-830">The first row in any set has a PERCENT_RANK of 0.</span><span class="sxs-lookup"><span data-stu-id="f017f-830">The first row in any set has a PERCENT_RANK of 0.</span></span>
* <span data-ttu-id="f017f-831">NULL values are treated as the lowest possible values.</span><span class="sxs-lookup"><span data-stu-id="f017f-831">NULL values are treated as the lowest possible values.</span></span>
* <span data-ttu-id="f017f-832">PERCENT_RANK requires an ORDER BY clause.</span><span class="sxs-lookup"><span data-stu-id="f017f-832">PERCENT_RANK requires an ORDER BY clause.</span></span>
* <span data-ttu-id="f017f-833">CUME_DIST is similar to the PERCENT_RANK function</span><span class="sxs-lookup"><span data-stu-id="f017f-833">CUME_DIST is similar to the PERCENT_RANK function</span></span> 

<span data-ttu-id="f017f-834">The following example uses the PERCENT_RANK function to compute the latency percentile for each query within a vertical.</span><span class="sxs-lookup"><span data-stu-id="f017f-834">The following example uses the PERCENT_RANK function to compute the latency percentile for each query within a vertical.</span></span> 

<span data-ttu-id="f017f-835">The PARTITION BY clause is specified to partition the rows in the result set by the vertical.</span><span class="sxs-lookup"><span data-stu-id="f017f-835">The PARTITION BY clause is specified to partition the rows in the result set by the vertical.</span></span> <span data-ttu-id="f017f-836">The ORDER BY clause in the OVER clause orders the rows in each partition.</span><span class="sxs-lookup"><span data-stu-id="f017f-836">The ORDER BY clause in the OVER clause orders the rows in each partition.</span></span> 

<span data-ttu-id="f017f-837">The value returned by the PERCENT_RANK function represents the rank of the queries’ latency within a vertical as a percentage.</span><span class="sxs-lookup"><span data-stu-id="f017f-837">The value returned by the PERCENT_RANK function represents the rank of the queries’ latency within a vertical as a percentage.</span></span> 

    @result=
        SELECT 
            *,
            PERCENT_RANK() OVER(PARTITION BY Vertical ORDER BY Latency) AS PercentRank
        FROM @querylog;

<span data-ttu-id="f017f-838">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-838">The results:</span></span>

| <span data-ttu-id="f017f-839">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-839">Query</span></span> | <span data-ttu-id="f017f-840">Latency: INT</span><span class="sxs-lookup"><span data-stu-id="f017f-840">Latency: INT</span></span> | <span data-ttu-id="f017f-841">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-841">Vertical</span></span> | <span data-ttu-id="f017f-842">PercentRank</span><span class="sxs-lookup"><span data-stu-id="f017f-842">PercentRank</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f017f-843">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-843">Banana</span></span> |<span data-ttu-id="f017f-844">300</span><span class="sxs-lookup"><span data-stu-id="f017f-844">300</span></span> |<span data-ttu-id="f017f-845">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-845">Image</span></span> |<span data-ttu-id="f017f-846">0</span><span class="sxs-lookup"><span data-stu-id="f017f-846">0</span></span> |
| <span data-ttu-id="f017f-847">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-847">Cherry</span></span> |<span data-ttu-id="f017f-848">300</span><span class="sxs-lookup"><span data-stu-id="f017f-848">300</span></span> |<span data-ttu-id="f017f-849">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-849">Image</span></span> |<span data-ttu-id="f017f-850">0</span><span class="sxs-lookup"><span data-stu-id="f017f-850">0</span></span> |
| <span data-ttu-id="f017f-851">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-851">Durian</span></span> |<span data-ttu-id="f017f-852">500</span><span class="sxs-lookup"><span data-stu-id="f017f-852">500</span></span> |<span data-ttu-id="f017f-853">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-853">Image</span></span> |<span data-ttu-id="f017f-854">1</span><span class="sxs-lookup"><span data-stu-id="f017f-854">1</span></span> |
| <span data-ttu-id="f017f-855">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-855">Apple</span></span> |<span data-ttu-id="f017f-856">100</span><span class="sxs-lookup"><span data-stu-id="f017f-856">100</span></span> |<span data-ttu-id="f017f-857">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-857">Web</span></span> |<span data-ttu-id="f017f-858">0</span><span class="sxs-lookup"><span data-stu-id="f017f-858">0</span></span> |
| <span data-ttu-id="f017f-859">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-859">Fig</span></span> |<span data-ttu-id="f017f-860">200</span><span class="sxs-lookup"><span data-stu-id="f017f-860">200</span></span> |<span data-ttu-id="f017f-861">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-861">Web</span></span> |<span data-ttu-id="f017f-862">0.2</span><span class="sxs-lookup"><span data-stu-id="f017f-862">0.2</span></span> |
| <span data-ttu-id="f017f-863">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-863">Papaya</span></span> |<span data-ttu-id="f017f-864">200</span><span class="sxs-lookup"><span data-stu-id="f017f-864">200</span></span> |<span data-ttu-id="f017f-865">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-865">Web</span></span> |<span data-ttu-id="f017f-866">0.2</span><span class="sxs-lookup"><span data-stu-id="f017f-866">0.2</span></span> |
| <span data-ttu-id="f017f-867">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-867">Fig</span></span> |<span data-ttu-id="f017f-868">300</span><span class="sxs-lookup"><span data-stu-id="f017f-868">300</span></span> |<span data-ttu-id="f017f-869">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-869">Web</span></span> |<span data-ttu-id="f017f-870">0.6</span><span class="sxs-lookup"><span data-stu-id="f017f-870">0.6</span></span> |
| <span data-ttu-id="f017f-871">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-871">Cherry</span></span> |<span data-ttu-id="f017f-872">400</span><span class="sxs-lookup"><span data-stu-id="f017f-872">400</span></span> |<span data-ttu-id="f017f-873">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-873">Web</span></span> |<span data-ttu-id="f017f-874">0.8</span><span class="sxs-lookup"><span data-stu-id="f017f-874">0.8</span></span> |
| <span data-ttu-id="f017f-875">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-875">Durian</span></span> |<span data-ttu-id="f017f-876">500</span><span class="sxs-lookup"><span data-stu-id="f017f-876">500</span></span> |<span data-ttu-id="f017f-877">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-877">Web</span></span> |<span data-ttu-id="f017f-878">1</span><span class="sxs-lookup"><span data-stu-id="f017f-878">1</span></span> |

### <a name="percentilecont--percentiledisc"></a><span data-ttu-id="f017f-879">PERCENTILE_CONT & PERCENTILE_DISC</span><span class="sxs-lookup"><span data-stu-id="f017f-879">PERCENTILE_CONT & PERCENTILE_DISC</span></span>
<span data-ttu-id="f017f-880">These two functions calculate a percentile based on a continuous or discrete distribution of the column values.</span><span class="sxs-lookup"><span data-stu-id="f017f-880">These two functions calculate a percentile based on a continuous or discrete distribution of the column values.</span></span>

<span data-ttu-id="f017f-881">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="f017f-881">**Syntax:**</span></span>

    [PERCENTILE_CONT | PERCENTILE_DISC] ( numeric_literal ) 
        WITHIN GROUP ( ORDER BY <identifier> [ ASC | DESC ] )
        OVER ( [ PARTITION BY <identifier,>…[n] ] ) AS <alias>

<span data-ttu-id="f017f-882">**numeric_literal** - The percentile to compute.</span><span class="sxs-lookup"><span data-stu-id="f017f-882">**numeric_literal** - The percentile to compute.</span></span> <span data-ttu-id="f017f-883">The value must range between 0.0 and 1.0.</span><span class="sxs-lookup"><span data-stu-id="f017f-883">The value must range between 0.0 and 1.0.</span></span>

<span data-ttu-id="f017f-884">WITHIN GROUP (ORDER BY <identifier> [ ASC | DESC ]) - Specifies a list of numeric values to sort and compute the percentile over.</span><span class="sxs-lookup"><span data-stu-id="f017f-884">WITHIN GROUP (ORDER BY <identifier> [ ASC | DESC ]) - Specifies a list of numeric values to sort and compute the percentile over.</span></span> <span data-ttu-id="f017f-885">Only one column identifier is allowed.</span><span class="sxs-lookup"><span data-stu-id="f017f-885">Only one column identifier is allowed.</span></span> <span data-ttu-id="f017f-886">The expression must evaluate to a numeric type.</span><span class="sxs-lookup"><span data-stu-id="f017f-886">The expression must evaluate to a numeric type.</span></span> <span data-ttu-id="f017f-887">Other data types are not allowed.</span><span class="sxs-lookup"><span data-stu-id="f017f-887">Other data types are not allowed.</span></span> <span data-ttu-id="f017f-888">The default sort order is ascending.</span><span class="sxs-lookup"><span data-stu-id="f017f-888">The default sort order is ascending.</span></span>

<span data-ttu-id="f017f-889">OVER ([ PARTITION BY <identifier,>…[n] ] ) - Divides the input rowset into partitions as per the partition key to which the percentile function is applied.</span><span class="sxs-lookup"><span data-stu-id="f017f-889">OVER ([ PARTITION BY <identifier,>…[n] ] ) - Divides the input rowset into partitions as per the partition key to which the percentile function is applied.</span></span> <span data-ttu-id="f017f-890">For more information, see RANKING section of this document.</span><span class="sxs-lookup"><span data-stu-id="f017f-890">For more information, see RANKING section of this document.</span></span>
<span data-ttu-id="f017f-891">Note: Any nulls in the data set are ignored.</span><span class="sxs-lookup"><span data-stu-id="f017f-891">Note: Any nulls in the data set are ignored.</span></span>

<span data-ttu-id="f017f-892">**PERCENTILE_CONT** calculates a percentile based on a continuous distribution of the column value.</span><span class="sxs-lookup"><span data-stu-id="f017f-892">**PERCENTILE_CONT** calculates a percentile based on a continuous distribution of the column value.</span></span> <span data-ttu-id="f017f-893">The result is interpolated and might not be equal to any of the specific values in the column.</span><span class="sxs-lookup"><span data-stu-id="f017f-893">The result is interpolated and might not be equal to any of the specific values in the column.</span></span> 

<span data-ttu-id="f017f-894">**PERCENTILE_DISC** calculates the percentile based on a discrete distribution of the column values.</span><span class="sxs-lookup"><span data-stu-id="f017f-894">**PERCENTILE_DISC** calculates the percentile based on a discrete distribution of the column values.</span></span> <span data-ttu-id="f017f-895">The result is equal to a specific value in the column.</span><span class="sxs-lookup"><span data-stu-id="f017f-895">The result is equal to a specific value in the column.</span></span> <span data-ttu-id="f017f-896">In other words, PERCENTILE_DISC, in contrast to PERCENTILE_CONT, always returns an actual (original input) value.</span><span class="sxs-lookup"><span data-stu-id="f017f-896">In other words, PERCENTILE_DISC, in contrast to PERCENTILE_CONT, always returns an actual (original input) value.</span></span>

<span data-ttu-id="f017f-897">You can see how both work in the example below which tries to find the median (percentile=0.50) value for Latency within each Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-897">You can see how both work in the example below which tries to find the median (percentile=0.50) value for Latency within each Vertical</span></span>

    @result = 
        SELECT 
            Vertical, 
            Query,
            PERCENTILE_CONT(0.5) 
                WITHIN GROUP (ORDER BY Latency)
                OVER ( PARTITION BY Vertical ) AS PercentileCont50,
            PERCENTILE_DISC(0.5) 
                WITHIN GROUP (ORDER BY Latency) 
                OVER ( PARTITION BY Vertical ) AS PercentileDisc50 

        FROM @querylog;

<span data-ttu-id="f017f-898">The results:</span><span class="sxs-lookup"><span data-stu-id="f017f-898">The results:</span></span>

| <span data-ttu-id="f017f-899">Query</span><span class="sxs-lookup"><span data-stu-id="f017f-899">Query</span></span> | <span data-ttu-id="f017f-900">Latency: INT</span><span class="sxs-lookup"><span data-stu-id="f017f-900">Latency: INT</span></span> | <span data-ttu-id="f017f-901">Vertical</span><span class="sxs-lookup"><span data-stu-id="f017f-901">Vertical</span></span> | <span data-ttu-id="f017f-902">PercentileCont50</span><span class="sxs-lookup"><span data-stu-id="f017f-902">PercentileCont50</span></span> | <span data-ttu-id="f017f-903">PercentilDisc50</span><span class="sxs-lookup"><span data-stu-id="f017f-903">PercentilDisc50</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f017f-904">Banana</span><span class="sxs-lookup"><span data-stu-id="f017f-904">Banana</span></span> |<span data-ttu-id="f017f-905">300</span><span class="sxs-lookup"><span data-stu-id="f017f-905">300</span></span> |<span data-ttu-id="f017f-906">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-906">Image</span></span> |<span data-ttu-id="f017f-907">300</span><span class="sxs-lookup"><span data-stu-id="f017f-907">300</span></span> |<span data-ttu-id="f017f-908">300</span><span class="sxs-lookup"><span data-stu-id="f017f-908">300</span></span> |
| <span data-ttu-id="f017f-909">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-909">Cherry</span></span> |<span data-ttu-id="f017f-910">300</span><span class="sxs-lookup"><span data-stu-id="f017f-910">300</span></span> |<span data-ttu-id="f017f-911">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-911">Image</span></span> |<span data-ttu-id="f017f-912">300</span><span class="sxs-lookup"><span data-stu-id="f017f-912">300</span></span> |<span data-ttu-id="f017f-913">300</span><span class="sxs-lookup"><span data-stu-id="f017f-913">300</span></span> |
| <span data-ttu-id="f017f-914">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-914">Durian</span></span> |<span data-ttu-id="f017f-915">500</span><span class="sxs-lookup"><span data-stu-id="f017f-915">500</span></span> |<span data-ttu-id="f017f-916">Image</span><span class="sxs-lookup"><span data-stu-id="f017f-916">Image</span></span> |<span data-ttu-id="f017f-917">300</span><span class="sxs-lookup"><span data-stu-id="f017f-917">300</span></span> |<span data-ttu-id="f017f-918">300</span><span class="sxs-lookup"><span data-stu-id="f017f-918">300</span></span> |
| <span data-ttu-id="f017f-919">Apple</span><span class="sxs-lookup"><span data-stu-id="f017f-919">Apple</span></span> |<span data-ttu-id="f017f-920">100</span><span class="sxs-lookup"><span data-stu-id="f017f-920">100</span></span> |<span data-ttu-id="f017f-921">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-921">Web</span></span> |<span data-ttu-id="f017f-922">250</span><span class="sxs-lookup"><span data-stu-id="f017f-922">250</span></span> |<span data-ttu-id="f017f-923">200</span><span class="sxs-lookup"><span data-stu-id="f017f-923">200</span></span> |
| <span data-ttu-id="f017f-924">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-924">Fig</span></span> |<span data-ttu-id="f017f-925">200</span><span class="sxs-lookup"><span data-stu-id="f017f-925">200</span></span> |<span data-ttu-id="f017f-926">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-926">Web</span></span> |<span data-ttu-id="f017f-927">250</span><span class="sxs-lookup"><span data-stu-id="f017f-927">250</span></span> |<span data-ttu-id="f017f-928">200</span><span class="sxs-lookup"><span data-stu-id="f017f-928">200</span></span> |
| <span data-ttu-id="f017f-929">Papaya</span><span class="sxs-lookup"><span data-stu-id="f017f-929">Papaya</span></span> |<span data-ttu-id="f017f-930">200</span><span class="sxs-lookup"><span data-stu-id="f017f-930">200</span></span> |<span data-ttu-id="f017f-931">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-931">Web</span></span> |<span data-ttu-id="f017f-932">250</span><span class="sxs-lookup"><span data-stu-id="f017f-932">250</span></span> |<span data-ttu-id="f017f-933">200</span><span class="sxs-lookup"><span data-stu-id="f017f-933">200</span></span> |
| <span data-ttu-id="f017f-934">Fig</span><span class="sxs-lookup"><span data-stu-id="f017f-934">Fig</span></span> |<span data-ttu-id="f017f-935">300</span><span class="sxs-lookup"><span data-stu-id="f017f-935">300</span></span> |<span data-ttu-id="f017f-936">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-936">Web</span></span> |<span data-ttu-id="f017f-937">250</span><span class="sxs-lookup"><span data-stu-id="f017f-937">250</span></span> |<span data-ttu-id="f017f-938">200</span><span class="sxs-lookup"><span data-stu-id="f017f-938">200</span></span> |
| <span data-ttu-id="f017f-939">Cherry</span><span class="sxs-lookup"><span data-stu-id="f017f-939">Cherry</span></span> |<span data-ttu-id="f017f-940">400</span><span class="sxs-lookup"><span data-stu-id="f017f-940">400</span></span> |<span data-ttu-id="f017f-941">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-941">Web</span></span> |<span data-ttu-id="f017f-942">250</span><span class="sxs-lookup"><span data-stu-id="f017f-942">250</span></span> |<span data-ttu-id="f017f-943">200</span><span class="sxs-lookup"><span data-stu-id="f017f-943">200</span></span> |
| <span data-ttu-id="f017f-944">Durian</span><span class="sxs-lookup"><span data-stu-id="f017f-944">Durian</span></span> |<span data-ttu-id="f017f-945">500</span><span class="sxs-lookup"><span data-stu-id="f017f-945">500</span></span> |<span data-ttu-id="f017f-946">Web</span><span class="sxs-lookup"><span data-stu-id="f017f-946">Web</span></span> |<span data-ttu-id="f017f-947">250</span><span class="sxs-lookup"><span data-stu-id="f017f-947">250</span></span> |<span data-ttu-id="f017f-948">200</span><span class="sxs-lookup"><span data-stu-id="f017f-948">200</span></span> |

<span data-ttu-id="f017f-949">For PERCENTILE_CONT because values can be interpolated, the median for web is 250 even though no query in the web vertical had a latency of 250.</span><span class="sxs-lookup"><span data-stu-id="f017f-949">For PERCENTILE_CONT because values can be interpolated, the median for web is 250 even though no query in the web vertical had a latency of 250.</span></span> 

<span data-ttu-id="f017f-950">PERCENTILE_DISC does not interpolate values, so the median for Web is 200 - which is an actual value found in the input rows.</span><span class="sxs-lookup"><span data-stu-id="f017f-950">PERCENTILE_DISC does not interpolate values, so the median for Web is 200 - which is an actual value found in the input rows.</span></span>

## <a name="see-also"></a><span data-ttu-id="f017f-951">See also</span><span class="sxs-lookup"><span data-stu-id="f017f-951">See also</span></span>
* [<span data-ttu-id="f017f-952">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f017f-952">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="f017f-953">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="f017f-953">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="f017f-954">Get started with Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f017f-954">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="f017f-955">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f017f-955">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="f017f-956">Use Azure Data Lake Analytics interactive tutorials</span><span class="sxs-lookup"><span data-stu-id="f017f-956">Use Azure Data Lake Analytics interactive tutorials</span></span>](data-lake-analytics-use-interactive-tutorials.md)
* [<span data-ttu-id="f017f-957">Analyze Website logs using Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f017f-957">Analyze Website logs using Azure Data Lake Analytics</span></span>](data-lake-analytics-analyze-weblogs.md)
* [<span data-ttu-id="f017f-958">Get started with Azure Data Lake Analytics U-SQL language</span><span class="sxs-lookup"><span data-stu-id="f017f-958">Get started with Azure Data Lake Analytics U-SQL language</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="f017f-959">Manage Azure Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="f017f-959">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="f017f-960">Manage Azure Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f017f-960">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="f017f-961">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="f017f-961">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)




