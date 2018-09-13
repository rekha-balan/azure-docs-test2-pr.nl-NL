---
title: Common query patterns in Azure Stream Analytics
description: This article describes a number of common query patterns and designs that are useful in Azure Stream Analytics jobs.
services: stream-analytics
author: jseb225
manager: kfile
ms.author: jeanb
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 08/08/2017
ms.openlocfilehash: 7f171fa1eb8c91b55119d0308b57fe3d3e70261b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830648"
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="f5547-103">Query examples for common Stream Analytics usage patterns</span><span class="sxs-lookup"><span data-stu-id="f5547-103">Query examples for common Stream Analytics usage patterns</span></span>

## <a name="introduction"></a><span data-ttu-id="f5547-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="f5547-104">Introduction</span></span>
<span data-ttu-id="f5547-105">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span><span class="sxs-lookup"><span data-stu-id="f5547-105">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="f5547-106">The language constructs are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span><span class="sxs-lookup"><span data-stu-id="f5547-106">The language constructs are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> 

<span data-ttu-id="f5547-107">The query design can express simple pass-through logic to move event data from one input stream into another output data store.</span><span class="sxs-lookup"><span data-stu-id="f5547-107">The query design can express simple pass-through logic to move event data from one input stream into another output data store.</span></span> <span data-ttu-id="f5547-108">Or it can do rich pattern matching and temporal analysis to calculate aggregates over various time windows as in the TollApp sample.</span><span class="sxs-lookup"><span data-stu-id="f5547-108">Or it can do rich pattern matching and temporal analysis to calculate aggregates over various time windows as in the TollApp sample.</span></span> <span data-ttu-id="f5547-109">You can join data from multiple inputs to combine streaming events, and do lookups against static reference data to enrich the event values.</span><span class="sxs-lookup"><span data-stu-id="f5547-109">You can join data from multiple inputs to combine streaming events, and do lookups against static reference data to enrich the event values.</span></span> <span data-ttu-id="f5547-110">Also you can write data to multiple outputs.</span><span class="sxs-lookup"><span data-stu-id="f5547-110">Also you can write data to multiple outputs.</span></span>

<span data-ttu-id="f5547-111">This article outlines solutions to several common query patterns, based on real-world scenarios.</span><span class="sxs-lookup"><span data-stu-id="f5547-111">This article outlines solutions to several common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="f5547-112">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span><span class="sxs-lookup"><span data-stu-id="f5547-112">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span></span>

## <a name="work-with-complex-data-types-in-json-and-avro"></a><span data-ttu-id="f5547-113">Work with complex Data Types in JSON and AVRO</span><span class="sxs-lookup"><span data-stu-id="f5547-113">Work with complex Data Types in JSON and AVRO</span></span> 
<span data-ttu-id="f5547-114">Azure Stream Analytics supports processing events in CSV, JSON and Avro data formats.</span><span class="sxs-lookup"><span data-stu-id="f5547-114">Azure Stream Analytics supports processing events in CSV, JSON and Avro data formats.</span></span>
<span data-ttu-id="f5547-115">Both JSON and Avro may contain complex types such as nested objects (records) or arrays.</span><span class="sxs-lookup"><span data-stu-id="f5547-115">Both JSON and Avro may contain complex types such as nested objects (records) or arrays.</span></span> <span data-ttu-id="f5547-116">In order to work with these complex data types, refer to the [Parsing JSON and AVRO data](stream-analytics-parsing-json.md) article.</span><span class="sxs-lookup"><span data-stu-id="f5547-116">In order to work with these complex data types, refer to the [Parsing JSON and AVRO data](stream-analytics-parsing-json.md) article.</span></span>


## <a name="query-example-convert-data-types"></a><span data-ttu-id="f5547-117">Query example: Convert data types</span><span class="sxs-lookup"><span data-stu-id="f5547-117">Query example: Convert data types</span></span>
<span data-ttu-id="f5547-118">**Description**: Define the types of properties on the input stream.</span><span class="sxs-lookup"><span data-stu-id="f5547-118">**Description**: Define the types of properties on the input stream.</span></span>
<span data-ttu-id="f5547-119">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span><span class="sxs-lookup"><span data-stu-id="f5547-119">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span></span>

<span data-ttu-id="f5547-120">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-120">**Input**:</span></span>

| <span data-ttu-id="f5547-121">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-121">Make</span></span> | <span data-ttu-id="f5547-122">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-122">Time</span></span> | <span data-ttu-id="f5547-123">Weight</span><span class="sxs-lookup"><span data-stu-id="f5547-123">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-124">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-124">Honda</span></span> |<span data-ttu-id="f5547-125">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-125">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="f5547-126">"1000"</span><span class="sxs-lookup"><span data-stu-id="f5547-126">"1000"</span></span> |
| <span data-ttu-id="f5547-127">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-127">Honda</span></span> |<span data-ttu-id="f5547-128">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-128">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="f5547-129">"2000"</span><span class="sxs-lookup"><span data-stu-id="f5547-129">"2000"</span></span> |

<span data-ttu-id="f5547-130">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-130">**Output**:</span></span>

| <span data-ttu-id="f5547-131">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-131">Make</span></span> | <span data-ttu-id="f5547-132">Weight</span><span class="sxs-lookup"><span data-stu-id="f5547-132">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-133">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-133">Honda</span></span> |<span data-ttu-id="f5547-134">3000</span><span class="sxs-lookup"><span data-stu-id="f5547-134">3000</span></span> |

<span data-ttu-id="f5547-135">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-135">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="f5547-136">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span><span class="sxs-lookup"><span data-stu-id="f5547-136">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span></span> <span data-ttu-id="f5547-137">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5547-137">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="f5547-138">Query example: Use Like/Not like to do pattern matching</span><span class="sxs-lookup"><span data-stu-id="f5547-138">Query example: Use Like/Not like to do pattern matching</span></span>
<span data-ttu-id="f5547-139">**Description**: Check that a field value on the event matches a certain pattern.</span><span class="sxs-lookup"><span data-stu-id="f5547-139">**Description**: Check that a field value on the event matches a certain pattern.</span></span>
<span data-ttu-id="f5547-140">For example, check that the result returns license plates that start with A and end with 9.</span><span class="sxs-lookup"><span data-stu-id="f5547-140">For example, check that the result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="f5547-141">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-141">**Input**:</span></span>

| <span data-ttu-id="f5547-142">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-142">Make</span></span> | <span data-ttu-id="f5547-143">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-143">LicensePlate</span></span> | <span data-ttu-id="f5547-144">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-144">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-145">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-145">Honda</span></span> |<span data-ttu-id="f5547-146">ABC-123</span><span class="sxs-lookup"><span data-stu-id="f5547-146">ABC-123</span></span> |<span data-ttu-id="f5547-147">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-147">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-148">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-148">Toyota</span></span> |<span data-ttu-id="f5547-149">AAA-999</span><span class="sxs-lookup"><span data-stu-id="f5547-149">AAA-999</span></span> |<span data-ttu-id="f5547-150">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-150">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-151">Nissan</span><span class="sxs-lookup"><span data-stu-id="f5547-151">Nissan</span></span> |<span data-ttu-id="f5547-152">ABC-369</span><span class="sxs-lookup"><span data-stu-id="f5547-152">ABC-369</span></span> |<span data-ttu-id="f5547-153">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-153">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f5547-154">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-154">**Output**:</span></span>

