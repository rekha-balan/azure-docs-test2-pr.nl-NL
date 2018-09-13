---
title: Splunk to Azure Log Analytics | Microsoft Docs
description: Assist for users who are familiar with Splunk in learning the Log Analytics query language.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/21/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 5ea9790695b8afe7bd42b98b071869756b301350
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870594"
---
# <a name="splunk-to-log-analytics"></a><span data-ttu-id="49e8a-103">Splunk to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-103">Splunk to Log Analytics</span></span>

<span data-ttu-id="49e8a-104">This article is intended to assist users who are familiar with Splunk in learning the Log Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="49e8a-104">This article is intended to assist users who are familiar with Splunk in learning the Log Analytics query language.</span></span> <span data-ttu-id="49e8a-105">Direct comparisons are made between the two to understand key differences and also similarities where you can leverage your existing knowledge.</span><span class="sxs-lookup"><span data-stu-id="49e8a-105">Direct comparisons are made between the two to understand key differences and also similarities where you can leverage your existing knowledge.</span></span>

## <a name="structure-and-concepts"></a><span data-ttu-id="49e8a-106">Structure and concepts</span><span class="sxs-lookup"><span data-stu-id="49e8a-106">Structure and concepts</span></span>

<span data-ttu-id="49e8a-107">The following table compares concepts and data structures between Splunk and Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="49e8a-107">The following table compares concepts and data structures between Splunk and Log Analytics.</span></span>

 | <span data-ttu-id="49e8a-108">Concept</span><span class="sxs-lookup"><span data-stu-id="49e8a-108">Concept</span></span>  | <span data-ttu-id="49e8a-109">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-109">Splunk</span></span> | <span data-ttu-id="49e8a-110">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-110">Log Analytics</span></span> |  <span data-ttu-id="49e8a-111">Comment</span><span class="sxs-lookup"><span data-stu-id="49e8a-111">Comment</span></span>
 | --- | --- | --- | ---
 | <span data-ttu-id="49e8a-112">Deployment unit</span><span class="sxs-lookup"><span data-stu-id="49e8a-112">Deployment unit</span></span>  | <span data-ttu-id="49e8a-113">cluster</span><span class="sxs-lookup"><span data-stu-id="49e8a-113">cluster</span></span> |  <span data-ttu-id="49e8a-114">cluster</span><span class="sxs-lookup"><span data-stu-id="49e8a-114">cluster</span></span> |  <span data-ttu-id="49e8a-115">Log Analytics allows arbitrary cross cluster queries.</span><span class="sxs-lookup"><span data-stu-id="49e8a-115">Log Analytics allows arbitrary cross cluster queries.</span></span> <span data-ttu-id="49e8a-116">Splunk does not.</span><span class="sxs-lookup"><span data-stu-id="49e8a-116">Splunk does not.</span></span> |
 | <span data-ttu-id="49e8a-117">Data caches</span><span class="sxs-lookup"><span data-stu-id="49e8a-117">Data caches</span></span> |  <span data-ttu-id="49e8a-118">buckets</span><span class="sxs-lookup"><span data-stu-id="49e8a-118">buckets</span></span>  |  <span data-ttu-id="49e8a-119">Caching and retention policies</span><span class="sxs-lookup"><span data-stu-id="49e8a-119">Caching and retention policies</span></span> |  <span data-ttu-id="49e8a-120">Controls the period and caching level for the data.</span><span class="sxs-lookup"><span data-stu-id="49e8a-120">Controls the period and caching level for the data.</span></span> <span data-ttu-id="49e8a-121">This setting directly impacts the performance of queries and cost of the deployment.</span><span class="sxs-lookup"><span data-stu-id="49e8a-121">This setting directly impacts the performance of queries and cost of the deployment.</span></span> |
 | <span data-ttu-id="49e8a-122">Logical partition of data</span><span class="sxs-lookup"><span data-stu-id="49e8a-122">Logical partition of data</span></span>  |  <span data-ttu-id="49e8a-123">index</span><span class="sxs-lookup"><span data-stu-id="49e8a-123">index</span></span>  |  <span data-ttu-id="49e8a-124">database</span><span class="sxs-lookup"><span data-stu-id="49e8a-124">database</span></span>  |  <span data-ttu-id="49e8a-125">Allows logical separation of the data.</span><span class="sxs-lookup"><span data-stu-id="49e8a-125">Allows logical separation of the data.</span></span> <span data-ttu-id="49e8a-126">Both implementations allow unions and joining across these partitions.</span><span class="sxs-lookup"><span data-stu-id="49e8a-126">Both implementations allow unions and joining across these partitions.</span></span> |
 | <span data-ttu-id="49e8a-127">Structured event metadata</span><span class="sxs-lookup"><span data-stu-id="49e8a-127">Structured event metadata</span></span> | <span data-ttu-id="49e8a-128">N/A</span><span class="sxs-lookup"><span data-stu-id="49e8a-128">N/A</span></span> | <span data-ttu-id="49e8a-129">table</span><span class="sxs-lookup"><span data-stu-id="49e8a-129">table</span></span> |  <span data-ttu-id="49e8a-130">Splunk does not have the concept exposed to the search language of event metadata.</span><span class="sxs-lookup"><span data-stu-id="49e8a-130">Splunk does not have the concept exposed to the search language of event metadata.</span></span> <span data-ttu-id="49e8a-131">Log Analytics has the concept of a table, which has columns.</span><span class="sxs-lookup"><span data-stu-id="49e8a-131">Log Analytics has the concept of a table, which has columns.</span></span> <span data-ttu-id="49e8a-132">Each event instance is mapped to a row.</span><span class="sxs-lookup"><span data-stu-id="49e8a-132">Each event instance is mapped to a row.</span></span> |
 | <span data-ttu-id="49e8a-133">Data record</span><span class="sxs-lookup"><span data-stu-id="49e8a-133">Data record</span></span> | <span data-ttu-id="49e8a-134">event</span><span class="sxs-lookup"><span data-stu-id="49e8a-134">event</span></span> | <span data-ttu-id="49e8a-135">row</span><span class="sxs-lookup"><span data-stu-id="49e8a-135">row</span></span> |  <span data-ttu-id="49e8a-136">Terminology change only.</span><span class="sxs-lookup"><span data-stu-id="49e8a-136">Terminology change only.</span></span> |
 | <span data-ttu-id="49e8a-137">Data record attribute</span><span class="sxs-lookup"><span data-stu-id="49e8a-137">Data record attribute</span></span> | <span data-ttu-id="49e8a-138">field</span><span class="sxs-lookup"><span data-stu-id="49e8a-138">field</span></span> |  <span data-ttu-id="49e8a-139">column</span><span class="sxs-lookup"><span data-stu-id="49e8a-139">column</span></span> |  <span data-ttu-id="49e8a-140">In Log Analytics, this is predefined as part of the table structure.</span><span class="sxs-lookup"><span data-stu-id="49e8a-140">In Log Analytics, this is predefined as part of the table structure.</span></span> <span data-ttu-id="49e8a-141">In Splunk, each event has its own set of fields.</span><span class="sxs-lookup"><span data-stu-id="49e8a-141">In Splunk, each event has its own set of fields.</span></span> |
 | <span data-ttu-id="49e8a-142">Types</span><span class="sxs-lookup"><span data-stu-id="49e8a-142">Types</span></span> | <span data-ttu-id="49e8a-143">datatype</span><span class="sxs-lookup"><span data-stu-id="49e8a-143">datatype</span></span> |  <span data-ttu-id="49e8a-144">datatype</span><span class="sxs-lookup"><span data-stu-id="49e8a-144">datatype</span></span> |  <span data-ttu-id="49e8a-145">Log Analytics datatypes are more explicit as they are set on the columns.</span><span class="sxs-lookup"><span data-stu-id="49e8a-145">Log Analytics datatypes are more explicit as they are set on the columns.</span></span> <span data-ttu-id="49e8a-146">Both have the ability to work dynamically with data types  and roughly equivalent set of datatypes including JSON support.</span><span class="sxs-lookup"><span data-stu-id="49e8a-146">Both have the ability to work dynamically with data types  and roughly equivalent set of datatypes including JSON support.</span></span> |
 | <span data-ttu-id="49e8a-147">Query and search</span><span class="sxs-lookup"><span data-stu-id="49e8a-147">Query and search</span></span>  | <span data-ttu-id="49e8a-148">search</span><span class="sxs-lookup"><span data-stu-id="49e8a-148">search</span></span> | <span data-ttu-id="49e8a-149">query</span><span class="sxs-lookup"><span data-stu-id="49e8a-149">query</span></span> |  <span data-ttu-id="49e8a-150">Concepts are essentially the same between both Log Analytics and Splunk.</span><span class="sxs-lookup"><span data-stu-id="49e8a-150">Concepts are essentially the same between both Log Analytics and Splunk.</span></span> |
 | <span data-ttu-id="49e8a-151">Event ingestion time</span><span class="sxs-lookup"><span data-stu-id="49e8a-151">Event ingestion time</span></span> | <span data-ttu-id="49e8a-152">System Time</span><span class="sxs-lookup"><span data-stu-id="49e8a-152">System Time</span></span> | <span data-ttu-id="49e8a-153">ingestion_time()</span><span class="sxs-lookup"><span data-stu-id="49e8a-153">ingestion_time()</span></span> |  <span data-ttu-id="49e8a-154">In Splunk, each event gets a system timestamp of the time that the event was indexed.</span><span class="sxs-lookup"><span data-stu-id="49e8a-154">In Splunk, each event gets a system timestamp of the time that the event was indexed.</span></span> <span data-ttu-id="49e8a-155">In Log Analytics, you can define a policy called ingestion_time that exposes a system column that can be referenced through the ingestion_time() function.</span><span class="sxs-lookup"><span data-stu-id="49e8a-155">In Log Analytics, you can define a policy called ingestion_time that exposes a system column that can be referenced through the ingestion_time() function.</span></span> |

