---
title: Get Started with queries in Azure Log Analytics| Microsoft Docs
description: This article provides a tutorial for getting started writing queries in Log Analytics.
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
ms.date: 08/06/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 71d50a55d9c584b61a1412bb03a03ad99f1bb96c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857335"
---
# <a name="get-started-with-queries-in-log-analytics"></a><span data-ttu-id="cd634-103">Get started with queries in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="cd634-103">Get started with queries in Log Analytics</span></span>


> [!NOTE]
> <span data-ttu-id="cd634-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) before completing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cd634-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) before completing this tutorial.</span></span>


<span data-ttu-id="cd634-105">In this tutorial you will learn to write Azure Log Analytics queries.</span><span class="sxs-lookup"><span data-stu-id="cd634-105">In this tutorial you will learn to write Azure Log Analytics queries.</span></span> <span data-ttu-id="cd634-106">It will teach you how to:</span><span class="sxs-lookup"><span data-stu-id="cd634-106">It will teach you how to:</span></span>

- <span data-ttu-id="cd634-107">Understand queries' structure</span><span class="sxs-lookup"><span data-stu-id="cd634-107">Understand queries' structure</span></span>
- <span data-ttu-id="cd634-108">Sort query results</span><span class="sxs-lookup"><span data-stu-id="cd634-108">Sort query results</span></span>
- <span data-ttu-id="cd634-109">Filter query results</span><span class="sxs-lookup"><span data-stu-id="cd634-109">Filter query results</span></span>
- <span data-ttu-id="cd634-110">Specify a time range</span><span class="sxs-lookup"><span data-stu-id="cd634-110">Specify a time range</span></span>
- <span data-ttu-id="cd634-111">Select which fields to include in the results</span><span class="sxs-lookup"><span data-stu-id="cd634-111">Select which fields to include in the results</span></span>
- <span data-ttu-id="cd634-112">Define and use custom fields</span><span class="sxs-lookup"><span data-stu-id="cd634-112">Define and use custom fields</span></span>
- <span data-ttu-id="cd634-113">Aggregate and group results</span><span class="sxs-lookup"><span data-stu-id="cd634-113">Aggregate and group results</span></span>


## <a name="writing-a-new-query"></a><span data-ttu-id="cd634-114">Writing a new query</span><span class="sxs-lookup"><span data-stu-id="cd634-114">Writing a new query</span></span>
<span data-ttu-id="cd634-115">Queries can start with either a table name or the *search* command.</span><span class="sxs-lookup"><span data-stu-id="cd634-115">Queries can start with either a table name or the *search* command.</span></span> <span data-ttu-id="cd634-116">You should start with a table name, since it defines a clear scope for the query and improves both query performance and relevance of the results.</span><span class="sxs-lookup"><span data-stu-id="cd634-116">You should start with a table name, since it defines a clear scope for the query and improves both query performance and relevance of the results.</span></span>

> [!NOTE]
> <span data-ttu-id="cd634-117">The Azure Log Analytics query language is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="cd634-117">The Azure Log Analytics query language is case-sensitive.</span></span> <span data-ttu-id="cd634-118">Language keywords are typically written in lower-case.</span><span class="sxs-lookup"><span data-stu-id="cd634-118">Language keywords are typically written in lower-case.</span></span> <span data-ttu-id="cd634-119">When using names of tables or columns in a query, make sure to use the correct case, as shown on the schema pane.</span><span class="sxs-lookup"><span data-stu-id="cd634-119">When using names of tables or columns in a query, make sure to use the correct case, as shown on the schema pane.</span></span>

### <a name="table-based-queries"></a><span data-ttu-id="cd634-120">Table-based queries</span><span class="sxs-lookup"><span data-stu-id="cd634-120">Table-based queries</span></span>
<span data-ttu-id="cd634-121">Azure Log Analytics organizes data in tables, each composed of multiple columns.</span><span class="sxs-lookup"><span data-stu-id="cd634-121">Azure Log Analytics organizes data in tables, each composed of multiple columns.</span></span> <span data-ttu-id="cd634-122">All tables and columns are shown on the schema pane, in the Analytics portal.</span><span class="sxs-lookup"><span data-stu-id="cd634-122">All tables and columns are shown on the schema pane, in the Analytics portal.</span></span> <span data-ttu-id="cd634-123">Identify a table that you're interested in and then take a look at a bit of data:</span><span class="sxs-lookup"><span data-stu-id="cd634-123">Identify a table that you're interested in and then take a look at a bit of data:</span></span>