| <span data-ttu-id="f5547-155">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-155">Make</span></span> | <span data-ttu-id="f5547-156">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-156">LicensePlate</span></span> | <span data-ttu-id="f5547-157">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-157">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-158">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-158">Toyota</span></span> |<span data-ttu-id="f5547-159">AAA-999</span><span class="sxs-lookup"><span data-stu-id="f5547-159">AAA-999</span></span> |<span data-ttu-id="f5547-160">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-160">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-161">Nissan</span><span class="sxs-lookup"><span data-stu-id="f5547-161">Nissan</span></span> |<span data-ttu-id="f5547-162">ABC-369</span><span class="sxs-lookup"><span data-stu-id="f5547-162">ABC-369</span></span> |<span data-ttu-id="f5547-163">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-163">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f5547-164">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-164">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="f5547-165">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span><span class="sxs-lookup"><span data-stu-id="f5547-165">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span></span> <span data-ttu-id="f5547-166">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span><span class="sxs-lookup"><span data-stu-id="f5547-166">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="f5547-167">Query example: Specify logic for different cases/values (CASE statements)</span><span class="sxs-lookup"><span data-stu-id="f5547-167">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="f5547-168">**Description**: Provide a different computation for a field, based on a particular criterion.</span><span class="sxs-lookup"><span data-stu-id="f5547-168">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="f5547-169">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span><span class="sxs-lookup"><span data-stu-id="f5547-169">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span></span>

<span data-ttu-id="f5547-170">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-170">**Input**:</span></span>

| <span data-ttu-id="f5547-171">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-171">Make</span></span> | <span data-ttu-id="f5547-172">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-172">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-173">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-173">Honda</span></span> |<span data-ttu-id="f5547-174">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-174">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-175">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-175">Toyota</span></span> |<span data-ttu-id="f5547-176">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-176">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-177">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-177">Toyota</span></span> |<span data-ttu-id="f5547-178">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-178">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f5547-179">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-179">**Output**:</span></span>

| <span data-ttu-id="f5547-180">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="f5547-180">CarsPassed</span></span> | <span data-ttu-id="f5547-181">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-181">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-182">1 Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-182">1 Honda</span></span> |<span data-ttu-id="f5547-183">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-183">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="f5547-184">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="f5547-184">2 Toyotas</span></span> |<span data-ttu-id="f5547-185">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-185">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="f5547-186">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-186">**Solution**:</span></span>

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

<span data-ttu-id="f5547-187">**Explanation**: The **CASE** expression compares an expression to a set of simple expressions to determine the result.</span><span class="sxs-lookup"><span data-stu-id="f5547-187">**Explanation**: The **CASE** expression compares an expression to a set of simple expressions to determine the result.</span></span> <span data-ttu-id="f5547-188">In this example, vehicle makes with a count of 1 returned a different string description than vehicle makes with a count other than 1.</span><span class="sxs-lookup"><span data-stu-id="f5547-188">In this example, vehicle makes with a count of 1 returned a different string description than vehicle makes with a count other than 1.</span></span> 

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="f5547-189">Query example: Send data to multiple outputs</span><span class="sxs-lookup"><span data-stu-id="f5547-189">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="f5547-190">**Description**: Send data to multiple output targets from a single job.</span><span class="sxs-lookup"><span data-stu-id="f5547-190">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="f5547-191">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span><span class="sxs-lookup"><span data-stu-id="f5547-191">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span></span>

<span data-ttu-id="f5547-192">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-192">**Input**:</span></span>

| <span data-ttu-id="f5547-193">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-193">Make</span></span> | <span data-ttu-id="f5547-194">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-194">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-195">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-195">Honda</span></span> |<span data-ttu-id="f5547-196">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-196">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-197">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-197">Honda</span></span> |<span data-ttu-id="f5547-198">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-198">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-199">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-199">Toyota</span></span> |<span data-ttu-id="f5547-200">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-200">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-201">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-201">Toyota</span></span> |<span data-ttu-id="f5547-202">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-202">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-203">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-203">Toyota</span></span> |<span data-ttu-id="f5547-204">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-204">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f5547-205">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="f5547-205">**Output1**:</span></span>

| <span data-ttu-id="f5547-206">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-206">Make</span></span> | <span data-ttu-id="f5547-207">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-207">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-208">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-208">Honda</span></span> |<span data-ttu-id="f5547-209">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-209">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-210">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-210">Honda</span></span> |<span data-ttu-id="f5547-211">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-211">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-212">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-212">Toyota</span></span> |<span data-ttu-id="f5547-213">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-213">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-214">Toyota</span></span> |<span data-ttu-id="f5547-215">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-215">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-216">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-216">Toyota</span></span> |<span data-ttu-id="f5547-217">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-217">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f5547-218">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="f5547-218">**Output2**:</span></span>

| <span data-ttu-id="f5547-219">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-219">Make</span></span> | <span data-ttu-id="f5547-220">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-220">Time</span></span> | <span data-ttu-id="f5547-221">Count</span><span class="sxs-lookup"><span data-stu-id="f5547-221">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-222">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-222">Toyota</span></span> |<span data-ttu-id="f5547-223">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-223">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="f5547-224">3</span><span class="sxs-lookup"><span data-stu-id="f5547-224">3</span></span> |

<span data-ttu-id="f5547-225">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-225">**Solution**:</span></span>

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

<span data-ttu-id="f5547-226">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span><span class="sxs-lookup"><span data-stu-id="f5547-226">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span></span>
<span data-ttu-id="f5547-227">The first query is a pass-through of the data received to an output that named **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="f5547-227">The first query is a pass-through of the data received to an output that named **ArchiveOutput**.</span></span>
<span data-ttu-id="f5547-228">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span><span class="sxs-lookup"><span data-stu-id="f5547-228">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span></span>

<span data-ttu-id="f5547-229">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span><span class="sxs-lookup"><span data-stu-id="f5547-229">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="f5547-230">This option has the added benefit of opening fewer readers to the input source.</span><span class="sxs-lookup"><span data-stu-id="f5547-230">This option has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="f5547-231">For example:</span><span class="sxs-lookup"><span data-stu-id="f5547-231">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="f5547-232">Query example: Count unique values</span><span class="sxs-lookup"><span data-stu-id="f5547-232">Query example: Count unique values</span></span>
<span data-ttu-id="f5547-233">**Description**: Count the number of unique field values that appear in the stream within a time window.</span><span class="sxs-lookup"><span data-stu-id="f5547-233">**Description**: Count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="f5547-234">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span><span class="sxs-lookup"><span data-stu-id="f5547-234">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span></span>

<span data-ttu-id="f5547-235">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-235">**Input**:</span></span>

| <span data-ttu-id="f5547-236">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-236">Make</span></span> | <span data-ttu-id="f5547-237">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-237">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-238">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-238">Honda</span></span> |<span data-ttu-id="f5547-239">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-239">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-240">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-240">Honda</span></span> |<span data-ttu-id="f5547-241">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-241">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-242">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-242">Toyota</span></span> |<span data-ttu-id="f5547-243">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-243">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-244">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-244">Toyota</span></span> |<span data-ttu-id="f5547-245">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-245">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-246">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-246">Toyota</span></span> |<span data-ttu-id="f5547-247">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-247">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f5547-248">**Output:**</span><span class="sxs-lookup"><span data-stu-id="f5547-248">**Output:**</span></span>

| <span data-ttu-id="f5547-249">CountMake</span><span class="sxs-lookup"><span data-stu-id="f5547-249">CountMake</span></span> | <span data-ttu-id="f5547-250">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-250">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-251">2</span><span class="sxs-lookup"><span data-stu-id="f5547-251">2</span></span> |<span data-ttu-id="f5547-252">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-252">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="f5547-253">1</span><span class="sxs-lookup"><span data-stu-id="f5547-253">1</span></span> |<span data-ttu-id="f5547-254">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-254">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="f5547-255">**Solution:**</span><span class="sxs-lookup"><span data-stu-id="f5547-255">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="f5547-256">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span><span class="sxs-lookup"><span data-stu-id="f5547-256">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="f5547-257">Query example: Determine if a value has changed</span><span class="sxs-lookup"><span data-stu-id="f5547-257">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="f5547-258">**Description**: Look at a previous value to determine if it is different than the current value.</span><span class="sxs-lookup"><span data-stu-id="f5547-258">**Description**: Look at a previous value to determine if it is different than the current value.</span></span>
<span data-ttu-id="f5547-259">For example, is the previous car on the toll road the same make as the current car?</span><span class="sxs-lookup"><span data-stu-id="f5547-259">For example, is the previous car on the toll road the same make as the current car?</span></span>

<span data-ttu-id="f5547-260">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-260">**Input**:</span></span>

| <span data-ttu-id="f5547-261">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-261">Make</span></span> | <span data-ttu-id="f5547-262">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-262">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-263">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-263">Honda</span></span> |<span data-ttu-id="f5547-264">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-264">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-265">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-265">Toyota</span></span> |<span data-ttu-id="f5547-266">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-266">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="f5547-267">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-267">**Output**:</span></span>

| <span data-ttu-id="f5547-268">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-268">Make</span></span> | <span data-ttu-id="f5547-269">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-269">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-270">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-270">Toyota</span></span> |<span data-ttu-id="f5547-271">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-271">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="f5547-272">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-272">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="f5547-273">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span><span class="sxs-lookup"><span data-stu-id="f5547-273">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="f5547-274">Then compare it to the **Make** value on the current event and output the event if they are different.</span><span class="sxs-lookup"><span data-stu-id="f5547-274">Then compare it to the **Make** value on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-the-first-event-in-a-window"></a><span data-ttu-id="f5547-275">Query example: Find the first event in a window</span><span class="sxs-lookup"><span data-stu-id="f5547-275">Query example: Find the first event in a window</span></span>
<span data-ttu-id="f5547-276">**Description**: Find the first car in every 10-minute interval.</span><span class="sxs-lookup"><span data-stu-id="f5547-276">**Description**: Find the first car in every 10-minute interval.</span></span>

<span data-ttu-id="f5547-277">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-277">**Input**:</span></span>

| <span data-ttu-id="f5547-278">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-278">LicensePlate</span></span> | <span data-ttu-id="f5547-279">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-279">Make</span></span> | <span data-ttu-id="f5547-280">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-280">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-281">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f5547-281">DXE 5291</span></span> |<span data-ttu-id="f5547-282">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-282">Honda</span></span> |<span data-ttu-id="f5547-283">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-283">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="f5547-284">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="f5547-284">YZK 5704</span></span> |<span data-ttu-id="f5547-285">Ford</span><span class="sxs-lookup"><span data-stu-id="f5547-285">Ford</span></span> |<span data-ttu-id="f5547-286">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-286">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="f5547-287">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="f5547-287">RMV 8282</span></span> |<span data-ttu-id="f5547-288">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-288">Honda</span></span> |<span data-ttu-id="f5547-289">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-289">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-290">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="f5547-290">YHN 6970</span></span> |<span data-ttu-id="f5547-291">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-291">Toyota</span></span> |<span data-ttu-id="f5547-292">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-292">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="f5547-293">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="f5547-293">VFE 1616</span></span> |<span data-ttu-id="f5547-294">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-294">Toyota</span></span> |<span data-ttu-id="f5547-295">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-295">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="f5547-296">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f5547-296">QYF 9358</span></span> |<span data-ttu-id="f5547-297">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-297">Honda</span></span> |<span data-ttu-id="f5547-298">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-298">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-299">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f5547-299">MDR 6128</span></span> |<span data-ttu-id="f5547-300">BMW</span><span class="sxs-lookup"><span data-stu-id="f5547-300">BMW</span></span> |<span data-ttu-id="f5547-301">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-301">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="f5547-302">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-302">**Output**:</span></span>

| <span data-ttu-id="f5547-303">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-303">LicensePlate</span></span> | <span data-ttu-id="f5547-304">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-304">Make</span></span> | <span data-ttu-id="f5547-305">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-305">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-306">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f5547-306">DXE 5291</span></span> |<span data-ttu-id="f5547-307">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-307">Honda</span></span> |<span data-ttu-id="f5547-308">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-308">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="f5547-309">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f5547-309">QYF 9358</span></span> |<span data-ttu-id="f5547-310">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-310">Honda</span></span> |<span data-ttu-id="f5547-311">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-311">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="f5547-312">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-312">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="f5547-313">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span><span class="sxs-lookup"><span data-stu-id="f5547-313">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="f5547-314">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-314">LicensePlate</span></span> | <span data-ttu-id="f5547-315">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-315">Make</span></span> | <span data-ttu-id="f5547-316">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-316">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-317">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f5547-317">DXE 5291</span></span> |<span data-ttu-id="f5547-318">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-318">Honda</span></span> |<span data-ttu-id="f5547-319">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-319">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="f5547-320">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="f5547-320">YZK 5704</span></span> |<span data-ttu-id="f5547-321">Ford</span><span class="sxs-lookup"><span data-stu-id="f5547-321">Ford</span></span> |<span data-ttu-id="f5547-322">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-322">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="f5547-323">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="f5547-323">YHN 6970</span></span> |<span data-ttu-id="f5547-324">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-324">Toyota</span></span> |<span data-ttu-id="f5547-325">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-325">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="f5547-326">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f5547-326">QYF 9358</span></span> |<span data-ttu-id="f5547-327">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-327">Honda</span></span> |<span data-ttu-id="f5547-328">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-328">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-329">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f5547-329">MDR 6128</span></span> |<span data-ttu-id="f5547-330">BMW</span><span class="sxs-lookup"><span data-stu-id="f5547-330">BMW</span></span> |<span data-ttu-id="f5547-331">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-331">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="f5547-332">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-332">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-the-last-event-in-a-window"></a><span data-ttu-id="f5547-333">Query example: Find the last event in a window</span><span class="sxs-lookup"><span data-stu-id="f5547-333">Query example: Find the last event in a window</span></span>
<span data-ttu-id="f5547-334">**Description**: Find the last car in every 10-minute interval.</span><span class="sxs-lookup"><span data-stu-id="f5547-334">**Description**: Find the last car in every 10-minute interval.</span></span>

<span data-ttu-id="f5547-335">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-335">**Input**:</span></span>

| <span data-ttu-id="f5547-336">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-336">LicensePlate</span></span> | <span data-ttu-id="f5547-337">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-337">Make</span></span> | <span data-ttu-id="f5547-338">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-338">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-339">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f5547-339">DXE 5291</span></span> |<span data-ttu-id="f5547-340">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-340">Honda</span></span> |<span data-ttu-id="f5547-341">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-341">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="f5547-342">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="f5547-342">YZK 5704</span></span> |<span data-ttu-id="f5547-343">Ford</span><span class="sxs-lookup"><span data-stu-id="f5547-343">Ford</span></span> |<span data-ttu-id="f5547-344">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-344">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="f5547-345">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="f5547-345">RMV 8282</span></span> |<span data-ttu-id="f5547-346">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-346">Honda</span></span> |<span data-ttu-id="f5547-347">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-347">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-348">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="f5547-348">YHN 6970</span></span> |<span data-ttu-id="f5547-349">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-349">Toyota</span></span> |<span data-ttu-id="f5547-350">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-350">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="f5547-351">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="f5547-351">VFE 1616</span></span> |<span data-ttu-id="f5547-352">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-352">Toyota</span></span> |<span data-ttu-id="f5547-353">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-353">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="f5547-354">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f5547-354">QYF 9358</span></span> |<span data-ttu-id="f5547-355">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-355">Honda</span></span> |<span data-ttu-id="f5547-356">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-356">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-357">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f5547-357">MDR 6128</span></span> |<span data-ttu-id="f5547-358">BMW</span><span class="sxs-lookup"><span data-stu-id="f5547-358">BMW</span></span> |<span data-ttu-id="f5547-359">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-359">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="f5547-360">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-360">**Output**:</span></span>

| <span data-ttu-id="f5547-361">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-361">LicensePlate</span></span> | <span data-ttu-id="f5547-362">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-362">Make</span></span> | <span data-ttu-id="f5547-363">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-363">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-364">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="f5547-364">VFE 1616</span></span> |<span data-ttu-id="f5547-365">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-365">Toyota</span></span> |<span data-ttu-id="f5547-366">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-366">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="f5547-367">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f5547-367">MDR 6128</span></span> |<span data-ttu-id="f5547-368">BMW</span><span class="sxs-lookup"><span data-stu-id="f5547-368">BMW</span></span> |<span data-ttu-id="f5547-369">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-369">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="f5547-370">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-370">**Solution**:</span></span>

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

<span data-ttu-id="f5547-371">**Explanation**: There are two steps in the query.</span><span class="sxs-lookup"><span data-stu-id="f5547-371">**Explanation**: There are two steps in the query.</span></span> <span data-ttu-id="f5547-372">The first one finds the latest time stamp in 10-minute windows.</span><span class="sxs-lookup"><span data-stu-id="f5547-372">The first one finds the latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="f5547-373">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span><span class="sxs-lookup"><span data-stu-id="f5547-373">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="f5547-374">Query example: Detect the absence of events</span><span class="sxs-lookup"><span data-stu-id="f5547-374">Query example: Detect the absence of events</span></span>
<span data-ttu-id="f5547-375">**Description**: Check that a stream has no value that matches a certain criterion.</span><span class="sxs-lookup"><span data-stu-id="f5547-375">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="f5547-376">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span><span class="sxs-lookup"><span data-stu-id="f5547-376">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span></span>

<span data-ttu-id="f5547-377">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-377">**Input**:</span></span>

| <span data-ttu-id="f5547-378">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-378">Make</span></span> | <span data-ttu-id="f5547-379">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-379">LicensePlate</span></span> | <span data-ttu-id="f5547-380">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-380">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-381">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-381">Honda</span></span> |<span data-ttu-id="f5547-382">ABC-123</span><span class="sxs-lookup"><span data-stu-id="f5547-382">ABC-123</span></span> |<span data-ttu-id="f5547-383">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-383">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f5547-384">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-384">Honda</span></span> |<span data-ttu-id="f5547-385">AAA-999</span><span class="sxs-lookup"><span data-stu-id="f5547-385">AAA-999</span></span> |<span data-ttu-id="f5547-386">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-386">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f5547-387">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-387">Toyota</span></span> |<span data-ttu-id="f5547-388">DEF-987</span><span class="sxs-lookup"><span data-stu-id="f5547-388">DEF-987</span></span> |<span data-ttu-id="f5547-389">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-389">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="f5547-390">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-390">Honda</span></span> |<span data-ttu-id="f5547-391">GHI-345</span><span class="sxs-lookup"><span data-stu-id="f5547-391">GHI-345</span></span> |<span data-ttu-id="f5547-392">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-392">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="f5547-393">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-393">**Output**:</span></span>

| <span data-ttu-id="f5547-394">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-394">Make</span></span> | <span data-ttu-id="f5547-395">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-395">Time</span></span> | <span data-ttu-id="f5547-396">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-396">CurrentCarLicensePlate</span></span> | <span data-ttu-id="f5547-397">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-397">FirstCarLicensePlate</span></span> | <span data-ttu-id="f5547-398">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="f5547-398">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f5547-399">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-399">Honda</span></span> |<span data-ttu-id="f5547-400">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-400">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="f5547-401">AAA-999</span><span class="sxs-lookup"><span data-stu-id="f5547-401">AAA-999</span></span> |<span data-ttu-id="f5547-402">ABC-123</span><span class="sxs-lookup"><span data-stu-id="f5547-402">ABC-123</span></span> |<span data-ttu-id="f5547-403">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-403">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="f5547-404">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-404">**Solution**:</span></span>

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

<span data-ttu-id="f5547-405">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span><span class="sxs-lookup"><span data-stu-id="f5547-405">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="f5547-406">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span><span class="sxs-lookup"><span data-stu-id="f5547-406">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span></span> <span data-ttu-id="f5547-407">You can also use **LAG** to get data about the previous car.</span><span class="sxs-lookup"><span data-stu-id="f5547-407">You can also use **LAG** to get data about the previous car.</span></span>

## <a name="query-example-detect-the-duration-between-events"></a><span data-ttu-id="f5547-408">Query example: Detect the duration between events</span><span class="sxs-lookup"><span data-stu-id="f5547-408">Query example: Detect the duration between events</span></span>
<span data-ttu-id="f5547-409">**Description**: Find the duration of a given event.</span><span class="sxs-lookup"><span data-stu-id="f5547-409">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="f5547-410">For example, given a web clickstream, determine the time spent on a feature.</span><span class="sxs-lookup"><span data-stu-id="f5547-410">For example, given a web clickstream, determine the time spent on a feature.</span></span>

<span data-ttu-id="f5547-411">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-411">**Input**:</span></span>  

| <span data-ttu-id="f5547-412">User</span><span class="sxs-lookup"><span data-stu-id="f5547-412">User</span></span> | <span data-ttu-id="f5547-413">Feature</span><span class="sxs-lookup"><span data-stu-id="f5547-413">Feature</span></span> | <span data-ttu-id="f5547-414">Event</span><span class="sxs-lookup"><span data-stu-id="f5547-414">Event</span></span> | <span data-ttu-id="f5547-415">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-415">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="f5547-416">RightMenu</span><span class="sxs-lookup"><span data-stu-id="f5547-416">RightMenu</span></span> |<span data-ttu-id="f5547-417">Start</span><span class="sxs-lookup"><span data-stu-id="f5547-417">Start</span></span> |<span data-ttu-id="f5547-418">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-418">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="f5547-419">RightMenu</span><span class="sxs-lookup"><span data-stu-id="f5547-419">RightMenu</span></span> |<span data-ttu-id="f5547-420">End</span><span class="sxs-lookup"><span data-stu-id="f5547-420">End</span></span> |<span data-ttu-id="f5547-421">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-421">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="f5547-422">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-422">**Output**:</span></span>  

| <span data-ttu-id="f5547-423">User</span><span class="sxs-lookup"><span data-stu-id="f5547-423">User</span></span> | <span data-ttu-id="f5547-424">Feature</span><span class="sxs-lookup"><span data-stu-id="f5547-424">Feature</span></span> | <span data-ttu-id="f5547-425">Duration</span><span class="sxs-lookup"><span data-stu-id="f5547-425">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="f5547-426">RightMenu</span><span class="sxs-lookup"><span data-stu-id="f5547-426">RightMenu</span></span> |<span data-ttu-id="f5547-427">7</span><span class="sxs-lookup"><span data-stu-id="f5547-427">7</span></span> |

<span data-ttu-id="f5547-428">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-428">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="f5547-429">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span><span class="sxs-lookup"><span data-stu-id="f5547-429">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span></span> <span data-ttu-id="f5547-430">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span><span class="sxs-lookup"><span data-stu-id="f5547-430">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span></span> <span data-ttu-id="f5547-431">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="f5547-431">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-the-duration-of-a-condition"></a><span data-ttu-id="f5547-432">Query example: Detect the duration of a condition</span><span class="sxs-lookup"><span data-stu-id="f5547-432">Query example: Detect the duration of a condition</span></span>
<span data-ttu-id="f5547-433">**Description**: Find out how long a condition occurred.</span><span class="sxs-lookup"><span data-stu-id="f5547-433">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="f5547-434">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds), and the duration of that bug must be computed.</span><span class="sxs-lookup"><span data-stu-id="f5547-434">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds), and the duration of that bug must be computed.</span></span>

<span data-ttu-id="f5547-435">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-435">**Input**:</span></span>