## <a name="functions"></a><span data-ttu-id="49e8a-156">Functions</span><span class="sxs-lookup"><span data-stu-id="49e8a-156">Functions</span></span>

<span data-ttu-id="49e8a-157">The following table specifies functions in Log Analytics that are equivalent to Splunk functions.</span><span class="sxs-lookup"><span data-stu-id="49e8a-157">The following table specifies functions in Log Analytics that are equivalent to Splunk functions.</span></span>

|<span data-ttu-id="49e8a-158">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-158">Splunk</span></span> | <span data-ttu-id="49e8a-159">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-159">Log Analytics</span></span> |<span data-ttu-id="49e8a-160">Comment</span><span class="sxs-lookup"><span data-stu-id="49e8a-160">Comment</span></span>
|---|---|---
|<span data-ttu-id="49e8a-161">strcat</span><span class="sxs-lookup"><span data-stu-id="49e8a-161">strcat</span></span> | <span data-ttu-id="49e8a-162">strcat()</span><span class="sxs-lookup"><span data-stu-id="49e8a-162">strcat()</span></span>| <span data-ttu-id="49e8a-163">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-163">(1)</span></span> |
|<span data-ttu-id="49e8a-164">split</span><span class="sxs-lookup"><span data-stu-id="49e8a-164">split</span></span>  | <span data-ttu-id="49e8a-165">split()</span><span class="sxs-lookup"><span data-stu-id="49e8a-165">split()</span></span> | <span data-ttu-id="49e8a-166">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-166">(1)</span></span> |
|<span data-ttu-id="49e8a-167">if</span><span class="sxs-lookup"><span data-stu-id="49e8a-167">if</span></span>     | <span data-ttu-id="49e8a-168">iff()</span><span class="sxs-lookup"><span data-stu-id="49e8a-168">iff()</span></span>   | <span data-ttu-id="49e8a-169">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-169">(1)</span></span> |
|<span data-ttu-id="49e8a-170">tonumber</span><span class="sxs-lookup"><span data-stu-id="49e8a-170">tonumber</span></span> | <span data-ttu-id="49e8a-171">todouble()</span><span class="sxs-lookup"><span data-stu-id="49e8a-171">todouble()</span></span><br><span data-ttu-id="49e8a-172">tolong()</span><span class="sxs-lookup"><span data-stu-id="49e8a-172">tolong()</span></span><br><span data-ttu-id="49e8a-173">toint()</span><span class="sxs-lookup"><span data-stu-id="49e8a-173">toint()</span></span> | <span data-ttu-id="49e8a-174">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-174">(1)</span></span> |
|<span data-ttu-id="49e8a-175">upper</span><span class="sxs-lookup"><span data-stu-id="49e8a-175">upper</span></span><br><span data-ttu-id="49e8a-176">lower</span><span class="sxs-lookup"><span data-stu-id="49e8a-176">lower</span></span> |<span data-ttu-id="49e8a-177">toupper()</span><span class="sxs-lookup"><span data-stu-id="49e8a-177">toupper()</span></span><br><span data-ttu-id="49e8a-178">tolower()</span><span class="sxs-lookup"><span data-stu-id="49e8a-178">tolower()</span></span>|<span data-ttu-id="49e8a-179">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-179">(1)</span></span> |
| <span data-ttu-id="49e8a-180">replace</span><span class="sxs-lookup"><span data-stu-id="49e8a-180">replace</span></span> | <span data-ttu-id="49e8a-181">replace()</span><span class="sxs-lookup"><span data-stu-id="49e8a-181">replace()</span></span> | <span data-ttu-id="49e8a-182">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-182">(1)</span></span><br> <span data-ttu-id="49e8a-183">Also note that while `replace()` takes three parameters in both products, the parameters are different.</span><span class="sxs-lookup"><span data-stu-id="49e8a-183">Also note that while `replace()` takes three parameters in both products, the parameters are different.</span></span> |
| <span data-ttu-id="49e8a-184">substr</span><span class="sxs-lookup"><span data-stu-id="49e8a-184">substr</span></span> | <span data-ttu-id="49e8a-185">substring()</span><span class="sxs-lookup"><span data-stu-id="49e8a-185">substring()</span></span> | <span data-ttu-id="49e8a-186">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-186">(1)</span></span><br><span data-ttu-id="49e8a-187">Also note that Splunk uses one-based indices.</span><span class="sxs-lookup"><span data-stu-id="49e8a-187">Also note that Splunk uses one-based indices.</span></span> <span data-ttu-id="49e8a-188">Log Analytics notes zero-based indices.</span><span class="sxs-lookup"><span data-stu-id="49e8a-188">Log Analytics notes zero-based indices.</span></span> |
| <span data-ttu-id="49e8a-189">tolower</span><span class="sxs-lookup"><span data-stu-id="49e8a-189">tolower</span></span> |  <span data-ttu-id="49e8a-190">tolower()</span><span class="sxs-lookup"><span data-stu-id="49e8a-190">tolower()</span></span> | <span data-ttu-id="49e8a-191">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-191">(1)</span></span> |
| <span data-ttu-id="49e8a-192">toupper</span><span class="sxs-lookup"><span data-stu-id="49e8a-192">toupper</span></span> | <span data-ttu-id="49e8a-193">toupper()</span><span class="sxs-lookup"><span data-stu-id="49e8a-193">toupper()</span></span> | <span data-ttu-id="49e8a-194">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-194">(1)</span></span> |
| <span data-ttu-id="49e8a-195">match</span><span class="sxs-lookup"><span data-stu-id="49e8a-195">match</span></span> | <span data-ttu-id="49e8a-196">matches regex</span><span class="sxs-lookup"><span data-stu-id="49e8a-196">matches regex</span></span> |  <span data-ttu-id="49e8a-197">(2)</span><span class="sxs-lookup"><span data-stu-id="49e8a-197">(2)</span></span>  |
| <span data-ttu-id="49e8a-198">regex</span><span class="sxs-lookup"><span data-stu-id="49e8a-198">regex</span></span> | <span data-ttu-id="49e8a-199">matches regex</span><span class="sxs-lookup"><span data-stu-id="49e8a-199">matches regex</span></span> | <span data-ttu-id="49e8a-200">In Splunk, `regex` is an operator.</span><span class="sxs-lookup"><span data-stu-id="49e8a-200">In Splunk, `regex` is an operator.</span></span> <span data-ttu-id="49e8a-201">In Log Analytics, it's a relational operator.</span><span class="sxs-lookup"><span data-stu-id="49e8a-201">In Log Analytics, it's a relational operator.</span></span> |
| <span data-ttu-id="49e8a-202">searchmatch</span><span class="sxs-lookup"><span data-stu-id="49e8a-202">searchmatch</span></span> | == | <span data-ttu-id="49e8a-203">In Splunk, `searchmatch` allows searching for the exact string.</span><span class="sxs-lookup"><span data-stu-id="49e8a-203">In Splunk, `searchmatch` allows searching for the exact string.</span></span>
| <span data-ttu-id="49e8a-204">random</span><span class="sxs-lookup"><span data-stu-id="49e8a-204">random</span></span> | <span data-ttu-id="49e8a-205">rand()</span><span class="sxs-lookup"><span data-stu-id="49e8a-205">rand()</span></span><br><span data-ttu-id="49e8a-206">rand(n)</span><span class="sxs-lookup"><span data-stu-id="49e8a-206">rand(n)</span></span> | <span data-ttu-id="49e8a-207">Splunk's function returns a number from zero to 2<sup>31</sup>-1.</span><span class="sxs-lookup"><span data-stu-id="49e8a-207">Splunk's function returns a number from zero to 2<sup>31</sup>-1.</span></span> <span data-ttu-id="49e8a-208">Log Analytics' returns a number between 0.0 and 1.0, or if a parameter provided, between 0 and n-1.</span><span class="sxs-lookup"><span data-stu-id="49e8a-208">Log Analytics' returns a number between 0.0 and 1.0, or if a parameter provided, between 0 and n-1.</span></span>
| <span data-ttu-id="49e8a-209">now</span><span class="sxs-lookup"><span data-stu-id="49e8a-209">now</span></span> | <span data-ttu-id="49e8a-210">now()</span><span class="sxs-lookup"><span data-stu-id="49e8a-210">now()</span></span> | <span data-ttu-id="49e8a-211">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-211">(1)</span></span>
| <span data-ttu-id="49e8a-212">relative_time</span><span class="sxs-lookup"><span data-stu-id="49e8a-212">relative_time</span></span> | <span data-ttu-id="49e8a-213">totimespan()</span><span class="sxs-lookup"><span data-stu-id="49e8a-213">totimespan()</span></span> | <span data-ttu-id="49e8a-214">(1)</span><span class="sxs-lookup"><span data-stu-id="49e8a-214">(1)</span></span><br><span data-ttu-id="49e8a-215">In Log Analytics, Splunk's equivalent of relative_time(datetimeVal, offsetVal) is datetimeVal + totimespan(offsetVal).</span><span class="sxs-lookup"><span data-stu-id="49e8a-215">In Log Analytics, Splunk's equivalent of relative_time(datetimeVal, offsetVal) is datetimeVal + totimespan(offsetVal).</span></span><br><span data-ttu-id="49e8a-216">For example, <code>search &#124; eval n=relative_time(now(), "-1d@d")</code> becomes <code>...  &#124; extend myTime = now() - totimespan("1d")</code>.</span><span class="sxs-lookup"><span data-stu-id="49e8a-216">For example, <code>search &#124; eval n=relative_time(now(), "-1d@d")</code> becomes <code>...  &#124; extend myTime = now() - totimespan("1d")</code>.</span></span>

<span data-ttu-id="49e8a-217">(1) In Splunk, the function is invoked with the `eval` operator.</span><span class="sxs-lookup"><span data-stu-id="49e8a-217">(1) In Splunk, the function is invoked with the `eval` operator.</span></span> <span data-ttu-id="49e8a-218">In Log Analytics, it is used as part of `extend` or `project`.</span><span class="sxs-lookup"><span data-stu-id="49e8a-218">In Log Analytics, it is used as part of `extend` or `project`.</span></span><br><span data-ttu-id="49e8a-219">(2) In Splunk, the function is invoked with the `eval` operator.</span><span class="sxs-lookup"><span data-stu-id="49e8a-219">(2) In Splunk, the function is invoked with the `eval` operator.</span></span> <span data-ttu-id="49e8a-220">In Log Analytics, it can be used with the `where` operator.</span><span class="sxs-lookup"><span data-stu-id="49e8a-220">In Log Analytics, it can be used with the `where` operator.</span></span>


## <a name="operators"></a><span data-ttu-id="49e8a-221">Operators</span><span class="sxs-lookup"><span data-stu-id="49e8a-221">Operators</span></span>

<span data-ttu-id="49e8a-222">The following sections give examples of using different operators between Splunk and Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="49e8a-222">The following sections give examples of using different operators between Splunk and Log Analytics.</span></span>

> [!NOTE]
> <span data-ttu-id="49e8a-223">For the purpose of the following example, the Splunk field _rule_ maps to a table in Azure Log Analytics, and Splunk's default timestamp maps to the Logs Analytics _ingestion_time()_ column.</span><span class="sxs-lookup"><span data-stu-id="49e8a-223">For the purpose of the following example, the Splunk field _rule_ maps to a table in Azure Log Analytics, and Splunk's default timestamp maps to the Logs Analytics _ingestion_time()_ column.</span></span>

### <a name="search"></a><span data-ttu-id="49e8a-224">Search</span><span class="sxs-lookup"><span data-stu-id="49e8a-224">Search</span></span>
<span data-ttu-id="49e8a-225">In Splunk, you can omit the `search` keyword and specify an unquoted string.</span><span class="sxs-lookup"><span data-stu-id="49e8a-225">In Splunk, you can omit the `search` keyword and specify an unquoted string.</span></span> <span data-ttu-id="49e8a-226">In Azure Log Analytics you must start each search with `find`, an unquoted string is a column name, and the lookup value must be a quoted string.</span><span class="sxs-lookup"><span data-stu-id="49e8a-226">In Azure Log Analytics you must start each search with `find`, an unquoted string is a column name, and the lookup value must be a quoted string.</span></span> 

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-227">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-227">Splunk</span></span> | <span data-ttu-id="49e8a-228">**search**</span><span class="sxs-lookup"><span data-stu-id="49e8a-228">**search**</span></span> | <code>search Session.Id="c8894ffd-e684-43c9-9125-42adc25cd3fc" earliest=-24h</code> |
| <span data-ttu-id="49e8a-229">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-229">Log Analytics</span></span> | <span data-ttu-id="49e8a-230">**find**</span><span class="sxs-lookup"><span data-stu-id="49e8a-230">**find**</span></span> | <code>find Session.Id=="c8894ffd-e684-43c9-9125-42adc25cd3fc" and ingestion_time()> ago(24h)</code> |
| | |

### <a name="filter"></a><span data-ttu-id="49e8a-231">Filter</span><span class="sxs-lookup"><span data-stu-id="49e8a-231">Filter</span></span>
<span data-ttu-id="49e8a-232">Azure Log Analytics queries start from a tabular result set where the filter.</span><span class="sxs-lookup"><span data-stu-id="49e8a-232">Azure Log Analytics queries start from a tabular result set where the filter.</span></span> <span data-ttu-id="49e8a-233">In Splunk, filtering is the default operation on the current index.</span><span class="sxs-lookup"><span data-stu-id="49e8a-233">In Splunk, filtering is the default operation on the current index.</span></span> <span data-ttu-id="49e8a-234">You can also use `where` operator in Splunk, but it is not recommended.</span><span class="sxs-lookup"><span data-stu-id="49e8a-234">You can also use `where` operator in Splunk, but it is not recommended.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-235">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-235">Splunk</span></span> | <span data-ttu-id="49e8a-236">**search**</span><span class="sxs-lookup"><span data-stu-id="49e8a-236">**search**</span></span> | <code>Event.Rule="330009.2" Session.Id="c8894ffd-e684-43c9-9125-42adc25cd3fc" _indextime>-24h</code> |
| <span data-ttu-id="49e8a-237">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-237">Log Analytics</span></span> | <span data-ttu-id="49e8a-238">**where**</span><span class="sxs-lookup"><span data-stu-id="49e8a-238">**where**</span></span> | <code>Office_Hub_OHubBGTaskError<br>&#124; where Session_Id == "c8894ffd-e684-43c9-9125-42adc25cd3fc" and ingestion_time() > ago(24h)</code> |
| | |


### <a name="getting-n-eventsrows-for-inspection"></a><span data-ttu-id="49e8a-239">Getting n events/rows for inspection</span><span class="sxs-lookup"><span data-stu-id="49e8a-239">Getting n events/rows for inspection</span></span> 
<span data-ttu-id="49e8a-240">Azure Log Analytics also supports `take` as an alias to `limit`.</span><span class="sxs-lookup"><span data-stu-id="49e8a-240">Azure Log Analytics also supports `take` as an alias to `limit`.</span></span> <span data-ttu-id="49e8a-241">In Splunk, if the results are ordered, `head` will return the first n results.</span><span class="sxs-lookup"><span data-stu-id="49e8a-241">In Splunk, if the results are ordered, `head` will return the first n results.</span></span> <span data-ttu-id="49e8a-242">In Azure Log Analytics, limit is not ordered but returns the first n rows that are found.</span><span class="sxs-lookup"><span data-stu-id="49e8a-242">In Azure Log Analytics, limit is not ordered but returns the first n rows that are found.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-243">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-243">Splunk</span></span> | <span data-ttu-id="49e8a-244">**head**</span><span class="sxs-lookup"><span data-stu-id="49e8a-244">**head**</span></span> | <code>Event.Rule=330009.2<br>&#124; head 100</code> |
| <span data-ttu-id="49e8a-245">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-245">Log Analytics</span></span> | <span data-ttu-id="49e8a-246">**limit**</span><span class="sxs-lookup"><span data-stu-id="49e8a-246">**limit**</span></span> | <code>Office_Hub_OHubBGTaskError<br>&#124; limit 100</code> |
| | |



### <a name="getting-the-first-n-eventsrows-ordered-by-a-fieldcolumn"></a><span data-ttu-id="49e8a-247">Getting the first n events/rows ordered by a field/column</span><span class="sxs-lookup"><span data-stu-id="49e8a-247">Getting the first n events/rows ordered by a field/column</span></span>
<span data-ttu-id="49e8a-248">For bottom results, in Splunk you use `tail`.</span><span class="sxs-lookup"><span data-stu-id="49e8a-248">For bottom results, in Splunk you use `tail`.</span></span> <span data-ttu-id="49e8a-249">In Azure Log Analytics you can specify the ordering direction with `asc`.</span><span class="sxs-lookup"><span data-stu-id="49e8a-249">In Azure Log Analytics you can specify the ordering direction with `asc`.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-250">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-250">Splunk</span></span> | <span data-ttu-id="49e8a-251">**head**</span><span class="sxs-lookup"><span data-stu-id="49e8a-251">**head**</span></span> |  <code>Event.Rule="330009.2"<br>&#124; sort Event.Sequence<br>&#124; head 20</code> |
| <span data-ttu-id="49e8a-252">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-252">Log Analytics</span></span> | <span data-ttu-id="49e8a-253">**top**</span><span class="sxs-lookup"><span data-stu-id="49e8a-253">**top**</span></span> | <code>Office_Hub_OHubBGTaskError<br>&#124; top 20 by Event_Sequence</code> |
| | |




### <a name="extending-the-result-set-with-new-fieldscolumns"></a><span data-ttu-id="49e8a-254">Extending the result set with new fields/columns</span><span class="sxs-lookup"><span data-stu-id="49e8a-254">Extending the result set with new fields/columns</span></span>
<span data-ttu-id="49e8a-255">Splunk also has an `eval` function, which is not to be comparable with the `eval` operator.</span><span class="sxs-lookup"><span data-stu-id="49e8a-255">Splunk also has an `eval` function, which is not to be comparable with the `eval` operator.</span></span> <span data-ttu-id="49e8a-256">Both the `eval` operator in Splunk and the `extend` operator in Azure Log Analytics only support scalar functions and arithmetic operators.</span><span class="sxs-lookup"><span data-stu-id="49e8a-256">Both the `eval` operator in Splunk and the `extend` operator in Azure Log Analytics only support scalar functions and arithmetic operators.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-257">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-257">Splunk</span></span> | <span data-ttu-id="49e8a-258">**eval**</span><span class="sxs-lookup"><span data-stu-id="49e8a-258">**eval**</span></span> |  <code>Event.Rule=330009.2<br>&#124; eval state= if(Data.Exception = "0", "success", "error")</code> |
| <span data-ttu-id="49e8a-259">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-259">Log Analytics</span></span> | <span data-ttu-id="49e8a-260">**extend**</span><span class="sxs-lookup"><span data-stu-id="49e8a-260">**extend**</span></span> | <code>Office_Hub_OHubBGTaskError<br>&#124; extend state = iif(Data_Exception == 0,"success" ,"error")</code> |
| | |


### <a name="rename"></a><span data-ttu-id="49e8a-261">Rename</span><span class="sxs-lookup"><span data-stu-id="49e8a-261">Rename</span></span> 
<span data-ttu-id="49e8a-262">Azure Log Analytics uses the same operator to rename and to create a new field.</span><span class="sxs-lookup"><span data-stu-id="49e8a-262">Azure Log Analytics uses the same operator to rename and to create a new field.</span></span> <span data-ttu-id="49e8a-263">Splunk has two separate operators, `eval` and `rename`.</span><span class="sxs-lookup"><span data-stu-id="49e8a-263">Splunk has two separate operators, `eval` and `rename`.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-264">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-264">Splunk</span></span> | <span data-ttu-id="49e8a-265">**rename**</span><span class="sxs-lookup"><span data-stu-id="49e8a-265">**rename**</span></span> |  <code>Event.Rule=330009.2<br>&#124; rename Date.Exception as execption</code> |
| <span data-ttu-id="49e8a-266">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-266">Log Analytics</span></span> | <span data-ttu-id="49e8a-267">**extend**</span><span class="sxs-lookup"><span data-stu-id="49e8a-267">**extend**</span></span> | <code>Office_Hub_OHubBGTaskError<br>&#124; extend exception = Date_Exception</code> |
| | |