```OQL
SecurityEvent
| take 10
```

<span data-ttu-id="cd634-124">The query shown above returns 10 results from the *SecurityEvent* table, in no specific order.</span><span class="sxs-lookup"><span data-stu-id="cd634-124">The query shown above returns 10 results from the *SecurityEvent* table, in no specific order.</span></span> <span data-ttu-id="cd634-125">This is a very common way to take a glance at a table and understand its structure and content.</span><span class="sxs-lookup"><span data-stu-id="cd634-125">This is a very common way to take a glance at a table and understand its structure and content.</span></span> <span data-ttu-id="cd634-126">Let's examine how it's built:</span><span class="sxs-lookup"><span data-stu-id="cd634-126">Let's examine how it's built:</span></span>

* <span data-ttu-id="cd634-127">The query starts with the table name *SecurityEvent* - this part defines the scope of the query.</span><span class="sxs-lookup"><span data-stu-id="cd634-127">The query starts with the table name *SecurityEvent* - this part defines the scope of the query.</span></span>
* <span data-ttu-id="cd634-128">The pipe (|) character separates commands, so the output of the first one in the input of the following command.</span><span class="sxs-lookup"><span data-stu-id="cd634-128">The pipe (|) character separates commands, so the output of the first one in the input of the following command.</span></span> <span data-ttu-id="cd634-129">You can add any number of piped elements.</span><span class="sxs-lookup"><span data-stu-id="cd634-129">You can add any number of piped elements.</span></span>
* <span data-ttu-id="cd634-130">Following the pipe is the **take** command, which returns a specific number of arbitrary records from the table.</span><span class="sxs-lookup"><span data-stu-id="cd634-130">Following the pipe is the **take** command, which returns a specific number of arbitrary records from the table.</span></span>

<span data-ttu-id="cd634-131">We could actually run the query even without adding `| take 10` - that would still be valid, but it could return up to 10,000 results.</span><span class="sxs-lookup"><span data-stu-id="cd634-131">We could actually run the query even without adding `| take 10` - that would still be valid, but it could return up to 10,000 results.</span></span>

### <a name="search-queries"></a><span data-ttu-id="cd634-132">Search queries</span><span class="sxs-lookup"><span data-stu-id="cd634-132">Search queries</span></span>
<span data-ttu-id="cd634-133">Search queries are less structured, and generally more suited for finding records that include a specific value in any of their columns:</span><span class="sxs-lookup"><span data-stu-id="cd634-133">Search queries are less structured, and generally more suited for finding records that include a specific value in any of their columns:</span></span>

```OQL
search in (SecurityEvent) "Cryptographic"
| take 10
```

<span data-ttu-id="cd634-134">This query searches the *SecurityEvent* table for records that contain the phrase "Cryptographic".</span><span class="sxs-lookup"><span data-stu-id="cd634-134">This query searches the *SecurityEvent* table for records that contain the phrase "Cryptographic".</span></span> <span data-ttu-id="cd634-135">Of those records, 10 records will be returned and displayed.</span><span class="sxs-lookup"><span data-stu-id="cd634-135">Of those records, 10 records will be returned and displayed.</span></span> <span data-ttu-id="cd634-136">If we omit the `in (SecurityEvent)` part and just run `search "Cryptographic"`, the search will go over *all* tables, which would take longer and be less efficient.</span><span class="sxs-lookup"><span data-stu-id="cd634-136">If we omit the `in (SecurityEvent)` part and just run `search "Cryptographic"`, the search will go over *all* tables, which would take longer and be less efficient.</span></span>

> [!NOTE]
> <span data-ttu-id="cd634-137">By default, a time range of _last 24 hours_ is set.</span><span class="sxs-lookup"><span data-stu-id="cd634-137">By default, a time range of _last 24 hours_ is set.</span></span> <span data-ttu-id="cd634-138">To use a different range, use the time-picker (located next to the *Go* button) or add an explicit time range filter to your query.</span><span class="sxs-lookup"><span data-stu-id="cd634-138">To use a different range, use the time-picker (located next to the *Go* button) or add an explicit time range filter to your query.</span></span>

## <a name="sort-and-top"></a><span data-ttu-id="cd634-139">Sort and top</span><span class="sxs-lookup"><span data-stu-id="cd634-139">Sort and top</span></span>
<span data-ttu-id="cd634-140">While **take** is useful to get a few records, the results are selected and displayed in no particular order.</span><span class="sxs-lookup"><span data-stu-id="cd634-140">While **take** is useful to get a few records, the results are selected and displayed in no particular order.</span></span> <span data-ttu-id="cd634-141">To get an ordered view, you could **sort** by the preferred column:</span><span class="sxs-lookup"><span data-stu-id="cd634-141">To get an ordered view, you could **sort** by the preferred column:</span></span>

```
SecurityEvent   
| sort by TimeGenerated desc
```

<span data-ttu-id="cd634-142">That could return too many results though and might also take some time.</span><span class="sxs-lookup"><span data-stu-id="cd634-142">That could return too many results though and might also take some time.</span></span> <span data-ttu-id="cd634-143">The above query sorts *the entire* SecurityEvent table by the TimeGenerated column.</span><span class="sxs-lookup"><span data-stu-id="cd634-143">The above query sorts *the entire* SecurityEvent table by the TimeGenerated column.</span></span> <span data-ttu-id="cd634-144">The Analytics portal then limits the display to show only 10,000 records.</span><span class="sxs-lookup"><span data-stu-id="cd634-144">The Analytics portal then limits the display to show only 10,000 records.</span></span> <span data-ttu-id="cd634-145">This approach is of course not optimal.</span><span class="sxs-lookup"><span data-stu-id="cd634-145">This approach is of course not optimal.</span></span>

<span data-ttu-id="cd634-146">The best way to get only the latest 10 records is to use **top**, which sorts the entire table on the server side and then returns the top records:</span><span class="sxs-lookup"><span data-stu-id="cd634-146">The best way to get only the latest 10 records is to use **top**, which sorts the entire table on the server side and then returns the top records:</span></span>

```OQL
SecurityEvent
| top 10 by TimeGenerated
```

<span data-ttu-id="cd634-147">Descending is the default sorting order, so we typically omit the **desc** argument.The output will look like this:</span><span class="sxs-lookup"><span data-stu-id="cd634-147">Descending is the default sorting order, so we typically omit the **desc** argument.The output will look like this:</span></span>

![Top 10](media/get-started-queries/top10.png)


## <a name="where-filtering-on-a-condition"></a><span data-ttu-id="cd634-149">Where: filtering on a condition</span><span class="sxs-lookup"><span data-stu-id="cd634-149">Where: filtering on a condition</span></span>
<span data-ttu-id="cd634-150">Filters, as indicated by their name, filter the data by a specific condition.</span><span class="sxs-lookup"><span data-stu-id="cd634-150">Filters, as indicated by their name, filter the data by a specific condition.</span></span> <span data-ttu-id="cd634-151">This is the most common way to limit query results to relevant information.</span><span class="sxs-lookup"><span data-stu-id="cd634-151">This is the most common way to limit query results to relevant information.</span></span>

<span data-ttu-id="cd634-152">To add a filter to a query, use the **where** operator followed by one or more conditions.</span><span class="sxs-lookup"><span data-stu-id="cd634-152">To add a filter to a query, use the **where** operator followed by one or more conditions.</span></span> <span data-ttu-id="cd634-153">For example, the following query returns only *SecurityEvent* records where _Level_ equals _8_:</span><span class="sxs-lookup"><span data-stu-id="cd634-153">For example, the following query returns only *SecurityEvent* records where _Level_ equals _8_:</span></span>

```OQL
SecurityEvent
| where Level == 8
```

<span data-ttu-id="cd634-154">When writing filter conditions, you can use the following expressions:</span><span class="sxs-lookup"><span data-stu-id="cd634-154">When writing filter conditions, you can use the following expressions:</span></span>

