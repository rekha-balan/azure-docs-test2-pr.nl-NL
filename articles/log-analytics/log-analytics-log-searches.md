---
title: Find data with log searches in Azure Log Analytics | Microsoft Docs
description: Log searches allow you to combine and correlate any machine data from multiple sources within your environment.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e4a4c7ec784476086cc218e91beca17200a656e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564017"
---
# <a name="find-data-using-log-searches"></a><span data-ttu-id="429c6-103">Find data using log searches</span><span class="sxs-lookup"><span data-stu-id="429c6-103">Find data using log searches</span></span>

<span data-ttu-id="429c6-104">At the core of Log Analytics is the log search feature which allows you to combine and correlate any machine data from multiple sources within your environment.</span><span class="sxs-lookup"><span data-stu-id="429c6-104">At the core of Log Analytics is the log search feature which allows you to combine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="429c6-105">Solutions are also powered by log search to bring you metrics pivoted around a particular problem area.</span><span class="sxs-lookup"><span data-stu-id="429c6-105">Solutions are also powered by log search to bring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="429c6-106">On the Search page, you can create a query, and then when you search, you can filter the results by using facet controls.</span><span class="sxs-lookup"><span data-stu-id="429c6-106">On the Search page, you can create a query, and then when you search, you can filter the results by using facet controls.</span></span> <span data-ttu-id="429c6-107">You can also create advanced queries to transform, filter, and report on your results.</span><span class="sxs-lookup"><span data-stu-id="429c6-107">You can also create advanced queries to transform, filter, and report on your results.</span></span>

<span data-ttu-id="429c6-108">Common log search queries appear on most solution pages.</span><span class="sxs-lookup"><span data-stu-id="429c6-108">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="429c6-109">Throughout the OMS console, you can click tiles or drill in to other items to view details about the item by using log search.</span><span class="sxs-lookup"><span data-stu-id="429c6-109">Throughout the OMS console, you can click tiles or drill in to other items to view details about the item by using log search.</span></span>

<span data-ttu-id="429c6-110">In this tutorial, we'll walk through examples to cover all the basics when you use log search.</span><span class="sxs-lookup"><span data-stu-id="429c6-110">In this tutorial, we'll walk through examples to cover all the basics when you use log search.</span></span>

<span data-ttu-id="429c6-111">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how to use the syntax to extract the insights you want from the data.</span><span class="sxs-lookup"><span data-stu-id="429c6-111">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how to use the syntax to extract the insights you want from the data.</span></span>

<span data-ttu-id="429c6-112">After you've familiar with search techniques, you can review the [Log Analytics log search reference](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="429c6-112">After you've familiar with search techniques, you can review the [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="429c6-113">Use basic filters</span><span class="sxs-lookup"><span data-stu-id="429c6-113">Use basic filters</span></span>
<span data-ttu-id="429c6-114">The first thing to know is that the first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span><span class="sxs-lookup"><span data-stu-id="429c6-114">The first thing to know is that the first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="429c6-115">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data to pull out of the OMS data store.</span><span class="sxs-lookup"><span data-stu-id="429c6-115">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data to pull out of the OMS data store.</span></span> <span data-ttu-id="429c6-116">Searching in the data store is largely about specifying the characteristics of the data that you want to extract, so it is natural that a query would start with the WHERE clause.</span><span class="sxs-lookup"><span data-stu-id="429c6-116">Searching in the data store is largely about specifying the characteristics of the data that you want to extract, so it is natural that a query would start with the WHERE clause.</span></span>

<span data-ttu-id="429c6-117">The most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span><span class="sxs-lookup"><span data-stu-id="429c6-117">The most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="429c6-118">These types of simple queries generally return diverse shapes of data within the same result set.</span><span class="sxs-lookup"><span data-stu-id="429c6-118">These types of simple queries generally return diverse shapes of data within the same result set.</span></span> <span data-ttu-id="429c6-119">This is because Log Analytics has different *types* of data in the system.</span><span class="sxs-lookup"><span data-stu-id="429c6-119">This is because Log Analytics has different *types* of data in the system.</span></span>

### <a name="to-conduct-a-simple-search"></a><span data-ttu-id="429c6-120">To conduct a simple search</span><span class="sxs-lookup"><span data-stu-id="429c6-120">To conduct a simple search</span></span>
1. <span data-ttu-id="429c6-121">In the OMS portal, click **Log Search**.</span><span class="sxs-lookup"><span data-stu-id="429c6-121">In the OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="429c6-122">![search tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="429c6-122">![search tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="429c6-123">In the query field, type `error` and then click **Search**.</span><span class="sxs-lookup"><span data-stu-id="429c6-123">In the query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="429c6-124">![search error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="429c6-124">![search error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="429c6-125">For example, the query for `error` in the following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by the Change Tracking).</span><span class="sxs-lookup"><span data-stu-id="429c6-125">For example, the query for `error` in the following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by the Change Tracking).</span></span>   
    <span data-ttu-id="429c6-126">![search results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="429c6-126">![search results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="429c6-127">These filters are not really object types/classes.</span><span class="sxs-lookup"><span data-stu-id="429c6-127">These filters are not really object types/classes.</span></span> <span data-ttu-id="429c6-128">*Type* is just a tag, or a property, or a string/name/category, that is attached to a piece of data.</span><span class="sxs-lookup"><span data-stu-id="429c6-128">*Type* is just a tag, or a property, or a string/name/category, that is attached to a piece of data.</span></span> <span data-ttu-id="429c6-129">Some documents in the system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span><span class="sxs-lookup"><span data-stu-id="429c6-129">Some documents in the system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="429c6-130">Each search result, document, record, or entry displays all the raw properties and their values for each of those pieces of data, and you can use those field names to specify in the filter when you want to retrieve only the records where the field has that given value.</span><span class="sxs-lookup"><span data-stu-id="429c6-130">Each search result, document, record, or entry displays all the raw properties and their values for each of those pieces of data, and you can use those field names to specify in the filter when you want to retrieve only the records where the field has that given value.</span></span>

<span data-ttu-id="429c6-131">*Type* is really just a field that all records have, it is not different from any other field.</span><span class="sxs-lookup"><span data-stu-id="429c6-131">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="429c6-132">This was established based on the value of the Type field.</span><span class="sxs-lookup"><span data-stu-id="429c6-132">This was established based on the value of the Type field.</span></span> <span data-ttu-id="429c6-133">That record will have a different shape or form.</span><span class="sxs-lookup"><span data-stu-id="429c6-133">That record will have a different shape or form.</span></span> <span data-ttu-id="429c6-134">Incidentally, **Type=Perf**, or **Type=Event** is also the syntax that you need to learn to query for performance data or events.</span><span class="sxs-lookup"><span data-stu-id="429c6-134">Incidentally, **Type=Perf**, or **Type=Event** is also the syntax that you need to learn to query for performance data or events.</span></span>

<span data-ttu-id="429c6-135">You can use either a colon (:) or an equal sign (=) after the field name and before the value.</span><span class="sxs-lookup"><span data-stu-id="429c6-135">You can use either a colon (:) or an equal sign (=) after the field name and before the value.</span></span> <span data-ttu-id="429c6-136">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose the style you prefer.</span><span class="sxs-lookup"><span data-stu-id="429c6-136">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose the style you prefer.</span></span>

<span data-ttu-id="429c6-137">So, if the Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="429c6-137">So, if the Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="429c6-138">This will give you only the performance data where the performance counter name is "% Processor Time".</span><span class="sxs-lookup"><span data-stu-id="429c6-138">This will give you only the performance data where the performance counter name is "% Processor Time".</span></span>

### <a name="to-search-for-processor-time-performance-data"></a><span data-ttu-id="429c6-139">To search for processor time performance data</span><span class="sxs-lookup"><span data-stu-id="429c6-139">To search for processor time performance data</span></span>
* <span data-ttu-id="429c6-140">In the search query field, type `Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="429c6-140">In the search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="429c6-141">You can also be more specific and use **InstanceName=_'Total'** in the query, which is a Windows performance counter.</span><span class="sxs-lookup"><span data-stu-id="429c6-141">You can also be more specific and use **InstanceName=_'Total'** in the query, which is a Windows performance counter.</span></span> <span data-ttu-id="429c6-142">You can also select a facet and another **field:value**.</span><span class="sxs-lookup"><span data-stu-id="429c6-142">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="429c6-143">The filter is automatically added to your filter in the query bar.</span><span class="sxs-lookup"><span data-stu-id="429c6-143">The filter is automatically added to your filter in the query bar.</span></span> <span data-ttu-id="429c6-144">You can see this in the following image.</span><span class="sxs-lookup"><span data-stu-id="429c6-144">You can see this in the following image.</span></span> <span data-ttu-id="429c6-145">It shows you where to click to add **InstanceName:’_Total’** to the query without typing anything.</span><span class="sxs-lookup"><span data-stu-id="429c6-145">It shows you where to click to add **InstanceName:’_Total’** to the query without typing anything.</span></span>

![search facet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="429c6-147">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="429c6-147">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="429c6-148">In this example, you don't have to specify **Type=Perf** to get to this result.</span><span class="sxs-lookup"><span data-stu-id="429c6-148">In this example, you don't have to specify **Type=Perf** to get to this result.</span></span> <span data-ttu-id="429c6-149">Because the fields CounterName and InstanceName only exist for records of Type=Perf, the query is specific enough to return the same results as the longer, previous one:</span><span class="sxs-lookup"><span data-stu-id="429c6-149">Because the fields CounterName and InstanceName only exist for records of Type=Perf, the query is specific enough to return the same results as the longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="429c6-150">This is because all the filters in the query are evaluated as being in *AND* with each other.</span><span class="sxs-lookup"><span data-stu-id="429c6-150">This is because all the filters in the query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="429c6-151">Effectively, the more fields you add to the criteria, you get less, more specific and refined results.</span><span class="sxs-lookup"><span data-stu-id="429c6-151">Effectively, the more fields you add to the criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="429c6-152">For example, the query `Type=Event EventLog="Windows PowerShell"` is identical to `Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="429c6-152">For example, the query `Type=Event EventLog="Windows PowerShell"` is identical to `Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="429c6-153">It returns all events that were logged in and collected from the Windows PowerShell event log.</span><span class="sxs-lookup"><span data-stu-id="429c6-153">It returns all events that were logged in and collected from the Windows PowerShell event log.</span></span> <span data-ttu-id="429c6-154">If you add a filter multiple times by repeatedly selecting the same facet, then the issue is purely cosmetic--it might clutter the Search bar, but it still returns the same results because the implicit AND operator is always there.</span><span class="sxs-lookup"><span data-stu-id="429c6-154">If you add a filter multiple times by repeatedly selecting the same facet, then the issue is purely cosmetic--it might clutter the Search bar, but it still returns the same results because the implicit AND operator is always there.</span></span>

<span data-ttu-id="429c6-155">You can easily reverse the implicit AND operator by using a NOT operator explicitly.</span><span class="sxs-lookup"><span data-stu-id="429c6-155">You can easily reverse the implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="429c6-156">For example:</span><span class="sxs-lookup"><span data-stu-id="429c6-156">For example:</span></span>

<span data-ttu-id="429c6-157">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT the Windows PowerShell log.</span><span class="sxs-lookup"><span data-stu-id="429c6-157">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT the Windows PowerShell log.</span></span>

<span data-ttu-id="429c6-158">Or, you can use other Boolean operator such as ‘OR’.</span><span class="sxs-lookup"><span data-stu-id="429c6-158">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="429c6-159">The following query returns records for which the EventLog is either Application OR System.</span><span class="sxs-lookup"><span data-stu-id="429c6-159">The following query returns records for which the EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="429c6-160">Using the above query, you’ll get entries for both logs in the same result set.</span><span class="sxs-lookup"><span data-stu-id="429c6-160">Using the above query, you’ll get entries for both logs in the same result set.</span></span>

<span data-ttu-id="429c6-161">However, if you remove the OR by leaving the implicit AND in place, then the following query will not produce any results because there isn’t an event log entry that belongs to BOTH logs.</span><span class="sxs-lookup"><span data-stu-id="429c6-161">However, if you remove the OR by leaving the implicit AND in place, then the following query will not produce any results because there isn’t an event log entry that belongs to BOTH logs.</span></span> <span data-ttu-id="429c6-162">Each event log entry was written to only one of the two logs.</span><span class="sxs-lookup"><span data-stu-id="429c6-162">Each event log entry was written to only one of the two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="429c6-163">Use additional filters</span><span class="sxs-lookup"><span data-stu-id="429c6-163">Use additional filters</span></span>
<span data-ttu-id="429c6-164">The following query returns entries for 2 event logs for all the computers that have sent data.</span><span class="sxs-lookup"><span data-stu-id="429c6-164">The following query returns entries for 2 event logs for all the computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![search results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="429c6-166">Selecting one of the fields or filters will narrow the query to a specific computer, excluding all other ones.</span><span class="sxs-lookup"><span data-stu-id="429c6-166">Selecting one of the fields or filters will narrow the query to a specific computer, excluding all other ones.</span></span> <span data-ttu-id="429c6-167">The resulting query would resemble the following.</span><span class="sxs-lookup"><span data-stu-id="429c6-167">The resulting query would resemble the following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="429c6-168">Which is equivalent to the following, because of the implicit AND.</span><span class="sxs-lookup"><span data-stu-id="429c6-168">Which is equivalent to the following, because of the implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="429c6-169">Each query is evaluated in the following explicit order.</span><span class="sxs-lookup"><span data-stu-id="429c6-169">Each query is evaluated in the following explicit order.</span></span> <span data-ttu-id="429c6-170">Note the parenthesis.</span><span class="sxs-lookup"><span data-stu-id="429c6-170">Note the parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="429c6-171">Just like the event log field, you can retrieve data only for a set of specific computers by adding OR.</span><span class="sxs-lookup"><span data-stu-id="429c6-171">Just like the event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="429c6-172">For example:</span><span class="sxs-lookup"><span data-stu-id="429c6-172">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="429c6-173">Similarly, this the following query return **% CPU Time** for the selected two computers only.</span><span class="sxs-lookup"><span data-stu-id="429c6-173">Similarly, this the following query return **% CPU Time** for the selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```


### <a name="boolean-operators"></a><span data-ttu-id="429c6-174">Boolean operators</span><span class="sxs-lookup"><span data-stu-id="429c6-174">Boolean operators</span></span>
<span data-ttu-id="429c6-175">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span><span class="sxs-lookup"><span data-stu-id="429c6-175">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="429c6-176">You can use simple operators such as >, < , >=, <= , != in the query search bar.</span><span class="sxs-lookup"><span data-stu-id="429c6-176">You can use simple operators such as >, < , >=, <= , != in the query search bar.</span></span>

<span data-ttu-id="429c6-177">You can query a specific event log for a specific period of time.</span><span class="sxs-lookup"><span data-stu-id="429c6-177">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="429c6-178">For example, the last 24 hours is expressed with the following mnemonic expression.</span><span class="sxs-lookup"><span data-stu-id="429c6-178">For example, the last 24 hours is expressed with the following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="to-search-using-a-boolean-operator"></a><span data-ttu-id="429c6-179">To search using a boolean operator</span><span class="sxs-lookup"><span data-stu-id="429c6-179">To search using a boolean operator</span></span>
* <span data-ttu-id="429c6-180">In the search query field, type `EventLog=System TimeGenerated>NOW-24HOURS"`</span><span class="sxs-lookup"><span data-stu-id="429c6-180">In the search query field, type `EventLog=System TimeGenerated>NOW-24HOURS"`</span></span>  
    <span data-ttu-id="429c6-181">![search with boolean](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="429c6-181">![search with boolean](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="429c6-182">Although you can control the time interval graphically, and most times you might want to do that, there are advantages to including a time filter directly into the query.</span><span class="sxs-lookup"><span data-stu-id="429c6-182">Although you can control the time interval graphically, and most times you might want to do that, there are advantages to including a time filter directly into the query.</span></span> <span data-ttu-id="429c6-183">For example, this works great with dashboards where you can override the time for each tile, regardless of the *global* time selector on the dashboard page.</span><span class="sxs-lookup"><span data-stu-id="429c6-183">For example, this works great with dashboards where you can override the time for each tile, regardless of the *global* time selector on the dashboard page.</span></span> <span data-ttu-id="429c6-184">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="429c6-184">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="429c6-185">When filtering by time, keep in mind that you get results for the *intersection* of the two time periods: the one specified in the OMS portal (S1) and the one specified in the query (S2).</span><span class="sxs-lookup"><span data-stu-id="429c6-185">When filtering by time, keep in mind that you get results for the *intersection* of the two time periods: the one specified in the OMS portal (S1) and the one specified in the query (S2).</span></span>

![intersection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="429c6-187">This means, if the time periods don’t intersect, for example in the OMS portal where you choose **This week** and in the query where you define **last week**, then there is no intersection and you won't receive any results.</span><span class="sxs-lookup"><span data-stu-id="429c6-187">This means, if the time periods don’t intersect, for example in the OMS portal where you choose **This week** and in the query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="429c6-188">Comparison operators used for the TimeGenerated field are also useful in other situations.</span><span class="sxs-lookup"><span data-stu-id="429c6-188">Comparison operators used for the TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="429c6-189">For example, with numeric fields.</span><span class="sxs-lookup"><span data-stu-id="429c6-189">For example, with numeric fields.</span></span>

<span data-ttu-id="429c6-190">For example, given that Configuration Assessment’s alerts have the following severity values:</span><span class="sxs-lookup"><span data-stu-id="429c6-190">For example, given that Configuration Assessment’s alerts have the following severity values:</span></span>

* <span data-ttu-id="429c6-191">0 = Information</span><span class="sxs-lookup"><span data-stu-id="429c6-191">0 = Information</span></span>
* <span data-ttu-id="429c6-192">1 = Warning</span><span class="sxs-lookup"><span data-stu-id="429c6-192">1 = Warning</span></span>
* <span data-ttu-id="429c6-193">2 = Critical</span><span class="sxs-lookup"><span data-stu-id="429c6-193">2 = Critical</span></span>

<span data-ttu-id="429c6-194">You can query for both warning and critical alerts and also exclude informational ones with the following query:</span><span class="sxs-lookup"><span data-stu-id="429c6-194">You can query for both warning and critical alerts and also exclude informational ones with the following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="429c6-195">You can also use range queries.</span><span class="sxs-lookup"><span data-stu-id="429c6-195">You can also use range queries.</span></span> <span data-ttu-id="429c6-196">This means that you can provide the beginning and end range of values in a sequence.</span><span class="sxs-lookup"><span data-stu-id="429c6-196">This means that you can provide the beginning and end range of values in a sequence.</span></span> <span data-ttu-id="429c6-197">For example, if you want events from the Operations Manager event log where the EventID is greater than or equal to 2100 but not greater than 2199, then the following query would return them.</span><span class="sxs-lookup"><span data-stu-id="429c6-197">For example, if you want events from the Operations Manager event log where the EventID is greater than or equal to 2100 but not greater than 2199, then the following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="429c6-198">The range syntax you must use is the colon (:) field:value separator and *not* the equal sign (=).</span><span class="sxs-lookup"><span data-stu-id="429c6-198">The range syntax you must use is the colon (:) field:value separator and *not* the equal sign (=).</span></span> <span data-ttu-id="429c6-199">Enclose the lower and upper end of the range in square brackets and separate them with two periods (..).</span><span class="sxs-lookup"><span data-stu-id="429c6-199">Enclose the lower and upper end of the range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="429c6-200">Manipulate search results</span><span class="sxs-lookup"><span data-stu-id="429c6-200">Manipulate search results</span></span>
<span data-ttu-id="429c6-201">When you're searching for data, you'll want to refine your search query and have a good level of control over the results.</span><span class="sxs-lookup"><span data-stu-id="429c6-201">When you're searching for data, you'll want to refine your search query and have a good level of control over the results.</span></span> <span data-ttu-id="429c6-202">When results are retrieved, you can apply commands to transform them.</span><span class="sxs-lookup"><span data-stu-id="429c6-202">When results are retrieved, you can apply commands to transform them.</span></span>

<span data-ttu-id="429c6-203">Commands in Log Analytics searches *must* follow after the vertical pipe character (|).</span><span class="sxs-lookup"><span data-stu-id="429c6-203">Commands in Log Analytics searches *must* follow after the vertical pipe character (|).</span></span> <span data-ttu-id="429c6-204">A filter must always be the first part of a query string.</span><span class="sxs-lookup"><span data-stu-id="429c6-204">A filter must always be the first part of a query string.</span></span> <span data-ttu-id="429c6-205">It defines the data set you're working with and then "pipes" those results into a command.</span><span class="sxs-lookup"><span data-stu-id="429c6-205">It defines the data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="429c6-206">You can then use the pipe to add additional commands.</span><span class="sxs-lookup"><span data-stu-id="429c6-206">You can then use the pipe to add additional commands.</span></span> <span data-ttu-id="429c6-207">This is loosely similar to the Windows PowerShell pipeline.</span><span class="sxs-lookup"><span data-stu-id="429c6-207">This is loosely similar to the Windows PowerShell pipeline.</span></span>

<span data-ttu-id="429c6-208">In general, the Log Analytics search language tries to follow PowerShell style and guidelines to make it similar to the IT pros, and to ease the learning curve.</span><span class="sxs-lookup"><span data-stu-id="429c6-208">In general, the Log Analytics search language tries to follow PowerShell style and guidelines to make it similar to the IT pros, and to ease the learning curve.</span></span>

<span data-ttu-id="429c6-209">Commands have names of verbs so you can easily tell what they do.</span><span class="sxs-lookup"><span data-stu-id="429c6-209">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="429c6-210">Sort</span><span class="sxs-lookup"><span data-stu-id="429c6-210">Sort</span></span>
<span data-ttu-id="429c6-211">The sort command allows you to define the sorting order by one or multiple fields.</span><span class="sxs-lookup"><span data-stu-id="429c6-211">The sort command allows you to define the sorting order by one or multiple fields.</span></span> <span data-ttu-id="429c6-212">Even if you don’t use it, by default, a time descending order is enforced.</span><span class="sxs-lookup"><span data-stu-id="429c6-212">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="429c6-213">The most recent results are always at the top of search results.</span><span class="sxs-lookup"><span data-stu-id="429c6-213">The most recent results are always at the top of search results.</span></span> <span data-ttu-id="429c6-214">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span><span class="sxs-lookup"><span data-stu-id="429c6-214">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="429c6-215">That's because it is the type of experience you are familiar with in logs.</span><span class="sxs-lookup"><span data-stu-id="429c6-215">That's because it is the type of experience you are familiar with in logs.</span></span> <span data-ttu-id="429c6-216">For example, in the Windows Event Viewer.</span><span class="sxs-lookup"><span data-stu-id="429c6-216">For example, in the Windows Event Viewer.</span></span>

<span data-ttu-id="429c6-217">You can use Sort to change the way results are returned.</span><span class="sxs-lookup"><span data-stu-id="429c6-217">You can use Sort to change the way results are returned.</span></span> <span data-ttu-id="429c6-218">The following examples show how this works.</span><span class="sxs-lookup"><span data-stu-id="429c6-218">The following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="429c6-219">The simple examples above show you how commands work--they change the shape of the results that the filter returned.</span><span class="sxs-lookup"><span data-stu-id="429c6-219">The simple examples above show you how commands work--they change the shape of the results that the filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="429c6-220">Limit and top</span><span class="sxs-lookup"><span data-stu-id="429c6-220">Limit and top</span></span>
<span data-ttu-id="429c6-221">Another less known command is LIMIT.</span><span class="sxs-lookup"><span data-stu-id="429c6-221">Another less known command is LIMIT.</span></span> <span data-ttu-id="429c6-222">Limit is a PowerShell-like verb.</span><span class="sxs-lookup"><span data-stu-id="429c6-222">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="429c6-223">Limit is functionally identical to the TOP command.</span><span class="sxs-lookup"><span data-stu-id="429c6-223">Limit is functionally identical to the TOP command.</span></span> <span data-ttu-id="429c6-224">The following queries return the same results.</span><span class="sxs-lookup"><span data-stu-id="429c6-224">The following queries return the same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="to-search-using-top"></a><span data-ttu-id="429c6-225">To search using top</span><span class="sxs-lookup"><span data-stu-id="429c6-225">To search using top</span></span>
* <span data-ttu-id="429c6-226">In the search query field, type `Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="429c6-226">In the search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="429c6-227">![search top](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="429c6-227">![search top](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="429c6-228">In the image above, there are 358 thousand records with EventID=600.</span><span class="sxs-lookup"><span data-stu-id="429c6-228">In the image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="429c6-229">The fields, facets, and filters on the left always show information about the results returned *by the filter portion* of the query, which is the part before any pipe character.</span><span class="sxs-lookup"><span data-stu-id="429c6-229">The fields, facets, and filters on the left always show information about the results returned *by the filter portion* of the query, which is the part before any pipe character.</span></span> <span data-ttu-id="429c6-230">The **Results** pane only returns the most recent 1 result, because the example command shaped and transformed the results.</span><span class="sxs-lookup"><span data-stu-id="429c6-230">The **Results** pane only returns the most recent 1 result, because the example command shaped and transformed the results.</span></span>

### <a name="select"></a><span data-ttu-id="429c6-231">Select</span><span class="sxs-lookup"><span data-stu-id="429c6-231">Select</span></span>
<span data-ttu-id="429c6-232">The SELECT command behaves like Select-Object in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="429c6-232">The SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="429c6-233">It returns filtered results that do not have all of their original properties.</span><span class="sxs-lookup"><span data-stu-id="429c6-233">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="429c6-234">Instead, it selects only the properties that you specify.</span><span class="sxs-lookup"><span data-stu-id="429c6-234">Instead, it selects only the properties that you specify.</span></span>

#### <a name="to-run-a-search-using-the-select-command"></a><span data-ttu-id="429c6-235">To run a search using the select command</span><span class="sxs-lookup"><span data-stu-id="429c6-235">To run a search using the select command</span></span>
1. <span data-ttu-id="429c6-236">In Search, type `Type=Event` and then click **Search**.</span><span class="sxs-lookup"><span data-stu-id="429c6-236">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="429c6-237">Click **+ show more** in one of the results to view all the properties that the results have.</span><span class="sxs-lookup"><span data-stu-id="429c6-237">Click **+ show more** in one of the results to view all the properties that the results have.</span></span>
3. <span data-ttu-id="429c6-238">Select some of those explicitly, and the query changes to `Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="429c6-238">Select some of those explicitly, and the query changes to `Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="429c6-239">![search select](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="429c6-239">![search select](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="429c6-240">This is command particularly useful when you want to control search output and choose only the portions of data that really matter for your exploration, which often isn’t the full record.</span><span class="sxs-lookup"><span data-stu-id="429c6-240">This is command particularly useful when you want to control search output and choose only the portions of data that really matter for your exploration, which often isn’t the full record.</span></span> <span data-ttu-id="429c6-241">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span><span class="sxs-lookup"><span data-stu-id="429c6-241">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="429c6-242">The, you can generate output that looks more naturally like a table, or work well when exported to a CSV file and then massaged in Excel.</span><span class="sxs-lookup"><span data-stu-id="429c6-242">The, you can generate output that looks more naturally like a table, or work well when exported to a CSV file and then massaged in Excel.</span></span>

## <a name="use-the-measure-command"></a><span data-ttu-id="429c6-243">Use the measure command</span><span class="sxs-lookup"><span data-stu-id="429c6-243">Use the measure command</span></span>
<span data-ttu-id="429c6-244">MEASURE is one of the most versatile commands in Log Analytics searches.</span><span class="sxs-lookup"><span data-stu-id="429c6-244">MEASURE is one of the most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="429c6-245">It allows you to apply statistical *functions* to your data and aggregate results grouped by a given field.</span><span class="sxs-lookup"><span data-stu-id="429c6-245">It allows you to apply statistical *functions* to your data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="429c6-246">There are multiple statistical functions that Measure supports.</span><span class="sxs-lookup"><span data-stu-id="429c6-246">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="429c6-247">Measure count()</span><span class="sxs-lookup"><span data-stu-id="429c6-247">Measure count()</span></span>
<span data-ttu-id="429c6-248">The first statistical function to work with, and one of the simplest to understand is the *count()* function.</span><span class="sxs-lookup"><span data-stu-id="429c6-248">The first statistical function to work with, and one of the simplest to understand is the *count()* function.</span></span>

<span data-ttu-id="429c6-249">Results from any search query such as `Type=Event`, show filters also called facets on the left side of search results.</span><span class="sxs-lookup"><span data-stu-id="429c6-249">Results from any search query such as `Type=Event`, show filters also called facets on the left side of search results.</span></span> <span data-ttu-id="429c6-250">The filters show a distribution of values by a given field for the results in the search executed.</span><span class="sxs-lookup"><span data-stu-id="429c6-250">The filters show a distribution of values by a given field for the results in the search executed.</span></span>

![search measure count](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="429c6-252">For example, in the image above you'll see the **Computer** field and it shows that within the almost 739 thousand events in the results, there are 68 unique and distinct values for the **Computer** field in those records.</span><span class="sxs-lookup"><span data-stu-id="429c6-252">For example, in the image above you'll see the **Computer** field and it shows that within the almost 739 thousand events in the results, there are 68 unique and distinct values for the **Computer** field in those records.</span></span> <span data-ttu-id="429c6-253">The tile only shows the top 5, which are the most common 5 values that are written in the **Computer** fields), sorted by the number of documents that contain that specific value in that field.</span><span class="sxs-lookup"><span data-stu-id="429c6-253">The tile only shows the top 5, which are the most common 5 values that are written in the **Computer** fields), sorted by the number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="429c6-254">In the image you can see that – among those almost 369 thousand events – 90 thousand come from the OpsInsights04.contoso.com computer, 83 thousand from the DB03.contoso.com computer, and so on.</span><span class="sxs-lookup"><span data-stu-id="429c6-254">In the image you can see that – among those almost 369 thousand events – 90 thousand come from the OpsInsights04.contoso.com computer, 83 thousand from the DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="429c6-255">What if you want to see all values, since the tile only shows only the top 5?</span><span class="sxs-lookup"><span data-stu-id="429c6-255">What if you want to see all values, since the tile only shows only the top 5?</span></span>

<span data-ttu-id="429c6-256">That’s what the measure command can do with the count() function.</span><span class="sxs-lookup"><span data-stu-id="429c6-256">That’s what the measure command can do with the count() function.</span></span> <span data-ttu-id="429c6-257">This function doesn't use any parameters.</span><span class="sxs-lookup"><span data-stu-id="429c6-257">This function doesn't use any parameters.</span></span> <span data-ttu-id="429c6-258">You just specify the field by which you want to group by – the **Computer** field in this case:</span><span class="sxs-lookup"><span data-stu-id="429c6-258">You just specify the field by which you want to group by – the **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![search measure count](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="429c6-260">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span><span class="sxs-lookup"><span data-stu-id="429c6-260">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="429c6-261">Just the values *in* the data can describe which entity generated them, and a number of other characteristics and aspects of the data – hence the term *facet*.</span><span class="sxs-lookup"><span data-stu-id="429c6-261">Just the values *in* the data can describe which entity generated them, and a number of other characteristics and aspects of the data – hence the term *facet*.</span></span> <span data-ttu-id="429c6-262">However, you can just as well group by other fields.</span><span class="sxs-lookup"><span data-stu-id="429c6-262">However, you can just as well group by other fields.</span></span> <span data-ttu-id="429c6-263">Because the original results of almost 739 thousand events that are piped into the measure command also have a field called **EventID**, you can apply the same technique to group by that field and get a count of events by EventID:</span><span class="sxs-lookup"><span data-stu-id="429c6-263">Because the original results of almost 739 thousand events that are piped into the measure command also have a field called **EventID**, you can apply the same technique to group by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="429c6-264">If you're not interested in the actual record count that contain a specific value, but instead if you only want a list of the values themselves, you can add a *Select* command at the end of it and just select the first column:</span><span class="sxs-lookup"><span data-stu-id="429c6-264">If you're not interested in the actual record count that contain a specific value, but instead if you only want a list of the values themselves, you can add a *Select* command at the end of it and just select the first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="429c6-265">Then you can get more intricate and pre-sort the results in the query, or you can just click the columns in the grid, too.</span><span class="sxs-lookup"><span data-stu-id="429c6-265">Then you can get more intricate and pre-sort the results in the query, or you can just click the columns in the grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="to-search-using-measure-count"></a><span data-ttu-id="429c6-266">To search using measure count</span><span class="sxs-lookup"><span data-stu-id="429c6-266">To search using measure count</span></span>
* <span data-ttu-id="429c6-267">In the search query field, type `Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="429c6-267">In the search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="429c6-268">Append `| Select EventID` to the end of the query.</span><span class="sxs-lookup"><span data-stu-id="429c6-268">Append `| Select EventID` to the end of the query.</span></span>
* <span data-ttu-id="429c6-269">Finally, append `| Sort EventID asc` to the end of the query.</span><span class="sxs-lookup"><span data-stu-id="429c6-269">Finally, append `| Sort EventID asc` to the end of the query.</span></span>

<span data-ttu-id="429c6-270">There are a couple important points to notice and emphasize:</span><span class="sxs-lookup"><span data-stu-id="429c6-270">There are a couple important points to notice and emphasize:</span></span>

<span data-ttu-id="429c6-271">First, the results you see are not the original raw results anymore.</span><span class="sxs-lookup"><span data-stu-id="429c6-271">First, the results you see are not the original raw results anymore.</span></span> <span data-ttu-id="429c6-272">Instead, they are aggregated results – essentially groups of results.</span><span class="sxs-lookup"><span data-stu-id="429c6-272">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="429c6-273">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from the original raw shape that gets created on the fly as a result of the aggregation/statistical function.</span><span class="sxs-lookup"><span data-stu-id="429c6-273">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from the original raw shape that gets created on the fly as a result of the aggregation/statistical function.</span></span>

<span data-ttu-id="429c6-274">Second, **Measure count** currently returns only the top 100 distinct results.</span><span class="sxs-lookup"><span data-stu-id="429c6-274">Second, **Measure count** currently returns only the top 100 distinct results.</span></span> <span data-ttu-id="429c6-275">This limit does not apply to the other statistical functions.</span><span class="sxs-lookup"><span data-stu-id="429c6-275">This limit does not apply to the other statistical functions.</span></span> <span data-ttu-id="429c6-276">So, you'll usually need to use a more precise filter first to search for specific items before you apply measure count().</span><span class="sxs-lookup"><span data-stu-id="429c6-276">So, you'll usually need to use a more precise filter first to search for specific items before you apply measure count().</span></span>

## <a name="use-the-max-and-min-functions-with-the-measure-command"></a><span data-ttu-id="429c6-277">Use the max and min functions with the measure command</span><span class="sxs-lookup"><span data-stu-id="429c6-277">Use the max and min functions with the measure command</span></span>
<span data-ttu-id="429c6-278">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span><span class="sxs-lookup"><span data-stu-id="429c6-278">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="429c6-279">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span><span class="sxs-lookup"><span data-stu-id="429c6-279">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="429c6-280">If you query for security events, they have a **Level** property that can vary.</span><span class="sxs-lookup"><span data-stu-id="429c6-280">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="429c6-281">For example:</span><span class="sxs-lookup"><span data-stu-id="429c6-281">For example:</span></span>

```
Type=SecurityEvent
```

![search measure count start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="429c6-283">If you want to view the highest value for all of the security events given a common Computer, the group by field, you can use</span><span class="sxs-lookup"><span data-stu-id="429c6-283">If you want to view the highest value for all of the security events given a common Computer, the group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![search measure max computer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="429c6-285">It will display that for the computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span><span class="sxs-lookup"><span data-stu-id="429c6-285">It will display that for the computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![search measure max time generated computer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="429c6-287">This function works well with numbers, but it also works with DateTime fields.</span><span class="sxs-lookup"><span data-stu-id="429c6-287">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="429c6-288">It is useful to check for the last or most recent time stamp for any piece of data indexed for each computer.</span><span class="sxs-lookup"><span data-stu-id="429c6-288">It is useful to check for the last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="429c6-289">For example: When was the most recent security event reported for each machine?</span><span class="sxs-lookup"><span data-stu-id="429c6-289">For example: When was the most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-the-avg-function-with-the-measure-command"></a><span data-ttu-id="429c6-290">Use the avg function with the measure command</span><span class="sxs-lookup"><span data-stu-id="429c6-290">Use the avg function with the measure command</span></span>
<span data-ttu-id="429c6-291">The Avg() statistical function used with measure allows you to calculate the average value for some field, and group results by the same or other field.</span><span class="sxs-lookup"><span data-stu-id="429c6-291">The Avg() statistical function used with measure allows you to calculate the average value for some field, and group results by the same or other field.</span></span> <span data-ttu-id="429c6-292">This is useful in a variety of cases, such as performance data.</span><span class="sxs-lookup"><span data-stu-id="429c6-292">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="429c6-293">We'll start with performance data.</span><span class="sxs-lookup"><span data-stu-id="429c6-293">We'll start with performance data.</span></span> <span data-ttu-id="429c6-294">Note that OMS currently collects performance counters for both Windows and Linux machines.</span><span class="sxs-lookup"><span data-stu-id="429c6-294">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="429c6-295">To search for *all* performance data, the most basic query is:</span><span class="sxs-lookup"><span data-stu-id="429c6-295">To search for *all* performance data, the most basic query is:</span></span>

```
Type=Perf
```

![search avg start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="429c6-297">The first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows the actual records behind the charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for the performance counters.</span><span class="sxs-lookup"><span data-stu-id="429c6-297">The first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows the actual records behind the charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for the performance counters.</span></span>

<span data-ttu-id="429c6-298">In the image above, there are two sets of fields marked that indicate the following:</span><span class="sxs-lookup"><span data-stu-id="429c6-298">In the image above, there are two sets of fields marked that indicate the following:</span></span>

* <span data-ttu-id="429c6-299">The first set identifies Windows Performance Counter Name, Object Name, and Instance Name in the query filter.</span><span class="sxs-lookup"><span data-stu-id="429c6-299">The first set identifies Windows Performance Counter Name, Object Name, and Instance Name in the query filter.</span></span> <span data-ttu-id="429c6-300">These are the fields you probably will most commonly use as facets/filters</span><span class="sxs-lookup"><span data-stu-id="429c6-300">These are the fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="429c6-301">**CounterValue** is the actual value of the counter.</span><span class="sxs-lookup"><span data-stu-id="429c6-301">**CounterValue** is the actual value of the counter.</span></span> <span data-ttu-id="429c6-302">In this example, the value is *75*.</span><span class="sxs-lookup"><span data-stu-id="429c6-302">In this example, the value is *75*.</span></span>
* <span data-ttu-id="429c6-303">**TimeGenerated** is 12:51, in 24-hour time format.</span><span class="sxs-lookup"><span data-stu-id="429c6-303">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="429c6-304">Here's a view of the metrics in a graph.</span><span class="sxs-lookup"><span data-stu-id="429c6-304">Here's a view of the metrics in a graph.</span></span>

![search avg start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="429c6-306">After reading about the Perf record shape, and having read about other search techniques, you can use measure Avg() to aggregate this type of numerical data.</span><span class="sxs-lookup"><span data-stu-id="429c6-306">After reading about the Perf record shape, and having read about other search techniques, you can use measure Avg() to aggregate this type of numerical data.</span></span>

<span data-ttu-id="429c6-307">Here's a simple example:</span><span class="sxs-lookup"><span data-stu-id="429c6-307">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![search avg samplevalue](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="429c6-309">In this example, you select the CPU Total Time performance counter and average by Computer.</span><span class="sxs-lookup"><span data-stu-id="429c6-309">In this example, you select the CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="429c6-310">If you want to narrow down your results to only the last 6 hours, you can either use the time filter control or specify in your query as follows:</span><span class="sxs-lookup"><span data-stu-id="429c6-310">If you want to narrow down your results to only the last 6 hours, you can either use the time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="to-search-using-the-avg-function-with-the-measure-command"></a><span data-ttu-id="429c6-311">To search using the avg function with the measure command</span><span class="sxs-lookup"><span data-stu-id="429c6-311">To search using the avg function with the measure command</span></span>
* <span data-ttu-id="429c6-312">In the Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="429c6-312">In the Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="429c6-313">You can aggregate and correlate data *across* computers.</span><span class="sxs-lookup"><span data-stu-id="429c6-313">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="429c6-314">For example, imagine that you have a set of hosts in some sort of farm where each node is equal to any other one and they just do all the same type of work and load should be roughly balanced.</span><span class="sxs-lookup"><span data-stu-id="429c6-314">For example, imagine that you have a set of hosts in some sort of farm where each node is equal to any other one and they just do all the same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="429c6-315">You could get their counters all in one go with the following query and get averages for the entire farm.</span><span class="sxs-lookup"><span data-stu-id="429c6-315">You could get their counters all in one go with the following query and get averages for the entire farm.</span></span> <span data-ttu-id="429c6-316">You can start by choosing the computers with the following example:</span><span class="sxs-lookup"><span data-stu-id="429c6-316">You can start by choosing the computers with the following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="429c6-317">Now that you have the computers, you also only want to select two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span><span class="sxs-lookup"><span data-stu-id="429c6-317">Now that you have the computers, you also only want to select two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="429c6-318">So, that part of the query becomes:</span><span class="sxs-lookup"><span data-stu-id="429c6-318">So, that part of the query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="429c6-319">Now you can add computers and counters with the following example:</span><span class="sxs-lookup"><span data-stu-id="429c6-319">Now you can add computers and counters with the following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="429c6-320">Because you have a very specific selection, the **measure Avg()** command can return the average not by computer, but across the farm, simply by grouping by CounterName.</span><span class="sxs-lookup"><span data-stu-id="429c6-320">Because you have a very specific selection, the **measure Avg()** command can return the average not by computer, but across the farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="429c6-321">For example:</span><span class="sxs-lookup"><span data-stu-id="429c6-321">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="429c6-322">This gives you a useful compact view of a couple of your environment's KPIs.</span><span class="sxs-lookup"><span data-stu-id="429c6-322">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![search avg grouping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="429c6-324">You can easily use the search query in a dashboard.</span><span class="sxs-lookup"><span data-stu-id="429c6-324">You can easily use the search query in a dashboard.</span></span> <span data-ttu-id="429c6-325">For example, you could save the search query and create a dashboard from it named *Web Farm KPIs*.</span><span class="sxs-lookup"><span data-stu-id="429c6-325">For example, you could save the search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="429c6-326">To learn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="429c6-326">To learn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![search avg dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-the-sum-function-with-the-measure-command"></a><span data-ttu-id="429c6-328">Use the sum function with the measure command</span><span class="sxs-lookup"><span data-stu-id="429c6-328">Use the sum function with the measure command</span></span>
<span data-ttu-id="429c6-329">The sum function is similar to other functions of the measure command.</span><span class="sxs-lookup"><span data-stu-id="429c6-329">The sum function is similar to other functions of the measure command.</span></span> <span data-ttu-id="429c6-330">You can see an example about how to use the sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="429c6-330">You can see an example about how to use the sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="429c6-331">You can use Max() and Min() with numbers, date times and text strings.</span><span class="sxs-lookup"><span data-stu-id="429c6-331">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="429c6-332">With text strings, they are sorted alphabetically and you get first and last.</span><span class="sxs-lookup"><span data-stu-id="429c6-332">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="429c6-333">However, you cannot use Sum() with anything other than numerical fields.</span><span class="sxs-lookup"><span data-stu-id="429c6-333">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="429c6-334">This also applies to Avg().</span><span class="sxs-lookup"><span data-stu-id="429c6-334">This also applies to Avg().</span></span>

### <a name="use-the-percentile-function-with-the-measure-command"></a><span data-ttu-id="429c6-335">Use the percentile function with the measure command</span><span class="sxs-lookup"><span data-stu-id="429c6-335">Use the percentile function with the measure command</span></span>
<span data-ttu-id="429c6-336">The percentile function is similar to Avg() and Sum() in that you can only use it for numerical fields.</span><span class="sxs-lookup"><span data-stu-id="429c6-336">The percentile function is similar to Avg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="429c6-337">You can use any percentile between 1 to 99 on a numeric field.</span><span class="sxs-lookup"><span data-stu-id="429c6-337">You can use any percentile between 1 to 99 on a numeric field.</span></span> <span data-ttu-id="429c6-338">You can also use both **percentile** and **pct** commands.</span><span class="sxs-lookup"><span data-stu-id="429c6-338">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="429c6-339">Here are few examples:</span><span class="sxs-lookup"><span data-stu-id="429c6-339">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-the-where-command"></a><span data-ttu-id="429c6-340">Use the where command</span><span class="sxs-lookup"><span data-stu-id="429c6-340">Use the where command</span></span>
<span data-ttu-id="429c6-341">The where command works like a filter, but it can be applied in the pipeline to further filter aggregated results that have been produced by a Measure command – as opposed to raw results that are filtered at the beginning of a query.</span><span class="sxs-lookup"><span data-stu-id="429c6-341">The where command works like a filter, but it can be applied in the pipeline to further filter aggregated results that have been produced by a Measure command – as opposed to raw results that are filtered at the beginning of a query.</span></span>

<span data-ttu-id="429c6-342">For example:</span><span class="sxs-lookup"><span data-stu-id="429c6-342">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="429c6-343">You can add another pipe "|" character and the Where command to only get computers whose average CPU is above 80%, with the following example:</span><span class="sxs-lookup"><span data-stu-id="429c6-343">You can add another pipe "|" character and the Where command to only get computers whose average CPU is above 80%, with the following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="429c6-344">If you're familiar with Microsoft System Center - Operations Manager, you can think of the where command in management pack terms.</span><span class="sxs-lookup"><span data-stu-id="429c6-344">If you're familiar with Microsoft System Center - Operations Manager, you can think of the where command in management pack terms.</span></span> <span data-ttu-id="429c6-345">If the example were a rule, the first part of the query would be the data source and the where command would be the condition detection.</span><span class="sxs-lookup"><span data-stu-id="429c6-345">If the example were a rule, the first part of the query would be the data source and the where command would be the condition detection.</span></span>

<span data-ttu-id="429c6-346">You can use the query as a tile in **My Dashboard**, as a monitor of sorts, to see when computer CPUs are over-utilized.</span><span class="sxs-lookup"><span data-stu-id="429c6-346">You can use the query as a tile in **My Dashboard**, as a monitor of sorts, to see when computer CPUs are over-utilized.</span></span> <span data-ttu-id="429c6-347">To learn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="429c6-347">To learn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="429c6-348">You can also create and use dashboards using the mobile app.</span><span class="sxs-lookup"><span data-stu-id="429c6-348">You can also create and use dashboards using the mobile app.</span></span> <span data-ttu-id="429c6-349">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="429c6-349">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="429c6-350">In the bottom two tiles of the following image, you can see the monitor displayed a list and as a number.</span><span class="sxs-lookup"><span data-stu-id="429c6-350">In the bottom two tiles of the following image, you can see the monitor displayed a list and as a number.</span></span> <span data-ttu-id="429c6-351">Essentially, you always want the number to be zero and the list to be empty.</span><span class="sxs-lookup"><span data-stu-id="429c6-351">Essentially, you always want the number to be zero and the list to be empty.</span></span> <span data-ttu-id="429c6-352">Otherwise, it indicates an alert condition.</span><span class="sxs-lookup"><span data-stu-id="429c6-352">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="429c6-353">If needed, you can use it to take a look at which machines are under pressure.</span><span class="sxs-lookup"><span data-stu-id="429c6-353">If needed, you can use it to take a look at which machines are under pressure.</span></span>

![mobile dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-the-in-operator"></a><span data-ttu-id="429c6-355">Use the in operator</span><span class="sxs-lookup"><span data-stu-id="429c6-355">Use the in operator</span></span>
<span data-ttu-id="429c6-356">The *IN* operator, along with *NOT IN* allows you to use subsearches, which are searches that include another search as an argument.</span><span class="sxs-lookup"><span data-stu-id="429c6-356">The *IN* operator, along with *NOT IN* allows you to use subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="429c6-357">They are contained in braces {} within another *primary* or *outer* search.</span><span class="sxs-lookup"><span data-stu-id="429c6-357">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="429c6-358">The result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span><span class="sxs-lookup"><span data-stu-id="429c6-358">The result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="429c6-359">You can use subsearches to match subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span><span class="sxs-lookup"><span data-stu-id="429c6-359">You can use subsearches to match subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="429c6-360">For example, if you’re interested in using one search to find all events from *computers missing security updates*, then you need to design a subsearch that first identifies that *computers missing security updates* before it finds events belonging to those hosts.</span><span class="sxs-lookup"><span data-stu-id="429c6-360">For example, if you’re interested in using one search to find all events from *computers missing security updates*, then you need to design a subsearch that first identifies that *computers missing security updates* before it finds events belonging to those hosts.</span></span>

<span data-ttu-id="429c6-361">So, you could express *computers currently missing required security updates* with the following query:</span><span class="sxs-lookup"><span data-stu-id="429c6-361">So, you could express *computers currently missing required security updates* with the following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN search example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="429c6-363">Once you have the list, you can use the search as an inner search to feed the list of computers into an outer (primary) search that will look for events for those computers.</span><span class="sxs-lookup"><span data-stu-id="429c6-363">Once you have the list, you can use the search as an inner search to feed the list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="429c6-364">You do this by enclosing the inner search in braces and feeding its results as possible values for a filter/field in the outer search using the IN operator.</span><span class="sxs-lookup"><span data-stu-id="429c6-364">You do this by enclosing the inner search in braces and feeding its results as possible values for a filter/field in the outer search using the IN operator.</span></span> <span data-ttu-id="429c6-365">The query would resemble:</span><span class="sxs-lookup"><span data-stu-id="429c6-365">The query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN search example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="429c6-367">Also notice the time filter used in the inner search because the System Update Assessment takes a snapshot of all computers every 24 hours.</span><span class="sxs-lookup"><span data-stu-id="429c6-367">Also notice the time filter used in the inner search because the System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="429c6-368">You can make the inner query more lightweight and precise by only searching for a day.</span><span class="sxs-lookup"><span data-stu-id="429c6-368">You can make the inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="429c6-369">The outer search instead uses the time selection in the user interface, retrieving events from the last 7 days.</span><span class="sxs-lookup"><span data-stu-id="429c6-369">The outer search instead uses the time selection in the user interface, retrieving events from the last 7 days.</span></span> <span data-ttu-id="429c6-370">See [Boolean operators](#boolean-operators) for more information about time operators.</span><span class="sxs-lookup"><span data-stu-id="429c6-370">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="429c6-371">Because you really only use the results of the inner search as a filter value for the outer one, you can still apply commands in the outer search.</span><span class="sxs-lookup"><span data-stu-id="429c6-371">Because you really only use the results of the inner search as a filter value for the outer one, you can still apply commands in the outer search.</span></span> <span data-ttu-id="429c6-372">For example, you can still group the above events with another measure command:</span><span class="sxs-lookup"><span data-stu-id="429c6-372">For example, you can still group the above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN search example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="429c6-374">Generally, you want your inner query to execute quickly because Log Analytics has service-side timeouts for it and also to return a small amount of results.</span><span class="sxs-lookup"><span data-stu-id="429c6-374">Generally, you want your inner query to execute quickly because Log Analytics has service-side timeouts for it and also to return a small amount of results.</span></span> <span data-ttu-id="429c6-375">If the inner query returns more results, the result list gets truncated, which could potentially cause the outer search to return incorrect results.</span><span class="sxs-lookup"><span data-stu-id="429c6-375">If the inner query returns more results, the result list gets truncated, which could potentially cause the outer search to return incorrect results.</span></span>

<span data-ttu-id="429c6-376">Another rule is that the inner search currently needs to provide *aggregated* results.</span><span class="sxs-lookup"><span data-stu-id="429c6-376">Another rule is that the inner search currently needs to provide *aggregated* results.</span></span> <span data-ttu-id="429c6-377">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span><span class="sxs-lookup"><span data-stu-id="429c6-377">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="429c6-378">Also, there can be only one IN operator and it must be the last filter in the query.</span><span class="sxs-lookup"><span data-stu-id="429c6-378">Also, there can be only one IN operator and it must be the last filter in the query.</span></span> <span data-ttu-id="429c6-379">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: the important point is that only one sub/inner search is possible for each outer search.</span><span class="sxs-lookup"><span data-stu-id="429c6-379">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: the important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="429c6-380">Even with these limits, IN enables many kinds of correlated searches, and allows you to define something similar to groups such as computers, users, or files – whatever the fields in your data contain.</span><span class="sxs-lookup"><span data-stu-id="429c6-380">Even with these limits, IN enables many kinds of correlated searches, and allows you to define something similar to groups such as computers, users, or files – whatever the fields in your data contain.</span></span> <span data-ttu-id="429c6-381">Here are more examples:</span><span class="sxs-lookup"><span data-stu-id="429c6-381">Here are more examples:</span></span>

<span data-ttu-id="429c6-382">**All updates missing from computers where Automatic Update setting is disabled**</span><span class="sxs-lookup"><span data-stu-id="429c6-382">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="429c6-383">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span><span class="sxs-lookup"><span data-stu-id="429c6-383">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="429c6-384">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span><span class="sxs-lookup"><span data-stu-id="429c6-384">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="429c6-385">**Which other accounts have logged on to the same computers where account BACONLAND\jochan has logged on?**</span><span class="sxs-lookup"><span data-stu-id="429c6-385">**Which other accounts have logged on to the same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-the-distinct-command"></a><span data-ttu-id="429c6-386">Use the distinct command</span><span class="sxs-lookup"><span data-stu-id="429c6-386">Use the distinct command</span></span>
<span data-ttu-id="429c6-387">As the name suggests, this command provides a list of distinct values for a field.</span><span class="sxs-lookup"><span data-stu-id="429c6-387">As the name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="429c6-388">It's surprisingly simple but quite useful.</span><span class="sxs-lookup"><span data-stu-id="429c6-388">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="429c6-389">The same could be achieved with measure count() command as well, as shown below.</span><span class="sxs-lookup"><span data-stu-id="429c6-389">The same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![DISTINCT search command example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="429c6-391">However, if all you're interested in is just a list of distinct values and not the count of documents that have that values, then DISTINCT can provide cleaner and easier to read output, and shorter syntax, as shown below.</span><span class="sxs-lookup"><span data-stu-id="429c6-391">However, if all you're interested in is just a list of distinct values and not the count of documents that have that values, then DISTINCT can provide cleaner and easier to read output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![DISTINCT search command example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-the-countdistinct-function-with-the-measure-command"></a><span data-ttu-id="429c6-393">Use the countdistinct function with the measure command</span><span class="sxs-lookup"><span data-stu-id="429c6-393">Use the countdistinct function with the measure command</span></span>
<span data-ttu-id="429c6-394">The countdistinct function counts the number of distinct values within each group.</span><span class="sxs-lookup"><span data-stu-id="429c6-394">The countdistinct function counts the number of distinct values within each group.</span></span> <span data-ttu-id="429c6-395">For example, it could be used to count the number of unique computers reporting for each Type:</span><span class="sxs-lookup"><span data-stu-id="429c6-395">For example, it could be used to count the number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-the-measure-interval-command"></a><span data-ttu-id="429c6-397">Use the measure interval command</span><span class="sxs-lookup"><span data-stu-id="429c6-397">Use the measure interval command</span></span>
<span data-ttu-id="429c6-398">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="429c6-398">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="429c6-399">Simply entering the query **Type:Perf** will return thousands of metric graphs based on the number of counters and servers in your Log Analytics environment.</span><span class="sxs-lookup"><span data-stu-id="429c6-399">Simply entering the query **Type:Perf** will return thousands of metric graphs based on the number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="429c6-400">With on-demand metric aggregation, you can look at the overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span><span class="sxs-lookup"><span data-stu-id="429c6-400">With on-demand metric aggregation, you can look at the overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="429c6-401">Let’s say that you want to know what is the average CPU across all your computers.</span><span class="sxs-lookup"><span data-stu-id="429c6-401">Let’s say that you want to know what is the average CPU across all your computers.</span></span> <span data-ttu-id="429c6-402">Looking at the average CPU for every computer might not be helpful because results may get smoothed out. To look into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span><span class="sxs-lookup"><span data-stu-id="429c6-402">Looking at the average CPU for every computer might not be helpful because results may get smoothed out. To look into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="429c6-403">For example, you can perform the hourly average of CPU usage across all your computers as follows:</span><span class="sxs-lookup"><span data-stu-id="429c6-403">For example, you can perform the hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![measure average interval](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="429c6-405">By default these results will be displayed in a multi-series interactive line chart.</span><span class="sxs-lookup"><span data-stu-id="429c6-405">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="429c6-406">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span><span class="sxs-lookup"><span data-stu-id="429c6-406">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="429c6-407">The table display option is still available for viewing the raw data if necessary.</span><span class="sxs-lookup"><span data-stu-id="429c6-407">The table display option is still available for viewing the raw data if necessary.</span></span>

<span data-ttu-id="429c6-408">You can also group by other fields.</span><span class="sxs-lookup"><span data-stu-id="429c6-408">You can also group by other fields.</span></span> <span data-ttu-id="429c6-409">In this example, I am looking at all the % counters for one specific computer, and I want to know what is the hourly 70 percentiles of every counter:</span><span class="sxs-lookup"><span data-stu-id="429c6-409">In this example, I am looking at all the % counters for one specific computer, and I want to know what is the hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="429c6-410">One thing to note is that these queries are not limited to performance counters.</span><span class="sxs-lookup"><span data-stu-id="429c6-410">One thing to note is that these queries are not limited to performance counters.</span></span> <span data-ttu-id="429c6-411">You can apply them to any metric.</span><span class="sxs-lookup"><span data-stu-id="429c6-411">You can apply them to any metric.</span></span> <span data-ttu-id="429c6-412">In this example, I’m looking at W3C IIS logs.</span><span class="sxs-lookup"><span data-stu-id="429c6-412">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="429c6-413">I want to know what is the maximum time it takes over a 5-minute interval for processing each request:</span><span class="sxs-lookup"><span data-stu-id="429c6-413">I want to know what is the maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="429c6-414">Use multiple aggregates in one query</span><span class="sxs-lookup"><span data-stu-id="429c6-414">Use multiple aggregates in one query</span></span>
<span data-ttu-id="429c6-415">You can specify multiple aggregate clauses in a measure command.</span><span class="sxs-lookup"><span data-stu-id="429c6-415">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="429c6-416">Each one can be aliased independently.</span><span class="sxs-lookup"><span data-stu-id="429c6-416">Each one can be aliased independently.</span></span>  <span data-ttu-id="429c6-417">If it is not given an alias the resulting field name will be the aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="429c6-417">If it is not given an alias the resulting field name will be the aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="429c6-419">Here is another example:</span><span class="sxs-lookup"><span data-stu-id="429c6-419">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="429c6-420">Next steps</span><span class="sxs-lookup"><span data-stu-id="429c6-420">Next steps</span></span>
<span data-ttu-id="429c6-421">For additional information about log searches, see:</span><span class="sxs-lookup"><span data-stu-id="429c6-421">For additional information about log searches, see:</span></span>

* <span data-ttu-id="429c6-422">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span><span class="sxs-lookup"><span data-stu-id="429c6-422">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
* <span data-ttu-id="429c6-423">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="429c6-423">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>




