### <a name="format-resultsprojection"></a><span data-ttu-id="49e8a-268">Format results/Projection</span><span class="sxs-lookup"><span data-stu-id="49e8a-268">Format results/Projection</span></span>
<span data-ttu-id="49e8a-269">Splunk does not seem to have an operator similar to `project-away`.</span><span class="sxs-lookup"><span data-stu-id="49e8a-269">Splunk does not seem to have an operator similar to `project-away`.</span></span> <span data-ttu-id="49e8a-270">You can use the UI to filter away fields.</span><span class="sxs-lookup"><span data-stu-id="49e8a-270">You can use the UI to filter away fields.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-271">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-271">Splunk</span></span> | <span data-ttu-id="49e8a-272">**table**</span><span class="sxs-lookup"><span data-stu-id="49e8a-272">**table**</span></span> |  <code>Event.Rule=330009.2<br>&#124; table rule, state</code> |
| <span data-ttu-id="49e8a-273">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-273">Log Analytics</span></span> | <span data-ttu-id="49e8a-274">**project**</span><span class="sxs-lookup"><span data-stu-id="49e8a-274">**project**</span></span><br><span data-ttu-id="49e8a-275">**project-away**</span><span class="sxs-lookup"><span data-stu-id="49e8a-275">**project-away**</span></span> | <code>Office_Hub_OHubBGTaskError<br>&#124; project exception, state</code> |
| | |



### <a name="aggregation"></a><span data-ttu-id="49e8a-276">Aggregation</span><span class="sxs-lookup"><span data-stu-id="49e8a-276">Aggregation</span></span>
<span data-ttu-id="49e8a-277">See the [Aggregations in Log Analytics queries](aggregations.md) for the different aggregation functions.</span><span class="sxs-lookup"><span data-stu-id="49e8a-277">See the [Aggregations in Log Analytics queries](aggregations.md) for the different aggregation functions.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-278">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-278">Splunk</span></span> | <span data-ttu-id="49e8a-279">**stats**</span><span class="sxs-lookup"><span data-stu-id="49e8a-279">**stats**</span></span> |  <code>search (Rule=120502.*)<br>&#124; stats count by OSEnv, Audience</code> |
| <span data-ttu-id="49e8a-280">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-280">Log Analytics</span></span> | <span data-ttu-id="49e8a-281">**summarize**</span><span class="sxs-lookup"><span data-stu-id="49e8a-281">**summarize**</span></span> | <code>Office_Hub_OHubBGTaskError<br>&#124; summarize count() by App_Platform, Release_Audience</code> |
| | |



### <a name="join"></a><span data-ttu-id="49e8a-282">Join</span><span class="sxs-lookup"><span data-stu-id="49e8a-282">Join</span></span>
<span data-ttu-id="49e8a-283">Join in Splunk has significant limitations.</span><span class="sxs-lookup"><span data-stu-id="49e8a-283">Join in Splunk has significant limitations.</span></span> <span data-ttu-id="49e8a-284">The subquery has a limit of 10000 results (set in the deployment configuration file), and there a limited number of join flavors.</span><span class="sxs-lookup"><span data-stu-id="49e8a-284">The subquery has a limit of 10000 results (set in the deployment configuration file), and there a limited number of join flavors.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-285">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-285">Splunk</span></span> | <span data-ttu-id="49e8a-286">**join**</span><span class="sxs-lookup"><span data-stu-id="49e8a-286">**join**</span></span> |  <code>Event.Rule=120103* &#124; stats by Client.Id, Data.Alias | <span data-ttu-id="49e8a-287">join Client.Id max=0 [search earliest=-24h Event.Rule="150310.0" Data.Hresult=-2147221040]</code></span><span class="sxs-lookup"><span data-stu-id="49e8a-287">join Client.Id max=0 [search earliest=-24h Event.Rule="150310.0" Data.Hresult=-2147221040]</code></span></span> |
| <span data-ttu-id="49e8a-288">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-288">Log Analytics</span></span> | <span data-ttu-id="49e8a-289">**join**</span><span class="sxs-lookup"><span data-stu-id="49e8a-289">**join**</span></span> | <code>cluster("OAriaPPT").database("Office PowerPoint").Office_PowerPoint_PPT_Exceptions<br>&#124; where  Data_Hresult== -2147221040<br>&#124; join kind = inner (Office_System_SystemHealthMetadata<br>&#124; summarize by Client_Id, Data_Alias)on Client_Id</code>   |
| | |