| <span data-ttu-id="cd634-155">Expression</span><span class="sxs-lookup"><span data-stu-id="cd634-155">Expression</span></span> | <span data-ttu-id="cd634-156">Description</span><span class="sxs-lookup"><span data-stu-id="cd634-156">Description</span></span> | <span data-ttu-id="cd634-157">Example</span><span class="sxs-lookup"><span data-stu-id="cd634-157">Example</span></span> |
|:---|:---|:---|
| == | <span data-ttu-id="cd634-158">Check equality</span><span class="sxs-lookup"><span data-stu-id="cd634-158">Check equality</span></span><br><span data-ttu-id="cd634-159">(case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="cd634-159">(case-sensitive)</span></span> | `Level == 8` |
| =~ | <span data-ttu-id="cd634-160">Check equality</span><span class="sxs-lookup"><span data-stu-id="cd634-160">Check equality</span></span><br><span data-ttu-id="cd634-161">(case-insensitive)</span><span class="sxs-lookup"><span data-stu-id="cd634-161">(case-insensitive)</span></span> | `EventSourceName =~ "microsoft-windows-security-auditing"` |
| <span data-ttu-id="cd634-162">!=, <></span><span class="sxs-lookup"><span data-stu-id="cd634-162">!=, <></span></span> | <span data-ttu-id="cd634-163">Check inequality</span><span class="sxs-lookup"><span data-stu-id="cd634-163">Check inequality</span></span><br><span data-ttu-id="cd634-164">(both expressions are identical)</span><span class="sxs-lookup"><span data-stu-id="cd634-164">(both expressions are identical)</span></span> | `Level != 4` |
| <span data-ttu-id="cd634-165">*and*, *or*</span><span class="sxs-lookup"><span data-stu-id="cd634-165">*and*, *or*</span></span> | <span data-ttu-id="cd634-166">Required between conditions</span><span class="sxs-lookup"><span data-stu-id="cd634-166">Required between conditions</span></span>| `Level == 16 or CommandLine != ""` |

<span data-ttu-id="cd634-167">To filter by multiple conditions, you can either use **and**:</span><span class="sxs-lookup"><span data-stu-id="cd634-167">To filter by multiple conditions, you can either use **and**:</span></span>

```OQL
SecurityEvent
| where Level == 8 and EventID == 4672
```

<span data-ttu-id="cd634-168">or pipe multiple **where** elements one after the other:</span><span class="sxs-lookup"><span data-stu-id="cd634-168">or pipe multiple **where** elements one after the other:</span></span>

```OQL
SecurityEvent
| where Level == 8 
| where EventID == 4672
```
    
> [!NOTE]
> <span data-ttu-id="cd634-169">Values can have different types, so you might need to cast them to perform comparison on the correct type.</span><span class="sxs-lookup"><span data-stu-id="cd634-169">Values can have different types, so you might need to cast them to perform comparison on the correct type.</span></span> <span data-ttu-id="cd634-170">For example, SecurityEvent *Level* column is of type String, so you must cast it to a numerical type such as *int* or *long*, before you can use numerical operators on it: `SecurityEvent | where toint(Level) >= 10`</span><span class="sxs-lookup"><span data-stu-id="cd634-170">For example, SecurityEvent *Level* column is of type String, so you must cast it to a numerical type such as *int* or *long*, before you can use numerical operators on it: `SecurityEvent | where toint(Level) >= 10`</span></span>

## <a name="specify-a-time-range"></a><span data-ttu-id="cd634-171">Specify a time range</span><span class="sxs-lookup"><span data-stu-id="cd634-171">Specify a time range</span></span>

### <a name="time-picker"></a><span data-ttu-id="cd634-172">Time picker</span><span class="sxs-lookup"><span data-stu-id="cd634-172">Time picker</span></span>
<span data-ttu-id="cd634-173">The time picker is in the top left corner , which indicates we’re querying only records from the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="cd634-173">The time picker is in the top left corner , which indicates we’re querying only records from the last 24 hours.</span></span> <span data-ttu-id="cd634-174">This is the default time range applied to all queries.</span><span class="sxs-lookup"><span data-stu-id="cd634-174">This is the default time range applied to all queries.</span></span> <span data-ttu-id="cd634-175">To get only records from the last hour, select _Last hour_ and run the query again.</span><span class="sxs-lookup"><span data-stu-id="cd634-175">To get only records from the last hour, select _Last hour_ and run the query again.</span></span>

![Time Picker](media/get-started-queries/timepicker.png)


### <a name="time-filter-in-query"></a><span data-ttu-id="cd634-177">Time filter in query</span><span class="sxs-lookup"><span data-stu-id="cd634-177">Time filter in query</span></span>
<span data-ttu-id="cd634-178">You can also define your own time range by adding a time filter to the query.</span><span class="sxs-lookup"><span data-stu-id="cd634-178">You can also define your own time range by adding a time filter to the query.</span></span> <span data-ttu-id="cd634-179">It’s best to place the time filter immediately after the table name:</span><span class="sxs-lookup"><span data-stu-id="cd634-179">It’s best to place the time filter immediately after the table name:</span></span> 

```OQL
SecurityEvent
| where TimeGenerated > ago(30m) 
| where toint(Level) >= 10
```

<span data-ttu-id="cd634-180">In the above time filter  `ago(30m)` means "30 minutes ago" so this query only returns records from the last 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="cd634-180">In the above time filter  `ago(30m)` means "30 minutes ago" so this query only returns records from the last 30 minutes.</span></span> <span data-ttu-id="cd634-181">Other units of time include days (2d), minutes (25m), and seconds (10s).</span><span class="sxs-lookup"><span data-stu-id="cd634-181">Other units of time include days (2d), minutes (25m), and seconds (10s).</span></span>


## <a name="project-and-extend-select-and-compute-columns"></a><span data-ttu-id="cd634-182">Project and Extend: select and compute columns</span><span class="sxs-lookup"><span data-stu-id="cd634-182">Project and Extend: select and compute columns</span></span>
<span data-ttu-id="cd634-183">Use **project** to select specific columns to include in the results:</span><span class="sxs-lookup"><span data-stu-id="cd634-183">Use **project** to select specific columns to include in the results:</span></span>

```OQL
SecurityEvent 
| top 10 by TimeGenerated 
| project TimeGenerated, Computer, Activity
```

<span data-ttu-id="cd634-184">The preceding example generates this output:</span><span class="sxs-lookup"><span data-stu-id="cd634-184">The preceding example generates this output:</span></span>

![Log Analytics project results](media/get-started-queries/project.png)

<span data-ttu-id="cd634-186">You can also use **project** to rename columns and define new ones.</span><span class="sxs-lookup"><span data-stu-id="cd634-186">You can also use **project** to rename columns and define new ones.</span></span> <span data-ttu-id="cd634-187">The following example uses project to do the following:</span><span class="sxs-lookup"><span data-stu-id="cd634-187">The following example uses project to do the following:</span></span>

* <span data-ttu-id="cd634-188">Select only the *Computer* and *TimeGenerated* original columns.</span><span class="sxs-lookup"><span data-stu-id="cd634-188">Select only the *Computer* and *TimeGenerated* original columns.</span></span>
* <span data-ttu-id="cd634-189">Rename the *Activity* column to *EventDetails*.</span><span class="sxs-lookup"><span data-stu-id="cd634-189">Rename the *Activity* column to *EventDetails*.</span></span>
* <span data-ttu-id="cd634-190">Create a new column named *EventCode*.</span><span class="sxs-lookup"><span data-stu-id="cd634-190">Create a new column named *EventCode*.</span></span> <span data-ttu-id="cd634-191">The **substring()** function is used to get only the first four characters from the Activity field.</span><span class="sxs-lookup"><span data-stu-id="cd634-191">The **substring()** function is used to get only the first four characters from the Activity field.</span></span>


```OQL
SecurityEvent
| top 10 by TimeGenerated 
| project Computer, TimeGenerated, EventDetails=Activity, EventCode=substring(Activity, 0, 4)
```

<span data-ttu-id="cd634-192">**extend** keeps all original columns in the result set and defines additional ones.</span><span class="sxs-lookup"><span data-stu-id="cd634-192">**extend** keeps all original columns in the result set and defines additional ones.</span></span> <span data-ttu-id="cd634-193">The following query uses **extend** to add a *localtime* column, which contains a localized TimeGenerated value.</span><span class="sxs-lookup"><span data-stu-id="cd634-193">The following query uses **extend** to add a *localtime* column, which contains a localized TimeGenerated value.</span></span>

```OQL
SecurityEvent
| top 10 by TimeGenerated
| extend localtime = TimeGenerated-8h
```

## <a name="summarize-aggregate-groups-of-rows"></a><span data-ttu-id="cd634-194">Summarize: aggregate groups of rows</span><span class="sxs-lookup"><span data-stu-id="cd634-194">Summarize: aggregate groups of rows</span></span>
<span data-ttu-id="cd634-195">Use **summarize** to identify groups of records, according to one or more columns, and apply aggregations to them.</span><span class="sxs-lookup"><span data-stu-id="cd634-195">Use **summarize** to identify groups of records, according to one or more columns, and apply aggregations to them.</span></span> <span data-ttu-id="cd634-196">The most common use os **summarize** is *count*, which returns the number of results in each group.</span><span class="sxs-lookup"><span data-stu-id="cd634-196">The most common use os **summarize** is *count*, which returns the number of results in each group.</span></span>

<span data-ttu-id="cd634-197">The following query reviews all *Perf* records from the last hour, groups them by *ObjectName*, and counts the records in each group:</span><span class="sxs-lookup"><span data-stu-id="cd634-197">The following query reviews all *Perf* records from the last hour, groups them by *ObjectName*, and counts the records in each group:</span></span> 
```OQL
Perf
| where TimeGenerated > ago(1h)
| summarize count() by ObjectName
```

<span data-ttu-id="cd634-198">Sometimes it makes sense to define groups by multiple dimensions.</span><span class="sxs-lookup"><span data-stu-id="cd634-198">Sometimes it makes sense to define groups by multiple dimensions.</span></span> <span data-ttu-id="cd634-199">Each unique combination of these values defines a separate group:</span><span class="sxs-lookup"><span data-stu-id="cd634-199">Each unique combination of these values defines a separate group:</span></span>

```OQL
Perf
| where TimeGenerated > ago(1h)
| summarize count() by ObjectName, CounterName
```

<span data-ttu-id="cd634-200">Another common use is to perform mathematical or statistical calculations on each group.</span><span class="sxs-lookup"><span data-stu-id="cd634-200">Another common use is to perform mathematical or statistical calculations on each group.</span></span> <span data-ttu-id="cd634-201">For example, the following calculates the average *CounterValue* for each computer:</span><span class="sxs-lookup"><span data-stu-id="cd634-201">For example, the following calculates the average *CounterValue* for each computer:</span></span>

```OQL
Perf
| where TimeGenerated > ago(1h)
| summarize avg(CounterValue) by Computer
```

<span data-ttu-id="cd634-202">Unfortunately, the results of this query are meaningless since we mixed together different performance counters.</span><span class="sxs-lookup"><span data-stu-id="cd634-202">Unfortunately, the results of this query are meaningless since we mixed together different performance counters.</span></span> <span data-ttu-id="cd634-203">To make this more meaningful, we should calculate the average separately for each combination of *CounterName* and *Computer*:</span><span class="sxs-lookup"><span data-stu-id="cd634-203">To make this more meaningful, we should calculate the average separately for each combination of *CounterName* and *Computer*:</span></span>

```OQL
Perf
| where TimeGenerated > ago(1h)
| summarize avg(CounterValue) by Computer, CounterName
```

### <a name="summarize-by-a-time-column"></a><span data-ttu-id="cd634-204">Summarize by a time column</span><span class="sxs-lookup"><span data-stu-id="cd634-204">Summarize by a time column</span></span>
<span data-ttu-id="cd634-205">Grouping results can also be based on a time column, or another continuous value.</span><span class="sxs-lookup"><span data-stu-id="cd634-205">Grouping results can also be based on a time column, or another continuous value.</span></span> <span data-ttu-id="cd634-206">Simply summarizing `by TimeGenerated` though would create groups for every single millisecond over the time range, since these are unique values.</span><span class="sxs-lookup"><span data-stu-id="cd634-206">Simply summarizing `by TimeGenerated` though would create groups for every single millisecond over the time range, since these are unique values.</span></span> 

<span data-ttu-id="cd634-207">To create groups based on continuous values, it is best to break the range into manageable units using **bin**.</span><span class="sxs-lookup"><span data-stu-id="cd634-207">To create groups based on continuous values, it is best to break the range into manageable units using **bin**.</span></span> <span data-ttu-id="cd634-208">The following query analyzes *Perf* records that measure free memory (*Available MBytes*) on a specific computer.</span><span class="sxs-lookup"><span data-stu-id="cd634-208">The following query analyzes *Perf* records that measure free memory (*Available MBytes*) on a specific computer.</span></span> <span data-ttu-id="cd634-209">It calculates the average value for each period if 1 hour, over the last 2 days:</span><span class="sxs-lookup"><span data-stu-id="cd634-209">It calculates the average value for each period if 1 hour, over the last 2 days:</span></span>

```OQL
Perf 
| where TimeGenerated > ago(2d)
| where Computer == "ContosoAzADDS2" 
| where CounterName == "Available MBytes" 
| summarize count() by bin(TimeGenerated, 1h)
```

<span data-ttu-id="cd634-210">To make the output clearer, you select to display it as a time-chart, showing the available memory over time:</span><span class="sxs-lookup"><span data-stu-id="cd634-210">To make the output clearer, you select to display it as a time-chart, showing the available memory over time:</span></span>

![Log Analytics memory over time](media/get-started-queries/chart.png)



## <a name="next-steps"></a><span data-ttu-id="cd634-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd634-212">Next steps</span></span>

- <span data-ttu-id="cd634-213">Learn about [writing search queries](search-queries.md)</span><span class="sxs-lookup"><span data-stu-id="cd634-213">Learn about [writing search queries](search-queries.md)</span></span>