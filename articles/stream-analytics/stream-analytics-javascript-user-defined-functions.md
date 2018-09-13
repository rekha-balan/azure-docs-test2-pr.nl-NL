---
title: Azure Stream Analytics JavaScript user-defined functions | Microsoft Docs
description: Perform advanced query mechanics with JavaScript user-defined functions
keywords: javascript, user defined functions, udf
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: ''
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 02733c4561e2bd4e6412d69ed1118af0758f05f9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663098"
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="6bf81-104">Azure Stream Analytics JavaScript user-defined functions</span><span class="sxs-lookup"><span data-stu-id="6bf81-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="6bf81-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6bf81-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="6bf81-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span><span class="sxs-lookup"><span data-stu-id="6bf81-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="6bf81-107">JavaScript user-defined functions</span><span class="sxs-lookup"><span data-stu-id="6bf81-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="6bf81-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span><span class="sxs-lookup"><span data-stu-id="6bf81-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="6bf81-109">The return value of a function can only be a scalar (single) value.</span><span class="sxs-lookup"><span data-stu-id="6bf81-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="6bf81-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span><span class="sxs-lookup"><span data-stu-id="6bf81-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="6bf81-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span><span class="sxs-lookup"><span data-stu-id="6bf81-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="6bf81-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="6bf81-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="6bf81-113">Decoding and encoding data, for example, binary-to-hex conversion</span><span class="sxs-lookup"><span data-stu-id="6bf81-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="6bf81-114">Performing mathematic computations with JavaScript **Math** functions</span><span class="sxs-lookup"><span data-stu-id="6bf81-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="6bf81-115">Performing array operations like sort, join, find, and fill</span><span class="sxs-lookup"><span data-stu-id="6bf81-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="6bf81-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="6bf81-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="6bf81-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span><span class="sxs-lookup"><span data-stu-id="6bf81-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="6bf81-118">Perform custom event format serialization or deserialization on inputs/outputs</span><span class="sxs-lookup"><span data-stu-id="6bf81-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="6bf81-119">Create custom aggregates</span><span class="sxs-lookup"><span data-stu-id="6bf81-119">Create custom aggregates</span></span>

<span data-ttu-id="6bf81-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span><span class="sxs-lookup"><span data-stu-id="6bf81-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="6bf81-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span><span class="sxs-lookup"><span data-stu-id="6bf81-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="6bf81-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span><span class="sxs-lookup"><span data-stu-id="6bf81-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="6bf81-123">Add a JavaScript user-defined function in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6bf81-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="6bf81-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span><span class="sxs-lookup"><span data-stu-id="6bf81-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="6bf81-125">In the Azure portal, find your Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="6bf81-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="6bf81-126">Under **JOB TOPOLOGY**, select your function.</span><span class="sxs-lookup"><span data-stu-id="6bf81-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="6bf81-127">An empty list of functions appears.</span><span class="sxs-lookup"><span data-stu-id="6bf81-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="6bf81-128">To create a new user-defined function, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6bf81-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="6bf81-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="6bf81-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="6bf81-130">A default function template appears in the editor.</span><span class="sxs-lookup"><span data-stu-id="6bf81-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="6bf81-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span><span class="sxs-lookup"><span data-stu-id="6bf81-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="6bf81-132">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6bf81-132">Select **Save**.</span></span> <span data-ttu-id="6bf81-133">Your function appears in the list of functions.</span><span class="sxs-lookup"><span data-stu-id="6bf81-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="6bf81-134">Select the new **hex2Int** function, and check the function definition.</span><span class="sxs-lookup"><span data-stu-id="6bf81-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="6bf81-135">All functions have a **UDF** prefix added to the function alias.</span><span class="sxs-lookup"><span data-stu-id="6bf81-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="6bf81-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span><span class="sxs-lookup"><span data-stu-id="6bf81-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="6bf81-137">In this case, you call **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="6bf81-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="6bf81-138">Call a JavaScript user-defined function in a query</span><span class="sxs-lookup"><span data-stu-id="6bf81-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="6bf81-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span><span class="sxs-lookup"><span data-stu-id="6bf81-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="6bf81-140">Edit your query, and then call the user-defined function, like this:</span><span class="sxs-lookup"><span data-stu-id="6bf81-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="6bf81-141">To upload the sample data file, right-click the job input.</span><span class="sxs-lookup"><span data-stu-id="6bf81-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="6bf81-142">To test your query, select **Test**.</span><span class="sxs-lookup"><span data-stu-id="6bf81-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="6bf81-143">Supported JavaScript objects</span><span class="sxs-lookup"><span data-stu-id="6bf81-143">Supported JavaScript objects</span></span>
<span data-ttu-id="6bf81-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span><span class="sxs-lookup"><span data-stu-id="6bf81-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="6bf81-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="6bf81-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="6bf81-146">Stream Analytics and JavaScript type conversion</span><span class="sxs-lookup"><span data-stu-id="6bf81-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="6bf81-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span><span class="sxs-lookup"><span data-stu-id="6bf81-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="6bf81-148">This table lists the conversion mappings between the two:</span><span class="sxs-lookup"><span data-stu-id="6bf81-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="6bf81-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6bf81-149">Stream Analytics</span></span> | <span data-ttu-id="6bf81-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6bf81-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="6bf81-151">bigint</span><span class="sxs-lookup"><span data-stu-id="6bf81-151">bigint</span></span> | <span data-ttu-id="6bf81-152">Number (JavaScript can only represent integers up to precisely 2^53)</span><span class="sxs-lookup"><span data-stu-id="6bf81-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="6bf81-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="6bf81-153">DateTime</span></span> | <span data-ttu-id="6bf81-154">Date (JavaScript only supports milliseconds)</span><span class="sxs-lookup"><span data-stu-id="6bf81-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="6bf81-155">double</span><span class="sxs-lookup"><span data-stu-id="6bf81-155">double</span></span> | <span data-ttu-id="6bf81-156">Number</span><span class="sxs-lookup"><span data-stu-id="6bf81-156">Number</span></span>
<span data-ttu-id="6bf81-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="6bf81-157">nvarchar(MAX)</span></span> | <span data-ttu-id="6bf81-158">String</span><span class="sxs-lookup"><span data-stu-id="6bf81-158">String</span></span>
<span data-ttu-id="6bf81-159">Record</span><span class="sxs-lookup"><span data-stu-id="6bf81-159">Record</span></span> | <span data-ttu-id="6bf81-160">Object</span><span class="sxs-lookup"><span data-stu-id="6bf81-160">Object</span></span>
<span data-ttu-id="6bf81-161">Array</span><span class="sxs-lookup"><span data-stu-id="6bf81-161">Array</span></span> | <span data-ttu-id="6bf81-162">Array</span><span class="sxs-lookup"><span data-stu-id="6bf81-162">Array</span></span>
<span data-ttu-id="6bf81-163">NULL</span><span class="sxs-lookup"><span data-stu-id="6bf81-163">NULL</span></span> | <span data-ttu-id="6bf81-164">Null</span><span class="sxs-lookup"><span data-stu-id="6bf81-164">Null</span></span>


<span data-ttu-id="6bf81-165">Here are JavaScript-to-Stream Analytics conversions:</span><span class="sxs-lookup"><span data-stu-id="6bf81-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="6bf81-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6bf81-166">JavaScript</span></span> | <span data-ttu-id="6bf81-167">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6bf81-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="6bf81-168">Number</span><span class="sxs-lookup"><span data-stu-id="6bf81-168">Number</span></span> | <span data-ttu-id="6bf81-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span><span class="sxs-lookup"><span data-stu-id="6bf81-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="6bf81-170">Date</span><span class="sxs-lookup"><span data-stu-id="6bf81-170">Date</span></span> | <span data-ttu-id="6bf81-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="6bf81-171">DateTime</span></span>
<span data-ttu-id="6bf81-172">String</span><span class="sxs-lookup"><span data-stu-id="6bf81-172">String</span></span> | <span data-ttu-id="6bf81-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="6bf81-173">nvarchar(MAX)</span></span>
<span data-ttu-id="6bf81-174">Object</span><span class="sxs-lookup"><span data-stu-id="6bf81-174">Object</span></span> | <span data-ttu-id="6bf81-175">Record</span><span class="sxs-lookup"><span data-stu-id="6bf81-175">Record</span></span>
<span data-ttu-id="6bf81-176">Array</span><span class="sxs-lookup"><span data-stu-id="6bf81-176">Array</span></span> | <span data-ttu-id="6bf81-177">Array</span><span class="sxs-lookup"><span data-stu-id="6bf81-177">Array</span></span>
<span data-ttu-id="6bf81-178">Null, Undefined</span><span class="sxs-lookup"><span data-stu-id="6bf81-178">Null, Undefined</span></span> | <span data-ttu-id="6bf81-179">NULL</span><span class="sxs-lookup"><span data-stu-id="6bf81-179">NULL</span></span>
<span data-ttu-id="6bf81-180">Any other type (for example, a function or error)</span><span class="sxs-lookup"><span data-stu-id="6bf81-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="6bf81-181">Not supported (results in runtime error)</span><span class="sxs-lookup"><span data-stu-id="6bf81-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6bf81-182">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="6bf81-182">Troubleshooting</span></span>
<span data-ttu-id="6bf81-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span><span class="sxs-lookup"><span data-stu-id="6bf81-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="6bf81-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span><span class="sxs-lookup"><span data-stu-id="6bf81-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="6bf81-185">Other JavaScript user-defined function patterns</span><span class="sxs-lookup"><span data-stu-id="6bf81-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="6bf81-186">Write nested JSON to output</span><span class="sxs-lookup"><span data-stu-id="6bf81-186">Write nested JSON to output</span></span>
<span data-ttu-id="6bf81-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span><span class="sxs-lookup"><span data-stu-id="6bf81-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="6bf81-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span><span class="sxs-lookup"><span data-stu-id="6bf81-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="6bf81-189">**JavaScript user-defined function definition:**</span><span class="sxs-lookup"><span data-stu-id="6bf81-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="6bf81-190">**Sample query:**</span><span class="sxs-lookup"><span data-stu-id="6bf81-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="6bf81-191">Get help</span><span class="sxs-lookup"><span data-stu-id="6bf81-191">Get help</span></span>
<span data-ttu-id="6bf81-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="6bf81-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bf81-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="6bf81-193">Next steps</span></span>
* [<span data-ttu-id="6bf81-194">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6bf81-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6bf81-195">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6bf81-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="6bf81-196">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="6bf81-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6bf81-197">Azure Stream Analytics query language reference</span><span class="sxs-lookup"><span data-stu-id="6bf81-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6bf81-198">Azure Stream Analytics management REST API reference</span><span class="sxs-lookup"><span data-stu-id="6bf81-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
