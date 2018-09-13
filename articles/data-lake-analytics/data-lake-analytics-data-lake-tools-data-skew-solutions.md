---
title: Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio | Microsoft Docs
description: Troubleshooting potential solutions for data-skew problems by using Azure Data Lake Tools for Visual Studio.
services: data-lake-analytics
documentationcenter: ''
author: yanancai
manager: ''
editor: ''
ms.assetid: ''
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 43da16c98bd00e8a07ae96f35011f83c09227fa7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660555"
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d102f-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d102f-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="d102f-104">What is data skew?</span><span class="sxs-lookup"><span data-stu-id="d102f-104">What is data skew?</span></span>

<span data-ttu-id="d102f-105">Briefly stated, data skew is an over-represented value.</span><span class="sxs-lookup"><span data-stu-id="d102f-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="d102f-106">Imagine that you have assigned 50 tax examiners to audit tax returns, one examiner for each US state.</span><span class="sxs-lookup"><span data-stu-id="d102f-106">Imagine that you have assigned 50 tax examiners to audit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="d102f-107">The Wyoming examiner, because the population there is small, has little to do.</span><span class="sxs-lookup"><span data-stu-id="d102f-107">The Wyoming examiner, because the population there is small, has little to do.</span></span> <span data-ttu-id="d102f-108">In California, however, the examiner is kept very busy because of the state's large population.</span><span class="sxs-lookup"><span data-stu-id="d102f-108">In California, however, the examiner is kept very busy because of the state's large population.</span></span>
    <span data-ttu-id="d102f-109">![Data-skew problem example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="d102f-109">![Data-skew problem example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="d102f-110">In our scenario, the data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span><span class="sxs-lookup"><span data-stu-id="d102f-110">In our scenario, the data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="d102f-111">In your own job, you frequently experience situations like the tax-examiner example here.</span><span class="sxs-lookup"><span data-stu-id="d102f-111">In your own job, you frequently experience situations like the tax-examiner example here.</span></span> <span data-ttu-id="d102f-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes the vertex work more than the others and that eventually slows down an entire job.</span><span class="sxs-lookup"><span data-stu-id="d102f-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes the vertex work more than the others and that eventually slows down an entire job.</span></span> <span data-ttu-id="d102f-113">What's worse, the job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span><span class="sxs-lookup"><span data-stu-id="d102f-113">What's worse, the job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="d102f-114">Resolving data-skew problems</span><span class="sxs-lookup"><span data-stu-id="d102f-114">Resolving data-skew problems</span></span>

<span data-ttu-id="d102f-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span><span class="sxs-lookup"><span data-stu-id="d102f-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="d102f-116">If a problem exists, you can resolve it by trying the solutions in this section.</span><span class="sxs-lookup"><span data-stu-id="d102f-116">If a problem exists, you can resolve it by trying the solutions in this section.</span></span>

### <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="d102f-117">Solution 1: Improve table partitioning</span><span class="sxs-lookup"><span data-stu-id="d102f-117">Solution 1: Improve table partitioning</span></span>

#### <a name="option-1-filter-the-skewed-key-value-in-advance"></a><span data-ttu-id="d102f-118">Option 1: Filter the skewed key value in advance</span><span class="sxs-lookup"><span data-stu-id="d102f-118">Option 1: Filter the skewed key value in advance</span></span>

<span data-ttu-id="d102f-119">If it does not affect your business logic, you can filter the higher-frequency values in advance.</span><span class="sxs-lookup"><span data-stu-id="d102f-119">If it does not affect your business logic, you can filter the higher-frequency values in advance.</span></span> <span data-ttu-id="d102f-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want to aggregate that value.</span><span class="sxs-lookup"><span data-stu-id="d102f-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want to aggregate that value.</span></span> <span data-ttu-id="d102f-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” to filter the high-frequency value.</span><span class="sxs-lookup"><span data-stu-id="d102f-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” to filter the high-frequency value.</span></span>

#### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="d102f-122">Option 2: Pick a different partition or distribution key</span><span class="sxs-lookup"><span data-stu-id="d102f-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="d102f-123">In the preceding example, if you want only to check the tax-audit workload all over the country, you can improve the data distribution by selecting the ID number as your key.</span><span class="sxs-lookup"><span data-stu-id="d102f-123">In the preceding example, if you want only to check the tax-audit workload all over the country, you can improve the data distribution by selecting the ID number as your key.</span></span> <span data-ttu-id="d102f-124">Picking a different partition or distribution key can sometimes distribute the data more evenly, but you need to make sure that this choice doesn’t affect your business logic.</span><span class="sxs-lookup"><span data-stu-id="d102f-124">Picking a different partition or distribution key can sometimes distribute the data more evenly, but you need to make sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="d102f-125">For instance, to calculate the tax sum for each state, you might want to designate _State_ as the partition key.</span><span class="sxs-lookup"><span data-stu-id="d102f-125">For instance, to calculate the tax sum for each state, you might want to designate _State_ as the partition key.</span></span> <span data-ttu-id="d102f-126">If you continue to experience this problem, try using Option 3.</span><span class="sxs-lookup"><span data-stu-id="d102f-126">If you continue to experience this problem, try using Option 3.</span></span>

#### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="d102f-127">Option 3: Add more partition or distribution keys</span><span class="sxs-lookup"><span data-stu-id="d102f-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="d102f-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span><span class="sxs-lookup"><span data-stu-id="d102f-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="d102f-129">For example, consider adding _ZIP Code_ as an additional partition key to reduce data-partition sizes and distribute the data more evenly.</span><span class="sxs-lookup"><span data-stu-id="d102f-129">For example, consider adding _ZIP Code_ as an additional partition key to reduce data-partition sizes and distribute the data more evenly.</span></span>

#### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="d102f-130">Option 4: Use round-robin distribution</span><span class="sxs-lookup"><span data-stu-id="d102f-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="d102f-131">If you cannot find an appropriate key for partition and distribution, you can try to use round-robin distribution.</span><span class="sxs-lookup"><span data-stu-id="d102f-131">If you cannot find an appropriate key for partition and distribution, you can try to use round-robin distribution.</span></span> <span data-ttu-id="d102f-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span><span class="sxs-lookup"><span data-stu-id="d102f-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="d102f-133">The data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span><span class="sxs-lookup"><span data-stu-id="d102f-133">The data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="d102f-134">Additionally, if you are doing aggregation for the skewed key anyway, the data-skew problem will persist.</span><span class="sxs-lookup"><span data-stu-id="d102f-134">Additionally, if you are doing aggregation for the skewed key anyway, the data-skew problem will persist.</span></span> <span data-ttu-id="d102f-135">To learn more about round-robin distribution, see the U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="d102f-135">To learn more about round-robin distribution, see the U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

### <a name="solution-2-improve-the-query-plan"></a><span data-ttu-id="d102f-136">Solution 2: Improve the query plan</span><span class="sxs-lookup"><span data-stu-id="d102f-136">Solution 2: Improve the query plan</span></span>

#### <a name="option-1-use-the-create-statistics-statement"></a><span data-ttu-id="d102f-137">Option 1: Use the CREATE STATISTICS statement</span><span class="sxs-lookup"><span data-stu-id="d102f-137">Option 1: Use the CREATE STATISTICS statement</span></span>

<span data-ttu-id="d102f-138">U-SQL provides the CREATE STATISTICS statement on tables.</span><span class="sxs-lookup"><span data-stu-id="d102f-138">U-SQL provides the CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="d102f-139">This statement gives more information to the query optimizer about the data characteristics, such as value distribution, that are stored in a table.</span><span class="sxs-lookup"><span data-stu-id="d102f-139">This statement gives more information to the query optimizer about the data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="d102f-140">For most queries, the query optimizer already generates the necessary statistics for a high-quality query plan.</span><span class="sxs-lookup"><span data-stu-id="d102f-140">For most queries, the query optimizer already generates the necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="d102f-141">Occasionally, you might need to improve query performance by creating additional statistics with CREATE STATISTICS or by modifying the query design.</span><span class="sxs-lookup"><span data-stu-id="d102f-141">Occasionally, you might need to improve query performance by creating additional statistics with CREATE STATISTICS or by modifying the query design.</span></span> <span data-ttu-id="d102f-142">For more information, see the [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="d102f-142">For more information, see the [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="d102f-143">Code example:</span><span class="sxs-lookup"><span data-stu-id="d102f-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="d102f-144">Statistics information is not updated automatically.</span><span class="sxs-lookup"><span data-stu-id="d102f-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="d102f-145">If you update the data in a table without re-creating the statistics, the query performance might decline.</span><span class="sxs-lookup"><span data-stu-id="d102f-145">If you update the data in a table without re-creating the statistics, the query performance might decline.</span></span>

#### <a name="option-2-use-skewfactor"></a><span data-ttu-id="d102f-146">Option 2: Use SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="d102f-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="d102f-147">If you want to sum the tax for each state, you must use GROUP BY state, an approach that doesn't avoid the data-skew problem.</span><span class="sxs-lookup"><span data-stu-id="d102f-147">If you want to sum the tax for each state, you must use GROUP BY state, an approach that doesn't avoid the data-skew problem.</span></span> <span data-ttu-id="d102f-148">However, you can provide a data hint in your query to identify data skew in keys so that the optimizer can prepare an execution plan for you.</span><span class="sxs-lookup"><span data-stu-id="d102f-148">However, you can provide a data hint in your query to identify data skew in keys so that the optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="d102f-149">Usually, you can set the parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span><span class="sxs-lookup"><span data-stu-id="d102f-149">Usually, you can set the parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="d102f-150">Because the hint affects execution-plan optimization for the current statement and all downstream statements, be sure to add the hint before the potential skewed key-wise aggregation.</span><span class="sxs-lookup"><span data-stu-id="d102f-150">Because the hint affects execution-plan optimization for the current statement and all downstream statements, be sure to add the hint before the potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that the given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="d102f-151">Code example:</span><span class="sxs-lookup"><span data-stu-id="d102f-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

<span data-ttu-id="d102f-152">In addition to SKEWFACTOR, for specific skewed-key join cases, if you know that the other joined row set is small, you can tell the optimizer by adding a ROWCOUNT hint in the U-SQL statement before JOIN.</span><span class="sxs-lookup"><span data-stu-id="d102f-152">In addition to SKEWFACTOR, for specific skewed-key join cases, if you know that the other joined row set is small, you can tell the optimizer by adding a ROWCOUNT hint in the U-SQL statement before JOIN.</span></span> <span data-ttu-id="d102f-153">This way, optimizer can choose a broadcast join strategy to help improve performance.</span><span class="sxs-lookup"><span data-stu-id="d102f-153">This way, optimizer can choose a broadcast join strategy to help improve performance.</span></span> <span data-ttu-id="d102f-154">Be aware that ROWCOUNT does not resolve the data-skew problem, but it can offer some additional help.</span><span class="sxs-lookup"><span data-stu-id="d102f-154">Be aware that ROWCOUNT does not resolve the data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="d102f-155">Code example:</span><span class="sxs-lookup"><span data-stu-id="d102f-155">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information to determine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

### <a name="solution-3-improve-the-user-defined-reducer-and-combiner"></a><span data-ttu-id="d102f-156">Solution 3: Improve the user-defined reducer and combiner</span><span class="sxs-lookup"><span data-stu-id="d102f-156">Solution 3: Improve the user-defined reducer and combiner</span></span>

<span data-ttu-id="d102f-157">You can sometimes write a user-defined operator to deal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span><span class="sxs-lookup"><span data-stu-id="d102f-157">You can sometimes write a user-defined operator to deal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

#### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="d102f-158">Option 1: Use a recursive reducer, if possible</span><span class="sxs-lookup"><span data-stu-id="d102f-158">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="d102f-159">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span><span class="sxs-lookup"><span data-stu-id="d102f-159">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="d102f-160">But if your data is skewed, the huge data sets might be processed in a single vertex and run for a long time.</span><span class="sxs-lookup"><span data-stu-id="d102f-160">But if your data is skewed, the huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="d102f-161">To improve performance, you can add an attribute in your code to define reducer to run in recursive mode.</span><span class="sxs-lookup"><span data-stu-id="d102f-161">To improve performance, you can add an attribute in your code to define reducer to run in recursive mode.</span></span> <span data-ttu-id="d102f-162">Then, the huge data sets can be distributed to multiple vertices and run in parallel, which speeds up your job.</span><span class="sxs-lookup"><span data-stu-id="d102f-162">Then, the huge data sets can be distributed to multiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="d102f-163">To change a non-recursive reducer to recursive, you need to make sure that your algorithm is associative.</span><span class="sxs-lookup"><span data-stu-id="d102f-163">To change a non-recursive reducer to recursive, you need to make sure that your algorithm is associative.</span></span> <span data-ttu-id="d102f-164">For example, the sum is associative, and the median is not.</span><span class="sxs-lookup"><span data-stu-id="d102f-164">For example, the sum is associative, and the median is not.</span></span> <span data-ttu-id="d102f-165">You also need to make sure that the input and output for reducer keep the same schema.</span><span class="sxs-lookup"><span data-stu-id="d102f-165">You also need to make sure that the input and output for reducer keep the same schema.</span></span>

<span data-ttu-id="d102f-166">Attribute of recursive reducer:</span><span class="sxs-lookup"><span data-stu-id="d102f-166">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="d102f-167">Code example:</span><span class="sxs-lookup"><span data-stu-id="d102f-167">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

#### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="d102f-168">Option 2: Use row-level combiner mode, if possible</span><span class="sxs-lookup"><span data-stu-id="d102f-168">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="d102f-169">Similar to the ROWCOUNT hint for specific skewed-key join cases, combiner mode tries to distribute huge skewed-key value sets to multiple vertices so that the work can be executed concurrently.</span><span class="sxs-lookup"><span data-stu-id="d102f-169">Similar to the ROWCOUNT hint for specific skewed-key join cases, combiner mode tries to distribute huge skewed-key value sets to multiple vertices so that the work can be executed concurrently.</span></span> <span data-ttu-id="d102f-170">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span><span class="sxs-lookup"><span data-stu-id="d102f-170">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="d102f-171">By default, the combiner mode is Full, which means that the left row set and right row set cannot be separated.</span><span class="sxs-lookup"><span data-stu-id="d102f-171">By default, the combiner mode is Full, which means that the left row set and right row set cannot be separated.</span></span> <span data-ttu-id="d102f-172">Setting the mode as Left/Right/Inner enables row-level join.</span><span class="sxs-lookup"><span data-stu-id="d102f-172">Setting the mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="d102f-173">The system separates the corresponding row sets and distributes them into multiple vertices that run in parallel.</span><span class="sxs-lookup"><span data-stu-id="d102f-173">The system separates the corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="d102f-174">However, before you configure the combiner mode, be careful to ensure that the corresponding row sets can be separated.</span><span class="sxs-lookup"><span data-stu-id="d102f-174">However, before you configure the combiner mode, be careful to ensure that the corresponding row sets can be separated.</span></span>

<span data-ttu-id="d102f-175">The example that follows shows a separated left row set.</span><span class="sxs-lookup"><span data-stu-id="d102f-175">The example that follows shows a separated left row set.</span></span> <span data-ttu-id="d102f-176">Each output row depends on a single input row from the left, and it potentially depends on all rows from the right with the same key value.</span><span class="sxs-lookup"><span data-stu-id="d102f-176">Each output row depends on a single input row from the left, and it potentially depends on all rows from the right with the same key value.</span></span> <span data-ttu-id="d102f-177">If you set the combiner mode as left, the system separates the huge left-row set into small ones and assigns them to multiple vertices.</span><span class="sxs-lookup"><span data-stu-id="d102f-177">If you set the combiner mode as left, the system separates the huge left-row set into small ones and assigns them to multiple vertices.</span></span>

![Combiner mode illustration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="d102f-179">If you set the wrong combiner mode, the combination is less efficient, and the results might be wrong.</span><span class="sxs-lookup"><span data-stu-id="d102f-179">If you set the wrong combiner mode, the combination is less efficient, and the results might be wrong.</span></span>

<span data-ttu-id="d102f-180">Attributes of combiner mode:</span><span class="sxs-lookup"><span data-stu-id="d102f-180">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all the input rows from left and right with the same key value.

- <span data-ttu-id="d102f-181">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from the left (and potentially all rows from the right with the same key value).</span><span class="sxs-lookup"><span data-stu-id="d102f-181">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from the left (and potentially all rows from the right with the same key value).</span></span>

- <span data-ttu-id="d102f-182">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from the right (and potentially all rows from the left with the same key value).</span><span class="sxs-lookup"><span data-stu-id="d102f-182">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from the right (and potentially all rows from the left with the same key value).</span></span>

- <span data-ttu-id="d102f-183">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from the left and the right with the same value.</span><span class="sxs-lookup"><span data-stu-id="d102f-183">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from the left and the right with the same value.</span></span>

<span data-ttu-id="d102f-184">Code example:</span><span class="sxs-lookup"><span data-stu-id="d102f-184">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }


