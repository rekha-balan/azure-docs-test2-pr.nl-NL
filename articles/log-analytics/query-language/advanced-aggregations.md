---
title: Advanced aggregations in Azure Log Analytics queries| Microsoft Docs
description: Describes some of the more advanced aggregation options available to Log Analytics queries.
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
ms.date: 08/16/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 4f2d49233a6eb92f567d4265210fcab394aa6461
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870517"
---
# <a name="advanced-aggregations-in-log-analytics-queries"></a><span data-ttu-id="177aa-103">Advanced aggregations in Log Analytics queries</span><span class="sxs-lookup"><span data-stu-id="177aa-103">Advanced aggregations in Log Analytics queries</span></span>

> [!NOTE]
> <span data-ttu-id="177aa-104">You should complete [Aggregations in Log Analytics queries](./aggregations.md) before completing this lesson.</span><span class="sxs-lookup"><span data-stu-id="177aa-104">You should complete [Aggregations in Log Analytics queries](./aggregations.md) before completing this lesson.</span></span>

<span data-ttu-id="177aa-105">This article describes some of the more advanced aggregation options available to Log Analytics queries.</span><span class="sxs-lookup"><span data-stu-id="177aa-105">This article describes some of the more advanced aggregation options available to Log Analytics queries.</span></span>

## <a name="generating-lists-and-sets"></a><span data-ttu-id="177aa-106">Generating lists and sets</span><span class="sxs-lookup"><span data-stu-id="177aa-106">Generating lists and sets</span></span>
<span data-ttu-id="177aa-107">You can use `makelist` to pivot data by the order of values in a particular column.</span><span class="sxs-lookup"><span data-stu-id="177aa-107">You can use `makelist` to pivot data by the order of values in a particular column.</span></span> <span data-ttu-id="177aa-108">For example, you may want to explore the most common order events take place on your machines.</span><span class="sxs-lookup"><span data-stu-id="177aa-108">For example, you may want to explore the most common order events take place on your machines.</span></span> <span data-ttu-id="177aa-109">You can essentially pivot the data by the order of EventIDs on each machine.</span><span class="sxs-lookup"><span data-stu-id="177aa-109">You can essentially pivot the data by the order of EventIDs on each machine.</span></span> 

```OQL
Event
| where TimeGenerated > ago(12h)
| order by TimeGenerated desc
| summarize makelist(EventID) by Computer
```
|<span data-ttu-id="177aa-110">Computer</span><span class="sxs-lookup"><span data-stu-id="177aa-110">Computer</span></span>|<span data-ttu-id="177aa-111">list_EventID</span><span class="sxs-lookup"><span data-stu-id="177aa-111">list_EventID</span></span>|
|---|---|
| <span data-ttu-id="177aa-112">computer1</span><span class="sxs-lookup"><span data-stu-id="177aa-112">computer1</span></span> | <span data-ttu-id="177aa-113">[704,701,1501,1500,1085,704,704,701]</span><span class="sxs-lookup"><span data-stu-id="177aa-113">[704,701,1501,1500,1085,704,704,701]</span></span> |
| <span data-ttu-id="177aa-114">computer2</span><span class="sxs-lookup"><span data-stu-id="177aa-114">computer2</span></span> | <span data-ttu-id="177aa-115">[326,105,302,301,300,102]</span><span class="sxs-lookup"><span data-stu-id="177aa-115">[326,105,302,301,300,102]</span></span> |
| <span data-ttu-id="177aa-116">...</span><span class="sxs-lookup"><span data-stu-id="177aa-116">...</span></span> | <span data-ttu-id="177aa-117">...</span><span class="sxs-lookup"><span data-stu-id="177aa-117">...</span></span> |

<span data-ttu-id="177aa-118">`makelist` generates a list in the order that data was passed into it.</span><span class="sxs-lookup"><span data-stu-id="177aa-118">`makelist` generates a list in the order that data was passed into it.</span></span> <span data-ttu-id="177aa-119">To sort events from oldest to newest, use `asc` in the order statement instead of `desc`.</span><span class="sxs-lookup"><span data-stu-id="177aa-119">To sort events from oldest to newest, use `asc` in the order statement instead of `desc`.</span></span> 