| <span data-ttu-id="f5547-436">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-436">Make</span></span> | <span data-ttu-id="f5547-437">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-437">Time</span></span> | <span data-ttu-id="f5547-438">Weight</span><span class="sxs-lookup"><span data-stu-id="f5547-438">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-439">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-439">Honda</span></span> |<span data-ttu-id="f5547-440">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-440">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="f5547-441">2000</span><span class="sxs-lookup"><span data-stu-id="f5547-441">2000</span></span> |
| <span data-ttu-id="f5547-442">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-442">Toyota</span></span> |<span data-ttu-id="f5547-443">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-443">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="f5547-444">25000</span><span class="sxs-lookup"><span data-stu-id="f5547-444">25000</span></span> |
| <span data-ttu-id="f5547-445">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-445">Honda</span></span> |<span data-ttu-id="f5547-446">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-446">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="f5547-447">26000</span><span class="sxs-lookup"><span data-stu-id="f5547-447">26000</span></span> |
| <span data-ttu-id="f5547-448">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-448">Toyota</span></span> |<span data-ttu-id="f5547-449">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-449">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="f5547-450">25000</span><span class="sxs-lookup"><span data-stu-id="f5547-450">25000</span></span> |
| <span data-ttu-id="f5547-451">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-451">Honda</span></span> |<span data-ttu-id="f5547-452">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-452">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="f5547-453">26000</span><span class="sxs-lookup"><span data-stu-id="f5547-453">26000</span></span> |
| <span data-ttu-id="f5547-454">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-454">Toyota</span></span> |<span data-ttu-id="f5547-455">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-455">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="f5547-456">25000</span><span class="sxs-lookup"><span data-stu-id="f5547-456">25000</span></span> |
| <span data-ttu-id="f5547-457">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-457">Honda</span></span> |<span data-ttu-id="f5547-458">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-458">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="f5547-459">26000</span><span class="sxs-lookup"><span data-stu-id="f5547-459">26000</span></span> |
| <span data-ttu-id="f5547-460">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-460">Toyota</span></span> |<span data-ttu-id="f5547-461">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-461">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="f5547-462">2000</span><span class="sxs-lookup"><span data-stu-id="f5547-462">2000</span></span> |

<span data-ttu-id="f5547-463">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-463">**Output**:</span></span>

| <span data-ttu-id="f5547-464">StartFault</span><span class="sxs-lookup"><span data-stu-id="f5547-464">StartFault</span></span> | <span data-ttu-id="f5547-465">EndFault</span><span class="sxs-lookup"><span data-stu-id="f5547-465">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-466">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-466">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="f5547-467">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-467">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="f5547-468">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-468">**Solution**:</span></span>

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

<span data-ttu-id="f5547-469">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span><span class="sxs-lookup"><span data-stu-id="f5547-469">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="f5547-470">Query example: Fill missing values</span><span class="sxs-lookup"><span data-stu-id="f5547-470">Query example: Fill missing values</span></span>
<span data-ttu-id="f5547-471">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span><span class="sxs-lookup"><span data-stu-id="f5547-471">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="f5547-472">For example, generate an event every 5 seconds that reports the most recently seen data point.</span><span class="sxs-lookup"><span data-stu-id="f5547-472">For example, generate an event every 5 seconds that reports the most recently seen data point.</span></span>

<span data-ttu-id="f5547-473">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-473">**Input**:</span></span>

| <span data-ttu-id="f5547-474">t</span><span class="sxs-lookup"><span data-stu-id="f5547-474">t</span></span> | <span data-ttu-id="f5547-475">value</span><span class="sxs-lookup"><span data-stu-id="f5547-475">value</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-476">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-476">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="f5547-477">1</span><span class="sxs-lookup"><span data-stu-id="f5547-477">1</span></span> |
| <span data-ttu-id="f5547-478">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="f5547-478">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="f5547-479">2</span><span class="sxs-lookup"><span data-stu-id="f5547-479">2</span></span> |
| <span data-ttu-id="f5547-480">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="f5547-480">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="f5547-481">3</span><span class="sxs-lookup"><span data-stu-id="f5547-481">3</span></span> |
| <span data-ttu-id="f5547-482">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="f5547-482">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="f5547-483">4</span><span class="sxs-lookup"><span data-stu-id="f5547-483">4</span></span> |
| <span data-ttu-id="f5547-484">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="f5547-484">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="f5547-485">5</span><span class="sxs-lookup"><span data-stu-id="f5547-485">5</span></span> |
| <span data-ttu-id="f5547-486">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="f5547-486">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="f5547-487">6</span><span class="sxs-lookup"><span data-stu-id="f5547-487">6</span></span> |

<span data-ttu-id="f5547-488">**Output (first 10 rows)**:</span><span class="sxs-lookup"><span data-stu-id="f5547-488">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="f5547-489">windowend</span><span class="sxs-lookup"><span data-stu-id="f5547-489">windowend</span></span> | <span data-ttu-id="f5547-490">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="f5547-490">lastevent.t</span></span> | <span data-ttu-id="f5547-491">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="f5547-491">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5547-492">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-492">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="f5547-493">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-493">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="f5547-494">1</span><span class="sxs-lookup"><span data-stu-id="f5547-494">1</span></span> |
| <span data-ttu-id="f5547-495">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-495">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="f5547-496">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-496">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="f5547-497">2</span><span class="sxs-lookup"><span data-stu-id="f5547-497">2</span></span> |
| <span data-ttu-id="f5547-498">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-498">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="f5547-499">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-499">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="f5547-500">3</span><span class="sxs-lookup"><span data-stu-id="f5547-500">3</span></span> |
| <span data-ttu-id="f5547-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="f5547-502">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-502">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="f5547-503">4</span><span class="sxs-lookup"><span data-stu-id="f5547-503">4</span></span> |
| <span data-ttu-id="f5547-504">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-504">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="f5547-505">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-505">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="f5547-506">4</span><span class="sxs-lookup"><span data-stu-id="f5547-506">4</span></span> |
| <span data-ttu-id="f5547-507">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-507">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="f5547-508">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-508">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="f5547-509">4</span><span class="sxs-lookup"><span data-stu-id="f5547-509">4</span></span> |
| <span data-ttu-id="f5547-510">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-510">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="f5547-511">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-511">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="f5547-512">5</span><span class="sxs-lookup"><span data-stu-id="f5547-512">5</span></span> |
| <span data-ttu-id="f5547-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="f5547-514">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-514">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="f5547-515">6</span><span class="sxs-lookup"><span data-stu-id="f5547-515">6</span></span> |
| <span data-ttu-id="f5547-516">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-516">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="f5547-517">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-517">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="f5547-518">6</span><span class="sxs-lookup"><span data-stu-id="f5547-518">6</span></span> |
| <span data-ttu-id="f5547-519">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-519">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="f5547-520">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-520">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="f5547-521">6</span><span class="sxs-lookup"><span data-stu-id="f5547-521">6</span></span> |

<span data-ttu-id="f5547-522">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-522">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="f5547-523">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span><span class="sxs-lookup"><span data-stu-id="f5547-523">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span></span> <span data-ttu-id="f5547-524">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span><span class="sxs-lookup"><span data-stu-id="f5547-524">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span></span>


## <a name="query-example-correlate-two-event-types-within-the-same-stream"></a><span data-ttu-id="f5547-525">Query example: Correlate two event types within the same stream</span><span class="sxs-lookup"><span data-stu-id="f5547-525">Query example: Correlate two event types within the same stream</span></span>
<span data-ttu-id="f5547-526">**Description**: Sometimes alerts need to be generated based on multiple event types that occurred in a certain time range.</span><span class="sxs-lookup"><span data-stu-id="f5547-526">**Description**: Sometimes alerts need to be generated based on multiple event types that occurred in a certain time range.</span></span>
<span data-ttu-id="f5547-527">For example, in an IoT scenario for home ovens, an alert must be generated when the fan temperature is less than 40 and the maximum power during the last 3 minutes is less than 10.</span><span class="sxs-lookup"><span data-stu-id="f5547-527">For example, in an IoT scenario for home ovens, an alert must be generated when the fan temperature is less than 40 and the maximum power during the last 3 minutes is less than 10.</span></span>

<span data-ttu-id="f5547-528">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-528">**Input**:</span></span>

| <span data-ttu-id="f5547-529">time</span><span class="sxs-lookup"><span data-stu-id="f5547-529">time</span></span> | <span data-ttu-id="f5547-530">deviceId</span><span class="sxs-lookup"><span data-stu-id="f5547-530">deviceId</span></span> | <span data-ttu-id="f5547-531">sensorName</span><span class="sxs-lookup"><span data-stu-id="f5547-531">sensorName</span></span> | <span data-ttu-id="f5547-532">value</span><span class="sxs-lookup"><span data-stu-id="f5547-532">value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f5547-533">"2018-01-01T16:01:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-533">"2018-01-01T16:01:00"</span></span> | <span data-ttu-id="f5547-534">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-534">"Oven1"</span></span> | <span data-ttu-id="f5547-535">"temp"</span><span class="sxs-lookup"><span data-stu-id="f5547-535">"temp"</span></span> |<span data-ttu-id="f5547-536">120</span><span class="sxs-lookup"><span data-stu-id="f5547-536">120</span></span> |
| <span data-ttu-id="f5547-537">"2018-01-01T16:01:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-537">"2018-01-01T16:01:00"</span></span> | <span data-ttu-id="f5547-538">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-538">"Oven1"</span></span> | <span data-ttu-id="f5547-539">"power"</span><span class="sxs-lookup"><span data-stu-id="f5547-539">"power"</span></span> |<span data-ttu-id="f5547-540">15</span><span class="sxs-lookup"><span data-stu-id="f5547-540">15</span></span> |
| <span data-ttu-id="f5547-541">"2018-01-01T16:02:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-541">"2018-01-01T16:02:00"</span></span> | <span data-ttu-id="f5547-542">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-542">"Oven1"</span></span> | <span data-ttu-id="f5547-543">"temp"</span><span class="sxs-lookup"><span data-stu-id="f5547-543">"temp"</span></span> |<span data-ttu-id="f5547-544">100</span><span class="sxs-lookup"><span data-stu-id="f5547-544">100</span></span> |
| <span data-ttu-id="f5547-545">"2018-01-01T16:02:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-545">"2018-01-01T16:02:00"</span></span> | <span data-ttu-id="f5547-546">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-546">"Oven1"</span></span> | <span data-ttu-id="f5547-547">"power"</span><span class="sxs-lookup"><span data-stu-id="f5547-547">"power"</span></span> |<span data-ttu-id="f5547-548">15</span><span class="sxs-lookup"><span data-stu-id="f5547-548">15</span></span> |
| <span data-ttu-id="f5547-549">"2018-01-01T16:03:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-549">"2018-01-01T16:03:00"</span></span> | <span data-ttu-id="f5547-550">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-550">"Oven1"</span></span> | <span data-ttu-id="f5547-551">"temp"</span><span class="sxs-lookup"><span data-stu-id="f5547-551">"temp"</span></span> |<span data-ttu-id="f5547-552">70</span><span class="sxs-lookup"><span data-stu-id="f5547-552">70</span></span> |
| <span data-ttu-id="f5547-553">"2018-01-01T16:03:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-553">"2018-01-01T16:03:00"</span></span> | <span data-ttu-id="f5547-554">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-554">"Oven1"</span></span> | <span data-ttu-id="f5547-555">"power"</span><span class="sxs-lookup"><span data-stu-id="f5547-555">"power"</span></span> |<span data-ttu-id="f5547-556">15</span><span class="sxs-lookup"><span data-stu-id="f5547-556">15</span></span> |
| <span data-ttu-id="f5547-557">"2018-01-01T16:04:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-557">"2018-01-01T16:04:00"</span></span> | <span data-ttu-id="f5547-558">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-558">"Oven1"</span></span> | <span data-ttu-id="f5547-559">"temp"</span><span class="sxs-lookup"><span data-stu-id="f5547-559">"temp"</span></span> |<span data-ttu-id="f5547-560">50</span><span class="sxs-lookup"><span data-stu-id="f5547-560">50</span></span> |
| <span data-ttu-id="f5547-561">"2018-01-01T16:04:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-561">"2018-01-01T16:04:00"</span></span> | <span data-ttu-id="f5547-562">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-562">"Oven1"</span></span> | <span data-ttu-id="f5547-563">"power"</span><span class="sxs-lookup"><span data-stu-id="f5547-563">"power"</span></span> |<span data-ttu-id="f5547-564">15</span><span class="sxs-lookup"><span data-stu-id="f5547-564">15</span></span> |
| <span data-ttu-id="f5547-565">"2018-01-01T16:05:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-565">"2018-01-01T16:05:00"</span></span> | <span data-ttu-id="f5547-566">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-566">"Oven1"</span></span> | <span data-ttu-id="f5547-567">"temp"</span><span class="sxs-lookup"><span data-stu-id="f5547-567">"temp"</span></span> |<span data-ttu-id="f5547-568">30</span><span class="sxs-lookup"><span data-stu-id="f5547-568">30</span></span> |
| <span data-ttu-id="f5547-569">"2018-01-01T16:05:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-569">"2018-01-01T16:05:00"</span></span> | <span data-ttu-id="f5547-570">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-570">"Oven1"</span></span> | <span data-ttu-id="f5547-571">"power"</span><span class="sxs-lookup"><span data-stu-id="f5547-571">"power"</span></span> |<span data-ttu-id="f5547-572">8</span><span class="sxs-lookup"><span data-stu-id="f5547-572">8</span></span> |
| <span data-ttu-id="f5547-573">"2018-01-01T16:06:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-573">"2018-01-01T16:06:00"</span></span> | <span data-ttu-id="f5547-574">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-574">"Oven1"</span></span> | <span data-ttu-id="f5547-575">"temp"</span><span class="sxs-lookup"><span data-stu-id="f5547-575">"temp"</span></span> |<span data-ttu-id="f5547-576">20</span><span class="sxs-lookup"><span data-stu-id="f5547-576">20</span></span> |
| <span data-ttu-id="f5547-577">"2018-01-01T16:06:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-577">"2018-01-01T16:06:00"</span></span> | <span data-ttu-id="f5547-578">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-578">"Oven1"</span></span> | <span data-ttu-id="f5547-579">"power"</span><span class="sxs-lookup"><span data-stu-id="f5547-579">"power"</span></span> |<span data-ttu-id="f5547-580">8</span><span class="sxs-lookup"><span data-stu-id="f5547-580">8</span></span> |
| <span data-ttu-id="f5547-581">"2018-01-01T16:07:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-581">"2018-01-01T16:07:00"</span></span> | <span data-ttu-id="f5547-582">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-582">"Oven1"</span></span> | <span data-ttu-id="f5547-583">"temp"</span><span class="sxs-lookup"><span data-stu-id="f5547-583">"temp"</span></span> |<span data-ttu-id="f5547-584">20</span><span class="sxs-lookup"><span data-stu-id="f5547-584">20</span></span> |
| <span data-ttu-id="f5547-585">"2018-01-01T16:07:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-585">"2018-01-01T16:07:00"</span></span> | <span data-ttu-id="f5547-586">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-586">"Oven1"</span></span> | <span data-ttu-id="f5547-587">"power"</span><span class="sxs-lookup"><span data-stu-id="f5547-587">"power"</span></span> |<span data-ttu-id="f5547-588">8</span><span class="sxs-lookup"><span data-stu-id="f5547-588">8</span></span> |
| <span data-ttu-id="f5547-589">"2018-01-01T16:08:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-589">"2018-01-01T16:08:00"</span></span> | <span data-ttu-id="f5547-590">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-590">"Oven1"</span></span> | <span data-ttu-id="f5547-591">"temp"</span><span class="sxs-lookup"><span data-stu-id="f5547-591">"temp"</span></span> |<span data-ttu-id="f5547-592">20</span><span class="sxs-lookup"><span data-stu-id="f5547-592">20</span></span> |
| <span data-ttu-id="f5547-593">"2018-01-01T16:08:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-593">"2018-01-01T16:08:00"</span></span> | <span data-ttu-id="f5547-594">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-594">"Oven1"</span></span> | <span data-ttu-id="f5547-595">"power"</span><span class="sxs-lookup"><span data-stu-id="f5547-595">"power"</span></span> |<span data-ttu-id="f5547-596">8</span><span class="sxs-lookup"><span data-stu-id="f5547-596">8</span></span> |