### <a name="sort"></a><span data-ttu-id="49e8a-290">Sort</span><span class="sxs-lookup"><span data-stu-id="49e8a-290">Sort</span></span>
<span data-ttu-id="49e8a-291">In Splunk, to sort in ascending order you must use the `reverse` operator.</span><span class="sxs-lookup"><span data-stu-id="49e8a-291">In Splunk, to sort in ascending order you must use the `reverse` operator.</span></span> <span data-ttu-id="49e8a-292">Azure Log Analytics also supports defining where to put nulls, at the beginning or at the end.</span><span class="sxs-lookup"><span data-stu-id="49e8a-292">Azure Log Analytics also supports defining where to put nulls, at the beginning or at the end.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-293">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-293">Splunk</span></span> | <span data-ttu-id="49e8a-294">**sort**</span><span class="sxs-lookup"><span data-stu-id="49e8a-294">**sort**</span></span> |  <code>Event.Rule=120103<br>&#124; sort Data.Hresult<br>&#124; reverse</code> |
| <span data-ttu-id="49e8a-295">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-295">Log Analytics</span></span> | <span data-ttu-id="49e8a-296">**order by**</span><span class="sxs-lookup"><span data-stu-id="49e8a-296">**order by**</span></span> | <code>Office_Hub_OHubBGTaskError<br>&#124; order by Data_Hresult,  desc</code> |
| | |



### <a name="multivalue-expand"></a><span data-ttu-id="49e8a-297">Multivalue expand</span><span class="sxs-lookup"><span data-stu-id="49e8a-297">Multivalue expand</span></span>
<span data-ttu-id="49e8a-298">This is a similar operator in both Splunk and Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="49e8a-298">This is a similar operator in both Splunk and Log Analytics.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-299">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-299">Splunk</span></span> | <span data-ttu-id="49e8a-300">**mvexpand**</span><span class="sxs-lookup"><span data-stu-id="49e8a-300">**mvexpand**</span></span> |  `mvexpand foo` |
| <span data-ttu-id="49e8a-301">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-301">Log Analytics</span></span> | <span data-ttu-id="49e8a-302">**mvexpand**</span><span class="sxs-lookup"><span data-stu-id="49e8a-302">**mvexpand**</span></span> | `mvexpand foo` |
| | |




### <a name="results-facets-interesting-fields"></a><span data-ttu-id="49e8a-303">Results facets, interesting fields</span><span class="sxs-lookup"><span data-stu-id="49e8a-303">Results facets, interesting fields</span></span>
<span data-ttu-id="49e8a-304">In the Log Analytics portal, only the first column is exposed.</span><span class="sxs-lookup"><span data-stu-id="49e8a-304">In the Log Analytics portal, only the first column is exposed.</span></span> <span data-ttu-id="49e8a-305">All columns are available through the API.</span><span class="sxs-lookup"><span data-stu-id="49e8a-305">All columns are available through the API.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-306">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-306">Splunk</span></span> | <span data-ttu-id="49e8a-307">**fields**</span><span class="sxs-lookup"><span data-stu-id="49e8a-307">**fields**</span></span> |  <code>Event.Rule=330009.2<br>&#124; fields App.Version, App.Platform</code> |
| <span data-ttu-id="49e8a-308">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-308">Log Analytics</span></span> | <span data-ttu-id="49e8a-309">**facets**</span><span class="sxs-lookup"><span data-stu-id="49e8a-309">**facets**</span></span> | <code>Office_Excel_BI_PivotTableCreate<br>&#124; facet by App_Branch, App_Version</code> |
| | |




### <a name="de-duplicate"></a><span data-ttu-id="49e8a-310">De-duplicate</span><span class="sxs-lookup"><span data-stu-id="49e8a-310">De-duplicate</span></span>
<span data-ttu-id="49e8a-311">You can use `summarize arg_min()` instead to reverse the order of which record gets chosen.</span><span class="sxs-lookup"><span data-stu-id="49e8a-311">You can use `summarize arg_min()` instead to reverse the order of which record gets chosen.</span></span>

| |  | |
|:---|:---|:---|
| <span data-ttu-id="49e8a-312">Splunk</span><span class="sxs-lookup"><span data-stu-id="49e8a-312">Splunk</span></span> | <span data-ttu-id="49e8a-313">**dedup**</span><span class="sxs-lookup"><span data-stu-id="49e8a-313">**dedup**</span></span> |  <code>Event.Rule=330009.2<br>&#124; dedup device_id sortby -batterylife</code> |
| <span data-ttu-id="49e8a-314">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49e8a-314">Log Analytics</span></span> | <span data-ttu-id="49e8a-315">**summarize arg_max()**</span><span class="sxs-lookup"><span data-stu-id="49e8a-315">**summarize arg_max()**</span></span> | <code>Office_Excel_BI_PivotTableCreate<br>&#124; summarize arg_max(batterylife, *) by device_id</code> |
| | |




## <a name="next-steps"></a><span data-ttu-id="49e8a-316">Next steps</span><span class="sxs-lookup"><span data-stu-id="49e8a-316">Next steps</span></span>

- <span data-ttu-id="49e8a-317">Go through a lesson on the [writing queries in Log Analytics](get-started-queries.md).</span><span class="sxs-lookup"><span data-stu-id="49e8a-317">Go through a lesson on the [writing queries in Log Analytics](get-started-queries.md).</span></span>