<span data-ttu-id="177aa-120">It is also useful to create a list of just distinct values.</span><span class="sxs-lookup"><span data-stu-id="177aa-120">It is also useful to create a list of just distinct values.</span></span> <span data-ttu-id="177aa-121">This is called a _Set_ and can be generated with `makeset`:</span><span class="sxs-lookup"><span data-stu-id="177aa-121">This is called a _Set_ and can be generated with `makeset`:</span></span>

```OQL
Event
| where TimeGenerated > ago(12h)
| order by TimeGenerated desc
| summarize makeset(EventID) by Computer
```
|<span data-ttu-id="177aa-122">Computer</span><span class="sxs-lookup"><span data-stu-id="177aa-122">Computer</span></span>|<span data-ttu-id="177aa-123">list_EventID</span><span class="sxs-lookup"><span data-stu-id="177aa-123">list_EventID</span></span>|
|---|---|
| <span data-ttu-id="177aa-124">computer1</span><span class="sxs-lookup"><span data-stu-id="177aa-124">computer1</span></span> | <span data-ttu-id="177aa-125">[704,701,1501,1500,1085]</span><span class="sxs-lookup"><span data-stu-id="177aa-125">[704,701,1501,1500,1085]</span></span> |
| <span data-ttu-id="177aa-126">computer2</span><span class="sxs-lookup"><span data-stu-id="177aa-126">computer2</span></span> | <span data-ttu-id="177aa-127">[326,105,302,301,300,102]</span><span class="sxs-lookup"><span data-stu-id="177aa-127">[326,105,302,301,300,102]</span></span> |
| <span data-ttu-id="177aa-128">...</span><span class="sxs-lookup"><span data-stu-id="177aa-128">...</span></span> | <span data-ttu-id="177aa-129">...</span><span class="sxs-lookup"><span data-stu-id="177aa-129">...</span></span> |

<span data-ttu-id="177aa-130">Like `makelist`, `makeset` also works with ordered data and will generate the arrays based on the order of the rows that are passed into it.</span><span class="sxs-lookup"><span data-stu-id="177aa-130">Like `makelist`, `makeset` also works with ordered data and will generate the arrays based on the order of the rows that are passed into it.</span></span>

## <a name="expanding-lists"></a><span data-ttu-id="177aa-131">Expanding lists</span><span class="sxs-lookup"><span data-stu-id="177aa-131">Expanding lists</span></span>
<span data-ttu-id="177aa-132">The inverse operation of `makelist` or `makeset` is `mvexpand`, which expands a list of values to separate rows.</span><span class="sxs-lookup"><span data-stu-id="177aa-132">The inverse operation of `makelist` or `makeset` is `mvexpand`, which expands a list of values to separate rows.</span></span> <span data-ttu-id="177aa-133">It can expand across any number of dynamic columns, both JSON and array.</span><span class="sxs-lookup"><span data-stu-id="177aa-133">It can expand across any number of dynamic columns, both JSON and array.</span></span> <span data-ttu-id="177aa-134">For example, you could check  the *Heartbeat* table for solutions sending data from computers that sent a heartbeat in the last hour:</span><span class="sxs-lookup"><span data-stu-id="177aa-134">For example, you could check  the *Heartbeat* table for solutions sending data from computers that sent a heartbeat in the last hour:</span></span>

```OQL
Heartbeat
| where TimeGenerated > ago(1h)
| project Computer, Solutions
```
| <span data-ttu-id="177aa-135">Computer</span><span class="sxs-lookup"><span data-stu-id="177aa-135">Computer</span></span> | <span data-ttu-id="177aa-136">Solutions</span><span class="sxs-lookup"><span data-stu-id="177aa-136">Solutions</span></span> | 
|--------------|----------------------|
| <span data-ttu-id="177aa-137">computer1</span><span class="sxs-lookup"><span data-stu-id="177aa-137">computer1</span></span> | <span data-ttu-id="177aa-138">"security", "updates", "changeTracking"</span><span class="sxs-lookup"><span data-stu-id="177aa-138">"security", "updates", "changeTracking"</span></span> |
| <span data-ttu-id="177aa-139">computer2</span><span class="sxs-lookup"><span data-stu-id="177aa-139">computer2</span></span> | <span data-ttu-id="177aa-140">"security", "updates"</span><span class="sxs-lookup"><span data-stu-id="177aa-140">"security", "updates"</span></span> |
| <span data-ttu-id="177aa-141">computer3</span><span class="sxs-lookup"><span data-stu-id="177aa-141">computer3</span></span> | <span data-ttu-id="177aa-142">"antiMalware", "changeTracking"</span><span class="sxs-lookup"><span data-stu-id="177aa-142">"antiMalware", "changeTracking"</span></span> |
| <span data-ttu-id="177aa-143">...</span><span class="sxs-lookup"><span data-stu-id="177aa-143">...</span></span> | <span data-ttu-id="177aa-144">...</span><span class="sxs-lookup"><span data-stu-id="177aa-144">...</span></span> | <span data-ttu-id="177aa-145">...</span><span class="sxs-lookup"><span data-stu-id="177aa-145">...</span></span> |

<span data-ttu-id="177aa-146">Use `mvexpand` to show each value in a separate row instead of a comma-separated list:</span><span class="sxs-lookup"><span data-stu-id="177aa-146">Use `mvexpand` to show each value in a separate row instead of a comma-separated list:</span></span>

<span data-ttu-id="177aa-147">Heartbeat | where TimeGenerated > ago(1h) | project Computer, split(Solutions, ",") | mvexpand Solutions</span><span class="sxs-lookup"><span data-stu-id="177aa-147">Heartbeat | where TimeGenerated > ago(1h) | project Computer, split(Solutions, ",") | mvexpand Solutions</span></span>
```
| Computer | Solutions | 
|--------------|----------------------|
| computer1 | "security" |
| computer1 | "updates" |
| computer1 | "changeTracking" |
| computer2 | "security" |
| computer2 | "updates" |
| computer3 | "antiMalware" |
| computer3 | "changeTracking" |
| ... | ... | ... |
```

<span data-ttu-id="177aa-148">You could then use `makelist` again to group items together, and this time see the list of computers per solution:</span><span class="sxs-lookup"><span data-stu-id="177aa-148">You could then use `makelist` again to group items together, and this time see the list of computers per solution:</span></span>

```OQL
Heartbeat
| where TimeGenerated > ago(1h)
| project Computer, split(Solutions, ",")
| mvexpand Solutions
| summarize makelist(Computer) by tostring(Solutions) 
```
|<span data-ttu-id="177aa-149">Solutions</span><span class="sxs-lookup"><span data-stu-id="177aa-149">Solutions</span></span> | <span data-ttu-id="177aa-150">list_Computer</span><span class="sxs-lookup"><span data-stu-id="177aa-150">list_Computer</span></span> |
|--------------|----------------------|
| <span data-ttu-id="177aa-151">"security"</span><span class="sxs-lookup"><span data-stu-id="177aa-151">"security"</span></span> | <span data-ttu-id="177aa-152">["computer1", "computer2"]</span><span class="sxs-lookup"><span data-stu-id="177aa-152">["computer1", "computer2"]</span></span> |
| <span data-ttu-id="177aa-153">"updates"</span><span class="sxs-lookup"><span data-stu-id="177aa-153">"updates"</span></span> | <span data-ttu-id="177aa-154">["computer1", "computer2"]</span><span class="sxs-lookup"><span data-stu-id="177aa-154">["computer1", "computer2"]</span></span> |
| <span data-ttu-id="177aa-155">"changeTracking"</span><span class="sxs-lookup"><span data-stu-id="177aa-155">"changeTracking"</span></span> | <span data-ttu-id="177aa-156">["computer1", "computer3"]</span><span class="sxs-lookup"><span data-stu-id="177aa-156">["computer1", "computer3"]</span></span> |
| <span data-ttu-id="177aa-157">"antiMalware"</span><span class="sxs-lookup"><span data-stu-id="177aa-157">"antiMalware"</span></span> | <span data-ttu-id="177aa-158">["computer3"]</span><span class="sxs-lookup"><span data-stu-id="177aa-158">["computer3"]</span></span> |
| <span data-ttu-id="177aa-159">...</span><span class="sxs-lookup"><span data-stu-id="177aa-159">...</span></span> | <span data-ttu-id="177aa-160">...</span><span class="sxs-lookup"><span data-stu-id="177aa-160">...</span></span> |

## <a name="handling-missing-bins"></a><span data-ttu-id="177aa-161">Handling missing bins</span><span class="sxs-lookup"><span data-stu-id="177aa-161">Handling missing bins</span></span>
<span data-ttu-id="177aa-162">A useful application of `mvexpand` is the need to fill default values in for missing bins. For example, suppose you're looking for the uptime of a particular machine by exploring its heartbeat.</span><span class="sxs-lookup"><span data-stu-id="177aa-162">A useful application of `mvexpand` is the need to fill default values in for missing bins. For example, suppose you're looking for the uptime of a particular machine by exploring its heartbeat.</span></span> <span data-ttu-id="177aa-163">You also want to see the source of the heartbeat  which is in the _category_ column.</span><span class="sxs-lookup"><span data-stu-id="177aa-163">You also want to see the source of the heartbeat  which is in the _category_ column.</span></span> <span data-ttu-id="177aa-164">Normally, we would use a simple summarize statement as follows:</span><span class="sxs-lookup"><span data-stu-id="177aa-164">Normally, we would use a simple summarize statement as follows:</span></span>

```OQL
Heartbeat
| where TimeGenerated > ago(12h)
| summarize count() by Category, bin(TimeGenerated, 1h)
```
| <span data-ttu-id="177aa-165">Category</span><span class="sxs-lookup"><span data-stu-id="177aa-165">Category</span></span> | <span data-ttu-id="177aa-166">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="177aa-166">TimeGenerated</span></span> | <span data-ttu-id="177aa-167">count_</span><span class="sxs-lookup"><span data-stu-id="177aa-167">count_</span></span> |
|--------------|----------------------|--------|
| <span data-ttu-id="177aa-168">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-168">Direct Agent</span></span> | <span data-ttu-id="177aa-169">2017-06-06T17:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-169">2017-06-06T17:00:00Z</span></span> | <span data-ttu-id="177aa-170">15</span><span class="sxs-lookup"><span data-stu-id="177aa-170">15</span></span> |
| <span data-ttu-id="177aa-171">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-171">Direct Agent</span></span> | <span data-ttu-id="177aa-172">2017-06-06T18:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-172">2017-06-06T18:00:00Z</span></span> | <span data-ttu-id="177aa-173">60</span><span class="sxs-lookup"><span data-stu-id="177aa-173">60</span></span> |
| <span data-ttu-id="177aa-174">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-174">Direct Agent</span></span> | <span data-ttu-id="177aa-175">2017-06-06T20:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-175">2017-06-06T20:00:00Z</span></span> | <span data-ttu-id="177aa-176">55</span><span class="sxs-lookup"><span data-stu-id="177aa-176">55</span></span> |
| <span data-ttu-id="177aa-177">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-177">Direct Agent</span></span> | <span data-ttu-id="177aa-178">2017-06-06T21:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-178">2017-06-06T21:00:00Z</span></span> | <span data-ttu-id="177aa-179">57</span><span class="sxs-lookup"><span data-stu-id="177aa-179">57</span></span> |
| <span data-ttu-id="177aa-180">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-180">Direct Agent</span></span> | <span data-ttu-id="177aa-181">2017-06-06T22:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-181">2017-06-06T22:00:00Z</span></span> | <span data-ttu-id="177aa-182">60</span><span class="sxs-lookup"><span data-stu-id="177aa-182">60</span></span> |
| <span data-ttu-id="177aa-183">...</span><span class="sxs-lookup"><span data-stu-id="177aa-183">...</span></span> | <span data-ttu-id="177aa-184">...</span><span class="sxs-lookup"><span data-stu-id="177aa-184">...</span></span> | <span data-ttu-id="177aa-185">...</span><span class="sxs-lookup"><span data-stu-id="177aa-185">...</span></span> |

<span data-ttu-id="177aa-186">In these results though the bucket associated with "2017-06-06T19:00:00Z" is missing because there isn't any heartbeat data for that hour.</span><span class="sxs-lookup"><span data-stu-id="177aa-186">In these results though the bucket associated with "2017-06-06T19:00:00Z" is missing because there isn't any heartbeat data for that hour.</span></span> <span data-ttu-id="177aa-187">Use the `make-series` function to assign a default value to empty buckets.</span><span class="sxs-lookup"><span data-stu-id="177aa-187">Use the `make-series` function to assign a default value to empty buckets.</span></span> <span data-ttu-id="177aa-188">This will generate a row for each category with two extra array columns, one for values, and one for matching time buckets:</span><span class="sxs-lookup"><span data-stu-id="177aa-188">This will generate a row for each category with two extra array columns, one for values, and one for matching time buckets:</span></span>

```OQL
Heartbeat
| make-series count() default=0 on TimeGenerated in range(ago(1d), now(), 1h) by Category 
```

| <span data-ttu-id="177aa-189">Category</span><span class="sxs-lookup"><span data-stu-id="177aa-189">Category</span></span> | <span data-ttu-id="177aa-190">count_</span><span class="sxs-lookup"><span data-stu-id="177aa-190">count_</span></span> | <span data-ttu-id="177aa-191">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="177aa-191">TimeGenerated</span></span> |
|---|---|---|
| <span data-ttu-id="177aa-192">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-192">Direct Agent</span></span> | <span data-ttu-id="177aa-193">[15,60,0,55,60,57,60,...]</span><span class="sxs-lookup"><span data-stu-id="177aa-193">[15,60,0,55,60,57,60,...]</span></span> | <span data-ttu-id="177aa-194">["2017-06-06T17:00:00.0000000Z","2017-06-06T18:00:00.0000000Z","2017-06-06T19:00:00.0000000Z","2017-06-06T20:00:00.0000000Z","2017-06-06T21:00:00.0000000Z",...]</span><span class="sxs-lookup"><span data-stu-id="177aa-194">["2017-06-06T17:00:00.0000000Z","2017-06-06T18:00:00.0000000Z","2017-06-06T19:00:00.0000000Z","2017-06-06T20:00:00.0000000Z","2017-06-06T21:00:00.0000000Z",...]</span></span> |
| <span data-ttu-id="177aa-195">...</span><span class="sxs-lookup"><span data-stu-id="177aa-195">...</span></span> | <span data-ttu-id="177aa-196">...</span><span class="sxs-lookup"><span data-stu-id="177aa-196">...</span></span> | <span data-ttu-id="177aa-197">...</span><span class="sxs-lookup"><span data-stu-id="177aa-197">...</span></span> |

<span data-ttu-id="177aa-198">The third element of the *count_* array is a 0 as expected, and there is a matching timestamp of "2017-06-06T19:00:00.0000000Z" in the _TimeGenerated_ array.</span><span class="sxs-lookup"><span data-stu-id="177aa-198">The third element of the *count_* array is a 0 as expected, and there is a matching timestamp of "2017-06-06T19:00:00.0000000Z" in the _TimeGenerated_ array.</span></span> <span data-ttu-id="177aa-199">This array format is difficult to read though.</span><span class="sxs-lookup"><span data-stu-id="177aa-199">This array format is difficult to read though.</span></span> <span data-ttu-id="177aa-200">Use `mvexpand` to expand the arrays and produce the same format output as generated by `summarize`:</span><span class="sxs-lookup"><span data-stu-id="177aa-200">Use `mvexpand` to expand the arrays and produce the same format output as generated by `summarize`:</span></span>

```OQL
Heartbeat
| make-series count() default=0 on TimeGenerated in range(ago(1d), now(), 1h) by Category 
| mvexpand TimeGenerated, count_
| project Category, TimeGenerated, count_
```
| <span data-ttu-id="177aa-201">Category</span><span class="sxs-lookup"><span data-stu-id="177aa-201">Category</span></span> | <span data-ttu-id="177aa-202">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="177aa-202">TimeGenerated</span></span> | <span data-ttu-id="177aa-203">count_</span><span class="sxs-lookup"><span data-stu-id="177aa-203">count_</span></span> |
|--------------|----------------------|--------|
| <span data-ttu-id="177aa-204">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-204">Direct Agent</span></span> | <span data-ttu-id="177aa-205">2017-06-06T17:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-205">2017-06-06T17:00:00Z</span></span> | <span data-ttu-id="177aa-206">15</span><span class="sxs-lookup"><span data-stu-id="177aa-206">15</span></span> |
| <span data-ttu-id="177aa-207">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-207">Direct Agent</span></span> | <span data-ttu-id="177aa-208">2017-06-06T18:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-208">2017-06-06T18:00:00Z</span></span> | <span data-ttu-id="177aa-209">60</span><span class="sxs-lookup"><span data-stu-id="177aa-209">60</span></span> |
| <span data-ttu-id="177aa-210">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-210">Direct Agent</span></span> | <span data-ttu-id="177aa-211">2017-06-06T19:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-211">2017-06-06T19:00:00Z</span></span> | <span data-ttu-id="177aa-212">0</span><span class="sxs-lookup"><span data-stu-id="177aa-212">0</span></span> |
| <span data-ttu-id="177aa-213">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-213">Direct Agent</span></span> | <span data-ttu-id="177aa-214">2017-06-06T20:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-214">2017-06-06T20:00:00Z</span></span> | <span data-ttu-id="177aa-215">55</span><span class="sxs-lookup"><span data-stu-id="177aa-215">55</span></span> |
| <span data-ttu-id="177aa-216">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-216">Direct Agent</span></span> | <span data-ttu-id="177aa-217">2017-06-06T21:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-217">2017-06-06T21:00:00Z</span></span> | <span data-ttu-id="177aa-218">57</span><span class="sxs-lookup"><span data-stu-id="177aa-218">57</span></span> |
| <span data-ttu-id="177aa-219">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="177aa-219">Direct Agent</span></span> | <span data-ttu-id="177aa-220">2017-06-06T22:00:00Z</span><span class="sxs-lookup"><span data-stu-id="177aa-220">2017-06-06T22:00:00Z</span></span> | <span data-ttu-id="177aa-221">60</span><span class="sxs-lookup"><span data-stu-id="177aa-221">60</span></span> |
| <span data-ttu-id="177aa-222">...</span><span class="sxs-lookup"><span data-stu-id="177aa-222">...</span></span> | <span data-ttu-id="177aa-223">...</span><span class="sxs-lookup"><span data-stu-id="177aa-223">...</span></span> | <span data-ttu-id="177aa-224">...</span><span class="sxs-lookup"><span data-stu-id="177aa-224">...</span></span> |



## <a name="narrowing-results-to-a-set-of-elements-let-makeset-toscalar-in"></a><span data-ttu-id="177aa-225">Narrowing results to a set of elements: `let`, `makeset`, `toscalar`, `in`</span><span class="sxs-lookup"><span data-stu-id="177aa-225">Narrowing results to a set of elements: `let`, `makeset`, `toscalar`, `in`</span></span>
<span data-ttu-id="177aa-226">A common scenario is to select the names of some specific entities based on a set of criteria and then filter a different data set down to that set of entities.</span><span class="sxs-lookup"><span data-stu-id="177aa-226">A common scenario is to select the names of some specific entities based on a set of criteria and then filter a different data set down to that set of entities.</span></span> <span data-ttu-id="177aa-227">For example you might find computers that are known to have missing updates and identify IPs that these computers called out to:</span><span class="sxs-lookup"><span data-stu-id="177aa-227">For example you might find computers that are known to have missing updates and identify IPs that these computers called out to:</span></span>


```OQL
let ComputersNeedingUpdate = toscalar(
    Update
    | summarize makeset(Computer)
    | project set_Computer
);
WindowsFirewall
| where Computer in (ComputersNeedingUpdate)
```

## <a name="next-steps"></a><span data-ttu-id="177aa-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="177aa-228">Next steps</span></span>

<span data-ttu-id="177aa-229">See other lessons for using the Log Analytics query language:</span><span class="sxs-lookup"><span data-stu-id="177aa-229">See other lessons for using the Log Analytics query language:</span></span>

- [<span data-ttu-id="177aa-230">String operations</span><span class="sxs-lookup"><span data-stu-id="177aa-230">String operations</span></span>](string-operations.md)
- [<span data-ttu-id="177aa-231">Date and time operations</span><span class="sxs-lookup"><span data-stu-id="177aa-231">Date and time operations</span></span>](datetime-operations.md)
- [<span data-ttu-id="177aa-232">Aggregation functions</span><span class="sxs-lookup"><span data-stu-id="177aa-232">Aggregation functions</span></span>](aggregations.md)
- [<span data-ttu-id="177aa-233">Advanced aggregations</span><span class="sxs-lookup"><span data-stu-id="177aa-233">Advanced aggregations</span></span>](advanced-aggregations.md)
- [<span data-ttu-id="177aa-234">JSON and data structures</span><span class="sxs-lookup"><span data-stu-id="177aa-234">JSON and data structures</span></span>](json-data-structures.md)
- [<span data-ttu-id="177aa-235">Joins</span><span class="sxs-lookup"><span data-stu-id="177aa-235">Joins</span></span>](joins.md)
- [<span data-ttu-id="177aa-236">Charts</span><span class="sxs-lookup"><span data-stu-id="177aa-236">Charts</span></span>](charts.md)