<span data-ttu-id="f5547-597">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-597">**Output**:</span></span>

| <span data-ttu-id="f5547-598">eventTime</span><span class="sxs-lookup"><span data-stu-id="f5547-598">eventTime</span></span> | <span data-ttu-id="f5547-599">deviceId</span><span class="sxs-lookup"><span data-stu-id="f5547-599">deviceId</span></span> | <span data-ttu-id="f5547-600">temp</span><span class="sxs-lookup"><span data-stu-id="f5547-600">temp</span></span> | <span data-ttu-id="f5547-601">alertMessage</span><span class="sxs-lookup"><span data-stu-id="f5547-601">alertMessage</span></span> | <span data-ttu-id="f5547-602">maxPowerDuringLast3mins</span><span class="sxs-lookup"><span data-stu-id="f5547-602">maxPowerDuringLast3mins</span></span> |
| --- | --- | --- | --- | --- | 
| <span data-ttu-id="f5547-603">"2018-01-01T16:05:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-603">"2018-01-01T16:05:00"</span></span> | <span data-ttu-id="f5547-604">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-604">"Oven1"</span></span> |<span data-ttu-id="f5547-605">30</span><span class="sxs-lookup"><span data-stu-id="f5547-605">30</span></span> | <span data-ttu-id="f5547-606">"Short circuit heating elements"</span><span class="sxs-lookup"><span data-stu-id="f5547-606">"Short circuit heating elements"</span></span> |<span data-ttu-id="f5547-607">15</span><span class="sxs-lookup"><span data-stu-id="f5547-607">15</span></span> |
| <span data-ttu-id="f5547-608">"2018-01-01T16:06:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-608">"2018-01-01T16:06:00"</span></span> | <span data-ttu-id="f5547-609">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-609">"Oven1"</span></span> |<span data-ttu-id="f5547-610">20</span><span class="sxs-lookup"><span data-stu-id="f5547-610">20</span></span> | <span data-ttu-id="f5547-611">"Short circuit heating elements"</span><span class="sxs-lookup"><span data-stu-id="f5547-611">"Short circuit heating elements"</span></span> |<span data-ttu-id="f5547-612">15</span><span class="sxs-lookup"><span data-stu-id="f5547-612">15</span></span> |
| <span data-ttu-id="f5547-613">"2018-01-01T16:07:00"</span><span class="sxs-lookup"><span data-stu-id="f5547-613">"2018-01-01T16:07:00"</span></span> | <span data-ttu-id="f5547-614">"Oven1"</span><span class="sxs-lookup"><span data-stu-id="f5547-614">"Oven1"</span></span> |<span data-ttu-id="f5547-615">20</span><span class="sxs-lookup"><span data-stu-id="f5547-615">20</span></span> | <span data-ttu-id="f5547-616">"Short circuit heating elements"</span><span class="sxs-lookup"><span data-stu-id="f5547-616">"Short circuit heating elements"</span></span> |<span data-ttu-id="f5547-617">15</span><span class="sxs-lookup"><span data-stu-id="f5547-617">15</span></span> |

<span data-ttu-id="f5547-618">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-618">**Solution**:</span></span>

````
WITH max_power_during_last_3_mins AS (
    SELECT 
        System.TimeStamp AS windowTime,
        deviceId,
        max(value) as maxPower
    FROM
        input TIMESTAMP BY t
    WHERE 
        sensorName = 'power' 
    GROUP BY 
        deviceId, 
        SlidingWindow(minute, 3) 
)

SELECT 
    t1.t AS eventTime,
    t1.deviceId, 
    t1.value AS temp,
    'Short circuit heating elements' as alertMessage,
    t2.maxPower AS maxPowerDuringLast3mins
    
INTO resultsr

FROM input t1 TIMESTAMP BY t
JOIN max_power_during_last_3_mins t2
    ON t1.deviceId = t2.deviceId 
    AND t1.t = t2.windowTime
    AND DATEDIFF(minute,t1,t2) between 0 and 3
    
WHERE
    t1.sensorName = 'temp'
    AND t1.value <= 40
    AND t2.maxPower > 10
````

<span data-ttu-id="f5547-619">**Explanation**: The first query `max_power_during_last_3_mins`, uses the [Sliding window](https://msdn.microsoft.com/azure/stream-analytics/reference/sliding-window-azure-stream-analytics) to find the max value of the power sensor for every device, during the last 3 minutes.</span><span class="sxs-lookup"><span data-stu-id="f5547-619">**Explanation**: The first query `max_power_during_last_3_mins`, uses the [Sliding window](https://msdn.microsoft.com/azure/stream-analytics/reference/sliding-window-azure-stream-analytics) to find the max value of the power sensor for every device, during the last 3 minutes.</span></span> <span data-ttu-id="f5547-620">The second query is joined to the first query to find the power value in the most recent window relevant for the current event.</span><span class="sxs-lookup"><span data-stu-id="f5547-620">The second query is joined to the first query to find the power value in the most recent window relevant for the current event.</span></span> <span data-ttu-id="f5547-621">And then, provided the conditions are met, an alert is generated for the device.</span><span class="sxs-lookup"><span data-stu-id="f5547-621">And then, provided the conditions are met, an alert is generated for the device.</span></span>

## <a name="query-example-process-events-independent-of-device-clock-skew-substreams"></a><span data-ttu-id="f5547-622">Query example: Process events independent of Device Clock Skew (substreams)</span><span class="sxs-lookup"><span data-stu-id="f5547-622">Query example: Process events independent of Device Clock Skew (substreams)</span></span>
<span data-ttu-id="f5547-623">**Description**: Events can arrive late or out of order due to clock skews between event producers, clock skews between partitions, or network latency.</span><span class="sxs-lookup"><span data-stu-id="f5547-623">**Description**: Events can arrive late or out of order due to clock skews between event producers, clock skews between partitions, or network latency.</span></span> <span data-ttu-id="f5547-624">In the following example, the device clock for TollID 2 is ten seconds behind TollID 1, and the device clock for TollID 3 is five seconds behind TollID 1.</span><span class="sxs-lookup"><span data-stu-id="f5547-624">In the following example, the device clock for TollID 2 is ten seconds behind TollID 1, and the device clock for TollID 3 is five seconds behind TollID 1.</span></span> 


<span data-ttu-id="f5547-625">**Input**:</span><span class="sxs-lookup"><span data-stu-id="f5547-625">**Input**:</span></span>
| <span data-ttu-id="f5547-626">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f5547-626">LicensePlate</span></span> | <span data-ttu-id="f5547-627">Make</span><span class="sxs-lookup"><span data-stu-id="f5547-627">Make</span></span> | <span data-ttu-id="f5547-628">Time</span><span class="sxs-lookup"><span data-stu-id="f5547-628">Time</span></span> | <span data-ttu-id="f5547-629">TollID</span><span class="sxs-lookup"><span data-stu-id="f5547-629">TollID</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f5547-630">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f5547-630">DXE 5291</span></span> |<span data-ttu-id="f5547-631">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-631">Honda</span></span> |<span data-ttu-id="f5547-632">2015-07-27T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-632">2015-07-27T00:00:01.0000000Z</span></span> | <span data-ttu-id="f5547-633">1</span><span class="sxs-lookup"><span data-stu-id="f5547-633">1</span></span> |
| <span data-ttu-id="f5547-634">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="f5547-634">YHN 6970</span></span> |<span data-ttu-id="f5547-635">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-635">Toyota</span></span> |<span data-ttu-id="f5547-636">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-636">2015-07-27T00:00:05.0000000Z</span></span> | <span data-ttu-id="f5547-637">1</span><span class="sxs-lookup"><span data-stu-id="f5547-637">1</span></span> |
| <span data-ttu-id="f5547-638">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f5547-638">QYF 9358</span></span> |<span data-ttu-id="f5547-639">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-639">Honda</span></span> |<span data-ttu-id="f5547-640">2015-07-27T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-640">2015-07-27T00:00:01.0000000Z</span></span> | <span data-ttu-id="f5547-641">2</span><span class="sxs-lookup"><span data-stu-id="f5547-641">2</span></span> |
| <span data-ttu-id="f5547-642">GXF 9462</span><span class="sxs-lookup"><span data-stu-id="f5547-642">GXF 9462</span></span> |<span data-ttu-id="f5547-643">BMW</span><span class="sxs-lookup"><span data-stu-id="f5547-643">BMW</span></span> |<span data-ttu-id="f5547-644">2015-07-27T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-644">2015-07-27T00:00:04.0000000Z</span></span> | <span data-ttu-id="f5547-645">2</span><span class="sxs-lookup"><span data-stu-id="f5547-645">2</span></span> |
| <span data-ttu-id="f5547-646">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="f5547-646">VFE 1616</span></span> |<span data-ttu-id="f5547-647">Toyota</span><span class="sxs-lookup"><span data-stu-id="f5547-647">Toyota</span></span> |<span data-ttu-id="f5547-648">2015-07-27T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-648">2015-07-27T00:00:10.0000000Z</span></span> | <span data-ttu-id="f5547-649">1</span><span class="sxs-lookup"><span data-stu-id="f5547-649">1</span></span> |
| <span data-ttu-id="f5547-650">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="f5547-650">RMV 8282</span></span> |<span data-ttu-id="f5547-651">Honda</span><span class="sxs-lookup"><span data-stu-id="f5547-651">Honda</span></span> |<span data-ttu-id="f5547-652">2015-07-27T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-652">2015-07-27T00:00:03.0000000Z</span></span> | <span data-ttu-id="f5547-653">3</span><span class="sxs-lookup"><span data-stu-id="f5547-653">3</span></span> |
| <span data-ttu-id="f5547-654">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f5547-654">MDR 6128</span></span> |<span data-ttu-id="f5547-655">BMW</span><span class="sxs-lookup"><span data-stu-id="f5547-655">BMW</span></span> |<span data-ttu-id="f5547-656">2015-07-27T00:00:11.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-656">2015-07-27T00:00:11.0000000Z</span></span> | <span data-ttu-id="f5547-657">2</span><span class="sxs-lookup"><span data-stu-id="f5547-657">2</span></span> |
| <span data-ttu-id="f5547-658">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="f5547-658">YZK 5704</span></span> |<span data-ttu-id="f5547-659">Ford</span><span class="sxs-lookup"><span data-stu-id="f5547-659">Ford</span></span> |<span data-ttu-id="f5547-660">2015-07-27T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f5547-660">2015-07-27T00:00:07.0000000Z</span></span> | <span data-ttu-id="f5547-661">3</span><span class="sxs-lookup"><span data-stu-id="f5547-661">3</span></span> |

<span data-ttu-id="f5547-662">**Output**:</span><span class="sxs-lookup"><span data-stu-id="f5547-662">**Output**:</span></span>
| <span data-ttu-id="f5547-663">TollID</span><span class="sxs-lookup"><span data-stu-id="f5547-663">TollID</span></span> | <span data-ttu-id="f5547-664">Count</span><span class="sxs-lookup"><span data-stu-id="f5547-664">Count</span></span> |
| --- | --- |
| <span data-ttu-id="f5547-665">1</span><span class="sxs-lookup"><span data-stu-id="f5547-665">1</span></span> | <span data-ttu-id="f5547-666">2</span><span class="sxs-lookup"><span data-stu-id="f5547-666">2</span></span> |
| <span data-ttu-id="f5547-667">2</span><span class="sxs-lookup"><span data-stu-id="f5547-667">2</span></span> | <span data-ttu-id="f5547-668">2</span><span class="sxs-lookup"><span data-stu-id="f5547-668">2</span></span> |
| <span data-ttu-id="f5547-669">1</span><span class="sxs-lookup"><span data-stu-id="f5547-669">1</span></span> | <span data-ttu-id="f5547-670">1</span><span class="sxs-lookup"><span data-stu-id="f5547-670">1</span></span> |
| <span data-ttu-id="f5547-671">3</span><span class="sxs-lookup"><span data-stu-id="f5547-671">3</span></span> | <span data-ttu-id="f5547-672">1</span><span class="sxs-lookup"><span data-stu-id="f5547-672">1</span></span> |
| <span data-ttu-id="f5547-673">2</span><span class="sxs-lookup"><span data-stu-id="f5547-673">2</span></span> | <span data-ttu-id="f5547-674">1</span><span class="sxs-lookup"><span data-stu-id="f5547-674">1</span></span> |
| <span data-ttu-id="f5547-675">3</span><span class="sxs-lookup"><span data-stu-id="f5547-675">3</span></span> | <span data-ttu-id="f5547-676">1</span><span class="sxs-lookup"><span data-stu-id="f5547-676">1</span></span> |

<span data-ttu-id="f5547-677">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="f5547-677">**Solution**:</span></span>

````
SELECT
      TollId,
      COUNT(*) AS Count
FROM input
      TIMESTAMP BY Time OVER TollId
GROUP BY TUMBLINGWINDOW(second, 5), TollId

````

<span data-ttu-id="f5547-678">**Explanation**: The [TIMESTAMP BY OVER](https://msdn.microsoft.com/azure/stream-analytics/reference/timestamp-by-azure-stream-analytics#over-clause-interacts-with-event-ordering) clause looks at each device timeline separately using substreams.</span><span class="sxs-lookup"><span data-stu-id="f5547-678">**Explanation**: The [TIMESTAMP BY OVER](https://msdn.microsoft.com/azure/stream-analytics/reference/timestamp-by-azure-stream-analytics#over-clause-interacts-with-event-ordering) clause looks at each device timeline separately using substreams.</span></span> <span data-ttu-id="f5547-679">The output events for each TollID are generated as they are computed, meaning that the events are in order with respect to each TollID instead of being reordered as if all devices were on the same clock.</span><span class="sxs-lookup"><span data-stu-id="f5547-679">The output events for each TollID are generated as they are computed, meaning that the events are in order with respect to each TollID instead of being reordered as if all devices were on the same clock.</span></span>


## <a name="get-help"></a><span data-ttu-id="f5547-680">Get help</span><span class="sxs-lookup"><span data-stu-id="f5547-680">Get help</span></span>
<span data-ttu-id="f5547-681">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f5547-681">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5547-682">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5547-682">Next steps</span></span>
* [<span data-ttu-id="f5547-683">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f5547-683">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f5547-684">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f5547-684">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f5547-685">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="f5547-685">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f5547-686">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="f5547-686">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f5547-687">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="f5547-687">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

