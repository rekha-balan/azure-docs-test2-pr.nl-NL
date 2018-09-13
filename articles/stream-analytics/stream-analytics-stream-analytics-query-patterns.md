---
title: Query examples for common usage patterns in Stream Analytics | Microsoft Docs
description: 'Common Azure Stream Analytics Query Patterns '
keywords: query examples
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: c181af409a1e9dd72c541e9831c354a7ca57103e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555643"
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="af1b1-104">Query examples for common Stream Analytics usage patterns</span><span class="sxs-lookup"><span data-stu-id="af1b1-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="af1b1-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="af1b1-105">Introduction</span></span>
<span data-ttu-id="af1b1-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language, which is documented in the [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span><span class="sxs-lookup"><span data-stu-id="af1b1-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language, which is documented in the [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span>  <span data-ttu-id="af1b1-107">This article outlines solutions to several common query patterns based on real world scenarios.</span><span class="sxs-lookup"><span data-stu-id="af1b1-107">This article outlines solutions to several common query patterns based on real world scenarios.</span></span>  <span data-ttu-id="af1b1-108">It is a work in progress and will continue to be updated with new patterns on an ongoing basis.</span><span class="sxs-lookup"><span data-stu-id="af1b1-108">It is a work in progress and will continue to be updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-data-type-conversions"></a><span data-ttu-id="af1b1-109">Query example: Data type conversions</span><span class="sxs-lookup"><span data-stu-id="af1b1-109">Query example: Data type conversions</span></span>
<span data-ttu-id="af1b1-110">**Description**: Define the types of the properties on the input stream.</span><span class="sxs-lookup"><span data-stu-id="af1b1-110">**Description**: Define the types of the properties on the input stream.</span></span>
<span data-ttu-id="af1b1-111">For example, car weight is coming on the input stream as strings and needs to be converted to INT to perform SUM it up.</span><span class="sxs-lookup"><span data-stu-id="af1b1-111">For example, car weight is coming on the input stream as strings and needs to be converted to INT to perform SUM it up.</span></span>

<span data-ttu-id="af1b1-112">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-112">**Input**:</span></span>

| <span data-ttu-id="af1b1-113">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-113">Make</span></span> | <span data-ttu-id="af1b1-114">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-114">Time</span></span> | <span data-ttu-id="af1b1-115">Weight</span><span class="sxs-lookup"><span data-stu-id="af1b1-115">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-116">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-116">Honda</span></span> |<span data-ttu-id="af1b1-117">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-117">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="af1b1-118">"1000"</span><span class="sxs-lookup"><span data-stu-id="af1b1-118">"1000"</span></span> |
| <span data-ttu-id="af1b1-119">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-119">Honda</span></span> |<span data-ttu-id="af1b1-120">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-120">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="af1b1-121">"2000"</span><span class="sxs-lookup"><span data-stu-id="af1b1-121">"2000"</span></span> |

<span data-ttu-id="af1b1-122">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-122">**Output**:</span></span>

| <span data-ttu-id="af1b1-123">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-123">Make</span></span> | <span data-ttu-id="af1b1-124">Weight</span><span class="sxs-lookup"><span data-stu-id="af1b1-124">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-125">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-125">Honda</span></span> |<span data-ttu-id="af1b1-126">3000</span><span class="sxs-lookup"><span data-stu-id="af1b1-126">3000</span></span> |

<span data-ttu-id="af1b1-127">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-127">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="af1b1-128">**Explanation**: Use a CAST statement on the Weight field to specify its type (see the list of supported Data Types [here](https://msdn.microsoft.com/library/azure/dn835065.aspx)).</span><span class="sxs-lookup"><span data-stu-id="af1b1-128">**Explanation**: Use a CAST statement on the Weight field to specify its type (see the list of supported Data Types [here](https://msdn.microsoft.com/library/azure/dn835065.aspx)).</span></span>

## <a name="query-example-using-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="af1b1-129">Query example: Using Like/Not like to do pattern matching</span><span class="sxs-lookup"><span data-stu-id="af1b1-129">Query example: Using Like/Not like to do pattern matching</span></span>
<span data-ttu-id="af1b1-130">**Description**: Check that a field value on the event matches a certain pattern For example, return license plates that start with A and end with 9</span><span class="sxs-lookup"><span data-stu-id="af1b1-130">**Description**: Check that a field value on the event matches a certain pattern For example, return license plates that start with A and end with 9</span></span>

<span data-ttu-id="af1b1-131">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-131">**Input**:</span></span>

| <span data-ttu-id="af1b1-132">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-132">Make</span></span> | <span data-ttu-id="af1b1-133">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-133">LicensePlate</span></span> | <span data-ttu-id="af1b1-134">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-134">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-135">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-135">Honda</span></span> |<span data-ttu-id="af1b1-136">ABC-123</span><span class="sxs-lookup"><span data-stu-id="af1b1-136">ABC-123</span></span> |<span data-ttu-id="af1b1-137">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-137">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-138">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-138">Toyota</span></span> |<span data-ttu-id="af1b1-139">AAA-999</span><span class="sxs-lookup"><span data-stu-id="af1b1-139">AAA-999</span></span> |<span data-ttu-id="af1b1-140">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-140">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-141">Nissan</span><span class="sxs-lookup"><span data-stu-id="af1b1-141">Nissan</span></span> |<span data-ttu-id="af1b1-142">ABC-369</span><span class="sxs-lookup"><span data-stu-id="af1b1-142">ABC-369</span></span> |<span data-ttu-id="af1b1-143">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-143">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="af1b1-144">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-144">**Output**:</span></span>

| <span data-ttu-id="af1b1-145">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-145">Make</span></span> | <span data-ttu-id="af1b1-146">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-146">LicensePlate</span></span> | <span data-ttu-id="af1b1-147">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-147">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-148">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-148">Toyota</span></span> |<span data-ttu-id="af1b1-149">AAA-999</span><span class="sxs-lookup"><span data-stu-id="af1b1-149">AAA-999</span></span> |<span data-ttu-id="af1b1-150">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-150">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-151">Nissan</span><span class="sxs-lookup"><span data-stu-id="af1b1-151">Nissan</span></span> |<span data-ttu-id="af1b1-152">ABC-369</span><span class="sxs-lookup"><span data-stu-id="af1b1-152">ABC-369</span></span> |<span data-ttu-id="af1b1-153">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-153">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="af1b1-154">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-154">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="af1b1-155">**Explanation**: Use the LIKE statement to check that the LicensePlate field value starts with A then has any string of zero or more characters and it ends with 9.</span><span class="sxs-lookup"><span data-stu-id="af1b1-155">**Explanation**: Use the LIKE statement to check that the LicensePlate field value starts with A then has any string of zero or more characters and it ends with 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="af1b1-156">Query example: Specify logic for different cases/values (CASE statements)</span><span class="sxs-lookup"><span data-stu-id="af1b1-156">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="af1b1-157">**Description**: Provide different computation for a field based on some criteria.</span><span class="sxs-lookup"><span data-stu-id="af1b1-157">**Description**: Provide different computation for a field based on some criteria.</span></span>
<span data-ttu-id="af1b1-158">For example, provide a string description for how many cars passed of the same make with a special case for 1.</span><span class="sxs-lookup"><span data-stu-id="af1b1-158">For example, provide a string description for how many cars passed of the same make with a special case for 1.</span></span>

<span data-ttu-id="af1b1-159">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-159">**Input**:</span></span>

| <span data-ttu-id="af1b1-160">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-160">Make</span></span> | <span data-ttu-id="af1b1-161">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-161">Time</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-162">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-162">Honda</span></span> |<span data-ttu-id="af1b1-163">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-163">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-164">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-164">Toyota</span></span> |<span data-ttu-id="af1b1-165">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-165">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-166">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-166">Toyota</span></span> |<span data-ttu-id="af1b1-167">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-167">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="af1b1-168">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-168">**Output**:</span></span>

| <span data-ttu-id="af1b1-169">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="af1b1-169">CarsPassed</span></span> | <span data-ttu-id="af1b1-170">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-170">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-171">1 Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-171">1 Honda</span></span> |<span data-ttu-id="af1b1-172">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-172">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="af1b1-173">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="af1b1-173">2 Toyotas</span></span> |<span data-ttu-id="af1b1-174">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-174">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="af1b1-175">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-175">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="af1b1-176">**Explanation**: The CASE clause allows us to provide a different computation based on some criteria (in our case the count of cars in the aggregate window).</span><span class="sxs-lookup"><span data-stu-id="af1b1-176">**Explanation**: The CASE clause allows us to provide a different computation based on some criteria (in our case the count of cars in the aggregate window).</span></span>

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="af1b1-177">Query example: Send data to multiple outputs</span><span class="sxs-lookup"><span data-stu-id="af1b1-177">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="af1b1-178">**Description**: Send data to multiple output targets from a single job.</span><span class="sxs-lookup"><span data-stu-id="af1b1-178">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="af1b1-179">For example, analyze data for a threshold-based alert and archive all events to blob storage</span><span class="sxs-lookup"><span data-stu-id="af1b1-179">For example, analyze data for a threshold-based alert and archive all events to blob storage</span></span>

<span data-ttu-id="af1b1-180">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-180">**Input**:</span></span>

| <span data-ttu-id="af1b1-181">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-181">Make</span></span> | <span data-ttu-id="af1b1-182">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-182">Time</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-183">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-183">Honda</span></span> |<span data-ttu-id="af1b1-184">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-184">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-185">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-185">Honda</span></span> |<span data-ttu-id="af1b1-186">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-186">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-187">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-187">Toyota</span></span> |<span data-ttu-id="af1b1-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-189">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-189">Toyota</span></span> |<span data-ttu-id="af1b1-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-191">Toyota</span></span> |<span data-ttu-id="af1b1-192">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-192">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="af1b1-193">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-193">**Output1**:</span></span>

| <span data-ttu-id="af1b1-194">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-194">Make</span></span> | <span data-ttu-id="af1b1-195">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-195">Time</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-196">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-196">Honda</span></span> |<span data-ttu-id="af1b1-197">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-197">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-198">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-198">Honda</span></span> |<span data-ttu-id="af1b1-199">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-199">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-200">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-200">Toyota</span></span> |<span data-ttu-id="af1b1-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-202">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-202">Toyota</span></span> |<span data-ttu-id="af1b1-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-204">Toyota</span></span> |<span data-ttu-id="af1b1-205">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-205">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="af1b1-206">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-206">**Output2**:</span></span>

| <span data-ttu-id="af1b1-207">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-207">Make</span></span> | <span data-ttu-id="af1b1-208">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-208">Time</span></span> | <span data-ttu-id="af1b1-209">Count</span><span class="sxs-lookup"><span data-stu-id="af1b1-209">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-210">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-210">Toyota</span></span> |<span data-ttu-id="af1b1-211">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-211">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="af1b1-212">3</span><span class="sxs-lookup"><span data-stu-id="af1b1-212">3</span></span> |

<span data-ttu-id="af1b1-213">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-213">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="af1b1-214">**Explanation**: The INTO clause tells Stream Analytics which of the outputs to write the data from this statement.</span><span class="sxs-lookup"><span data-stu-id="af1b1-214">**Explanation**: The INTO clause tells Stream Analytics which of the outputs to write the data from this statement.</span></span>
<span data-ttu-id="af1b1-215">The first query is a pass-through of the data we received to an output that we named ArchiveOutput.</span><span class="sxs-lookup"><span data-stu-id="af1b1-215">The first query is a pass-through of the data we received to an output that we named ArchiveOutput.</span></span>
<span data-ttu-id="af1b1-216">The second query does some simple aggregation and filtering and sends the results to a downstream alerting system.</span><span class="sxs-lookup"><span data-stu-id="af1b1-216">The second query does some simple aggregation and filtering and sends the results to a downstream alerting system.</span></span>
<span data-ttu-id="af1b1-217">*Note*: You can also reuse results of CTEs (i.e. WITH statements) in multiple output statements – this has the added benefit of opening fewer readers to the input source.</span><span class="sxs-lookup"><span data-stu-id="af1b1-217">*Note*: You can also reuse results of CTEs (i.e. WITH statements) in multiple output statements – this has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="af1b1-218">For example,</span><span class="sxs-lookup"><span data-stu-id="af1b1-218">For example,</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-counting-unique-values"></a><span data-ttu-id="af1b1-219">Query example: Counting unique values</span><span class="sxs-lookup"><span data-stu-id="af1b1-219">Query example: Counting unique values</span></span>
<span data-ttu-id="af1b1-220">**Description**: count the number of unique field values that appear in the stream within a time window.</span><span class="sxs-lookup"><span data-stu-id="af1b1-220">**Description**: count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="af1b1-221">For example, how many unique make of cars passed through the toll booth in a 2 second window?</span><span class="sxs-lookup"><span data-stu-id="af1b1-221">For example, how many unique make of cars passed through the toll booth in a 2 second window?</span></span>

<span data-ttu-id="af1b1-222">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-222">**Input**:</span></span>

| <span data-ttu-id="af1b1-223">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-223">Make</span></span> | <span data-ttu-id="af1b1-224">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-224">Time</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-225">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-225">Honda</span></span> |<span data-ttu-id="af1b1-226">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-226">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-227">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-227">Honda</span></span> |<span data-ttu-id="af1b1-228">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-228">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-229">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-229">Toyota</span></span> |<span data-ttu-id="af1b1-230">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-230">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-231">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-231">Toyota</span></span> |<span data-ttu-id="af1b1-232">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-232">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-233">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-233">Toyota</span></span> |<span data-ttu-id="af1b1-234">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-234">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="af1b1-235">**Output:**</span><span class="sxs-lookup"><span data-stu-id="af1b1-235">**Output:**</span></span>

| <span data-ttu-id="af1b1-236">Count</span><span class="sxs-lookup"><span data-stu-id="af1b1-236">Count</span></span> | <span data-ttu-id="af1b1-237">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-237">Time</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-238">2</span><span class="sxs-lookup"><span data-stu-id="af1b1-238">2</span></span> |<span data-ttu-id="af1b1-239">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-239">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="af1b1-240">1</span><span class="sxs-lookup"><span data-stu-id="af1b1-240">1</span></span> |<span data-ttu-id="af1b1-241">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-241">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="af1b1-242">**Solution:**</span><span class="sxs-lookup"><span data-stu-id="af1b1-242">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="af1b1-243">**Explanation:** COUNT(DISTINCT Make) returns the number of distinct values of the “Make” column within a time window.</span><span class="sxs-lookup"><span data-stu-id="af1b1-243">**Explanation:** COUNT(DISTINCT Make) returns the number of distinct values of the “Make” column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="af1b1-244">Query example: Determine if a value has changed</span><span class="sxs-lookup"><span data-stu-id="af1b1-244">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="af1b1-245">**Description**: Look at a previous value to determine if it is different than the current value For example, is the previous car on the Toll Road the same make as the current car?</span><span class="sxs-lookup"><span data-stu-id="af1b1-245">**Description**: Look at a previous value to determine if it is different than the current value For example, is the previous car on the Toll Road the same make as the current car?</span></span>

<span data-ttu-id="af1b1-246">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-246">**Input**:</span></span>

| <span data-ttu-id="af1b1-247">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-247">Make</span></span> | <span data-ttu-id="af1b1-248">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-248">Time</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-249">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-249">Honda</span></span> |<span data-ttu-id="af1b1-250">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-250">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-251">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-251">Toyota</span></span> |<span data-ttu-id="af1b1-252">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-252">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="af1b1-253">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-253">**Output**:</span></span>

| <span data-ttu-id="af1b1-254">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-254">Make</span></span> | <span data-ttu-id="af1b1-255">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-255">Time</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-256">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-256">Toyota</span></span> |<span data-ttu-id="af1b1-257">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-257">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="af1b1-258">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-258">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="af1b1-259">**Explanation**: Use LAG to peek into the input stream one event back and get the Make value.</span><span class="sxs-lookup"><span data-stu-id="af1b1-259">**Explanation**: Use LAG to peek into the input stream one event back and get the Make value.</span></span> <span data-ttu-id="af1b1-260">Then compare it to the Make on the current event and output the event if they are different.</span><span class="sxs-lookup"><span data-stu-id="af1b1-260">Then compare it to the Make on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-first-event-in-a-window"></a><span data-ttu-id="af1b1-261">Query example: Find first event in a window</span><span class="sxs-lookup"><span data-stu-id="af1b1-261">Query example: Find first event in a window</span></span>
<span data-ttu-id="af1b1-262">**Description**: Find first car in every 10 minute interval?</span><span class="sxs-lookup"><span data-stu-id="af1b1-262">**Description**: Find first car in every 10 minute interval?</span></span>

<span data-ttu-id="af1b1-263">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-263">**Input**:</span></span>

| <span data-ttu-id="af1b1-264">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-264">LicensePlate</span></span> | <span data-ttu-id="af1b1-265">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-265">Make</span></span> | <span data-ttu-id="af1b1-266">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-266">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-267">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="af1b1-267">DXE 5291</span></span> |<span data-ttu-id="af1b1-268">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-268">Honda</span></span> |<span data-ttu-id="af1b1-269">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-269">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="af1b1-270">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="af1b1-270">YZK 5704</span></span> |<span data-ttu-id="af1b1-271">Ford</span><span class="sxs-lookup"><span data-stu-id="af1b1-271">Ford</span></span> |<span data-ttu-id="af1b1-272">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-272">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="af1b1-273">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="af1b1-273">RMV 8282</span></span> |<span data-ttu-id="af1b1-274">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-274">Honda</span></span> |<span data-ttu-id="af1b1-275">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-275">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-276">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="af1b1-276">YHN 6970</span></span> |<span data-ttu-id="af1b1-277">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-277">Toyota</span></span> |<span data-ttu-id="af1b1-278">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-278">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="af1b1-279">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="af1b1-279">VFE 1616</span></span> |<span data-ttu-id="af1b1-280">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-280">Toyota</span></span> |<span data-ttu-id="af1b1-281">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-281">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="af1b1-282">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="af1b1-282">QYF 9358</span></span> |<span data-ttu-id="af1b1-283">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-283">Honda</span></span> |<span data-ttu-id="af1b1-284">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-284">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-285">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="af1b1-285">MDR 6128</span></span> |<span data-ttu-id="af1b1-286">BMW</span><span class="sxs-lookup"><span data-stu-id="af1b1-286">BMW</span></span> |<span data-ttu-id="af1b1-287">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-287">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="af1b1-288">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-288">**Output**:</span></span>

| <span data-ttu-id="af1b1-289">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-289">LicensePlate</span></span> | <span data-ttu-id="af1b1-290">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-290">Make</span></span> | <span data-ttu-id="af1b1-291">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-291">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-292">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="af1b1-292">DXE 5291</span></span> |<span data-ttu-id="af1b1-293">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-293">Honda</span></span> |<span data-ttu-id="af1b1-294">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-294">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="af1b1-295">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="af1b1-295">QYF 9358</span></span> |<span data-ttu-id="af1b1-296">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-296">Honda</span></span> |<span data-ttu-id="af1b1-297">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-297">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="af1b1-298">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-298">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="af1b1-299">Now let’s change the problem and find first car of particular Make in every 10 minute interval.</span><span class="sxs-lookup"><span data-stu-id="af1b1-299">Now let’s change the problem and find first car of particular Make in every 10 minute interval.</span></span>

| <span data-ttu-id="af1b1-300">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-300">LicensePlate</span></span> | <span data-ttu-id="af1b1-301">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-301">Make</span></span> | <span data-ttu-id="af1b1-302">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-302">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-303">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="af1b1-303">DXE 5291</span></span> |<span data-ttu-id="af1b1-304">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-304">Honda</span></span> |<span data-ttu-id="af1b1-305">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-305">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="af1b1-306">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="af1b1-306">YZK 5704</span></span> |<span data-ttu-id="af1b1-307">Ford</span><span class="sxs-lookup"><span data-stu-id="af1b1-307">Ford</span></span> |<span data-ttu-id="af1b1-308">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-308">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="af1b1-309">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="af1b1-309">YHN 6970</span></span> |<span data-ttu-id="af1b1-310">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-310">Toyota</span></span> |<span data-ttu-id="af1b1-311">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-311">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="af1b1-312">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="af1b1-312">QYF 9358</span></span> |<span data-ttu-id="af1b1-313">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-313">Honda</span></span> |<span data-ttu-id="af1b1-314">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-314">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-315">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="af1b1-315">MDR 6128</span></span> |<span data-ttu-id="af1b1-316">BMW</span><span class="sxs-lookup"><span data-stu-id="af1b1-316">BMW</span></span> |<span data-ttu-id="af1b1-317">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-317">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="af1b1-318">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-318">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-last-event-in-a-window"></a><span data-ttu-id="af1b1-319">Query example: Find last event in a window</span><span class="sxs-lookup"><span data-stu-id="af1b1-319">Query example: Find last event in a window</span></span>
<span data-ttu-id="af1b1-320">**Description**: Find last car in every 10 minute interval.</span><span class="sxs-lookup"><span data-stu-id="af1b1-320">**Description**: Find last car in every 10 minute interval.</span></span>

<span data-ttu-id="af1b1-321">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-321">**Input**:</span></span>

| <span data-ttu-id="af1b1-322">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-322">LicensePlate</span></span> | <span data-ttu-id="af1b1-323">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-323">Make</span></span> | <span data-ttu-id="af1b1-324">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-324">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-325">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="af1b1-325">DXE 5291</span></span> |<span data-ttu-id="af1b1-326">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-326">Honda</span></span> |<span data-ttu-id="af1b1-327">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-327">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="af1b1-328">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="af1b1-328">YZK 5704</span></span> |<span data-ttu-id="af1b1-329">Ford</span><span class="sxs-lookup"><span data-stu-id="af1b1-329">Ford</span></span> |<span data-ttu-id="af1b1-330">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-330">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="af1b1-331">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="af1b1-331">RMV 8282</span></span> |<span data-ttu-id="af1b1-332">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-332">Honda</span></span> |<span data-ttu-id="af1b1-333">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-333">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-334">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="af1b1-334">YHN 6970</span></span> |<span data-ttu-id="af1b1-335">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-335">Toyota</span></span> |<span data-ttu-id="af1b1-336">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-336">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="af1b1-337">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="af1b1-337">VFE 1616</span></span> |<span data-ttu-id="af1b1-338">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-338">Toyota</span></span> |<span data-ttu-id="af1b1-339">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-339">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="af1b1-340">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="af1b1-340">QYF 9358</span></span> |<span data-ttu-id="af1b1-341">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-341">Honda</span></span> |<span data-ttu-id="af1b1-342">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-342">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-343">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="af1b1-343">MDR 6128</span></span> |<span data-ttu-id="af1b1-344">BMW</span><span class="sxs-lookup"><span data-stu-id="af1b1-344">BMW</span></span> |<span data-ttu-id="af1b1-345">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-345">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="af1b1-346">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-346">**Output**:</span></span>

| <span data-ttu-id="af1b1-347">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-347">LicensePlate</span></span> | <span data-ttu-id="af1b1-348">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-348">Make</span></span> | <span data-ttu-id="af1b1-349">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-349">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-350">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="af1b1-350">VFE 1616</span></span> |<span data-ttu-id="af1b1-351">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-351">Toyota</span></span> |<span data-ttu-id="af1b1-352">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-352">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="af1b1-353">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="af1b1-353">MDR 6128</span></span> |<span data-ttu-id="af1b1-354">BMW</span><span class="sxs-lookup"><span data-stu-id="af1b1-354">BMW</span></span> |<span data-ttu-id="af1b1-355">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-355">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="af1b1-356">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-356">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="af1b1-357">**Explanation**: There are two steps in the query – the first one finds latest timestamp in 10 minute windows.</span><span class="sxs-lookup"><span data-stu-id="af1b1-357">**Explanation**: There are two steps in the query – the first one finds latest timestamp in 10 minute windows.</span></span> <span data-ttu-id="af1b1-358">The second step joins results of the first query with original stream to find events matching last timestamps in each window.</span><span class="sxs-lookup"><span data-stu-id="af1b1-358">The second step joins results of the first query with original stream to find events matching last timestamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="af1b1-359">Query example: Detect the absence of events</span><span class="sxs-lookup"><span data-stu-id="af1b1-359">Query example: Detect the absence of events</span></span>
<span data-ttu-id="af1b1-360">**Description**: Check that a stream has no value that matches a certain criteria.</span><span class="sxs-lookup"><span data-stu-id="af1b1-360">**Description**: Check that a stream has no value that matches a certain criteria.</span></span>
<span data-ttu-id="af1b1-361">For example, have 2 consecutive cars from the same make entered the toll road within 90 seconds?</span><span class="sxs-lookup"><span data-stu-id="af1b1-361">For example, have 2 consecutive cars from the same make entered the toll road within 90 seconds?</span></span>

<span data-ttu-id="af1b1-362">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-362">**Input**:</span></span>

| <span data-ttu-id="af1b1-363">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-363">Make</span></span> | <span data-ttu-id="af1b1-364">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-364">LicensePlate</span></span> | <span data-ttu-id="af1b1-365">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-365">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-366">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-366">Honda</span></span> |<span data-ttu-id="af1b1-367">ABC-123</span><span class="sxs-lookup"><span data-stu-id="af1b1-367">ABC-123</span></span> |<span data-ttu-id="af1b1-368">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-368">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="af1b1-369">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-369">Honda</span></span> |<span data-ttu-id="af1b1-370">AAA-999</span><span class="sxs-lookup"><span data-stu-id="af1b1-370">AAA-999</span></span> |<span data-ttu-id="af1b1-371">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-371">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="af1b1-372">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-372">Toyota</span></span> |<span data-ttu-id="af1b1-373">DEF-987</span><span class="sxs-lookup"><span data-stu-id="af1b1-373">DEF-987</span></span> |<span data-ttu-id="af1b1-374">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-374">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="af1b1-375">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-375">Honda</span></span> |<span data-ttu-id="af1b1-376">GHI-345</span><span class="sxs-lookup"><span data-stu-id="af1b1-376">GHI-345</span></span> |<span data-ttu-id="af1b1-377">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-377">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="af1b1-378">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-378">**Output**:</span></span>

| <span data-ttu-id="af1b1-379">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-379">Make</span></span> | <span data-ttu-id="af1b1-380">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-380">Time</span></span> | <span data-ttu-id="af1b1-381">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-381">CurrentCarLicensePlate</span></span> | <span data-ttu-id="af1b1-382">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="af1b1-382">FirstCarLicensePlate</span></span> | <span data-ttu-id="af1b1-383">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="af1b1-383">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="af1b1-384">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-384">Honda</span></span> |<span data-ttu-id="af1b1-385">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-385">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="af1b1-386">AAA-999</span><span class="sxs-lookup"><span data-stu-id="af1b1-386">AAA-999</span></span> |<span data-ttu-id="af1b1-387">ABC-123</span><span class="sxs-lookup"><span data-stu-id="af1b1-387">ABC-123</span></span> |<span data-ttu-id="af1b1-388">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-388">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="af1b1-389">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-389">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="af1b1-390">**Explanation**: Use LAG to peek into the input stream one event back and get the Make value.</span><span class="sxs-lookup"><span data-stu-id="af1b1-390">**Explanation**: Use LAG to peek into the input stream one event back and get the Make value.</span></span> <span data-ttu-id="af1b1-391">Then compare it to the Make on the current event and output the event if they are the same and use LAG to get data about the previous car.</span><span class="sxs-lookup"><span data-stu-id="af1b1-391">Then compare it to the Make on the current event and output the event if they are the same and use LAG to get data about the previous car.</span></span>

## <a name="query-example-detect-duration-between-events"></a><span data-ttu-id="af1b1-392">Query example: Detect duration between events</span><span class="sxs-lookup"><span data-stu-id="af1b1-392">Query example: Detect duration between events</span></span>
<span data-ttu-id="af1b1-393">**Description**: Find the duration of a given event.</span><span class="sxs-lookup"><span data-stu-id="af1b1-393">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="af1b1-394">For example, given a web clickstream determine time spent on a feature.</span><span class="sxs-lookup"><span data-stu-id="af1b1-394">For example, given a web clickstream determine time spent on a feature.</span></span>

<span data-ttu-id="af1b1-395">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-395">**Input**:</span></span>  

| <span data-ttu-id="af1b1-396">User</span><span class="sxs-lookup"><span data-stu-id="af1b1-396">User</span></span> | <span data-ttu-id="af1b1-397">Feature</span><span class="sxs-lookup"><span data-stu-id="af1b1-397">Feature</span></span> | <span data-ttu-id="af1b1-398">Event</span><span class="sxs-lookup"><span data-stu-id="af1b1-398">Event</span></span> | <span data-ttu-id="af1b1-399">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-399">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="af1b1-400">RightMenu</span><span class="sxs-lookup"><span data-stu-id="af1b1-400">RightMenu</span></span> |<span data-ttu-id="af1b1-401">Start</span><span class="sxs-lookup"><span data-stu-id="af1b1-401">Start</span></span> |<span data-ttu-id="af1b1-402">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-402">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="af1b1-403">RightMenu</span><span class="sxs-lookup"><span data-stu-id="af1b1-403">RightMenu</span></span> |<span data-ttu-id="af1b1-404">End</span><span class="sxs-lookup"><span data-stu-id="af1b1-404">End</span></span> |<span data-ttu-id="af1b1-405">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-405">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="af1b1-406">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-406">**Output**:</span></span>  

| <span data-ttu-id="af1b1-407">User</span><span class="sxs-lookup"><span data-stu-id="af1b1-407">User</span></span> | <span data-ttu-id="af1b1-408">Feature</span><span class="sxs-lookup"><span data-stu-id="af1b1-408">Feature</span></span> | <span data-ttu-id="af1b1-409">Duration</span><span class="sxs-lookup"><span data-stu-id="af1b1-409">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="af1b1-410">RightMenu</span><span class="sxs-lookup"><span data-stu-id="af1b1-410">RightMenu</span></span> |<span data-ttu-id="af1b1-411">7</span><span class="sxs-lookup"><span data-stu-id="af1b1-411">7</span></span> |

<span data-ttu-id="af1b1-412">**Solution**</span><span class="sxs-lookup"><span data-stu-id="af1b1-412">**Solution**</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="af1b1-413">**Explanation**: Use LAST function to retrieve last Time value when event type was ‘Start’.</span><span class="sxs-lookup"><span data-stu-id="af1b1-413">**Explanation**: Use LAST function to retrieve last Time value when event type was ‘Start’.</span></span> <span data-ttu-id="af1b1-414">Note that LAST function uses PARTITION BY [user] to indicate that result shall be computed per unique user.</span><span class="sxs-lookup"><span data-stu-id="af1b1-414">Note that LAST function uses PARTITION BY [user] to indicate that result shall be computed per unique user.</span></span>  <span data-ttu-id="af1b1-415">The query has a 1 hour maximum threshold for time difference between ‘Start’ and ‘Stop’ events but is configurable as needed (LIMIT DURATION(hour, 1).</span><span class="sxs-lookup"><span data-stu-id="af1b1-415">The query has a 1 hour maximum threshold for time difference between ‘Start’ and ‘Stop’ events but is configurable as needed (LIMIT DURATION(hour, 1).</span></span>

## <a name="query-example-detect-duration-of-a-condition"></a><span data-ttu-id="af1b1-416">Query example: Detect duration of a condition</span><span class="sxs-lookup"><span data-stu-id="af1b1-416">Query example: Detect duration of a condition</span></span>
<span data-ttu-id="af1b1-417">**Description**: Find out how long a condition occurred for.</span><span class="sxs-lookup"><span data-stu-id="af1b1-417">**Description**: Find out how long a condition occurred for.</span></span>
<span data-ttu-id="af1b1-418">For example, suppose that a bug that resulted in all cars having an incorrect weight (above 20,000 pounds) – we want to compute the duration of the bug.</span><span class="sxs-lookup"><span data-stu-id="af1b1-418">For example, suppose that a bug that resulted in all cars having an incorrect weight (above 20,000 pounds) – we want to compute the duration of the bug.</span></span>

<span data-ttu-id="af1b1-419">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-419">**Input**:</span></span>

| <span data-ttu-id="af1b1-420">Make</span><span class="sxs-lookup"><span data-stu-id="af1b1-420">Make</span></span> | <span data-ttu-id="af1b1-421">Time</span><span class="sxs-lookup"><span data-stu-id="af1b1-421">Time</span></span> | <span data-ttu-id="af1b1-422">Weight</span><span class="sxs-lookup"><span data-stu-id="af1b1-422">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-423">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-423">Honda</span></span> |<span data-ttu-id="af1b1-424">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-424">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="af1b1-425">2000</span><span class="sxs-lookup"><span data-stu-id="af1b1-425">2000</span></span> |
| <span data-ttu-id="af1b1-426">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-426">Toyota</span></span> |<span data-ttu-id="af1b1-427">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-427">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="af1b1-428">25000</span><span class="sxs-lookup"><span data-stu-id="af1b1-428">25000</span></span> |
| <span data-ttu-id="af1b1-429">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-429">Honda</span></span> |<span data-ttu-id="af1b1-430">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-430">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="af1b1-431">26000</span><span class="sxs-lookup"><span data-stu-id="af1b1-431">26000</span></span> |
| <span data-ttu-id="af1b1-432">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-432">Toyota</span></span> |<span data-ttu-id="af1b1-433">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-433">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="af1b1-434">25000</span><span class="sxs-lookup"><span data-stu-id="af1b1-434">25000</span></span> |
| <span data-ttu-id="af1b1-435">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-435">Honda</span></span> |<span data-ttu-id="af1b1-436">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-436">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="af1b1-437">26000</span><span class="sxs-lookup"><span data-stu-id="af1b1-437">26000</span></span> |
| <span data-ttu-id="af1b1-438">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-438">Toyota</span></span> |<span data-ttu-id="af1b1-439">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-439">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="af1b1-440">25000</span><span class="sxs-lookup"><span data-stu-id="af1b1-440">25000</span></span> |
| <span data-ttu-id="af1b1-441">Honda</span><span class="sxs-lookup"><span data-stu-id="af1b1-441">Honda</span></span> |<span data-ttu-id="af1b1-442">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-442">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="af1b1-443">26000</span><span class="sxs-lookup"><span data-stu-id="af1b1-443">26000</span></span> |
| <span data-ttu-id="af1b1-444">Toyota</span><span class="sxs-lookup"><span data-stu-id="af1b1-444">Toyota</span></span> |<span data-ttu-id="af1b1-445">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-445">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="af1b1-446">2000</span><span class="sxs-lookup"><span data-stu-id="af1b1-446">2000</span></span> |

<span data-ttu-id="af1b1-447">**Output**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-447">**Output**:</span></span>

| <span data-ttu-id="af1b1-448">StartFault</span><span class="sxs-lookup"><span data-stu-id="af1b1-448">StartFault</span></span> | <span data-ttu-id="af1b1-449">EndFault</span><span class="sxs-lookup"><span data-stu-id="af1b1-449">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-450">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-450">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="af1b1-451">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-451">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="af1b1-452">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-452">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="af1b1-453">**Explanation**: Use LAG to view the input stream for 24 hours and look for instances where StartFault and StopFault are spanned by weight < 20000.</span><span class="sxs-lookup"><span data-stu-id="af1b1-453">**Explanation**: Use LAG to view the input stream for 24 hours and look for instances where StartFault and StopFault are spanned by weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="af1b1-454">Query example: Fill missing values</span><span class="sxs-lookup"><span data-stu-id="af1b1-454">Query example: Fill missing values</span></span>
<span data-ttu-id="af1b1-455">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span><span class="sxs-lookup"><span data-stu-id="af1b1-455">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="af1b1-456">For example, generate event every 5 seconds that will report the most recently seen data point.</span><span class="sxs-lookup"><span data-stu-id="af1b1-456">For example, generate event every 5 seconds that will report the most recently seen data point.</span></span>

<span data-ttu-id="af1b1-457">**Input**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-457">**Input**:</span></span>

| <span data-ttu-id="af1b1-458">t</span><span class="sxs-lookup"><span data-stu-id="af1b1-458">t</span></span> | <span data-ttu-id="af1b1-459">value</span><span class="sxs-lookup"><span data-stu-id="af1b1-459">value</span></span> |
| --- | --- |
| <span data-ttu-id="af1b1-460">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="af1b1-460">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="af1b1-461">1</span><span class="sxs-lookup"><span data-stu-id="af1b1-461">1</span></span> |
| <span data-ttu-id="af1b1-462">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="af1b1-462">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="af1b1-463">2</span><span class="sxs-lookup"><span data-stu-id="af1b1-463">2</span></span> |
| <span data-ttu-id="af1b1-464">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="af1b1-464">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="af1b1-465">3</span><span class="sxs-lookup"><span data-stu-id="af1b1-465">3</span></span> |
| <span data-ttu-id="af1b1-466">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="af1b1-466">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="af1b1-467">4</span><span class="sxs-lookup"><span data-stu-id="af1b1-467">4</span></span> |
| <span data-ttu-id="af1b1-468">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="af1b1-468">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="af1b1-469">5</span><span class="sxs-lookup"><span data-stu-id="af1b1-469">5</span></span> |
| <span data-ttu-id="af1b1-470">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="af1b1-470">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="af1b1-471">6</span><span class="sxs-lookup"><span data-stu-id="af1b1-471">6</span></span> |

<span data-ttu-id="af1b1-472">**Output (first 10 rows)**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-472">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="af1b1-473">windowend</span><span class="sxs-lookup"><span data-stu-id="af1b1-473">windowend</span></span> | <span data-ttu-id="af1b1-474">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="af1b1-474">lastevent.t</span></span> | <span data-ttu-id="af1b1-475">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="af1b1-475">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af1b1-476">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-476">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="af1b1-477">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-477">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="af1b1-478">1</span><span class="sxs-lookup"><span data-stu-id="af1b1-478">1</span></span> |
| <span data-ttu-id="af1b1-479">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-479">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="af1b1-480">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-480">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="af1b1-481">2</span><span class="sxs-lookup"><span data-stu-id="af1b1-481">2</span></span> |
| <span data-ttu-id="af1b1-482">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-482">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="af1b1-483">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-483">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="af1b1-484">3</span><span class="sxs-lookup"><span data-stu-id="af1b1-484">3</span></span> |
| <span data-ttu-id="af1b1-485">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-485">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="af1b1-486">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-486">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="af1b1-487">4</span><span class="sxs-lookup"><span data-stu-id="af1b1-487">4</span></span> |
| <span data-ttu-id="af1b1-488">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-488">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="af1b1-489">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-489">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="af1b1-490">4</span><span class="sxs-lookup"><span data-stu-id="af1b1-490">4</span></span> |
| <span data-ttu-id="af1b1-491">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-491">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="af1b1-492">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-492">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="af1b1-493">4</span><span class="sxs-lookup"><span data-stu-id="af1b1-493">4</span></span> |
| <span data-ttu-id="af1b1-494">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-494">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="af1b1-495">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-495">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="af1b1-496">5</span><span class="sxs-lookup"><span data-stu-id="af1b1-496">5</span></span> |
| <span data-ttu-id="af1b1-497">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-497">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="af1b1-498">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-498">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="af1b1-499">6</span><span class="sxs-lookup"><span data-stu-id="af1b1-499">6</span></span> |
| <span data-ttu-id="af1b1-500">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-500">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="af1b1-501">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-501">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="af1b1-502">6</span><span class="sxs-lookup"><span data-stu-id="af1b1-502">6</span></span> |
| <span data-ttu-id="af1b1-503">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-503">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="af1b1-504">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="af1b1-504">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="af1b1-505">6</span><span class="sxs-lookup"><span data-stu-id="af1b1-505">6</span></span> |

<span data-ttu-id="af1b1-506">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="af1b1-506">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="af1b1-507">**Explanation**: This query will generate events every 5 second and will output the last event that was received before.</span><span class="sxs-lookup"><span data-stu-id="af1b1-507">**Explanation**: This query will generate events every 5 second and will output the last event that was received before.</span></span> <span data-ttu-id="af1b1-508">[Hopping Window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping Window - Azure Stream Analytics") duration determines how far back the query will look to find the latest event (300 seconds in this example).</span><span class="sxs-lookup"><span data-stu-id="af1b1-508">[Hopping Window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping Window - Azure Stream Analytics") duration determines how far back the query will look to find the latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="af1b1-509">Get help</span><span class="sxs-lookup"><span data-stu-id="af1b1-509">Get help</span></span>
<span data-ttu-id="af1b1-510">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="af1b1-510">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="af1b1-511">Next steps</span><span class="sxs-lookup"><span data-stu-id="af1b1-511">Next steps</span></span>
* [<span data-ttu-id="af1b1-512">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="af1b1-512">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="af1b1-513">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="af1b1-513">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="af1b1-514">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="af1b1-514">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="af1b1-515">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="af1b1-515">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="af1b1-516">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="af1b1-516">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

