---
title: Reference for Analytics in Azure Application Insights | Microsoft Docs
description: 'Reference for statements in Analytics, the powerful search tool of Application Insights. '
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: eea324de-d5e5-4064-9933-beb3a97b350b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: awills
ms.openlocfilehash: 448ef94f7308b8178645fb87424bf2e202242f29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554355"
---
# <a name="reference-for-analytics"></a><span data-ttu-id="442a8-103">Reference for Analytics</span><span class="sxs-lookup"><span data-stu-id="442a8-103">Reference for Analytics</span></span>
<span data-ttu-id="442a8-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="442a8-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="442a8-105">These pages describe the Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="442a8-105">These pages describe the Analytics query language.</span></span>

<span data-ttu-id="442a8-106">Additional sources of information:</span><span class="sxs-lookup"><span data-stu-id="442a8-106">Additional sources of information:</span></span>

* <span data-ttu-id="442a8-107">Much reference material is available in Analytics as you type.</span><span class="sxs-lookup"><span data-stu-id="442a8-107">Much reference material is available in Analytics as you type.</span></span> <span data-ttu-id="442a8-108">Just start typing a query and you're prompted with possible completions.</span><span class="sxs-lookup"><span data-stu-id="442a8-108">Just start typing a query and you're prompted with possible completions.</span></span>
* <span data-ttu-id="442a8-109">[The tutorial page](app-insights-analytics-tour.md) gives a step-by-step introduction to the language features.</span><span class="sxs-lookup"><span data-stu-id="442a8-109">[The tutorial page](app-insights-analytics-tour.md) gives a step-by-step introduction to the language features.</span></span>
* <span data-ttu-id="442a8-110">[SQL users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span><span class="sxs-lookup"><span data-stu-id="442a8-110">[SQL users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>
* <span data-ttu-id="442a8-111">[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo) if your own app isn't yet sending data to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="442a8-111">[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo) if your own app isn't yet sending data to Application Insights.</span></span>
 

## <a name="index"></a><span data-ttu-id="442a8-112">Index</span><span class="sxs-lookup"><span data-stu-id="442a8-112">Index</span></span>
<span data-ttu-id="442a8-113">**Let** [let](#let-clause) | [materialize](#materialize)</span><span class="sxs-lookup"><span data-stu-id="442a8-113">**Let** [let](#let-clause) | [materialize](#materialize)</span></span> 

<span data-ttu-id="442a8-114">**Queries and operators** [as](#as-operator) | [count](#count-operator) | [datatable](#datatable-operator) | [distinct](#distinct-operator) | [evaluate](#evaluate-operator) | [extend](#extend-operator) | [find](#find-operator) | [getschema](#getschema-operator) | [join](#join-operator) | [limit](#limit-operator) | [make-series](#make-series-operator) | [mvexpand](#mvexpand-operator) | [parse](#parse-operator) | [project](#project-operator) | [project-away](#project-away-operator) | [range](#range-operator) | [reduce](#reduce-operator) | [render directive](#render-directive) | [restrict clause](#restrict-clause) | [sample](#sample-operator) | [sample-distinct](#sample-distinct-operator) | [sort](#sort-operator) | [summarize](#summarize-operator) | [table](#table-operator) | [take](#take-operator) | [top](#top-operator) | [top-nested](#top-nested-operator) | [union](#union-operator) | [where](#where-operator)</span><span class="sxs-lookup"><span data-stu-id="442a8-114">**Queries and operators** [as](#as-operator) | [count](#count-operator) | [datatable](#datatable-operator) | [distinct](#distinct-operator) | [evaluate](#evaluate-operator) | [extend](#extend-operator) | [find](#find-operator) | [getschema](#getschema-operator) | [join](#join-operator) | [limit](#limit-operator) | [make-series](#make-series-operator) | [mvexpand](#mvexpand-operator) | [parse](#parse-operator) | [project](#project-operator) | [project-away](#project-away-operator) | [range](#range-operator) | [reduce](#reduce-operator) | [render directive](#render-directive) | [restrict clause](#restrict-clause) | [sample](#sample-operator) | [sample-distinct](#sample-distinct-operator) | [sort](#sort-operator) | [summarize](#summarize-operator) | [table](#table-operator) | [take](#take-operator) | [top](#top-operator) | [top-nested](#top-nested-operator) | [union](#union-operator) | [where](#where-operator)</span></span> 

<span data-ttu-id="442a8-115">**Aggregations** [any](#any) | [argmax](#argmax) | [argmin](#argmin) | [avg](#avg) | [buildschema](#buildschema) | [count](#count) | [countif](#countif) | [dcount](#dcount) | [dcountif](#dcountif) | [makelist](#makelist) | [makeset](#makeset) | [max](#max) | [min](#min) | [percentile](#percentile) | [percentiles](#percentiles) | [percentilesw](#percentilesw) | [percentilew](#percentilew) | [stdev](#stdev) | [sum](#sum) | [variance](#variance)</span><span class="sxs-lookup"><span data-stu-id="442a8-115">**Aggregations** [any](#any) | [argmax](#argmax) | [argmin](#argmin) | [avg](#avg) | [buildschema](#buildschema) | [count](#count) | [countif](#countif) | [dcount](#dcount) | [dcountif](#dcountif) | [makelist](#makelist) | [makeset](#makeset) | [max](#max) | [min](#min) | [percentile](#percentile) | [percentiles](#percentiles) | [percentilesw](#percentilesw) | [percentilew](#percentilew) | [stdev](#stdev) | [sum](#sum) | [variance](#variance)</span></span>

<span data-ttu-id="442a8-116">**Scalars** [Boolean Literals](#boolean-literals) | [Boolean operators](#boolean-operators) | [Casts](#casts) | [Scalar comparisons](#scalar-comparisons) | [gettype](#gettype) | [hash](#hash) | [iff](#iff) | [isnotnull](#isnotnull) | [isnull](#isnull) | [notnull](#notnull) | [toscalar](#toscalar)</span><span class="sxs-lookup"><span data-stu-id="442a8-116">**Scalars** [Boolean Literals](#boolean-literals) | [Boolean operators](#boolean-operators) | [Casts](#casts) | [Scalar comparisons](#scalar-comparisons) | [gettype](#gettype) | [hash](#hash) | [iff](#iff) | [isnotnull](#isnotnull) | [isnull](#isnull) | [notnull](#notnull) | [toscalar](#toscalar)</span></span>

<span data-ttu-id="442a8-117">**Numbers** [Arithmetic operators](#arithmetic-operators) | [Numeric literals](#numeric-literals) | [abs](#abs) | [bin](#bin) | [exp](#exp) | [floor](#floor) | [gamma](#gamma) | [log](#log) | [rand](#rand) | [sqrt](#sqrt) | [todouble](#todouble) | [toint](#toint) | [tolong](#tolong)</span><span class="sxs-lookup"><span data-stu-id="442a8-117">**Numbers** [Arithmetic operators](#arithmetic-operators) | [Numeric literals](#numeric-literals) | [abs](#abs) | [bin](#bin) | [exp](#exp) | [floor](#floor) | [gamma](#gamma) | [log](#log) | [rand](#rand) | [sqrt](#sqrt) | [todouble](#todouble) | [toint](#toint) | [tolong](#tolong)</span></span>

<span data-ttu-id="442a8-118">**Date and time** [Date and time expressions](#date-and-time-expressions) | [Date and time literals](#date-and-time-literals) | [ago](#ago) | [datepart](#datepart) | [dayofmonth](#dayofmonth) | [dayofweek](#dayofweek) | [dayofyear](#dayofyear) | [endofday](#endofday) | [endofmonth](#endofmonth) | [endofweek](#endofweek) | [endofyear](#endofyear) | [getmonth](#getmonth) | [getyear](#getyear) | [now](#now) | [startofday](#startofday) | [startofmonth](#startofmonth) | [startofweek](#startofweek) | [startofyear](#startofyear) | [todatetime](#todatetime) | [totimespan](#totimespan) | [weekofyear](#weekofyear)</span><span class="sxs-lookup"><span data-stu-id="442a8-118">**Date and time** [Date and time expressions](#date-and-time-expressions) | [Date and time literals](#date-and-time-literals) | [ago](#ago) | [datepart](#datepart) | [dayofmonth](#dayofmonth) | [dayofweek](#dayofweek) | [dayofyear](#dayofyear) | [endofday](#endofday) | [endofmonth](#endofmonth) | [endofweek](#endofweek) | [endofyear](#endofyear) | [getmonth](#getmonth) | [getyear](#getyear) | [now](#now) | [startofday](#startofday) | [startofmonth](#startofmonth) | [startofweek](#startofweek) | [startofyear](#startofyear) | [todatetime](#todatetime) | [totimespan](#totimespan) | [weekofyear](#weekofyear)</span></span>

<span data-ttu-id="442a8-119">**String** [GUIDs](#guids) | [Obfuscated String Literals](#obfuscated-string-literals) | [String Literals](#string-literals) | [String comparisons](#string-comparisons) | [countof](#countof) | [extract](#extract) | [in, !in](#in) | [isempty](#isempty) | [isnotempty](#isnotempty) | [notempty](#notempty)| [parseurl](#parseurl) | [replace](#replace) | [split](#split) | [strcat](#strcat) | [strlen](#strlen) | [substring](#substring) | [tolower](#tolower) | [toupper](#toupper)</span><span class="sxs-lookup"><span data-stu-id="442a8-119">**String** [GUIDs](#guids) | [Obfuscated String Literals](#obfuscated-string-literals) | [String Literals](#string-literals) | [String comparisons](#string-comparisons) | [countof](#countof) | [extract](#extract) | [in, !in](#in) | [isempty](#isempty) | [isnotempty](#isnotempty) | [notempty](#notempty)| [parseurl](#parseurl) | [replace](#replace) | [split](#split) | [strcat](#strcat) | [strlen](#strlen) | [substring](#substring) | [tolower](#tolower) | [toupper](#toupper)</span></span>

<span data-ttu-id="442a8-120">**Arrays, objects and dynamic** [Array and object literals](#array-and-object-literals) | [Dynamic object functions](#dynamic-object-functions) | [Dynamic objects in let clauses](#dynamic-objects-in-let-clauses) | [JSON Path expressions](#json-path-expressions) | [Names](#names) | [arraylength](#arraylength) | [extractjson](#extractjson) | [in, !in](#in) | [parsejson](#parsejson) | [range](#range) | [todynamic](#todynamic) | [treepath](#treepath)</span><span class="sxs-lookup"><span data-stu-id="442a8-120">**Arrays, objects and dynamic** [Array and object literals](#array-and-object-literals) | [Dynamic object functions](#dynamic-object-functions) | [Dynamic objects in let clauses](#dynamic-objects-in-let-clauses) | [JSON Path expressions](#json-path-expressions) | [Names](#names) | [arraylength](#arraylength) | [extractjson](#extractjson) | [in, !in](#in) | [parsejson](#parsejson) | [range](#range) | [todynamic](#todynamic) | [treepath](#treepath)</span></span>

## <a name="let"></a><span data-ttu-id="442a8-121">Let</span><span class="sxs-lookup"><span data-stu-id="442a8-121">Let</span></span>
### <a name="let-clause"></a><span data-ttu-id="442a8-122">let clause</span><span class="sxs-lookup"><span data-stu-id="442a8-122">let clause</span></span>
<span data-ttu-id="442a8-123">**Tabular let - naming a table**</span><span class="sxs-lookup"><span data-stu-id="442a8-123">**Tabular let - naming a table**</span></span>

    let recentReqs = requests | where timestamp > ago(3d); 
    recentReqs | count

<span data-ttu-id="442a8-124">**Scalar let - naming a value**</span><span class="sxs-lookup"><span data-stu-id="442a8-124">**Scalar let - naming a value**</span></span>

    let interval = 3d; 
    requests | where timestamp > ago(interval)

<span data-ttu-id="442a8-125">**Lambda let - naming a function**</span><span class="sxs-lookup"><span data-stu-id="442a8-125">**Lambda let - naming a function**</span></span>

    let Recent = 
       (interval:timespan) { requests | where timestamp > ago(interval) };
    Recent(3h) | count

    let us_date = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ", 
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests 
    | summarize count() by bin(timestamp, 1h) 
    | project count_, pacificTime=us_date(timestamp-8h)

<span data-ttu-id="442a8-126">A let clause binds a [name](#names) to a tabular result, scalar value or function.</span><span class="sxs-lookup"><span data-stu-id="442a8-126">A let clause binds a [name](#names) to a tabular result, scalar value or function.</span></span> <span data-ttu-id="442a8-127">The clause is a prefix to a query, and the scope of the binding is that query.</span><span class="sxs-lookup"><span data-stu-id="442a8-127">The clause is a prefix to a query, and the scope of the binding is that query.</span></span> <span data-ttu-id="442a8-128">(Let doesn't provide a way to name things that you use later in your session.)</span><span class="sxs-lookup"><span data-stu-id="442a8-128">(Let doesn't provide a way to name things that you use later in your session.)</span></span>

<span data-ttu-id="442a8-129">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-129">**Syntax**</span></span>

    let name = scalar_constant_expression ; query

    let name = query ; query

    let name = (parameterName : type [, ...]) { plain_query }; query

    let name = (parameterName : type [, ...]) { scalar_expression }; query

* <span data-ttu-id="442a8-130">*type:* `bool`, `int`, `long`, `double`, `string`, `timespan`, `datetime`, `guid`, [`dynamic`](#dynamic-type)</span><span class="sxs-lookup"><span data-stu-id="442a8-130">*type:* `bool`, `int`, `long`, `double`, `string`, `timespan`, `datetime`, `guid`, [`dynamic`](#dynamic-type)</span></span>
* <span data-ttu-id="442a8-131">*plain_query:* A query not prefixed by a let-clause.</span><span class="sxs-lookup"><span data-stu-id="442a8-131">*plain_query:* A query not prefixed by a let-clause.</span></span>

<span data-ttu-id="442a8-132">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-132">**Examples**</span></span>

    let rows = (n:long) { range steps from 1 to n step 1 };
    rows(10) | ...

<span data-ttu-id="442a8-133">Convert a table result to a scalar and use in a query:</span><span class="sxs-lookup"><span data-stu-id="442a8-133">Convert a table result to a scalar and use in a query:</span></span>

```
let topCities =  toscalar ( // convert single column to value
   requests
   | summarize count() by client_City 
   | top 4 by count_ 
   | summarize makeset(client_City)) ;
requests
| where client_City in (topCities) 
| summarize count() by client_City;
```

### <a name="materialize"></a><span data-ttu-id="442a8-134">materialize</span><span class="sxs-lookup"><span data-stu-id="442a8-134">materialize</span></span>

<span data-ttu-id="442a8-135">Use materialize() to improve the performance where the result of a let clause is used more than once downstream.</span><span class="sxs-lookup"><span data-stu-id="442a8-135">Use materialize() to improve the performance where the result of a let clause is used more than once downstream.</span></span> <span data-ttu-id="442a8-136">Materialize() evaluates and caches the result of a tabular let clause at the time of query execution, ensuring that the query isn't executed more than once.</span><span class="sxs-lookup"><span data-stu-id="442a8-136">Materialize() evaluates and caches the result of a tabular let clause at the time of query execution, ensuring that the query isn't executed more than once.</span></span>

<span data-ttu-id="442a8-137">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-137">**Syntax**</span></span>

    materialize(expression)

<span data-ttu-id="442a8-138">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-138">**Arguments**</span></span>

* <span data-ttu-id="442a8-139">`expresion`: Tabular expression to be evaluated and cached during query execution.</span><span class="sxs-lookup"><span data-stu-id="442a8-139">`expresion`: Tabular expression to be evaluated and cached during query execution.</span></span>

<span data-ttu-id="442a8-140">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-140">**Tips**</span></span>

* <span data-ttu-id="442a8-141">Use materialize when you have join/union where their operands has mutual sub-queries that can be executed once (see the examples below).</span><span class="sxs-lookup"><span data-stu-id="442a8-141">Use materialize when you have join/union where their operands has mutual sub-queries that can be executed once (see the examples below).</span></span>
* <span data-ttu-id="442a8-142">Useful also in scenarios when we need to join/union fork legs.</span><span class="sxs-lookup"><span data-stu-id="442a8-142">Useful also in scenarios when we need to join/union fork legs.</span></span>
* <span data-ttu-id="442a8-143">Materialize is allowed to be used only in let statements by giving the cached result a name.</span><span class="sxs-lookup"><span data-stu-id="442a8-143">Materialize is allowed to be used only in let statements by giving the cached result a name.</span></span>
* <span data-ttu-id="442a8-144">Materialze has a cache size limit which is 5 GB.</span><span class="sxs-lookup"><span data-stu-id="442a8-144">Materialze has a cache size limit which is 5 GB.</span></span> <span data-ttu-id="442a8-145">This limit is per cluster node and is mutual for all the queries.</span><span class="sxs-lookup"><span data-stu-id="442a8-145">This limit is per cluster node and is mutual for all the queries.</span></span>

<span data-ttu-id="442a8-146">**Example: self-join**</span><span class="sxs-lookup"><span data-stu-id="442a8-146">**Example: self-join**</span></span>


```AIQL
let totalPagesPerDay = pageViews
| summarize by name, Day = startofday(timestamp)
| summarize count() by Day;
let materializedScope = pageViews
| summarize by name, Day = startofday(timestamp);
let cachedResult = materialize(materializedScope);
cachedResult
| project name, Day1 = Day
| join kind = inner
(
    cachedResult
    | project name, Day2 = Day
)
on name
| where Day2 > Day1
| summarize count() by Day1, Day2
| join kind = inner
    totalPagesPerDay
on $left.Day1 == $right.Day
| project Day1, Day2, Percentage = count_*100.0/count_1
```

<span data-ttu-id="442a8-147">The uncached version uses the result `scope` twice:</span><span class="sxs-lookup"><span data-stu-id="442a8-147">The uncached version uses the result `scope` twice:</span></span>

```AIQL
let totalPagesPerDay = pageViews
| summarize by name, Day = startofday(timestamp)
| summarize count() by Day;
let scope = pageViews
| summarize by name, Day = startofday(timestamp);
scope      // First use of this table.
| project name, Day1 = Day
| join kind = inner
(
    scope  // Second use can cause evaluation twice.
    | project name, Day2 = Day
)
on name
| where Day2 > Day1
| summarize count() by Day1, Day2
| join kind = inner
    totalPagesPerDay
on $left.Day1 == $right.Day
| project Day1, Day2, Percentage = count_*100.0/count_1
```

## <a name="queries-and-operators"></a><span data-ttu-id="442a8-148">Queries and operators</span><span class="sxs-lookup"><span data-stu-id="442a8-148">Queries and operators</span></span>
<span data-ttu-id="442a8-149">A query over your telemetry is made up of a reference to a source stream, followed by a pipeline of filters.</span><span class="sxs-lookup"><span data-stu-id="442a8-149">A query over your telemetry is made up of a reference to a source stream, followed by a pipeline of filters.</span></span> <span data-ttu-id="442a8-150">For example:</span><span class="sxs-lookup"><span data-stu-id="442a8-150">For example:</span></span>

```AIQL
requests // The request table starts this pipeline.
| where client_City == "London" // filter the records
   and timestamp > ago(3d)
| count 
```

<span data-ttu-id="442a8-151">Each filter prefixed by the pipe character `|` is an instance of an *operator*, with some parameters.</span><span class="sxs-lookup"><span data-stu-id="442a8-151">Each filter prefixed by the pipe character `|` is an instance of an *operator*, with some parameters.</span></span> <span data-ttu-id="442a8-152">The input to the operator is the table that is the result of the preceding pipeline.</span><span class="sxs-lookup"><span data-stu-id="442a8-152">The input to the operator is the table that is the result of the preceding pipeline.</span></span> <span data-ttu-id="442a8-153">In most cases, any parameters are [scalar expressions](#scalars) over the columns of the input.</span><span class="sxs-lookup"><span data-stu-id="442a8-153">In most cases, any parameters are [scalar expressions](#scalars) over the columns of the input.</span></span> <span data-ttu-id="442a8-154">In a few cases, the parameters are the names of input columns, and in a few cases, the parameter is a second table.</span><span class="sxs-lookup"><span data-stu-id="442a8-154">In a few cases, the parameters are the names of input columns, and in a few cases, the parameter is a second table.</span></span> <span data-ttu-id="442a8-155">The result of a query is always a table, even if it only has one column and one row.</span><span class="sxs-lookup"><span data-stu-id="442a8-155">The result of a query is always a table, even if it only has one column and one row.</span></span>

<span data-ttu-id="442a8-156">Queries may contain single line breaks, but are terminated by a blank line.</span><span class="sxs-lookup"><span data-stu-id="442a8-156">Queries may contain single line breaks, but are terminated by a blank line.</span></span> <span data-ttu-id="442a8-157">They may contain comments between `//` and end of line.</span><span class="sxs-lookup"><span data-stu-id="442a8-157">They may contain comments between `//` and end of line.</span></span>

<span data-ttu-id="442a8-158">A query may be prefixed by one or more [let clauses](#let-clause), which define scalars, tables, or functions that can be used within the query.</span><span class="sxs-lookup"><span data-stu-id="442a8-158">A query may be prefixed by one or more [let clauses](#let-clause), which define scalars, tables, or functions that can be used within the query.</span></span>

```AIQL

    let interval = 3d ;
    let city = "London" ;
    let req = (city:string) {
      requests
      | where client_City == city and timestamp > ago(interval) };
    req(city) | count
```

> <span data-ttu-id="442a8-159">`T` is used in query examples below to denote the preceding pipeline or source table.</span><span class="sxs-lookup"><span data-stu-id="442a8-159">`T` is used in query examples below to denote the preceding pipeline or source table.</span></span>
> 
> 

### <a name="as-operator"></a><span data-ttu-id="442a8-160">as operator</span><span class="sxs-lookup"><span data-stu-id="442a8-160">as operator</span></span>

<span data-ttu-id="442a8-161">Temporarily binds a name to the input tabular expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-161">Temporarily binds a name to the input tabular expression.</span></span>

<span data-ttu-id="442a8-162">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-162">**Syntax**</span></span>

    T | as name

<span data-ttu-id="442a8-163">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-163">**Arguments**</span></span>

* <span data-ttu-id="442a8-164">*name:* A temporary name for the table</span><span class="sxs-lookup"><span data-stu-id="442a8-164">*name:* A temporary name for the table</span></span>

<span data-ttu-id="442a8-165">**Notes**</span><span class="sxs-lookup"><span data-stu-id="442a8-165">**Notes**</span></span>

* <span data-ttu-id="442a8-166">Use [let](#let-clause) instead of *as* if you want to use the name in a later subexpression.</span><span class="sxs-lookup"><span data-stu-id="442a8-166">Use [let](#let-clause) instead of *as* if you want to use the name in a later subexpression.</span></span>
* <span data-ttu-id="442a8-167">Use *as* to specify the name of the table as it appears in the result of a [union](#union-operator), [find](#find-operator), or [search](#search-operator).</span><span class="sxs-lookup"><span data-stu-id="442a8-167">Use *as* to specify the name of the table as it appears in the result of a [union](#union-operator), [find](#find-operator), or [search](#search-operator).</span></span>

<span data-ttu-id="442a8-168">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-168">**Example**</span></span>

```AIQL
range x from 1 to 10 step 1 | as T1
| union withsource=TableName (requests | take 10 | as T2)
```

### <a name="count-operator"></a><span data-ttu-id="442a8-169">count operator</span><span class="sxs-lookup"><span data-stu-id="442a8-169">count operator</span></span>
<span data-ttu-id="442a8-170">The `count` operator returns the number of records (rows) in the input record set.</span><span class="sxs-lookup"><span data-stu-id="442a8-170">The `count` operator returns the number of records (rows) in the input record set.</span></span>

<span data-ttu-id="442a8-171">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-171">**Syntax**</span></span>

    T | count

<span data-ttu-id="442a8-172">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-172">**Arguments**</span></span>

* <span data-ttu-id="442a8-173">*T*: The tabular data whose records are to be counted.</span><span class="sxs-lookup"><span data-stu-id="442a8-173">*T*: The tabular data whose records are to be counted.</span></span>

<span data-ttu-id="442a8-174">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-174">**Returns**</span></span>

<span data-ttu-id="442a8-175">This function returns a table with a single record and column of type `long`.</span><span class="sxs-lookup"><span data-stu-id="442a8-175">This function returns a table with a single record and column of type `long`.</span></span> <span data-ttu-id="442a8-176">The value of the only cell is the number of records in *T*.</span><span class="sxs-lookup"><span data-stu-id="442a8-176">The value of the only cell is the number of records in *T*.</span></span> 

<span data-ttu-id="442a8-177">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-177">**Example**</span></span>

```AIQL
requests | count
```

### <a name="datatable-operator"></a><span data-ttu-id="442a8-178">datatable operator</span><span class="sxs-lookup"><span data-stu-id="442a8-178">datatable operator</span></span>

<span data-ttu-id="442a8-179">Specify a table inline.</span><span class="sxs-lookup"><span data-stu-id="442a8-179">Specify a table inline.</span></span> <span data-ttu-id="442a8-180">The schema and values are defined in the query itself.</span><span class="sxs-lookup"><span data-stu-id="442a8-180">The schema and values are defined in the query itself.</span></span>

<span data-ttu-id="442a8-181">Note that this operator does not have a pipeline input.</span><span class="sxs-lookup"><span data-stu-id="442a8-181">Note that this operator does not have a pipeline input.</span></span>

<span data-ttu-id="442a8-182">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-182">**Syntax**</span></span>

    datatable ( ColumnName1 : ColumnType1 , ...) [ScalarValue1, ...]

* <span data-ttu-id="442a8-183">*ColumnName* A name for a column.</span><span class="sxs-lookup"><span data-stu-id="442a8-183">*ColumnName* A name for a column.</span></span>
* <span data-ttu-id="442a8-184">*ColumnType* A [data type](#scalars).</span><span class="sxs-lookup"><span data-stu-id="442a8-184">*ColumnType* A [data type](#scalars).</span></span> 
* <span data-ttu-id="442a8-185">*ScalarValue* A value of the appropriate type.</span><span class="sxs-lookup"><span data-stu-id="442a8-185">*ScalarValue* A value of the appropriate type.</span></span> <span data-ttu-id="442a8-186">The count of values must be a multiple of the number of columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-186">The count of values must be a multiple of the number of columns.</span></span> 

<span data-ttu-id="442a8-187">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-187">**Returns**</span></span>

<span data-ttu-id="442a8-188">A table containing the specified values.</span><span class="sxs-lookup"><span data-stu-id="442a8-188">A table containing the specified values.</span></span>

<span data-ttu-id="442a8-189">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-189">**Example**</span></span>

```AIQL
datatable (Date:datetime, Event:string)
    [datetime(1910-06-11), "Born",
     datetime(1930-01-01), "Enters Ecole Navale",
     datetime(1953-01-01), "Published first book",
     datetime(1997-06-25), "Died"]
| where strlen(Event) > 4
```

### <a name="distinct-operator"></a><span data-ttu-id="442a8-190">distinct operator</span><span class="sxs-lookup"><span data-stu-id="442a8-190">distinct operator</span></span>

<span data-ttu-id="442a8-191">Returns a table containing the set of rows that have distinct combinations of values.</span><span class="sxs-lookup"><span data-stu-id="442a8-191">Returns a table containing the set of rows that have distinct combinations of values.</span></span> <span data-ttu-id="442a8-192">Optionally projects to a subset of the columns before the operation.</span><span class="sxs-lookup"><span data-stu-id="442a8-192">Optionally projects to a subset of the columns before the operation.</span></span>

<span data-ttu-id="442a8-193">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-193">**Syntax**</span></span>

    T | distinct *              // All columns
    T | distinct Column1, ...   // Columns to project

<span data-ttu-id="442a8-194">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-194">**Example**</span></span>

```AIQL
datatable (Supplier: string, Fruit: string, Price:int) 
["Contoso", "Grapes", 22,
"Fabrikam", "Apples", 14,
"Contoso", "Apples", 15,
"Fabrikam", "Grapes", 22]
| distinct Fruit, Price 
```


|<span data-ttu-id="442a8-195">Fruit</span><span class="sxs-lookup"><span data-stu-id="442a8-195">Fruit</span></span>|<span data-ttu-id="442a8-196">Price</span><span class="sxs-lookup"><span data-stu-id="442a8-196">Price</span></span>|
|---|---|
|<span data-ttu-id="442a8-197">Grapes</span><span class="sxs-lookup"><span data-stu-id="442a8-197">Grapes</span></span>|<span data-ttu-id="442a8-198">22</span><span class="sxs-lookup"><span data-stu-id="442a8-198">22</span></span>|
|<span data-ttu-id="442a8-199">Apples</span><span class="sxs-lookup"><span data-stu-id="442a8-199">Apples</span></span>|<span data-ttu-id="442a8-200">14</span><span class="sxs-lookup"><span data-stu-id="442a8-200">14</span></span>|
|<span data-ttu-id="442a8-201">Apples</span><span class="sxs-lookup"><span data-stu-id="442a8-201">Apples</span></span>|<span data-ttu-id="442a8-202">15</span><span class="sxs-lookup"><span data-stu-id="442a8-202">15</span></span>|


### <a name="evaluate-operator"></a><span data-ttu-id="442a8-203">evaluate operator</span><span class="sxs-lookup"><span data-stu-id="442a8-203">evaluate operator</span></span>
<span data-ttu-id="442a8-204">`evaluate` is an extension mechanism that allows specialized algorithms to be appended to queries.</span><span class="sxs-lookup"><span data-stu-id="442a8-204">`evaluate` is an extension mechanism that allows specialized algorithms to be appended to queries.</span></span>

<span data-ttu-id="442a8-205">`evaluate` must be the last operator in the query pipeline (except for a possible `render`).</span><span class="sxs-lookup"><span data-stu-id="442a8-205">`evaluate` must be the last operator in the query pipeline (except for a possible `render`).</span></span> <span data-ttu-id="442a8-206">It must not appear in a function body.</span><span class="sxs-lookup"><span data-stu-id="442a8-206">It must not appear in a function body.</span></span>

<span data-ttu-id="442a8-207">[evaluate autocluster](#evaluate-autocluster) | [evaluate basket](#evaluate-basket) | [evaluate diffpatterns](#evaluate-diffpatterns) | [evaluate extractcolumns](#evaluate-extractcolumns)</span><span class="sxs-lookup"><span data-stu-id="442a8-207">[evaluate autocluster](#evaluate-autocluster) | [evaluate basket](#evaluate-basket) | [evaluate diffpatterns](#evaluate-diffpatterns) | [evaluate extractcolumns](#evaluate-extractcolumns)</span></span>

#### <a name="evaluate-autocluster"></a><span data-ttu-id="442a8-208">evaluate autocluster</span><span class="sxs-lookup"><span data-stu-id="442a8-208">evaluate autocluster</span></span>
     T | evaluate autocluster()

<span data-ttu-id="442a8-209">AutoCluster finds common patterns of discrete attributes (dimensions) in the data and will reduce the results of the original query (whether it's 100 or 100k rows) to a small number of patterns.</span><span class="sxs-lookup"><span data-stu-id="442a8-209">AutoCluster finds common patterns of discrete attributes (dimensions) in the data and will reduce the results of the original query (whether it's 100 or 100k rows) to a small number of patterns.</span></span> <span data-ttu-id="442a8-210">AutoCluster was developed to help analyze failures (e.g. exceptions, crashes) but can potentially work on any filtered data set.</span><span class="sxs-lookup"><span data-stu-id="442a8-210">AutoCluster was developed to help analyze failures (e.g. exceptions, crashes) but can potentially work on any filtered data set.</span></span> 

<span data-ttu-id="442a8-211">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-211">**Syntax**</span></span>

    T | evaluate autocluster( arguments )

<span data-ttu-id="442a8-212">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-212">**Returns**</span></span>

<span data-ttu-id="442a8-213">AutoCluster returns a (usually small) set of patterns that capture portions of the data with shared common values across multiple discrete attributes.</span><span class="sxs-lookup"><span data-stu-id="442a8-213">AutoCluster returns a (usually small) set of patterns that capture portions of the data with shared common values across multiple discrete attributes.</span></span> <span data-ttu-id="442a8-214">Each pattern is represented by a row in the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-214">Each pattern is represented by a row in the results.</span></span> 

<span data-ttu-id="442a8-215">The first two columns are the count and percentage of rows out of the original query that are captured by the pattern.</span><span class="sxs-lookup"><span data-stu-id="442a8-215">The first two columns are the count and percentage of rows out of the original query that are captured by the pattern.</span></span> <span data-ttu-id="442a8-216">The remaining columns are from the original query and their value is either a specific value from the column or '\*' meaning variable values.</span><span class="sxs-lookup"><span data-stu-id="442a8-216">The remaining columns are from the original query and their value is either a specific value from the column or '\*' meaning variable values.</span></span> 

<span data-ttu-id="442a8-217">Note that the patterns are not disjoint: they may be overlapping, and usually do not cover all the original rows.</span><span class="sxs-lookup"><span data-stu-id="442a8-217">Note that the patterns are not disjoint: they may be overlapping, and usually do not cover all the original rows.</span></span> <span data-ttu-id="442a8-218">Some rows may not fall under any pattern.</span><span class="sxs-lookup"><span data-stu-id="442a8-218">Some rows may not fall under any pattern.</span></span>

<span data-ttu-id="442a8-219">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-219">**Tips**</span></span>

* <span data-ttu-id="442a8-220">Use `where` and `project` in the input pipe to reduce the data to just what you're interested in.</span><span class="sxs-lookup"><span data-stu-id="442a8-220">Use `where` and `project` in the input pipe to reduce the data to just what you're interested in.</span></span>
* <span data-ttu-id="442a8-221">When you find an interesting row, you might want to drill into it further by adding its specific values to your `where` filter.</span><span class="sxs-lookup"><span data-stu-id="442a8-221">When you find an interesting row, you might want to drill into it further by adding its specific values to your `where` filter.</span></span>

<span data-ttu-id="442a8-222">**Arguments (all optional)**</span><span class="sxs-lookup"><span data-stu-id="442a8-222">**Arguments (all optional)**</span></span>

* `output=all | values | minimal` 
  
    <span data-ttu-id="442a8-223">The format of the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-223">The format of the results.</span></span> <span data-ttu-id="442a8-224">The Count and Percent columns always appear in the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-224">The Count and Percent columns always appear in the results.</span></span> 
  
  * <span data-ttu-id="442a8-225">`all` - all the columns from the input are output</span><span class="sxs-lookup"><span data-stu-id="442a8-225">`all` - all the columns from the input are output</span></span>
  * <span data-ttu-id="442a8-226">`values` - filters out columns with only '\*' in the results</span><span class="sxs-lookup"><span data-stu-id="442a8-226">`values` - filters out columns with only '\*' in the results</span></span>
  * <span data-ttu-id="442a8-227">`minimal` - also filters out columns that are identical for all the rows in the original query.</span><span class="sxs-lookup"><span data-stu-id="442a8-227">`minimal` - also filters out columns that are identical for all the rows in the original query.</span></span> 
* <span data-ttu-id="442a8-228">`min_percent=`*double* (default: 1)</span><span class="sxs-lookup"><span data-stu-id="442a8-228">`min_percent=`*double* (default: 1)</span></span>
  
    <span data-ttu-id="442a8-229">The minimum percentage coverage of the generated rows.</span><span class="sxs-lookup"><span data-stu-id="442a8-229">The minimum percentage coverage of the generated rows.</span></span>
  
    <span data-ttu-id="442a8-230">Example: `T | evaluate autocluster("min_percent=5.5")`</span><span class="sxs-lookup"><span data-stu-id="442a8-230">Example: `T | evaluate autocluster("min_percent=5.5")`</span></span>
* <span data-ttu-id="442a8-231">`num_seeds=` *int* (default: 25)</span><span class="sxs-lookup"><span data-stu-id="442a8-231">`num_seeds=` *int* (default: 25)</span></span> 
  
    <span data-ttu-id="442a8-232">The number of seeds determines the number of initial local search points of the algorithm.</span><span class="sxs-lookup"><span data-stu-id="442a8-232">The number of seeds determines the number of initial local search points of the algorithm.</span></span> <span data-ttu-id="442a8-233">In some cases, depending on the structure of the data, increasing the number of seeds increases the number (or quality) of the results through increased search space at slower query tradeoff.</span><span class="sxs-lookup"><span data-stu-id="442a8-233">In some cases, depending on the structure of the data, increasing the number of seeds increases the number (or quality) of the results through increased search space at slower query tradeoff.</span></span> <span data-ttu-id="442a8-234">The num_seeds argument has diminishing results in both directions so decreasing it below 5 will achieve negligible performance improvements and increasing above 50 will rarely generate additional patterns.</span><span class="sxs-lookup"><span data-stu-id="442a8-234">The num_seeds argument has diminishing results in both directions so decreasing it below 5 will achieve negligible performance improvements and increasing above 50 will rarely generate additional patterns.</span></span>
  
    <span data-ttu-id="442a8-235">Example: `T | evaluate autocluster("num_seeds=50")`</span><span class="sxs-lookup"><span data-stu-id="442a8-235">Example: `T | evaluate autocluster("num_seeds=50")`</span></span>
* <span data-ttu-id="442a8-236">`size_weight=` *0<double<1*+ (default: 0.5)</span><span class="sxs-lookup"><span data-stu-id="442a8-236">`size_weight=` *0<double<1*+ (default: 0.5)</span></span>
  
    <span data-ttu-id="442a8-237">Gives you some control over the balance between generic (high coverage) and informative (many shared values).</span><span class="sxs-lookup"><span data-stu-id="442a8-237">Gives you some control over the balance between generic (high coverage) and informative (many shared values).</span></span> <span data-ttu-id="442a8-238">Increasing size_weight usually reduces the number of patterns, and each pattern tends to cover a larger percentage.</span><span class="sxs-lookup"><span data-stu-id="442a8-238">Increasing size_weight usually reduces the number of patterns, and each pattern tends to cover a larger percentage.</span></span> <span data-ttu-id="442a8-239">Decreasing size_weight usually produces more specific patterns with more shared values and smaller percentage coverage.</span><span class="sxs-lookup"><span data-stu-id="442a8-239">Decreasing size_weight usually produces more specific patterns with more shared values and smaller percentage coverage.</span></span> <span data-ttu-id="442a8-240">The under the hood formula is a weighted geometric mean between the normalized generic score and informative score with size_weight and 1-size_weight as the weights.</span><span class="sxs-lookup"><span data-stu-id="442a8-240">The under the hood formula is a weighted geometric mean between the normalized generic score and informative score with size_weight and 1-size_weight as the weights.</span></span> 
  
    <span data-ttu-id="442a8-241">Example: `T | evaluate autocluster("size_weight=0.8")`</span><span class="sxs-lookup"><span data-stu-id="442a8-241">Example: `T | evaluate autocluster("size_weight=0.8")`</span></span>
* <span data-ttu-id="442a8-242">`weight_column=` *column_name*</span><span class="sxs-lookup"><span data-stu-id="442a8-242">`weight_column=` *column_name*</span></span>
  
    <span data-ttu-id="442a8-243">Considers each row in the input according to the specified weight (by default each row has a weight of '1'), common usage of a weight column is to take into account sampling or bucketing/aggregation of the data that is already embedded into each row.</span><span class="sxs-lookup"><span data-stu-id="442a8-243">Considers each row in the input according to the specified weight (by default each row has a weight of '1'), common usage of a weight column is to take into account sampling or bucketing/aggregation of the data that is already embedded into each row.</span></span>
  
    <span data-ttu-id="442a8-244">Example: `T | evaluate autocluster("weight_column=sample_Count")`</span><span class="sxs-lookup"><span data-stu-id="442a8-244">Example: `T | evaluate autocluster("weight_column=sample_Count")`</span></span> 

#### <a name="evaluate-basket"></a><span data-ttu-id="442a8-245">evaluate basket</span><span class="sxs-lookup"><span data-stu-id="442a8-245">evaluate basket</span></span>
     T | evaluate basket()

<span data-ttu-id="442a8-246">Basket finds all frequent patterns of discrete attributes (dimensions) in the data and will return all frequent patterns that passed the frequency threshold in the original query.</span><span class="sxs-lookup"><span data-stu-id="442a8-246">Basket finds all frequent patterns of discrete attributes (dimensions) in the data and will return all frequent patterns that passed the frequency threshold in the original query.</span></span> <span data-ttu-id="442a8-247">Basket is guaranteed to find all frequent patterns in the data but is not guaranteed to have polynomial run-time.</span><span class="sxs-lookup"><span data-stu-id="442a8-247">Basket is guaranteed to find all frequent patterns in the data but is not guaranteed to have polynomial run-time.</span></span> <span data-ttu-id="442a8-248">The run-time of the query is linear in the number of rows but in some cases might be exponential in the number of columns (dimensions).</span><span class="sxs-lookup"><span data-stu-id="442a8-248">The run-time of the query is linear in the number of rows but in some cases might be exponential in the number of columns (dimensions).</span></span> <span data-ttu-id="442a8-249">Basket is based on the Apriori algorithm originally developed for basket analysis data mining.</span><span class="sxs-lookup"><span data-stu-id="442a8-249">Basket is based on the Apriori algorithm originally developed for basket analysis data mining.</span></span> 

<span data-ttu-id="442a8-250">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-250">**Returns**</span></span>

<span data-ttu-id="442a8-251">All patterns appearing in more than a specified fraction (default 0.05) of the events.</span><span class="sxs-lookup"><span data-stu-id="442a8-251">All patterns appearing in more than a specified fraction (default 0.05) of the events.</span></span>

<span data-ttu-id="442a8-252">**Arguments (all optional)**</span><span class="sxs-lookup"><span data-stu-id="442a8-252">**Arguments (all optional)**</span></span>

* <span data-ttu-id="442a8-253">`threshold=` *0.015<double<1* (default: 0.05)</span><span class="sxs-lookup"><span data-stu-id="442a8-253">`threshold=` *0.015<double<1* (default: 0.05)</span></span> 
  
    <span data-ttu-id="442a8-254">Sets the minimal ratio of the rows to be considered frequent (patterns with smaller ratio will not be returned).</span><span class="sxs-lookup"><span data-stu-id="442a8-254">Sets the minimal ratio of the rows to be considered frequent (patterns with smaller ratio will not be returned).</span></span>
  
    <span data-ttu-id="442a8-255">Example: `T | evaluate basket("threshold=0.02")`</span><span class="sxs-lookup"><span data-stu-id="442a8-255">Example: `T | evaluate basket("threshold=0.02")`</span></span>
* <span data-ttu-id="442a8-256">`weight_column=` *column_name*</span><span class="sxs-lookup"><span data-stu-id="442a8-256">`weight_column=` *column_name*</span></span>
  
    <span data-ttu-id="442a8-257">Considers each row in the input according to the specified weight (by default each row has a weight of '1'), common usage of a weight column is to take into account sampling or bucketing/aggregation of the data that is already embedded into each row.</span><span class="sxs-lookup"><span data-stu-id="442a8-257">Considers each row in the input according to the specified weight (by default each row has a weight of '1'), common usage of a weight column is to take into account sampling or bucketing/aggregation of the data that is already embedded into each row.</span></span>
  
    <span data-ttu-id="442a8-258">Example: T | evaluate basket("weight_column=sample_Count")</span><span class="sxs-lookup"><span data-stu-id="442a8-258">Example: T | evaluate basket("weight_column=sample_Count")</span></span>
* <span data-ttu-id="442a8-259">`max_dims=` *1<int* (default: 5)</span><span class="sxs-lookup"><span data-stu-id="442a8-259">`max_dims=` *1<int* (default: 5)</span></span>
  
    <span data-ttu-id="442a8-260">Sets the maximal number of uncorrelated dimensions per basket, limited by default to decrease the query runtime.</span><span class="sxs-lookup"><span data-stu-id="442a8-260">Sets the maximal number of uncorrelated dimensions per basket, limited by default to decrease the query runtime.</span></span>
* `output=minimize` | `all` 
  
    <span data-ttu-id="442a8-261">The format of the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-261">The format of the results.</span></span> <span data-ttu-id="442a8-262">The Count and Percent columns always appear in the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-262">The Count and Percent columns always appear in the results.</span></span>
  
  * <span data-ttu-id="442a8-263">`minimize` - filters out columns with only '\*' in the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-263">`minimize` - filters out columns with only '\*' in the results.</span></span>
  * <span data-ttu-id="442a8-264">`all` - all the columns from the input are output.</span><span class="sxs-lookup"><span data-stu-id="442a8-264">`all` - all the columns from the input are output.</span></span>

#### <a name="evaluate-diffpatterns"></a><span data-ttu-id="442a8-265">evaluate diffpatterns</span><span class="sxs-lookup"><span data-stu-id="442a8-265">evaluate diffpatterns</span></span>
     requests | evaluate diffpatterns("split=success")

<span data-ttu-id="442a8-266">Diffpatterns compares two data sets of the same structure and finds patterns of discrete attributes (dimensions) that characterize differences between the two data sets.</span><span class="sxs-lookup"><span data-stu-id="442a8-266">Diffpatterns compares two data sets of the same structure and finds patterns of discrete attributes (dimensions) that characterize differences between the two data sets.</span></span> <span data-ttu-id="442a8-267">Diffpatterns was developed to help analyze failures (e.g. by comparing failures to non-failures in a given time frame) but can potentially find differences between any two data sets of the same structure.</span><span class="sxs-lookup"><span data-stu-id="442a8-267">Diffpatterns was developed to help analyze failures (e.g. by comparing failures to non-failures in a given time frame) but can potentially find differences between any two data sets of the same structure.</span></span> 

<span data-ttu-id="442a8-268">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-268">**Syntax**</span></span>

<span data-ttu-id="442a8-269">`T | evaluate diffpatterns("split=` *BinaryColumn* `" [, arguments] )`</span><span class="sxs-lookup"><span data-stu-id="442a8-269">`T | evaluate diffpatterns("split=` *BinaryColumn* `" [, arguments] )`</span></span>

<span data-ttu-id="442a8-270">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-270">**Returns**</span></span>

<span data-ttu-id="442a8-271">Diffpatterns returns a (usually small) set of patterns that capture different portions of the data in the two sets (i.e. a pattern capturing a large percentage of the rows in the first data set and low percentage of the rows in the second set).</span><span class="sxs-lookup"><span data-stu-id="442a8-271">Diffpatterns returns a (usually small) set of patterns that capture different portions of the data in the two sets (i.e. a pattern capturing a large percentage of the rows in the first data set and low percentage of the rows in the second set).</span></span> <span data-ttu-id="442a8-272">Each pattern is represented by a row in the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-272">Each pattern is represented by a row in the results.</span></span>

<span data-ttu-id="442a8-273">The first four columns are the count and percentage of rows out of the original query that are captured by the pattern in each set, the fifth column is the difference (in absolute percentage points) between the two sets.</span><span class="sxs-lookup"><span data-stu-id="442a8-273">The first four columns are the count and percentage of rows out of the original query that are captured by the pattern in each set, the fifth column is the difference (in absolute percentage points) between the two sets.</span></span> <span data-ttu-id="442a8-274">The remaining columns are from the original query and their value is either a specific value from the column or \* meaning variable values.</span><span class="sxs-lookup"><span data-stu-id="442a8-274">The remaining columns are from the original query and their value is either a specific value from the column or \* meaning variable values.</span></span> 

<span data-ttu-id="442a8-275">Note that the patterns are not distinct: they may be overlapping, and usually do not cover all the original rows.</span><span class="sxs-lookup"><span data-stu-id="442a8-275">Note that the patterns are not distinct: they may be overlapping, and usually do not cover all the original rows.</span></span> <span data-ttu-id="442a8-276">Some rows may not fall under any pattern.</span><span class="sxs-lookup"><span data-stu-id="442a8-276">Some rows may not fall under any pattern.</span></span>

<span data-ttu-id="442a8-277">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-277">**Tips**</span></span>

* <span data-ttu-id="442a8-278">Use where and project in the input pipe to reduce the data to just what you're interested in.</span><span class="sxs-lookup"><span data-stu-id="442a8-278">Use where and project in the input pipe to reduce the data to just what you're interested in.</span></span>
* <span data-ttu-id="442a8-279">When you find an interesting row, you might want to drill into it further by adding its specific values to your where filter.</span><span class="sxs-lookup"><span data-stu-id="442a8-279">When you find an interesting row, you might want to drill into it further by adding its specific values to your where filter.</span></span>

<span data-ttu-id="442a8-280">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-280">**Arguments**</span></span>

* <span data-ttu-id="442a8-281">`split=` *column name* (required)</span><span class="sxs-lookup"><span data-stu-id="442a8-281">`split=` *column name* (required)</span></span>
  
    <span data-ttu-id="442a8-282">The column must have precisely two values.</span><span class="sxs-lookup"><span data-stu-id="442a8-282">The column must have precisely two values.</span></span> <span data-ttu-id="442a8-283">If necessary, create such a column:</span><span class="sxs-lookup"><span data-stu-id="442a8-283">If necessary, create such a column:</span></span>
  
    `requests | extend fault = toint(resultCode) >= 500` <br/>
    `| evaluate diffpatterns("split=fault")`
* <span data-ttu-id="442a8-284">`target=` *string*</span><span class="sxs-lookup"><span data-stu-id="442a8-284">`target=` *string*</span></span>
  
    <span data-ttu-id="442a8-285">Tells the algorithm to only look for patterns which have higher percentage in the target data set, the target must be one of the two values of the split column.</span><span class="sxs-lookup"><span data-stu-id="442a8-285">Tells the algorithm to only look for patterns which have higher percentage in the target data set, the target must be one of the two values of the split column.</span></span>
  
    `requests | evaluate diffpatterns("split=success", "target=false")`
* <span data-ttu-id="442a8-286">`threshold=` *0.015<double<1* (default: 0.05)</span><span class="sxs-lookup"><span data-stu-id="442a8-286">`threshold=` *0.015<double<1* (default: 0.05)</span></span> 
  
    <span data-ttu-id="442a8-287">Sets the minimal pattern (ratio) difference between the two sets.</span><span class="sxs-lookup"><span data-stu-id="442a8-287">Sets the minimal pattern (ratio) difference between the two sets.</span></span>
  
    `requests | evaluate diffpatterns("split=success", "threshold=0.04")`
* `output=minimize | all`
  
    <span data-ttu-id="442a8-288">The format of the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-288">The format of the results.</span></span> <span data-ttu-id="442a8-289">The Count and Percent columns always appear in the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-289">The Count and Percent columns always appear in the results.</span></span> 
  
  * <span data-ttu-id="442a8-290">`minimize` - filters out columns with only '\*' in the results</span><span class="sxs-lookup"><span data-stu-id="442a8-290">`minimize` - filters out columns with only '\*' in the results</span></span>
  * <span data-ttu-id="442a8-291">`all` - all the columns from the input are output</span><span class="sxs-lookup"><span data-stu-id="442a8-291">`all` - all the columns from the input are output</span></span>
* <span data-ttu-id="442a8-292">`weight_column=` *column_name*</span><span class="sxs-lookup"><span data-stu-id="442a8-292">`weight_column=` *column_name*</span></span>
  
    <span data-ttu-id="442a8-293">Considers each row in the input according to the specified weight (by default each row has a weight of '1').</span><span class="sxs-lookup"><span data-stu-id="442a8-293">Considers each row in the input according to the specified weight (by default each row has a weight of '1').</span></span> <span data-ttu-id="442a8-294">A common use of a weight column is to take into account sampling or bucketing/aggregation of the data that is already embedded into each row.</span><span class="sxs-lookup"><span data-stu-id="442a8-294">A common use of a weight column is to take into account sampling or bucketing/aggregation of the data that is already embedded into each row.</span></span>
  
    `requests | evaluate autocluster("weight_column=itemCount")`

#### <a name="evaluate-extractcolumns"></a><span data-ttu-id="442a8-295">evaluate extractcolumns</span><span class="sxs-lookup"><span data-stu-id="442a8-295">evaluate extractcolumns</span></span>
     exceptions | take 1000 | evaluate extractcolumns("details=json") 

<span data-ttu-id="442a8-296">Extractcolumns is used to enrich a table with multiple simple columns that are dynamically extracted out of (semi) structured column(s) based on their type.</span><span class="sxs-lookup"><span data-stu-id="442a8-296">Extractcolumns is used to enrich a table with multiple simple columns that are dynamically extracted out of (semi) structured column(s) based on their type.</span></span> <span data-ttu-id="442a8-297">Currently it supports json columns only, both dynamic and string serialization of jsons.</span><span class="sxs-lookup"><span data-stu-id="442a8-297">Currently it supports json columns only, both dynamic and string serialization of jsons.</span></span>

* <span data-ttu-id="442a8-298">`max_columns=` *int* (default: 10)</span><span class="sxs-lookup"><span data-stu-id="442a8-298">`max_columns=` *int* (default: 10)</span></span> 
  
    <span data-ttu-id="442a8-299">The number of new added columns is dynamic and it can be very big (actually it’s the number of distinct keys in all json records) so we must limit it.</span><span class="sxs-lookup"><span data-stu-id="442a8-299">The number of new added columns is dynamic and it can be very big (actually it’s the number of distinct keys in all json records) so we must limit it.</span></span> <span data-ttu-id="442a8-300">The new columns are sorted in descending order based on their frequency and up to max_columns are added to the table.</span><span class="sxs-lookup"><span data-stu-id="442a8-300">The new columns are sorted in descending order based on their frequency and up to max_columns are added to the table.</span></span>
  
    `T | evaluate extractcolumns("json_column_name=json", "max_columns=30")`
* <span data-ttu-id="442a8-301">`min_percent=` *double* (default: 10.0)</span><span class="sxs-lookup"><span data-stu-id="442a8-301">`min_percent=` *double* (default: 10.0)</span></span> 
  
    <span data-ttu-id="442a8-302">Another way to limit new columns by ignoring columns whose frequency is lower than min_percent.</span><span class="sxs-lookup"><span data-stu-id="442a8-302">Another way to limit new columns by ignoring columns whose frequency is lower than min_percent.</span></span>
  
    `T | evaluate extractcolumns("json_column_name=json", "min_percent=60")`
* <span data-ttu-id="442a8-303">`add_prefix=` *bool* (default: true)</span><span class="sxs-lookup"><span data-stu-id="442a8-303">`add_prefix=` *bool* (default: true)</span></span> 
  
    <span data-ttu-id="442a8-304">If true the name of the complex column will be added as a prefix to the extracted columns names.</span><span class="sxs-lookup"><span data-stu-id="442a8-304">If true the name of the complex column will be added as a prefix to the extracted columns names.</span></span>
* <span data-ttu-id="442a8-305">`prefix_delimiter=` *string* (default: "_")</span><span class="sxs-lookup"><span data-stu-id="442a8-305">`prefix_delimiter=` *string* (default: "_")</span></span> 
  
    <span data-ttu-id="442a8-306">If add_prefix=true this parameter defines the delimiter that will be used to concatenate the names of the new columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-306">If add_prefix=true this parameter defines the delimiter that will be used to concatenate the names of the new columns.</span></span>
  
    `T | evaluate extractcolumns("json_column_name=json",` <br/>
    `"add_prefix=true", "prefix_delimiter=@")`
* <span data-ttu-id="442a8-307">`keep_original=` *bool* (default: false)</span><span class="sxs-lookup"><span data-stu-id="442a8-307">`keep_original=` *bool* (default: false)</span></span> 
  
    <span data-ttu-id="442a8-308">If true the original (json) columns will be kept in the output table.</span><span class="sxs-lookup"><span data-stu-id="442a8-308">If true the original (json) columns will be kept in the output table.</span></span>
* `output=query | table` 
  
    <span data-ttu-id="442a8-309">The format of the results.</span><span class="sxs-lookup"><span data-stu-id="442a8-309">The format of the results.</span></span> 
  
  * <span data-ttu-id="442a8-310">`table` - The output is the same table as received minus the specified input columns plus new columns that were extracted from the input columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-310">`table` - The output is the same table as received minus the specified input columns plus new columns that were extracted from the input columns.</span></span>
  * <span data-ttu-id="442a8-311">`query` - The output is a string representing the query you would make to get the result as table.</span><span class="sxs-lookup"><span data-stu-id="442a8-311">`query` - The output is a string representing the query you would make to get the result as table.</span></span> 

### <a name="extend-operator"></a><span data-ttu-id="442a8-312">extend operator</span><span class="sxs-lookup"><span data-stu-id="442a8-312">extend operator</span></span>
     T | extend duration = stopTime - startTime

<span data-ttu-id="442a8-313">Append one or more calculated columns to a table.</span><span class="sxs-lookup"><span data-stu-id="442a8-313">Append one or more calculated columns to a table.</span></span> 

<span data-ttu-id="442a8-314">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-314">**Syntax**</span></span>

    T | extend ColumnName = Expression [, ...]

<span data-ttu-id="442a8-315">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-315">**Arguments**</span></span>

* <span data-ttu-id="442a8-316">*T:* The input table.</span><span class="sxs-lookup"><span data-stu-id="442a8-316">*T:* The input table.</span></span>
* <span data-ttu-id="442a8-317">*ColumnName:* The name of a columns to add.</span><span class="sxs-lookup"><span data-stu-id="442a8-317">*ColumnName:* The name of a columns to add.</span></span> <span data-ttu-id="442a8-318">[Names](#names) are case-sensitive and can contain alphabetic, numeric or '_' characters.</span><span class="sxs-lookup"><span data-stu-id="442a8-318">[Names](#names) are case-sensitive and can contain alphabetic, numeric or '_' characters.</span></span> <span data-ttu-id="442a8-319">Use `['...']` or `["..."]` to quote keywords or names with other characters.</span><span class="sxs-lookup"><span data-stu-id="442a8-319">Use `['...']` or `["..."]` to quote keywords or names with other characters.</span></span>
* <span data-ttu-id="442a8-320">*Expression:* A calculation over the existing columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-320">*Expression:* A calculation over the existing columns.</span></span>

<span data-ttu-id="442a8-321">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-321">**Returns**</span></span>

<span data-ttu-id="442a8-322">A copy of the input table, with the specified additional columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-322">A copy of the input table, with the specified additional columns.</span></span>

<span data-ttu-id="442a8-323">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-323">**Tips**</span></span>

* <span data-ttu-id="442a8-324">Use [`project`](#project-operator) instead, if you also want to drop or rename some columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-324">Use [`project`](#project-operator) instead, if you also want to drop or rename some columns.</span></span>
* <span data-ttu-id="442a8-325">Don't use `extend` simply to get a shorter name to use in a long expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-325">Don't use `extend` simply to get a shorter name to use in a long expression.</span></span> `...| extend x = anonymous_user_id_from_client | ... func(x) ...` 
  
    <span data-ttu-id="442a8-326">The native columns of the table have been indexed; your new name defines an additional column that isn't indexed, so the query is likely to run slower.</span><span class="sxs-lookup"><span data-stu-id="442a8-326">The native columns of the table have been indexed; your new name defines an additional column that isn't indexed, so the query is likely to run slower.</span></span>

<span data-ttu-id="442a8-327">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-327">**Example**</span></span>

```AIQL
traces
| extend
    Age = now() - timestamp
```

### <a name="find-operator"></a><span data-ttu-id="442a8-328">find operator</span><span class="sxs-lookup"><span data-stu-id="442a8-328">find operator</span></span>

    find in (Table1, Table2, Table3) where id=="a string"
    find in (Table1, Table2, Table3) where id=="a string" project column1, column2
    find in (Table1, Table2, Table3) where * has "a string"
    find in (Table1, Table2, Table3) where appName in ("string 1", "string 2", "string 3")

<span data-ttu-id="442a8-329">Find rows that match a predicate across a set of tables.</span><span class="sxs-lookup"><span data-stu-id="442a8-329">Find rows that match a predicate across a set of tables.</span></span>

<span data-ttu-id="442a8-330">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-330">**Syntax**</span></span>

    find in (Table1, ...) 
    where Predicate 
    [project Column1, ...]

<span data-ttu-id="442a8-331">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-331">**Arguments**</span></span>

* <span data-ttu-id="442a8-332">*Table1* A table name or query.</span><span class="sxs-lookup"><span data-stu-id="442a8-332">*Table1* A table name or query.</span></span> <span data-ttu-id="442a8-333">It can be a let-defined table, but not a function.</span><span class="sxs-lookup"><span data-stu-id="442a8-333">It can be a let-defined table, but not a function.</span></span> <span data-ttu-id="442a8-334">A table name performs better than a query.</span><span class="sxs-lookup"><span data-stu-id="442a8-334">A table name performs better than a query.</span></span>
* <span data-ttu-id="442a8-335">*Predicate* A boolean expression evaluated for every row in the specified tables.</span><span class="sxs-lookup"><span data-stu-id="442a8-335">*Predicate* A boolean expression evaluated for every row in the specified tables.</span></span>
 * <span data-ttu-id="442a8-336">You can use "\*" in place of a column name in string comparisons</span><span class="sxs-lookup"><span data-stu-id="442a8-336">You can use "\*" in place of a column name in string comparisons</span></span>
* <span data-ttu-id="442a8-337">*Column1* The `project` option allows you to specify which columns must always appear in the output.</span><span class="sxs-lookup"><span data-stu-id="442a8-337">*Column1* The `project` option allows you to specify which columns must always appear in the output.</span></span> 

<span data-ttu-id="442a8-338">**Result**</span><span class="sxs-lookup"><span data-stu-id="442a8-338">**Result**</span></span>

<span data-ttu-id="442a8-339">By default, the output table contains:</span><span class="sxs-lookup"><span data-stu-id="442a8-339">By default, the output table contains:</span></span>

* <span data-ttu-id="442a8-340">`source_` - An indicator of the source table for each row.</span><span class="sxs-lookup"><span data-stu-id="442a8-340">`source_` - An indicator of the source table for each row.</span></span> <span data-ttu-id="442a8-341">Use [as](#as-operator) at the end of each table expression, if you want to specify the name that appears in this column.</span><span class="sxs-lookup"><span data-stu-id="442a8-341">Use [as](#as-operator) at the end of each table expression, if you want to specify the name that appears in this column.</span></span>
* <span data-ttu-id="442a8-342">Columns explicitly mentioned in the predicate</span><span class="sxs-lookup"><span data-stu-id="442a8-342">Columns explicitly mentioned in the predicate</span></span>
* <span data-ttu-id="442a8-343">Non-empty columns common to all the input tables.</span><span class="sxs-lookup"><span data-stu-id="442a8-343">Non-empty columns common to all the input tables.</span></span>
* <span data-ttu-id="442a8-344">`pack_` - A property bag containing the data from the other columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-344">`pack_` - A property bag containing the data from the other columns.</span></span>

<span data-ttu-id="442a8-345">Notice that this format can change with changes in the input data or predicate.</span><span class="sxs-lookup"><span data-stu-id="442a8-345">Notice that this format can change with changes in the input data or predicate.</span></span> <span data-ttu-id="442a8-346">To specify a fixed set of columns, use `project`.</span><span class="sxs-lookup"><span data-stu-id="442a8-346">To specify a fixed set of columns, use `project`.</span></span>

<span data-ttu-id="442a8-347">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-347">**Example**</span></span>

<span data-ttu-id="442a8-348">Get all the requests and exceptions, excluding those from availability tests and robots:</span><span class="sxs-lookup"><span data-stu-id="442a8-348">Get all the requests and exceptions, excluding those from availability tests and robots:</span></span>

```AIQL

    find in (requests, exceptions) where isempty(operation_SyntheticSource)
```

<span data-ttu-id="442a8-349">Find all requests and exceptions from UK, excluding those from availability tests and robots:</span><span class="sxs-lookup"><span data-stu-id="442a8-349">Find all requests and exceptions from UK, excluding those from availability tests and robots:</span></span>

```AIQL

    let requk = requests
    | where client_CountryOrRegion == "United Kingdom";
    let exuk = exceptions
    | where client_CountryOrRegion == "United Kingdom";
    find in (requk, exuk) where isempty(operation_SyntheticSource)
```

<span data-ttu-id="442a8-350">Find most recent telemetry where any field contains the term 'test':</span><span class="sxs-lookup"><span data-stu-id="442a8-350">Find most recent telemetry where any field contains the term 'test':</span></span>

```AIQL

    find in (traces, requests, pageViews, dependencies, customEvents, availabilityResults, exceptions) 
    where * has 'test' 
    | top 100 by timestamp desc
```

<span data-ttu-id="442a8-351">**Performance Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-351">**Performance Tips**</span></span>

* <span data-ttu-id="442a8-352">Add time-based terms to the `where` predicate.</span><span class="sxs-lookup"><span data-stu-id="442a8-352">Add time-based terms to the `where` predicate.</span></span>
* <span data-ttu-id="442a8-353">Use `let` clauses rather than writing queries inline.</span><span class="sxs-lookup"><span data-stu-id="442a8-353">Use `let` clauses rather than writing queries inline.</span></span>

### <a name="getschema-operator"></a><span data-ttu-id="442a8-354">getschema operator</span><span class="sxs-lookup"><span data-stu-id="442a8-354">getschema operator</span></span>

   <span data-ttu-id="442a8-355">T | getschema</span><span class="sxs-lookup"><span data-stu-id="442a8-355">T | getschema</span></span>
   
<span data-ttu-id="442a8-356">Yields a table that shows the column names and types of the input table.</span><span class="sxs-lookup"><span data-stu-id="442a8-356">Yields a table that shows the column names and types of the input table.</span></span>

```AIQL
requests
| project appId, appName, customDimensions, duration, iKey, itemCount, success, timestamp 
| getschema 
```

![Results of getschema](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/getschema.png)

### <a name="join-operator"></a><span data-ttu-id="442a8-358">join operator</span><span class="sxs-lookup"><span data-stu-id="442a8-358">join operator</span></span>
    Table1 | join (Table2) on CommonColumn

<span data-ttu-id="442a8-359">Merges the rows of two tables by matching values of the specified column.</span><span class="sxs-lookup"><span data-stu-id="442a8-359">Merges the rows of two tables by matching values of the specified column.</span></span>

<span data-ttu-id="442a8-360">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-360">**Syntax**</span></span>

    Table1 | join [kind=Kind] (Table2) on CommonColumn [, ...]

<span data-ttu-id="442a8-361">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-361">**Arguments**</span></span>

* <span data-ttu-id="442a8-362">*Table1* - the 'left side' of the join.</span><span class="sxs-lookup"><span data-stu-id="442a8-362">*Table1* - the 'left side' of the join.</span></span>
* <span data-ttu-id="442a8-363">*Table2* - the 'right side' of the join.</span><span class="sxs-lookup"><span data-stu-id="442a8-363">*Table2* - the 'right side' of the join.</span></span> <span data-ttu-id="442a8-364">It can be a nested query expression that outputs a table.</span><span class="sxs-lookup"><span data-stu-id="442a8-364">It can be a nested query expression that outputs a table.</span></span>
* <span data-ttu-id="442a8-365">*CommonColumn* - a column that has the same name in the two tables.</span><span class="sxs-lookup"><span data-stu-id="442a8-365">*CommonColumn* - a column that has the same name in the two tables.</span></span>
* <span data-ttu-id="442a8-366">*Kind* - specifies how rows from the two tables are to be matched.</span><span class="sxs-lookup"><span data-stu-id="442a8-366">*Kind* - specifies how rows from the two tables are to be matched.</span></span>

<span data-ttu-id="442a8-367">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-367">**Returns**</span></span>

<span data-ttu-id="442a8-368">A table with:</span><span class="sxs-lookup"><span data-stu-id="442a8-368">A table with:</span></span>

* <span data-ttu-id="442a8-369">A column for every column in each of the two tables, including the matching keys.</span><span class="sxs-lookup"><span data-stu-id="442a8-369">A column for every column in each of the two tables, including the matching keys.</span></span> <span data-ttu-id="442a8-370">The columns of the right side will be automatically renamed if there are name clashes.</span><span class="sxs-lookup"><span data-stu-id="442a8-370">The columns of the right side will be automatically renamed if there are name clashes.</span></span>
* <span data-ttu-id="442a8-371">A row for every match between the input tables.</span><span class="sxs-lookup"><span data-stu-id="442a8-371">A row for every match between the input tables.</span></span> <span data-ttu-id="442a8-372">A match is a row selected from one table that has the same value for all the `on` fields as a row in the other table.</span><span class="sxs-lookup"><span data-stu-id="442a8-372">A match is a row selected from one table that has the same value for all the `on` fields as a row in the other table.</span></span> 
* <span data-ttu-id="442a8-373">`Kind` unspecified or `= innerunique`</span><span class="sxs-lookup"><span data-stu-id="442a8-373">`Kind` unspecified or `= innerunique`</span></span>
  
    <span data-ttu-id="442a8-374">Only one row from the left side is matched for each value of the `on` key.</span><span class="sxs-lookup"><span data-stu-id="442a8-374">Only one row from the left side is matched for each value of the `on` key.</span></span> <span data-ttu-id="442a8-375">The output contains a row for each match of this row with rows from the right.</span><span class="sxs-lookup"><span data-stu-id="442a8-375">The output contains a row for each match of this row with rows from the right.</span></span>
* `kind=inner`
  
     <span data-ttu-id="442a8-376">There's a row in the output for every combination of matching rows from left and right.</span><span class="sxs-lookup"><span data-stu-id="442a8-376">There's a row in the output for every combination of matching rows from left and right.</span></span>
* <span data-ttu-id="442a8-377">`kind=leftouter` (or `kind=rightouter` or `kind=fullouter`)</span><span class="sxs-lookup"><span data-stu-id="442a8-377">`kind=leftouter` (or `kind=rightouter` or `kind=fullouter`)</span></span>
  
     <span data-ttu-id="442a8-378">In addition to the inner matches, there's a row for every row on the left (and/or right), even if it has no match.</span><span class="sxs-lookup"><span data-stu-id="442a8-378">In addition to the inner matches, there's a row for every row on the left (and/or right), even if it has no match.</span></span> <span data-ttu-id="442a8-379">In that case, the unmatched output cells contain nulls.</span><span class="sxs-lookup"><span data-stu-id="442a8-379">In that case, the unmatched output cells contain nulls.</span></span>
* `kind=leftanti`
  
     <span data-ttu-id="442a8-380">Returns all the records from the left side that do not have matches from the right.</span><span class="sxs-lookup"><span data-stu-id="442a8-380">Returns all the records from the left side that do not have matches from the right.</span></span> <span data-ttu-id="442a8-381">The result table just has the columns from the left side.</span><span class="sxs-lookup"><span data-stu-id="442a8-381">The result table just has the columns from the left side.</span></span> 
* <span data-ttu-id="442a8-382">`kind=leftsemi` (or `leftantisemi`)</span><span class="sxs-lookup"><span data-stu-id="442a8-382">`kind=leftsemi` (or `leftantisemi`)</span></span>

    <span data-ttu-id="442a8-383">Returns a row from the left table if there is (or is not) a match for it in the right table.</span><span class="sxs-lookup"><span data-stu-id="442a8-383">Returns a row from the left table if there is (or is not) a match for it in the right table.</span></span> <span data-ttu-id="442a8-384">The result does not include data from the right.</span><span class="sxs-lookup"><span data-stu-id="442a8-384">The result does not include data from the right.</span></span>


<span data-ttu-id="442a8-385">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-385">**Tips**</span></span>

<span data-ttu-id="442a8-386">There is a limit of 64MB on the result table.</span><span class="sxs-lookup"><span data-stu-id="442a8-386">There is a limit of 64MB on the result table.</span></span>

<span data-ttu-id="442a8-387">For best performance:</span><span class="sxs-lookup"><span data-stu-id="442a8-387">For best performance:</span></span>

* <span data-ttu-id="442a8-388">Use `where` and `project` to reduce the numbers of rows and columns in the input tables, before the `join`.</span><span class="sxs-lookup"><span data-stu-id="442a8-388">Use `where` and `project` to reduce the numbers of rows and columns in the input tables, before the `join`.</span></span> 
* <span data-ttu-id="442a8-389">If one table is always smaller than the other, use it as the left (piped) side of the join.</span><span class="sxs-lookup"><span data-stu-id="442a8-389">If one table is always smaller than the other, use it as the left (piped) side of the join.</span></span>
* <span data-ttu-id="442a8-390">The columns for the join match must have the same name.</span><span class="sxs-lookup"><span data-stu-id="442a8-390">The columns for the join match must have the same name.</span></span> <span data-ttu-id="442a8-391">Use the project operator if necessary to rename a column in one of the tables.</span><span class="sxs-lookup"><span data-stu-id="442a8-391">Use the project operator if necessary to rename a column in one of the tables.</span></span>



<span data-ttu-id="442a8-392">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-392">**Example**</span></span>

<span data-ttu-id="442a8-393">Get extended activities from a log in which some entries mark the start and end of an activity.</span><span class="sxs-lookup"><span data-stu-id="442a8-393">Get extended activities from a log in which some entries mark the start and end of an activity.</span></span> 

```AIQL
    let Events = MyLogTable | where type=="Event" ;
    Events
    | where Name == "Start"
    | project Name, City, ActivityId, StartTime=timestamp
    | join (Events
           | where Name == "Stop"
           | project StopTime=timestamp, ActivityId)
        on ActivityId
    | project City, ActivityId, StartTime, StopTime, Duration, StopTime, StartTime

```


### <a name="limit-operator"></a><span data-ttu-id="442a8-394">limit operator</span><span class="sxs-lookup"><span data-stu-id="442a8-394">limit operator</span></span>
     T | limit 5

<span data-ttu-id="442a8-395">Returns up to the specified number of rows from the input table.</span><span class="sxs-lookup"><span data-stu-id="442a8-395">Returns up to the specified number of rows from the input table.</span></span> <span data-ttu-id="442a8-396">There is no guarantee which records are returned.</span><span class="sxs-lookup"><span data-stu-id="442a8-396">There is no guarantee which records are returned.</span></span> <span data-ttu-id="442a8-397">(To return specific records, use [`top`](#top-operator).)</span><span class="sxs-lookup"><span data-stu-id="442a8-397">(To return specific records, use [`top`](#top-operator).)</span></span>

<span data-ttu-id="442a8-398">**Alias** `take`</span><span class="sxs-lookup"><span data-stu-id="442a8-398">**Alias** `take`</span></span>

<span data-ttu-id="442a8-399">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-399">**Syntax**</span></span>

    T | limit NumberOfRows


<span data-ttu-id="442a8-400">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-400">**Tips**</span></span>

<span data-ttu-id="442a8-401">`Take` is a simple and efficient way to see a sample of your results when you're working interactively.</span><span class="sxs-lookup"><span data-stu-id="442a8-401">`Take` is a simple and efficient way to see a sample of your results when you're working interactively.</span></span> <span data-ttu-id="442a8-402">Be aware that it doesn't guarantee to produce any particular rows, or to produce them in any particular order.</span><span class="sxs-lookup"><span data-stu-id="442a8-402">Be aware that it doesn't guarantee to produce any particular rows, or to produce them in any particular order.</span></span>

<span data-ttu-id="442a8-403">There's an implicit limit on the number of rows returned to the client, even if you don't use `take`.</span><span class="sxs-lookup"><span data-stu-id="442a8-403">There's an implicit limit on the number of rows returned to the client, even if you don't use `take`.</span></span> <span data-ttu-id="442a8-404">To lift this limit, use the `notruncation` client request option.</span><span class="sxs-lookup"><span data-stu-id="442a8-404">To lift this limit, use the `notruncation` client request option.</span></span>

### <a name="make-series-operator"></a><span data-ttu-id="442a8-405">make-series operator</span><span class="sxs-lookup"><span data-stu-id="442a8-405">make-series operator</span></span>

<span data-ttu-id="442a8-406">Performs an aggregation.</span><span class="sxs-lookup"><span data-stu-id="442a8-406">Performs an aggregation.</span></span> <span data-ttu-id="442a8-407">Unlike [summarize](#summarize-operator), there is one output row for each group.</span><span class="sxs-lookup"><span data-stu-id="442a8-407">Unlike [summarize](#summarize-operator), there is one output row for each group.</span></span> <span data-ttu-id="442a8-408">In the result columns, the values in each group are packed into arrays.</span><span class="sxs-lookup"><span data-stu-id="442a8-408">In the result columns, the values in each group are packed into arrays.</span></span> 

<span data-ttu-id="442a8-409">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-409">**Syntax**</span></span>

    T | 
    make-series [Column =] Aggregation default = DefaultValue [, ...] 
    on AxisColumn in range(start, stop, step) 
    by [Column =] GroupExpression [, ...]


<span data-ttu-id="442a8-410">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-410">**Arguments**</span></span>

* <span data-ttu-id="442a8-411">*Column:* Optional name for a result column.</span><span class="sxs-lookup"><span data-stu-id="442a8-411">*Column:* Optional name for a result column.</span></span> <span data-ttu-id="442a8-412">Defaults to a name derived from the expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-412">Defaults to a name derived from the expression.</span></span>
* <span data-ttu-id="442a8-413">*DefaultValue:* If there is no row with specific values of AxisColumn and GroupExpression then in the results the correponding element of the array will be assigned with a DefaultValue.</span><span class="sxs-lookup"><span data-stu-id="442a8-413">*DefaultValue:* If there is no row with specific values of AxisColumn and GroupExpression then in the results the correponding element of the array will be assigned with a DefaultValue.</span></span> 
* <span data-ttu-id="442a8-414">*Aggregation:* A numeric expression using an [aggregation function](#aggregations).</span><span class="sxs-lookup"><span data-stu-id="442a8-414">*Aggregation:* A numeric expression using an [aggregation function](#aggregations).</span></span> 
* <span data-ttu-id="442a8-415">*AxisColumn:* A column on which the series is ordered.</span><span class="sxs-lookup"><span data-stu-id="442a8-415">*AxisColumn:* A column on which the series is ordered.</span></span> <span data-ttu-id="442a8-416">It can be considered as a timeline, but any numeric types are accepted.</span><span class="sxs-lookup"><span data-stu-id="442a8-416">It can be considered as a timeline, but any numeric types are accepted.</span></span>
<span data-ttu-id="442a8-417">*start, stop, step:* Defines the list of values of AxisColumn for every row.</span><span class="sxs-lookup"><span data-stu-id="442a8-417">*start, stop, step:* Defines the list of values of AxisColumn for every row.</span></span> <span data-ttu-id="442a8-418">Every other result aggregation column has an array of the same length.</span><span class="sxs-lookup"><span data-stu-id="442a8-418">Every other result aggregation column has an array of the same length.</span></span> 
* <span data-ttu-id="442a8-419">*GroupExpression:* An expression over the columns, that provides a set of distinct values.</span><span class="sxs-lookup"><span data-stu-id="442a8-419">*GroupExpression:* An expression over the columns, that provides a set of distinct values.</span></span> <span data-ttu-id="442a8-420">There is one row in the output for each value of the GroupExpression.</span><span class="sxs-lookup"><span data-stu-id="442a8-420">There is one row in the output for each value of the GroupExpression.</span></span> <span data-ttu-id="442a8-421">Typically it's a column name that already provides a restricted set of values.</span><span class="sxs-lookup"><span data-stu-id="442a8-421">Typically it's a column name that already provides a restricted set of values.</span></span> 

<span data-ttu-id="442a8-422">**Tip**</span><span class="sxs-lookup"><span data-stu-id="442a8-422">**Tip**</span></span>

<span data-ttu-id="442a8-423">The result arrays are rendered in an Analytics chart in the same way as the corresponding summarize operation.</span><span class="sxs-lookup"><span data-stu-id="442a8-423">The result arrays are rendered in an Analytics chart in the same way as the corresponding summarize operation.</span></span>

<span data-ttu-id="442a8-424">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-424">**Example**</span></span>

```AIQL
requests
| make-series sum(itemCount) default=0, avg(duration) default=0
  on timestamp in range (ago(7d), now(), 1d)
  by client_City
```

![Results of make-series](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/make-series.png)

### <a name="mvexpand-operator"></a><span data-ttu-id="442a8-426">mvexpand operator</span><span class="sxs-lookup"><span data-stu-id="442a8-426">mvexpand operator</span></span>
    T | mvexpand listColumn 

<span data-ttu-id="442a8-427">Expands an list from a dynamic-typed (JSON) cell so that each entry has a separate row.</span><span class="sxs-lookup"><span data-stu-id="442a8-427">Expands an list from a dynamic-typed (JSON) cell so that each entry has a separate row.</span></span> <span data-ttu-id="442a8-428">All the other cells in an expanded row are duplicated.</span><span class="sxs-lookup"><span data-stu-id="442a8-428">All the other cells in an expanded row are duplicated.</span></span> 

<span data-ttu-id="442a8-429">(See also [`summarize makelist`](#summarize-operator) which performs the opposite function.)</span><span class="sxs-lookup"><span data-stu-id="442a8-429">(See also [`summarize makelist`](#summarize-operator) which performs the opposite function.)</span></span>

<span data-ttu-id="442a8-430">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-430">**Example**</span></span>

<span data-ttu-id="442a8-431">Assume the input table is:</span><span class="sxs-lookup"><span data-stu-id="442a8-431">Assume the input table is:</span></span>

| <span data-ttu-id="442a8-432">A:int</span><span class="sxs-lookup"><span data-stu-id="442a8-432">A:int</span></span> | <span data-ttu-id="442a8-433">B:string</span><span class="sxs-lookup"><span data-stu-id="442a8-433">B:string</span></span> | <span data-ttu-id="442a8-434">D:dynamic</span><span class="sxs-lookup"><span data-stu-id="442a8-434">D:dynamic</span></span> |
| --- | --- | --- |
| <span data-ttu-id="442a8-435">1</span><span class="sxs-lookup"><span data-stu-id="442a8-435">1</span></span> |<span data-ttu-id="442a8-436">"hello"</span><span class="sxs-lookup"><span data-stu-id="442a8-436">"hello"</span></span> |<span data-ttu-id="442a8-437">{"key":"value"}</span><span class="sxs-lookup"><span data-stu-id="442a8-437">{"key":"value"}</span></span> |
| <span data-ttu-id="442a8-438">2</span><span class="sxs-lookup"><span data-stu-id="442a8-438">2</span></span> |<span data-ttu-id="442a8-439">"world"</span><span class="sxs-lookup"><span data-stu-id="442a8-439">"world"</span></span> |<span data-ttu-id="442a8-440">[0,1,"k","v"]</span><span class="sxs-lookup"><span data-stu-id="442a8-440">[0,1,"k","v"]</span></span> |

    mvexpand D

<span data-ttu-id="442a8-441">Result is:</span><span class="sxs-lookup"><span data-stu-id="442a8-441">Result is:</span></span>

| <span data-ttu-id="442a8-442">A:int</span><span class="sxs-lookup"><span data-stu-id="442a8-442">A:int</span></span> | <span data-ttu-id="442a8-443">B:string</span><span class="sxs-lookup"><span data-stu-id="442a8-443">B:string</span></span> | <span data-ttu-id="442a8-444">D:dynamic</span><span class="sxs-lookup"><span data-stu-id="442a8-444">D:dynamic</span></span> |
| --- | --- | --- |
| <span data-ttu-id="442a8-445">1</span><span class="sxs-lookup"><span data-stu-id="442a8-445">1</span></span> |<span data-ttu-id="442a8-446">"hello"</span><span class="sxs-lookup"><span data-stu-id="442a8-446">"hello"</span></span> |<span data-ttu-id="442a8-447">{"key":"value"}</span><span class="sxs-lookup"><span data-stu-id="442a8-447">{"key":"value"}</span></span> |
| <span data-ttu-id="442a8-448">2</span><span class="sxs-lookup"><span data-stu-id="442a8-448">2</span></span> |<span data-ttu-id="442a8-449">"world"</span><span class="sxs-lookup"><span data-stu-id="442a8-449">"world"</span></span> |<span data-ttu-id="442a8-450">0</span><span class="sxs-lookup"><span data-stu-id="442a8-450">0</span></span> |
| <span data-ttu-id="442a8-451">2</span><span class="sxs-lookup"><span data-stu-id="442a8-451">2</span></span> |<span data-ttu-id="442a8-452">"world"</span><span class="sxs-lookup"><span data-stu-id="442a8-452">"world"</span></span> |<span data-ttu-id="442a8-453">1</span><span class="sxs-lookup"><span data-stu-id="442a8-453">1</span></span> |
| <span data-ttu-id="442a8-454">2</span><span class="sxs-lookup"><span data-stu-id="442a8-454">2</span></span> |<span data-ttu-id="442a8-455">"world"</span><span class="sxs-lookup"><span data-stu-id="442a8-455">"world"</span></span> |<span data-ttu-id="442a8-456">"k"</span><span class="sxs-lookup"><span data-stu-id="442a8-456">"k"</span></span> |
| <span data-ttu-id="442a8-457">2</span><span class="sxs-lookup"><span data-stu-id="442a8-457">2</span></span> |<span data-ttu-id="442a8-458">"world"</span><span class="sxs-lookup"><span data-stu-id="442a8-458">"world"</span></span> |<span data-ttu-id="442a8-459">"v"</span><span class="sxs-lookup"><span data-stu-id="442a8-459">"v"</span></span> |

<span data-ttu-id="442a8-460">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-460">**Syntax**</span></span>

    T | mvexpand  [bagexpansion=(bag | array)] ColumnName [limit Rowlimit]

    T | mvexpand  [bagexpansion=(bag | array)] [Name =] ArrayExpression [to typeof(Typename)] [limit Rowlimit]

<span data-ttu-id="442a8-461">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-461">**Arguments**</span></span>

* <span data-ttu-id="442a8-462">*ColumnName:* In the result, arrays in the named column are expanded to multiple rows.</span><span class="sxs-lookup"><span data-stu-id="442a8-462">*ColumnName:* In the result, arrays in the named column are expanded to multiple rows.</span></span> 
* <span data-ttu-id="442a8-463">*ArrayExpression:* An expression yielding an array.</span><span class="sxs-lookup"><span data-stu-id="442a8-463">*ArrayExpression:* An expression yielding an array.</span></span> <span data-ttu-id="442a8-464">If this form is used, a new column is added and the existing one is preserved.</span><span class="sxs-lookup"><span data-stu-id="442a8-464">If this form is used, a new column is added and the existing one is preserved.</span></span>
* <span data-ttu-id="442a8-465">*Name:* A name for the new column.</span><span class="sxs-lookup"><span data-stu-id="442a8-465">*Name:* A name for the new column.</span></span>
* <span data-ttu-id="442a8-466">*Typename:* Casts the expanded expression to a particular type</span><span class="sxs-lookup"><span data-stu-id="442a8-466">*Typename:* Casts the expanded expression to a particular type</span></span>
* <span data-ttu-id="442a8-467">*RowLimit:* The maximum number of rows generated from each original row.</span><span class="sxs-lookup"><span data-stu-id="442a8-467">*RowLimit:* The maximum number of rows generated from each original row.</span></span> <span data-ttu-id="442a8-468">The default is 128.</span><span class="sxs-lookup"><span data-stu-id="442a8-468">The default is 128.</span></span>

<span data-ttu-id="442a8-469">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-469">**Returns**</span></span>

<span data-ttu-id="442a8-470">Multiple rows for each of the values in any array in the named column or in the array expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-470">Multiple rows for each of the values in any array in the named column or in the array expression.</span></span>

<span data-ttu-id="442a8-471">The expanded column always has dynamic type.</span><span class="sxs-lookup"><span data-stu-id="442a8-471">The expanded column always has dynamic type.</span></span> <span data-ttu-id="442a8-472">Use a cast such as `todatetime()` or `toint()` if you want to compute or aggregate values.</span><span class="sxs-lookup"><span data-stu-id="442a8-472">Use a cast such as `todatetime()` or `toint()` if you want to compute or aggregate values.</span></span>

<span data-ttu-id="442a8-473">Two modes of property-bag expansions are supported:</span><span class="sxs-lookup"><span data-stu-id="442a8-473">Two modes of property-bag expansions are supported:</span></span>

* <span data-ttu-id="442a8-474">`bagexpansion=bag`: Property bags are expanded into single-entry property bags.</span><span class="sxs-lookup"><span data-stu-id="442a8-474">`bagexpansion=bag`: Property bags are expanded into single-entry property bags.</span></span> <span data-ttu-id="442a8-475">This is the default expansion.</span><span class="sxs-lookup"><span data-stu-id="442a8-475">This is the default expansion.</span></span>
* <span data-ttu-id="442a8-476">`bagexpansion=array`: Property bags are expanded into two-element `[`*key*`,`*value*`]` array structures, allowing uniform access to keys and values (as well as, for example, running a distinct-count aggregation over property names).</span><span class="sxs-lookup"><span data-stu-id="442a8-476">`bagexpansion=array`: Property bags are expanded into two-element `[`*key*`,`*value*`]` array structures, allowing uniform access to keys and values (as well as, for example, running a distinct-count aggregation over property names).</span></span>

<span data-ttu-id="442a8-477">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-477">**Examples**</span></span>

    exceptions | take 1
    | mvexpand details[0]

<span data-ttu-id="442a8-478">Splits an exception record into rows for each item in the details field.</span><span class="sxs-lookup"><span data-stu-id="442a8-478">Splits an exception record into rows for each item in the details field.</span></span>

### <a name="parse-operator"></a><span data-ttu-id="442a8-479">parse operator</span><span class="sxs-lookup"><span data-stu-id="442a8-479">parse operator</span></span>
    T | parse "I got 2 socks for my birthday when I was 63 years old"
    with * "got" counter:long " " present "for" * "was" year:long *


    T | parse kind=relaxed
          "I got no socks for my birthday when I was 63 years old"
    with * "got" counter:long " " present "for" * "was" year:long *

    T |  parse kind=regex "I got socks for my 63rd birthday"
    with "(I|She) got " present " for .*?" year:long *

<span data-ttu-id="442a8-480">Extracts values from a string.</span><span class="sxs-lookup"><span data-stu-id="442a8-480">Extracts values from a string.</span></span> <span data-ttu-id="442a8-481">Can use simple or regular expression matching.</span><span class="sxs-lookup"><span data-stu-id="442a8-481">Can use simple or regular expression matching.</span></span>

<span data-ttu-id="442a8-482">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-482">**Syntax**</span></span>

    T | parse [kind=regex|relaxed] SourceText
        with [Match | Column [: Type [*]] ]  ...

<span data-ttu-id="442a8-483">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-483">**Arguments**</span></span>

* <span data-ttu-id="442a8-484">`T`: The input table.</span><span class="sxs-lookup"><span data-stu-id="442a8-484">`T`: The input table.</span></span>
* <span data-ttu-id="442a8-485">`kind`:</span><span class="sxs-lookup"><span data-stu-id="442a8-485">`kind`:</span></span> 
  * <span data-ttu-id="442a8-486">`simple` (default): the `Match` strings are plain strings.</span><span class="sxs-lookup"><span data-stu-id="442a8-486">`simple` (default): the `Match` strings are plain strings.</span></span>
  * <span data-ttu-id="442a8-487">`relaxed`: if the text doesn't parse as the type of a column, the column is set to null and the parse continues</span><span class="sxs-lookup"><span data-stu-id="442a8-487">`relaxed`: if the text doesn't parse as the type of a column, the column is set to null and the parse continues</span></span> 
  * <span data-ttu-id="442a8-488">`regex`: the `Match` strings are regular expressions.</span><span class="sxs-lookup"><span data-stu-id="442a8-488">`regex`: the `Match` strings are regular expressions.</span></span>
* <span data-ttu-id="442a8-489">`Text`: A column or other expression that evaluates to or can be converted to a string.</span><span class="sxs-lookup"><span data-stu-id="442a8-489">`Text`: A column or other expression that evaluates to or can be converted to a string.</span></span>
* <span data-ttu-id="442a8-490">*Match:* Match the next part of the string, and discard it.</span><span class="sxs-lookup"><span data-stu-id="442a8-490">*Match:* Match the next part of the string, and discard it.</span></span>
* <span data-ttu-id="442a8-491">*Column:* Assign the next part of the string to this column.</span><span class="sxs-lookup"><span data-stu-id="442a8-491">*Column:* Assign the next part of the string to this column.</span></span> <span data-ttu-id="442a8-492">The column is created if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="442a8-492">The column is created if it does not exist.</span></span>
* <span data-ttu-id="442a8-493">*Type:* Parse the next part of the string as the specified type, such as int, date, double.</span><span class="sxs-lookup"><span data-stu-id="442a8-493">*Type:* Parse the next part of the string as the specified type, such as int, date, double.</span></span> 

<span data-ttu-id="442a8-494">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-494">**Returns**</span></span>

<span data-ttu-id="442a8-495">The input table, extended according to the list of Columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-495">The input table, extended according to the list of Columns.</span></span>

<span data-ttu-id="442a8-496">The elements in the `with` clause are matched against the source text in turn.</span><span class="sxs-lookup"><span data-stu-id="442a8-496">The elements in the `with` clause are matched against the source text in turn.</span></span> <span data-ttu-id="442a8-497">Each element chews off a chunk of the source text:</span><span class="sxs-lookup"><span data-stu-id="442a8-497">Each element chews off a chunk of the source text:</span></span> 

* <span data-ttu-id="442a8-498">A literal string or regular expression moves the matching cursor by the length of the match.</span><span class="sxs-lookup"><span data-stu-id="442a8-498">A literal string or regular expression moves the matching cursor by the length of the match.</span></span>
* <span data-ttu-id="442a8-499">In a regex parse, a regular expression can use the minimization operator '?' to move as soon as possible to the following match.</span><span class="sxs-lookup"><span data-stu-id="442a8-499">In a regex parse, a regular expression can use the minimization operator '?' to move as soon as possible to the following match.</span></span>
* <span data-ttu-id="442a8-500">A column name with a type parses the text as the specified type.</span><span class="sxs-lookup"><span data-stu-id="442a8-500">A column name with a type parses the text as the specified type.</span></span> <span data-ttu-id="442a8-501">Unless kind=relaxed, an unsuccessful parse invalidates matching the whole pattern.</span><span class="sxs-lookup"><span data-stu-id="442a8-501">Unless kind=relaxed, an unsuccessful parse invalidates matching the whole pattern.</span></span>
* <span data-ttu-id="442a8-502">A column name without a type, or with the type 'string', copies the minimum number of characters to get to the following match.</span><span class="sxs-lookup"><span data-stu-id="442a8-502">A column name without a type, or with the type 'string', copies the minimum number of characters to get to the following match.</span></span>
* <span data-ttu-id="442a8-503">' \* ' Skips the minimum number of characters to get to the following match.</span><span class="sxs-lookup"><span data-stu-id="442a8-503">' \* ' Skips the minimum number of characters to get to the following match.</span></span> <span data-ttu-id="442a8-504">You can use '\*' at the start and end of the pattern, or after a type other than string, or between string matches.</span><span class="sxs-lookup"><span data-stu-id="442a8-504">You can use '\*' at the start and end of the pattern, or after a type other than string, or between string matches.</span></span>

<span data-ttu-id="442a8-505">All of the elements in a parse pattern must match correctly; otherwise, no results will be produced.</span><span class="sxs-lookup"><span data-stu-id="442a8-505">All of the elements in a parse pattern must match correctly; otherwise, no results will be produced.</span></span> <span data-ttu-id="442a8-506">The exception to this rule is that when kind=relaxed, if parsing a typed variable fails, the rest of the parse continues.</span><span class="sxs-lookup"><span data-stu-id="442a8-506">The exception to this rule is that when kind=relaxed, if parsing a typed variable fails, the rest of the parse continues.</span></span>

<span data-ttu-id="442a8-507">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-507">**Examples**</span></span>

<span data-ttu-id="442a8-508">*Simple:*</span><span class="sxs-lookup"><span data-stu-id="442a8-508">*Simple:*</span></span>

```AIQL

// Test without reading a table:
 range x from 1 to 1 step 1 
 | parse "I got 2 socks for my birthday when I was 63 years old" 
    with 
     *   // skip until next match
     "got" 
     counter: long // read a number
     " " // separate fields
     present // copy string up to next match
     "for" 
     *  // skip until next match
     "was" 
     year:long // parse number
     *  // skip rest of string
```

| <span data-ttu-id="442a8-509">x</span><span class="sxs-lookup"><span data-stu-id="442a8-509">x</span></span> | <span data-ttu-id="442a8-510">counter</span><span class="sxs-lookup"><span data-stu-id="442a8-510">counter</span></span> | <span data-ttu-id="442a8-511">present</span><span class="sxs-lookup"><span data-stu-id="442a8-511">present</span></span> | <span data-ttu-id="442a8-512">Year</span><span class="sxs-lookup"><span data-stu-id="442a8-512">Year</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="442a8-513">1</span><span class="sxs-lookup"><span data-stu-id="442a8-513">1</span></span> |<span data-ttu-id="442a8-514">2</span><span class="sxs-lookup"><span data-stu-id="442a8-514">2</span></span> |<span data-ttu-id="442a8-515">socks</span><span class="sxs-lookup"><span data-stu-id="442a8-515">socks</span></span> |<span data-ttu-id="442a8-516">63</span><span class="sxs-lookup"><span data-stu-id="442a8-516">63</span></span> |

<span data-ttu-id="442a8-517">*Relaxed:*</span><span class="sxs-lookup"><span data-stu-id="442a8-517">*Relaxed:*</span></span>

<span data-ttu-id="442a8-518">When the input contains a correct match for every typed column, a relaxed parse produces the same results as a simple parse.</span><span class="sxs-lookup"><span data-stu-id="442a8-518">When the input contains a correct match for every typed column, a relaxed parse produces the same results as a simple parse.</span></span> <span data-ttu-id="442a8-519">But if one of the typed columns doesn't parse correctly, a relaxed parse continues to process the rest of the pattern, whereas a simple parse stops and fails to generate any result.</span><span class="sxs-lookup"><span data-stu-id="442a8-519">But if one of the typed columns doesn't parse correctly, a relaxed parse continues to process the rest of the pattern, whereas a simple parse stops and fails to generate any result.</span></span>

```AIQL

// Test without reading a table:
 range x from 1 to 1 step 1 
 | parse kind="relaxed"
        "I got several socks for my birthday when I was 63 years old" 
    with 
     *   // skip until next match
     "got" 
     counter: long // read a number
     " " // separate fields
     present // copy string up to next match
     "for" 
     *  // skip until next match
     "was" 
     year:long // parse number
     *  // skip rest of string
```


| <span data-ttu-id="442a8-520">x</span><span class="sxs-lookup"><span data-stu-id="442a8-520">x</span></span> | <span data-ttu-id="442a8-521">present</span><span class="sxs-lookup"><span data-stu-id="442a8-521">present</span></span> | <span data-ttu-id="442a8-522">Year</span><span class="sxs-lookup"><span data-stu-id="442a8-522">Year</span></span> |
| --- | --- | --- |
| <span data-ttu-id="442a8-523">1</span><span class="sxs-lookup"><span data-stu-id="442a8-523">1</span></span> |<span data-ttu-id="442a8-524">socks</span><span class="sxs-lookup"><span data-stu-id="442a8-524">socks</span></span> |<span data-ttu-id="442a8-525">63</span><span class="sxs-lookup"><span data-stu-id="442a8-525">63</span></span> |

<span data-ttu-id="442a8-526">*Regex:*</span><span class="sxs-lookup"><span data-stu-id="442a8-526">*Regex:*</span></span>

```AIQL

// Run a test without reading a table:
range x from 1 to 1 step 1 
// Test string:
| extend s = "Event: NotifySliceRelease (resourceName=Scheduler, totalSlices=27, sliceNumber=16, lockTime=02/17/2016 07:31, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 06:20:00 ) }" 
// Parse it:
| parse kind=regex s 
  with ".*?=" resource 
       ", total.*?sliceNumber=" slice:long *
       "lockTime=" lock
       ",.*?releaseTime=" release 
       ",.*?previousLockTime=" previous:date 
       @".*\)" *
| project-away x, s
```

| <span data-ttu-id="442a8-527">resource</span><span class="sxs-lookup"><span data-stu-id="442a8-527">resource</span></span> | <span data-ttu-id="442a8-528">slice</span><span class="sxs-lookup"><span data-stu-id="442a8-528">slice</span></span> | <span data-ttu-id="442a8-529">lock</span><span class="sxs-lookup"><span data-stu-id="442a8-529">lock</span></span> | <span data-ttu-id="442a8-530">release</span><span class="sxs-lookup"><span data-stu-id="442a8-530">release</span></span> | <span data-ttu-id="442a8-531">previous</span><span class="sxs-lookup"><span data-stu-id="442a8-531">previous</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="442a8-532">Scheduler</span><span class="sxs-lookup"><span data-stu-id="442a8-532">Scheduler</span></span> |<span data-ttu-id="442a8-533">16</span><span class="sxs-lookup"><span data-stu-id="442a8-533">16</span></span> |<span data-ttu-id="442a8-534">02/17/2016 07:31:00</span><span class="sxs-lookup"><span data-stu-id="442a8-534">02/17/2016 07:31:00</span></span> |<span data-ttu-id="442a8-535">02/17/2016 08:41</span><span class="sxs-lookup"><span data-stu-id="442a8-535">02/17/2016 08:41</span></span> |<span data-ttu-id="442a8-536">2016-02-17T06:20:00Z</span><span class="sxs-lookup"><span data-stu-id="442a8-536">2016-02-17T06:20:00Z</span></span> |

### <a name="project-operator"></a><span data-ttu-id="442a8-537">project operator</span><span class="sxs-lookup"><span data-stu-id="442a8-537">project operator</span></span>
    T | project cost=price*quantity, price

<span data-ttu-id="442a8-538">Select the columns to include, rename or drop, and insert new computed columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-538">Select the columns to include, rename or drop, and insert new computed columns.</span></span> <span data-ttu-id="442a8-539">The order of the columns in the result is specified by the order of the arguments.</span><span class="sxs-lookup"><span data-stu-id="442a8-539">The order of the columns in the result is specified by the order of the arguments.</span></span> <span data-ttu-id="442a8-540">Only the columns specified in the arguments are included in the result: any others in the input are dropped.</span><span class="sxs-lookup"><span data-stu-id="442a8-540">Only the columns specified in the arguments are included in the result: any others in the input are dropped.</span></span>  <span data-ttu-id="442a8-541">(See also `extend`.)</span><span class="sxs-lookup"><span data-stu-id="442a8-541">(See also `extend`.)</span></span>

<span data-ttu-id="442a8-542">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-542">**Syntax**</span></span>

    T | project ColumnName [= Expression] [, ...]

<span data-ttu-id="442a8-543">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-543">**Arguments**</span></span>

* <span data-ttu-id="442a8-544">*T:* The input table.</span><span class="sxs-lookup"><span data-stu-id="442a8-544">*T:* The input table.</span></span>
* <span data-ttu-id="442a8-545">*ColumnName:* The name of a column to appear in the output.</span><span class="sxs-lookup"><span data-stu-id="442a8-545">*ColumnName:* The name of a column to appear in the output.</span></span> <span data-ttu-id="442a8-546">If there is no *Expression*, a column of that name must appear in the input.</span><span class="sxs-lookup"><span data-stu-id="442a8-546">If there is no *Expression*, a column of that name must appear in the input.</span></span> <span data-ttu-id="442a8-547">[Names](#names) are case-sensitive and can contain alphabetic, numeric or '_' characters.</span><span class="sxs-lookup"><span data-stu-id="442a8-547">[Names](#names) are case-sensitive and can contain alphabetic, numeric or '_' characters.</span></span> <span data-ttu-id="442a8-548">Use `['...']` or `["..."]` to quote keywords or names with other characters.</span><span class="sxs-lookup"><span data-stu-id="442a8-548">Use `['...']` or `["..."]` to quote keywords or names with other characters.</span></span>
* <span data-ttu-id="442a8-549">*Expression:* Optional scalar expression referencing the input columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-549">*Expression:* Optional scalar expression referencing the input columns.</span></span> 
  
    <span data-ttu-id="442a8-550">It is legal to return a new calculated column with the same name as an existing column in the input.</span><span class="sxs-lookup"><span data-stu-id="442a8-550">It is legal to return a new calculated column with the same name as an existing column in the input.</span></span>

<span data-ttu-id="442a8-551">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-551">**Returns**</span></span>

<span data-ttu-id="442a8-552">A table that has the columns named as arguments, and as many rows as the input table.</span><span class="sxs-lookup"><span data-stu-id="442a8-552">A table that has the columns named as arguments, and as many rows as the input table.</span></span>

<span data-ttu-id="442a8-553">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-553">**Example**</span></span>

<span data-ttu-id="442a8-554">The following example shows several kinds of manipulations that can be done using the `project` operator.</span><span class="sxs-lookup"><span data-stu-id="442a8-554">The following example shows several kinds of manipulations that can be done using the `project` operator.</span></span> <span data-ttu-id="442a8-555">The input table `T` has three columns of type `int`: `A`, `B`, and `C`.</span><span class="sxs-lookup"><span data-stu-id="442a8-555">The input table `T` has three columns of type `int`: `A`, `B`, and `C`.</span></span> 

```AIQL
T
| project
    X=C,               // Rename column C to X
    A=2*B,             // Calculate a new column A from the old B
    C=strcat("-",tostring(C)), // Calculate a new column C from the old C
    B=2*B,              // Calculate a new column B from the old B
    ['where'] = client_City // rename, using a keyword as a column name
```

### <a name="project-away-operator"></a><span data-ttu-id="442a8-556">project-away operator</span><span class="sxs-lookup"><span data-stu-id="442a8-556">project-away operator</span></span>
    T | project-away column1, column2, ...

<span data-ttu-id="442a8-557">Exclude specified columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-557">Exclude specified columns.</span></span> <span data-ttu-id="442a8-558">The result contains all the input columns except those you name.</span><span class="sxs-lookup"><span data-stu-id="442a8-558">The result contains all the input columns except those you name.</span></span>

### <a name="range-operator"></a><span data-ttu-id="442a8-559">range operator</span><span class="sxs-lookup"><span data-stu-id="442a8-559">range operator</span></span>
    range LastWeek from ago(7d) to now() step 1d

<span data-ttu-id="442a8-560">Generates a single-column table of values.</span><span class="sxs-lookup"><span data-stu-id="442a8-560">Generates a single-column table of values.</span></span> <span data-ttu-id="442a8-561">Notice that it doesn't have a pipeline input.</span><span class="sxs-lookup"><span data-stu-id="442a8-561">Notice that it doesn't have a pipeline input.</span></span> 

| <span data-ttu-id="442a8-562">LastWeek</span><span class="sxs-lookup"><span data-stu-id="442a8-562">LastWeek</span></span> |
| --- |
| <span data-ttu-id="442a8-563">2015-12-05 09:10:04.627</span><span class="sxs-lookup"><span data-stu-id="442a8-563">2015-12-05 09:10:04.627</span></span> |
| <span data-ttu-id="442a8-564">2015-12-06 09:10:04.627</span><span class="sxs-lookup"><span data-stu-id="442a8-564">2015-12-06 09:10:04.627</span></span> |
| <span data-ttu-id="442a8-565">...</span><span class="sxs-lookup"><span data-stu-id="442a8-565">...</span></span> |
| <span data-ttu-id="442a8-566">2015-12-12 09:10:04.627</span><span class="sxs-lookup"><span data-stu-id="442a8-566">2015-12-12 09:10:04.627</span></span> |

<span data-ttu-id="442a8-567">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-567">**Syntax**</span></span>

    range ColumnName from Start to Stop step Step

<span data-ttu-id="442a8-568">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-568">**Arguments**</span></span>

* <span data-ttu-id="442a8-569">*ColumnName:* The name of the single column in the output table.</span><span class="sxs-lookup"><span data-stu-id="442a8-569">*ColumnName:* The name of the single column in the output table.</span></span>
* <span data-ttu-id="442a8-570">*Start:* The smallest value in the output.</span><span class="sxs-lookup"><span data-stu-id="442a8-570">*Start:* The smallest value in the output.</span></span>
* <span data-ttu-id="442a8-571">*Stop:* The highest value being generated in the output (or a bound on the highest value, if *step* steps over this value).</span><span class="sxs-lookup"><span data-stu-id="442a8-571">*Stop:* The highest value being generated in the output (or a bound on the highest value, if *step* steps over this value).</span></span>
* <span data-ttu-id="442a8-572">*Step:* The difference between two consecutive values.</span><span class="sxs-lookup"><span data-stu-id="442a8-572">*Step:* The difference between two consecutive values.</span></span> 

<span data-ttu-id="442a8-573">The arguments must be numeric, date or timespan values.</span><span class="sxs-lookup"><span data-stu-id="442a8-573">The arguments must be numeric, date or timespan values.</span></span> <span data-ttu-id="442a8-574">They can't reference the columns of any table.</span><span class="sxs-lookup"><span data-stu-id="442a8-574">They can't reference the columns of any table.</span></span> <span data-ttu-id="442a8-575">(If you want to compute the range based on an input table, use the [range *function*](#range), maybe with the [mvexpand operator](#mvexpand-operator).)</span><span class="sxs-lookup"><span data-stu-id="442a8-575">(If you want to compute the range based on an input table, use the [range *function*](#range), maybe with the [mvexpand operator](#mvexpand-operator).)</span></span> 

<span data-ttu-id="442a8-576">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-576">**Returns**</span></span>

<span data-ttu-id="442a8-577">A table with a single column called *ColumnName*, whose values are *Start*, *Start* + *Step*, ... up to and including *Stop*.</span><span class="sxs-lookup"><span data-stu-id="442a8-577">A table with a single column called *ColumnName*, whose values are *Start*, *Start* + *Step*, ... up to and including *Stop*.</span></span>

<span data-ttu-id="442a8-578">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-578">**Example**</span></span>  

```AIQL
range Steps from 1 to 8 step 3
```

<span data-ttu-id="442a8-579">A table with a single column called `Steps` whose type is `long` and whose values are `1`, `4`, and `7`.</span><span class="sxs-lookup"><span data-stu-id="442a8-579">A table with a single column called `Steps` whose type is `long` and whose values are `1`, `4`, and `7`.</span></span>

<span data-ttu-id="442a8-580">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-580">**Example**</span></span>

    range LastWeek from bin(ago(7d),1d) to now() step 1d

<span data-ttu-id="442a8-581">A table of midnight at the past seven days.</span><span class="sxs-lookup"><span data-stu-id="442a8-581">A table of midnight at the past seven days.</span></span> <span data-ttu-id="442a8-582">The bin (floor) function reduces each time to the start of the day.</span><span class="sxs-lookup"><span data-stu-id="442a8-582">The bin (floor) function reduces each time to the start of the day.</span></span>

<span data-ttu-id="442a8-583">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-583">**Example**</span></span>  

```AIQL
range timestamp from ago(4h) to now() step 1m
| join kind=fullouter
  (traces
      | where timestamp > ago(4h)
      | summarize Count=count() by bin(timestamp, 1m)
  ) on timestamp
| project Count=iff(isnull(Count), 0, Count), timestamp
| render timechart  
```

<span data-ttu-id="442a8-584">Shows how the `range` operator can be used to create a small, ad-hoc, dimension table which is then used to introduce zeros where the source data has no values.</span><span class="sxs-lookup"><span data-stu-id="442a8-584">Shows how the `range` operator can be used to create a small, ad-hoc, dimension table which is then used to introduce zeros where the source data has no values.</span></span>

### <a name="reduce-operator"></a><span data-ttu-id="442a8-585">reduce operator</span><span class="sxs-lookup"><span data-stu-id="442a8-585">reduce operator</span></span>
    exceptions | reduce by outerMessage

<span data-ttu-id="442a8-586">Tries to group together similar records.</span><span class="sxs-lookup"><span data-stu-id="442a8-586">Tries to group together similar records.</span></span> <span data-ttu-id="442a8-587">For each group, the operator outputs the `Pattern` it thinks best describes that group, and the `Count` of records in that group.</span><span class="sxs-lookup"><span data-stu-id="442a8-587">For each group, the operator outputs the `Pattern` it thinks best describes that group, and the `Count` of records in that group.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/reduce.png)

<span data-ttu-id="442a8-588">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-588">**Syntax**</span></span>

    T | reduce by  ColumnName [ with threshold=Threshold ]

<span data-ttu-id="442a8-589">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-589">**Arguments**</span></span>

* <span data-ttu-id="442a8-590">*ColumnName:* The column to examine.</span><span class="sxs-lookup"><span data-stu-id="442a8-590">*ColumnName:* The column to examine.</span></span> <span data-ttu-id="442a8-591">It must be of string type.</span><span class="sxs-lookup"><span data-stu-id="442a8-591">It must be of string type.</span></span>
* <span data-ttu-id="442a8-592">*Threshold:* A value in the range {0..1}.</span><span class="sxs-lookup"><span data-stu-id="442a8-592">*Threshold:* A value in the range {0..1}.</span></span> <span data-ttu-id="442a8-593">Default is 0.001.</span><span class="sxs-lookup"><span data-stu-id="442a8-593">Default is 0.001.</span></span> <span data-ttu-id="442a8-594">For large inputs, threshold should be small.</span><span class="sxs-lookup"><span data-stu-id="442a8-594">For large inputs, threshold should be small.</span></span> 

<span data-ttu-id="442a8-595">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-595">**Returns**</span></span>

<span data-ttu-id="442a8-596">Two columns, `Pattern` and `Count`.</span><span class="sxs-lookup"><span data-stu-id="442a8-596">Two columns, `Pattern` and `Count`.</span></span> <span data-ttu-id="442a8-597">In many cases, Pattern will be a complete value from the column.</span><span class="sxs-lookup"><span data-stu-id="442a8-597">In many cases, Pattern will be a complete value from the column.</span></span> <span data-ttu-id="442a8-598">In some cases, it can identify common terms and replace the variable parts with '\*'.</span><span class="sxs-lookup"><span data-stu-id="442a8-598">In some cases, it can identify common terms and replace the variable parts with '\*'.</span></span>

<span data-ttu-id="442a8-599">For example, the result of `reduce by city` might include:</span><span class="sxs-lookup"><span data-stu-id="442a8-599">For example, the result of `reduce by city` might include:</span></span> 

| <span data-ttu-id="442a8-600">Pattern</span><span class="sxs-lookup"><span data-stu-id="442a8-600">Pattern</span></span> | <span data-ttu-id="442a8-601">Count</span><span class="sxs-lookup"><span data-stu-id="442a8-601">Count</span></span> |
| --- | --- |
| <span data-ttu-id="442a8-602">San \*</span><span class="sxs-lookup"><span data-stu-id="442a8-602">San \*</span></span> |<span data-ttu-id="442a8-603">5182</span><span class="sxs-lookup"><span data-stu-id="442a8-603">5182</span></span> |
| <span data-ttu-id="442a8-604">Saint \*</span><span class="sxs-lookup"><span data-stu-id="442a8-604">Saint \*</span></span> |<span data-ttu-id="442a8-605">2846</span><span class="sxs-lookup"><span data-stu-id="442a8-605">2846</span></span> |
| <span data-ttu-id="442a8-606">Moscow</span><span class="sxs-lookup"><span data-stu-id="442a8-606">Moscow</span></span> |<span data-ttu-id="442a8-607">3726</span><span class="sxs-lookup"><span data-stu-id="442a8-607">3726</span></span> |
| <span data-ttu-id="442a8-608">\* -on- \*</span><span class="sxs-lookup"><span data-stu-id="442a8-608">\* -on- \*</span></span> |<span data-ttu-id="442a8-609">2730</span><span class="sxs-lookup"><span data-stu-id="442a8-609">2730</span></span> |
| <span data-ttu-id="442a8-610">Paris</span><span class="sxs-lookup"><span data-stu-id="442a8-610">Paris</span></span> |<span data-ttu-id="442a8-611">27163</span><span class="sxs-lookup"><span data-stu-id="442a8-611">27163</span></span> |

### <a name="render-directive"></a><span data-ttu-id="442a8-612">render directive</span><span class="sxs-lookup"><span data-stu-id="442a8-612">render directive</span></span>
    T | render [ table | timechart  | barchart | piechart | areachart | scatterchart ] 
        [kind= default|stacked|stacked100|unstacked]

<span data-ttu-id="442a8-613">Render directs the presentation layer how to show the table.</span><span class="sxs-lookup"><span data-stu-id="442a8-613">Render directs the presentation layer how to show the table.</span></span> <span data-ttu-id="442a8-614">It should be the last element of the pipe.</span><span class="sxs-lookup"><span data-stu-id="442a8-614">It should be the last element of the pipe.</span></span> <span data-ttu-id="442a8-615">It's a convenient alternative to using the controls on the display, allowing you to save a query with a particular presentation method.</span><span class="sxs-lookup"><span data-stu-id="442a8-615">It's a convenient alternative to using the controls on the display, allowing you to save a query with a particular presentation method.</span></span>

<span data-ttu-id="442a8-616">For some types of chart, `kind` provides additional options.</span><span class="sxs-lookup"><span data-stu-id="442a8-616">For some types of chart, `kind` provides additional options.</span></span> <span data-ttu-id="442a8-617">For example, a `stacked` barchart segments each bar by a chosen dimension, showing the contribution to the total from different values of the dimension.</span><span class="sxs-lookup"><span data-stu-id="442a8-617">For example, a `stacked` barchart segments each bar by a chosen dimension, showing the contribution to the total from different values of the dimension.</span></span> <span data-ttu-id="442a8-618">In a `stacked100` chart, every bar is the same height of 100%, so that you can compare the relative contributions.</span><span class="sxs-lookup"><span data-stu-id="442a8-618">In a `stacked100` chart, every bar is the same height of 100%, so that you can compare the relative contributions.</span></span>


### <a name="restrict-clause"></a><span data-ttu-id="442a8-619">restrict clause</span><span class="sxs-lookup"><span data-stu-id="442a8-619">restrict clause</span></span>
<span data-ttu-id="442a8-620">Specifies the set of table names available to operators that follow.</span><span class="sxs-lookup"><span data-stu-id="442a8-620">Specifies the set of table names available to operators that follow.</span></span> <span data-ttu-id="442a8-621">For example:</span><span class="sxs-lookup"><span data-stu-id="442a8-621">For example:</span></span>

    let e1 = requests | project name, client_City;
    let e2 =  requests | project name, success;
    // Exclude predefined tables from the union:
    restrict access to (e1, e2);
    union * |  take 10 

### <a name="sample-operator"></a><span data-ttu-id="442a8-622">sample operator</span><span class="sxs-lookup"><span data-stu-id="442a8-622">sample operator</span></span>

<span data-ttu-id="442a8-623">Returns uniformly distributed random rows from the input table.</span><span class="sxs-lookup"><span data-stu-id="442a8-623">Returns uniformly distributed random rows from the input table.</span></span>


<span data-ttu-id="442a8-624">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-624">**Syntax**</span></span>

    T | sample NumerOfRows

* <span data-ttu-id="442a8-625">*NumberOfRows* The number of rows to return in the sample.</span><span class="sxs-lookup"><span data-stu-id="442a8-625">*NumberOfRows* The number of rows to return in the sample.</span></span>

<span data-ttu-id="442a8-626">**Tip**</span><span class="sxs-lookup"><span data-stu-id="442a8-626">**Tip**</span></span>

<span data-ttu-id="442a8-627">Use `Take` when you don't need a uniformly distributed sample.</span><span class="sxs-lookup"><span data-stu-id="442a8-627">Use `Take` when you don't need a uniformly distributed sample.</span></span>


### <a name="sample-distinct-operator"></a><span data-ttu-id="442a8-628">sample-distinct operator</span><span class="sxs-lookup"><span data-stu-id="442a8-628">sample-distinct operator</span></span>

<span data-ttu-id="442a8-629">Returns a single column that contains up to the specified number of distinct values of the requested column.</span><span class="sxs-lookup"><span data-stu-id="442a8-629">Returns a single column that contains up to the specified number of distinct values of the requested column.</span></span> <span data-ttu-id="442a8-630">Does not currently return a fairly distributed sample.</span><span class="sxs-lookup"><span data-stu-id="442a8-630">Does not currently return a fairly distributed sample.</span></span>

<span data-ttu-id="442a8-631">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-631">**Syntax**</span></span>

    T | sample-distinct NumberOfValues of ColumnName

* <span data-ttu-id="442a8-632">*NumberOfValues* The length of the table you want.</span><span class="sxs-lookup"><span data-stu-id="442a8-632">*NumberOfValues* The length of the table you want.</span></span>
* <span data-ttu-id="442a8-633">*ColumnName* The column you want.</span><span class="sxs-lookup"><span data-stu-id="442a8-633">*ColumnName* The column you want.</span></span>

<span data-ttu-id="442a8-634">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-634">**Tips**</span></span>

<span data-ttu-id="442a8-635">Can be handy to sample a population by putting sample-distinct in a let statement and later filter using the in operator (see example).</span><span class="sxs-lookup"><span data-stu-id="442a8-635">Can be handy to sample a population by putting sample-distinct in a let statement and later filter using the in operator (see example).</span></span>
 
<span data-ttu-id="442a8-636">If you want the top values rather than just a sample, you can use the top-hitters operator.</span><span class="sxs-lookup"><span data-stu-id="442a8-636">If you want the top values rather than just a sample, you can use the top-hitters operator.</span></span>

<span data-ttu-id="442a8-637">If you want to sample data rows (rather than values of a specific column), refer to the [sample operator](#sample-operator).</span><span class="sxs-lookup"><span data-stu-id="442a8-637">If you want to sample data rows (rather than values of a specific column), refer to the [sample operator](#sample-operator).</span></span>

<span data-ttu-id="442a8-638">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-638">**Example**</span></span>

<span data-ttu-id="442a8-639">Sample a population and do further computation knowing the summarize won't exceed query limits.</span><span class="sxs-lookup"><span data-stu-id="442a8-639">Sample a population and do further computation knowing the summarize won't exceed query limits.</span></span>

```AIQL
let sampleops = toscalar(requests | sample-distinct 10 of OperationName);
requests | where OperationName in (sampleops) | summarize total=count() by OperationName
```
### <a name="search-operator"></a><span data-ttu-id="442a8-640">search operator</span><span class="sxs-lookup"><span data-stu-id="442a8-640">search operator</span></span>

<span data-ttu-id="442a8-641">Search for strings in multiple tables and columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-641">Search for strings in multiple tables and columns.</span></span>

<span data-ttu-id="442a8-642">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-642">**Syntax**</span></span>

    search [kind=case_sensitive] [in (TableName, ...)] SearchToken

    T | search [kind=case_sensitive] SearchToken

    search [kind=case_sensitive] [in (TableName, ...)] SearchPredicate

    T | search [kind=case_sensitive] SearchPredicate

<span data-ttu-id="442a8-643">Finds occurrences of the given token string in any column of any table.</span><span class="sxs-lookup"><span data-stu-id="442a8-643">Finds occurrences of the given token string in any column of any table.</span></span>
 
* <span data-ttu-id="442a8-644">*TableName* Name of a table that is defined globally (requests, exceptions, ...) or by a [let clause](#let-clause).</span><span class="sxs-lookup"><span data-stu-id="442a8-644">*TableName* Name of a table that is defined globally (requests, exceptions, ...) or by a [let clause](#let-clause).</span></span> <span data-ttu-id="442a8-645">You can use wildcards such as r\*.</span><span class="sxs-lookup"><span data-stu-id="442a8-645">You can use wildcards such as r\*.</span></span>
* <span data-ttu-id="442a8-646">*SearchToken:* A token string, which must match a whole word.</span><span class="sxs-lookup"><span data-stu-id="442a8-646">*SearchToken:* A token string, which must match a whole word.</span></span> <span data-ttu-id="442a8-647">You can use trailing wildcards.</span><span class="sxs-lookup"><span data-stu-id="442a8-647">You can use trailing wildcards.</span></span> <span data-ttu-id="442a8-648">"Amster\*" matches "Amsterdam", but "Amster" does not.</span><span class="sxs-lookup"><span data-stu-id="442a8-648">"Amster\*" matches "Amsterdam", but "Amster" does not.</span></span>
* <span data-ttu-id="442a8-649">*SearchPredicate:* A Boolean expression over the columns in the tables.</span><span class="sxs-lookup"><span data-stu-id="442a8-649">*SearchPredicate:* A Boolean expression over the columns in the tables.</span></span> <span data-ttu-id="442a8-650">You can use "\*" as a wildcard in column names.</span><span class="sxs-lookup"><span data-stu-id="442a8-650">You can use "\*" as a wildcard in column names.</span></span>

<span data-ttu-id="442a8-651">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-651">**Examples**</span></span>

```AIQL
search "Amster*"  //All columns, all tables

search name has "home"  // one column

search * has "home"     // all columns

search in (requests, exceptions) "Amster*"  // two tables

requests | search "Amster*"

requests | search name has "home"

```




### <a name="sort-operator"></a><span data-ttu-id="442a8-652">sort operator</span><span class="sxs-lookup"><span data-stu-id="442a8-652">sort operator</span></span>
    T | sort by country asc, price desc

<span data-ttu-id="442a8-653">Sort the rows of the input table into order by one or more columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-653">Sort the rows of the input table into order by one or more columns.</span></span>

<span data-ttu-id="442a8-654">**Alias** `order`</span><span class="sxs-lookup"><span data-stu-id="442a8-654">**Alias** `order`</span></span>

<span data-ttu-id="442a8-655">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-655">**Syntax**</span></span>

    T  | sort by Column [ asc | desc ] [ , ... ]

<span data-ttu-id="442a8-656">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-656">**Arguments**</span></span>

* <span data-ttu-id="442a8-657">*T:* The table input to sort.</span><span class="sxs-lookup"><span data-stu-id="442a8-657">*T:* The table input to sort.</span></span>
* <span data-ttu-id="442a8-658">*Column:* Column of *T* by which to sort.</span><span class="sxs-lookup"><span data-stu-id="442a8-658">*Column:* Column of *T* by which to sort.</span></span> <span data-ttu-id="442a8-659">The type of the values must be numeric, date, time or string.</span><span class="sxs-lookup"><span data-stu-id="442a8-659">The type of the values must be numeric, date, time or string.</span></span>
* <span data-ttu-id="442a8-660">`asc` Sort by into ascending order, low to high.</span><span class="sxs-lookup"><span data-stu-id="442a8-660">`asc` Sort by into ascending order, low to high.</span></span> <span data-ttu-id="442a8-661">The default is `desc`, descending high to low.</span><span class="sxs-lookup"><span data-stu-id="442a8-661">The default is `desc`, descending high to low.</span></span>

<span data-ttu-id="442a8-662">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-662">**Example**</span></span>

```AIQL
Traces
| where ActivityId == "479671d99b7b"
| sort by Timestamp asc
```
<span data-ttu-id="442a8-663">All rows in table Traces that have a specific `ActivityId`, sorted by their timestamp.</span><span class="sxs-lookup"><span data-stu-id="442a8-663">All rows in table Traces that have a specific `ActivityId`, sorted by their timestamp.</span></span>

### <a name="summarize-operator"></a><span data-ttu-id="442a8-664">summarize operator</span><span class="sxs-lookup"><span data-stu-id="442a8-664">summarize operator</span></span>
<span data-ttu-id="442a8-665">Produces a table that aggregates the content of the input table.</span><span class="sxs-lookup"><span data-stu-id="442a8-665">Produces a table that aggregates the content of the input table.</span></span>

    requests
    | summarize count(), avg(duration), makeset(client_City) 
      by client_CountryOrRegion

<span data-ttu-id="442a8-666">A table that shows the number, average request duration and set of cities in each country.</span><span class="sxs-lookup"><span data-stu-id="442a8-666">A table that shows the number, average request duration and set of cities in each country.</span></span> <span data-ttu-id="442a8-667">There's a row in the output for each distinct country.</span><span class="sxs-lookup"><span data-stu-id="442a8-667">There's a row in the output for each distinct country.</span></span> <span data-ttu-id="442a8-668">The output columns show the count, average duration, cities and country.</span><span class="sxs-lookup"><span data-stu-id="442a8-668">The output columns show the count, average duration, cities and country.</span></span> <span data-ttu-id="442a8-669">All other input columns are ignored.</span><span class="sxs-lookup"><span data-stu-id="442a8-669">All other input columns are ignored.</span></span>

    T | summarize count() by price_range=bin(price, 10.0)

<span data-ttu-id="442a8-670">A table that shows how many items have prices in each interval  [0,10.0], [10.0,20.0], and so on.</span><span class="sxs-lookup"><span data-stu-id="442a8-670">A table that shows how many items have prices in each interval  [0,10.0], [10.0,20.0], and so on.</span></span> <span data-ttu-id="442a8-671">This example has a column for the count and one for the price range.</span><span class="sxs-lookup"><span data-stu-id="442a8-671">This example has a column for the count and one for the price range.</span></span> <span data-ttu-id="442a8-672">All other input columns are ignored.</span><span class="sxs-lookup"><span data-stu-id="442a8-672">All other input columns are ignored.</span></span>

<span data-ttu-id="442a8-673">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-673">**Syntax**</span></span>

    T | summarize
         [  [ Column = ] Aggregation [ , ... ] ]
         [ by
            [ Column = ] GroupExpression [ , ... ] ]

<span data-ttu-id="442a8-674">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-674">**Arguments**</span></span>

* <span data-ttu-id="442a8-675">*Column:* Optional name for a result column.</span><span class="sxs-lookup"><span data-stu-id="442a8-675">*Column:* Optional name for a result column.</span></span> <span data-ttu-id="442a8-676">Defaults to a name derived from the expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-676">Defaults to a name derived from the expression.</span></span> <span data-ttu-id="442a8-677">[Names](#names) are case-sensitive and can contain alphabetic, numeric or '_' characters.</span><span class="sxs-lookup"><span data-stu-id="442a8-677">[Names](#names) are case-sensitive and can contain alphabetic, numeric or '_' characters.</span></span> <span data-ttu-id="442a8-678">Use `['...']` or `["..."]` to quote keywords or names with other characters.</span><span class="sxs-lookup"><span data-stu-id="442a8-678">Use `['...']` or `["..."]` to quote keywords or names with other characters.</span></span>
* <span data-ttu-id="442a8-679">*Aggregation:* A call to an aggregation function such as `count()` or `avg()`, with column names as arguments.</span><span class="sxs-lookup"><span data-stu-id="442a8-679">*Aggregation:* A call to an aggregation function such as `count()` or `avg()`, with column names as arguments.</span></span> <span data-ttu-id="442a8-680">See [aggregations](#aggregations).</span><span class="sxs-lookup"><span data-stu-id="442a8-680">See [aggregations](#aggregations).</span></span>
* <span data-ttu-id="442a8-681">*GroupExpression:* An expression over the columns, that provides a set of distinct values.</span><span class="sxs-lookup"><span data-stu-id="442a8-681">*GroupExpression:* An expression over the columns, that provides a set of distinct values.</span></span> <span data-ttu-id="442a8-682">Typically it's either a column name that already provides a restricted set of values, or `bin()` with a numeric or time column as argument.</span><span class="sxs-lookup"><span data-stu-id="442a8-682">Typically it's either a column name that already provides a restricted set of values, or `bin()` with a numeric or time column as argument.</span></span> 

<span data-ttu-id="442a8-683">If you provide a numeric or time expression without using `bin()`, Analytics automatically applies it with an interval of `1h` for times, or `1.0` for numbers.</span><span class="sxs-lookup"><span data-stu-id="442a8-683">If you provide a numeric or time expression without using `bin()`, Analytics automatically applies it with an interval of `1h` for times, or `1.0` for numbers.</span></span>

<span data-ttu-id="442a8-684">If you don't provide a *GroupExpression,* the whole table is summarized in a single output row.</span><span class="sxs-lookup"><span data-stu-id="442a8-684">If you don't provide a *GroupExpression,* the whole table is summarized in a single output row.</span></span>

<span data-ttu-id="442a8-685">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-685">**Returns**</span></span>

<span data-ttu-id="442a8-686">The input rows are arranged into groups having the same values of the `by` expressions.</span><span class="sxs-lookup"><span data-stu-id="442a8-686">The input rows are arranged into groups having the same values of the `by` expressions.</span></span> <span data-ttu-id="442a8-687">Then the specified aggregation functions are computed over each group, producing a row for each group.</span><span class="sxs-lookup"><span data-stu-id="442a8-687">Then the specified aggregation functions are computed over each group, producing a row for each group.</span></span> <span data-ttu-id="442a8-688">The result contains the `by` columns and also at least one column for each computed aggregate.</span><span class="sxs-lookup"><span data-stu-id="442a8-688">The result contains the `by` columns and also at least one column for each computed aggregate.</span></span> <span data-ttu-id="442a8-689">(Some aggregation functions return multiple columns.)</span><span class="sxs-lookup"><span data-stu-id="442a8-689">(Some aggregation functions return multiple columns.)</span></span>

<span data-ttu-id="442a8-690">The result has as many rows as there are distinct combinations of `by` values.</span><span class="sxs-lookup"><span data-stu-id="442a8-690">The result has as many rows as there are distinct combinations of `by` values.</span></span> <span data-ttu-id="442a8-691">If you want to summarize over ranges of numeric values, use `bin()` to reduce ranges to discrete values.</span><span class="sxs-lookup"><span data-stu-id="442a8-691">If you want to summarize over ranges of numeric values, use `bin()` to reduce ranges to discrete values.</span></span>

> [!NOTE]
> <span data-ttu-id="442a8-692">Although you can provide arbitrary expressions for both the aggregation and grouping expressions, it's more efficient to use simple column names, or apply `bin()` to a numeric column.</span><span class="sxs-lookup"><span data-stu-id="442a8-692">Although you can provide arbitrary expressions for both the aggregation and grouping expressions, it's more efficient to use simple column names, or apply `bin()` to a numeric column.</span></span>

### <a name="table-operator"></a><span data-ttu-id="442a8-693">table operator</span><span class="sxs-lookup"><span data-stu-id="442a8-693">table operator</span></span>

    table('pageViews')

<span data-ttu-id="442a8-694">The table named in the argument string.</span><span class="sxs-lookup"><span data-stu-id="442a8-694">The table named in the argument string.</span></span>

<span data-ttu-id="442a8-695">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-695">**Syntax**</span></span>

    table(tableName)

<span data-ttu-id="442a8-696">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-696">**Arguments**</span></span>

* <span data-ttu-id="442a8-697">*tableName:* A string.</span><span class="sxs-lookup"><span data-stu-id="442a8-697">*tableName:* A string.</span></span> <span data-ttu-id="442a8-698">The name of a table, which can either be static, or the result of a let clause.</span><span class="sxs-lookup"><span data-stu-id="442a8-698">The name of a table, which can either be static, or the result of a let clause.</span></span>

<span data-ttu-id="442a8-699">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-699">**Examples**</span></span>

    table('requests');


    let size = (tableName: string) {
        table(tableName) | summarize sum(itemCount)
    };
    size('pageViews');



### <a name="take-operator"></a><span data-ttu-id="442a8-700">take operator</span><span class="sxs-lookup"><span data-stu-id="442a8-700">take operator</span></span>
<span data-ttu-id="442a8-701">Alias of [limit](#limit-operator)</span><span class="sxs-lookup"><span data-stu-id="442a8-701">Alias of [limit](#limit-operator)</span></span>

### <a name="top-operator"></a><span data-ttu-id="442a8-702">top operator</span><span class="sxs-lookup"><span data-stu-id="442a8-702">top operator</span></span>
    T | top 5 by Name desc nulls first

<span data-ttu-id="442a8-703">Returns the first *N* records sorted by the specified columns.</span><span class="sxs-lookup"><span data-stu-id="442a8-703">Returns the first *N* records sorted by the specified columns.</span></span>

<span data-ttu-id="442a8-704">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-704">**Syntax**</span></span>

    T | top NumberOfRows by Sort_expression [ asc | desc ] [nulls first|nulls last] [, ... ]

<span data-ttu-id="442a8-705">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-705">**Arguments**</span></span>

* <span data-ttu-id="442a8-706">*NumberOfRows:* The number of rows of *T* to return.</span><span class="sxs-lookup"><span data-stu-id="442a8-706">*NumberOfRows:* The number of rows of *T* to return.</span></span>
* <span data-ttu-id="442a8-707">*Sort_expression:* An expression by which to sort the rows.</span><span class="sxs-lookup"><span data-stu-id="442a8-707">*Sort_expression:* An expression by which to sort the rows.</span></span> <span data-ttu-id="442a8-708">It's typically just a column name.</span><span class="sxs-lookup"><span data-stu-id="442a8-708">It's typically just a column name.</span></span> <span data-ttu-id="442a8-709">You can specify more than one sort_expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-709">You can specify more than one sort_expression.</span></span>
* <span data-ttu-id="442a8-710">`asc` or `desc` (the default) may appear to control whether selection is actually from the "bottom" or "top" of the range.</span><span class="sxs-lookup"><span data-stu-id="442a8-710">`asc` or `desc` (the default) may appear to control whether selection is actually from the "bottom" or "top" of the range.</span></span>
* <span data-ttu-id="442a8-711">`nulls first` or `nulls last` controls where null values appear.</span><span class="sxs-lookup"><span data-stu-id="442a8-711">`nulls first` or `nulls last` controls where null values appear.</span></span> <span data-ttu-id="442a8-712">`First` is the default for `asc`, `last` is the default for `desc`.</span><span class="sxs-lookup"><span data-stu-id="442a8-712">`First` is the default for `asc`, `last` is the default for `desc`.</span></span>

<span data-ttu-id="442a8-713">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-713">**Tips**</span></span>

<span data-ttu-id="442a8-714">`top 5 by name` is superficially equivalent to `sort by name | take 5`.</span><span class="sxs-lookup"><span data-stu-id="442a8-714">`top 5 by name` is superficially equivalent to `sort by name | take 5`.</span></span> <span data-ttu-id="442a8-715">However, it runs faster and always returns sorted results, whereas `take` makes no such guarantee.</span><span class="sxs-lookup"><span data-stu-id="442a8-715">However, it runs faster and always returns sorted results, whereas `take` makes no such guarantee.</span></span>

### <a name="top-nested-operator"></a><span data-ttu-id="442a8-716">top-nested operator</span><span class="sxs-lookup"><span data-stu-id="442a8-716">top-nested operator</span></span>
    requests
    | top-nested 5 of name by count()
    , top-nested 3 of performanceBucket by count()
    , top-nested 3 of client_CountryOrRegion by count()
    | render barchart

<span data-ttu-id="442a8-717">Produces hierarchical results, where each level is a drill-down from the previous level.</span><span class="sxs-lookup"><span data-stu-id="442a8-717">Produces hierarchical results, where each level is a drill-down from the previous level.</span></span> <span data-ttu-id="442a8-718">It's useful for answering questions that sound like "What are the top 5 requests, and for each of them, what are the top 3 performance buckets, and for each of them, which are the top 3 countries the requests come from?"</span><span class="sxs-lookup"><span data-stu-id="442a8-718">It's useful for answering questions that sound like "What are the top 5 requests, and for each of them, what are the top 3 performance buckets, and for each of them, which are the top 3 countries the requests come from?"</span></span>

<span data-ttu-id="442a8-719">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-719">**Syntax**</span></span>

   <span data-ttu-id="442a8-720">T | top-nested N of COLUMN by AGGREGATION [, ...]</span><span class="sxs-lookup"><span data-stu-id="442a8-720">T | top-nested N of COLUMN by AGGREGATION [, ...]</span></span>

<span data-ttu-id="442a8-721">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-721">**Arguments**</span></span>

* <span data-ttu-id="442a8-722">N:int - number of rows to return or pass to the next level.</span><span class="sxs-lookup"><span data-stu-id="442a8-722">N:int - number of rows to return or pass to the next level.</span></span> <span data-ttu-id="442a8-723">In a query with three levels where N is 5, 3, and 3, the total number of rows will be 45.</span><span class="sxs-lookup"><span data-stu-id="442a8-723">In a query with three levels where N is 5, 3, and 3, the total number of rows will be 45.</span></span>
* <span data-ttu-id="442a8-724">COLUMN - A column to group by for aggregation.</span><span class="sxs-lookup"><span data-stu-id="442a8-724">COLUMN - A column to group by for aggregation.</span></span> 
* <span data-ttu-id="442a8-725">AGGREGATION - An [aggregation function](#aggregations) to apply to each group of rows.</span><span class="sxs-lookup"><span data-stu-id="442a8-725">AGGREGATION - An [aggregation function](#aggregations) to apply to each group of rows.</span></span> <span data-ttu-id="442a8-726">The results of these aggregations will determine the top groups to be displayed.</span><span class="sxs-lookup"><span data-stu-id="442a8-726">The results of these aggregations will determine the top groups to be displayed.</span></span>

### <a name="union-operator"></a><span data-ttu-id="442a8-727">union operator</span><span class="sxs-lookup"><span data-stu-id="442a8-727">union operator</span></span>
     Table1 | union Table2, Table3

<span data-ttu-id="442a8-728">Takes two or more tables and returns the rows of all of them.</span><span class="sxs-lookup"><span data-stu-id="442a8-728">Takes two or more tables and returns the rows of all of them.</span></span> 

<span data-ttu-id="442a8-729">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-729">**Syntax**</span></span>

    T | union [ kind= inner | outer ] [ withsource = ColumnName ] Table2 [ , ...]  

    union [ kind= inner | outer ] [ withsource = ColumnName ] Table1, Table2 [ , ...]  

<span data-ttu-id="442a8-730">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-730">**Arguments**</span></span>

* <span data-ttu-id="442a8-731">*Table1*, *Table2* ...</span><span class="sxs-lookup"><span data-stu-id="442a8-731">*Table1*, *Table2* ...</span></span>
  * <span data-ttu-id="442a8-732">The name of a table, such as `requests`, or a table defined in a [let clause](#let-clause); or</span><span class="sxs-lookup"><span data-stu-id="442a8-732">The name of a table, such as `requests`, or a table defined in a [let clause](#let-clause); or</span></span>
  * <span data-ttu-id="442a8-733">A query expression, such as `(requests | where success=="True")`</span><span class="sxs-lookup"><span data-stu-id="442a8-733">A query expression, such as `(requests | where success=="True")`</span></span>
  * <span data-ttu-id="442a8-734">A set of tables specified with a wildcard.</span><span class="sxs-lookup"><span data-stu-id="442a8-734">A set of tables specified with a wildcard.</span></span> <span data-ttu-id="442a8-735">For example, `e*` would form the union of all the tables defined in previous let clauses whose name began with 'e', together with the 'exceptions' table.</span><span class="sxs-lookup"><span data-stu-id="442a8-735">For example, `e*` would form the union of all the tables defined in previous let clauses whose name began with 'e', together with the 'exceptions' table.</span></span>
* <span data-ttu-id="442a8-736">`kind`:</span><span class="sxs-lookup"><span data-stu-id="442a8-736">`kind`:</span></span> 
  * <span data-ttu-id="442a8-737">`inner` - The result has the subset of columns that are common to all of the input tables.</span><span class="sxs-lookup"><span data-stu-id="442a8-737">`inner` - The result has the subset of columns that are common to all of the input tables.</span></span>
  * <span data-ttu-id="442a8-738">`outer` - The result has all the columns that occur in any of the inputs.</span><span class="sxs-lookup"><span data-stu-id="442a8-738">`outer` - The result has all the columns that occur in any of the inputs.</span></span> <span data-ttu-id="442a8-739">Cells that were not defined by an input row are set to `null`.</span><span class="sxs-lookup"><span data-stu-id="442a8-739">Cells that were not defined by an input row are set to `null`.</span></span>
* <span data-ttu-id="442a8-740">`withsource=`*ColumnName:* If specified, the output will include a column called *ColumnName* whose value indicates which source table has contributed each row.</span><span class="sxs-lookup"><span data-stu-id="442a8-740">`withsource=`*ColumnName:* If specified, the output will include a column called *ColumnName* whose value indicates which source table has contributed each row.</span></span> <span data-ttu-id="442a8-741">Use [as](#as-operator) at the end of each table expression, if you want to specify the name that appears in this column.</span><span class="sxs-lookup"><span data-stu-id="442a8-741">Use [as](#as-operator) at the end of each table expression, if you want to specify the name that appears in this column.</span></span>

<span data-ttu-id="442a8-742">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-742">**Returns**</span></span>

<span data-ttu-id="442a8-743">A table with as many rows as there are in all the input tables, and as many columns as there are unique column names in the inputs.</span><span class="sxs-lookup"><span data-stu-id="442a8-743">A table with as many rows as there are in all the input tables, and as many columns as there are unique column names in the inputs.</span></span>

<span data-ttu-id="442a8-744">There is no guaranteed ordering in the rows.</span><span class="sxs-lookup"><span data-stu-id="442a8-744">There is no guaranteed ordering in the rows.</span></span>


<span data-ttu-id="442a8-745">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-745">**Example**</span></span>

<span data-ttu-id="442a8-746">The number of distinct users that have produced either a `exceptions` event or a `traces` event over the past 12h.</span><span class="sxs-lookup"><span data-stu-id="442a8-746">The number of distinct users that have produced either a `exceptions` event or a `traces` event over the past 12h.</span></span> <span data-ttu-id="442a8-747">In the result, the 'SourceTable' column will indicate either "exceptions" or "traces":</span><span class="sxs-lookup"><span data-stu-id="442a8-747">In the result, the 'SourceTable' column will indicate either "exceptions" or "traces":</span></span>

```AIQL
    
    union withsource=SourceTable kind=outer exceptions, traces
    | where timestamp > ago(12h)
    | summarize dcount(user_Id) by SourceTable
```

<span data-ttu-id="442a8-748">This more efficient version produces the same result.</span><span class="sxs-lookup"><span data-stu-id="442a8-748">This more efficient version produces the same result.</span></span> <span data-ttu-id="442a8-749">It filters each table before creating the union:</span><span class="sxs-lookup"><span data-stu-id="442a8-749">It filters each table before creating the union:</span></span>

```AIQL
    exceptions
    | where timestamp > ago(24h) | as exceptions
    | union withsource=SourceTable kind=outer (requests | where timestamp > ago(12h) | as traces)
    | summarize dcount(user_Id) by SourceTable 
```

<span data-ttu-id="442a8-750">Use [as](#as-operator) to specify the name that will appear in the source column.</span><span class="sxs-lookup"><span data-stu-id="442a8-750">Use [as](#as-operator) to specify the name that will appear in the source column.</span></span>

#### <a name="forcing-an-order-of-results"></a><span data-ttu-id="442a8-751">Forcing an order of results</span><span class="sxs-lookup"><span data-stu-id="442a8-751">Forcing an order of results</span></span>

<span data-ttu-id="442a8-752">Union doesn't guarantee a specific ordering in the rows of results.</span><span class="sxs-lookup"><span data-stu-id="442a8-752">Union doesn't guarantee a specific ordering in the rows of results.</span></span>
<span data-ttu-id="442a8-753">To get the same order every time you run the query, append a tag column to each input table:</span><span class="sxs-lookup"><span data-stu-id="442a8-753">To get the same order every time you run the query, append a tag column to each input table:</span></span>

    let r1 = (traces | count | extend tag = 'r1');
    let r2 = (requests | count| extend tag = 'r2');
    let r3 = (pageViews | count | extend tag = 'r3');
    r1 | union r2,r3 | sort by tag

#### <a name="see-also"></a><span data-ttu-id="442a8-754">See also</span><span class="sxs-lookup"><span data-stu-id="442a8-754">See also</span></span>

<span data-ttu-id="442a8-755">Consider the [join operator](#join-operator) as an alternative.</span><span class="sxs-lookup"><span data-stu-id="442a8-755">Consider the [join operator](#join-operator) as an alternative.</span></span>

### <a name="where-operator"></a><span data-ttu-id="442a8-756">where operator</span><span class="sxs-lookup"><span data-stu-id="442a8-756">where operator</span></span>
     requests | where resultCode=="200"

<span data-ttu-id="442a8-757">Filters a table to the subset of rows that satisfy a predicate.</span><span class="sxs-lookup"><span data-stu-id="442a8-757">Filters a table to the subset of rows that satisfy a predicate.</span></span>

<span data-ttu-id="442a8-758">**Alias** `filter`</span><span class="sxs-lookup"><span data-stu-id="442a8-758">**Alias** `filter`</span></span>

<span data-ttu-id="442a8-759">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-759">**Syntax**</span></span>

    T | where Predicate
    T | where * has Term

<span data-ttu-id="442a8-760">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-760">**Arguments**</span></span>

* <span data-ttu-id="442a8-761">*T:* The tabular input whose records are to be filtered.</span><span class="sxs-lookup"><span data-stu-id="442a8-761">*T:* The tabular input whose records are to be filtered.</span></span>
* <span data-ttu-id="442a8-762">*Predicate:* A `boolean` [expression](#boolean) over the columns of *T*. It is evaluated for each row in *T*.</span><span class="sxs-lookup"><span data-stu-id="442a8-762">*Predicate:* A `boolean` [expression](#boolean) over the columns of *T*. It is evaluated for each row in *T*.</span></span>
* <span data-ttu-id="442a8-763">*Term* - a string that must match the whole of a word in a column.</span><span class="sxs-lookup"><span data-stu-id="442a8-763">*Term* - a string that must match the whole of a word in a column.</span></span>

<span data-ttu-id="442a8-764">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-764">**Returns**</span></span>

<span data-ttu-id="442a8-765">Rows in *T* for which *Predicate* is `true`.</span><span class="sxs-lookup"><span data-stu-id="442a8-765">Rows in *T* for which *Predicate* is `true`.</span></span>

<span data-ttu-id="442a8-766">**Tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-766">**Tips**</span></span>

<span data-ttu-id="442a8-767">To get the fastest performance:</span><span class="sxs-lookup"><span data-stu-id="442a8-767">To get the fastest performance:</span></span>

* <span data-ttu-id="442a8-768">**Use simple comparisons** between column names and constants.</span><span class="sxs-lookup"><span data-stu-id="442a8-768">**Use simple comparisons** between column names and constants.</span></span> <span data-ttu-id="442a8-769">('Constant' means constant over the table - so `now()` and `ago()` are OK, and so are scalar values assigned using a [`let` clause](#let-clause).)</span><span class="sxs-lookup"><span data-stu-id="442a8-769">('Constant' means constant over the table - so `now()` and `ago()` are OK, and so are scalar values assigned using a [`let` clause](#let-clause).)</span></span>
  
    <span data-ttu-id="442a8-770">For example, prefer `where Timestamp >= ago(1d)` to `where floor(Timestamp, 1d) == ago(1d)`.</span><span class="sxs-lookup"><span data-stu-id="442a8-770">For example, prefer `where Timestamp >= ago(1d)` to `where floor(Timestamp, 1d) == ago(1d)`.</span></span>
* <span data-ttu-id="442a8-771">**Simplest terms first**: If you have multiple clauses conjoined with `and`, put first the clauses that involve just one column.</span><span class="sxs-lookup"><span data-stu-id="442a8-771">**Simplest terms first**: If you have multiple clauses conjoined with `and`, put first the clauses that involve just one column.</span></span> <span data-ttu-id="442a8-772">So `Timestamp > ago(1d) and OpId == EventId` is better than the other way around.</span><span class="sxs-lookup"><span data-stu-id="442a8-772">So `Timestamp > ago(1d) and OpId == EventId` is better than the other way around.</span></span>

<span data-ttu-id="442a8-773">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-773">**Example**</span></span>

```AIQL
traces
| where Timestamp > ago(1h)
    and Source == "Kuskus"
    and ActivityId == SubActivityIt 
```

<span data-ttu-id="442a8-774">Records that are no older than 1 hour, and come from the Source called "Kuskus", and have two columns of the same value.</span><span class="sxs-lookup"><span data-stu-id="442a8-774">Records that are no older than 1 hour, and come from the Source called "Kuskus", and have two columns of the same value.</span></span> 

<span data-ttu-id="442a8-775">Notice that we put the comparison between two columns last, as it can't utilize the index and forces a scan.</span><span class="sxs-lookup"><span data-stu-id="442a8-775">Notice that we put the comparison between two columns last, as it can't utilize the index and forces a scan.</span></span>



## <a name="aggregations"></a><span data-ttu-id="442a8-776">Aggregations</span><span class="sxs-lookup"><span data-stu-id="442a8-776">Aggregations</span></span>
<span data-ttu-id="442a8-777">Aggregations are functions used to combine values in groups created in the [summarize operation](#summarize-operator).</span><span class="sxs-lookup"><span data-stu-id="442a8-777">Aggregations are functions used to combine values in groups created in the [summarize operation](#summarize-operator).</span></span> <span data-ttu-id="442a8-778">For example, in this query, dcount() is an aggregation function:</span><span class="sxs-lookup"><span data-stu-id="442a8-778">For example, in this query, dcount() is an aggregation function:</span></span>

    requests | summarize dcount(name) by success

### <a name="any"></a><span data-ttu-id="442a8-779">any</span><span class="sxs-lookup"><span data-stu-id="442a8-779">any</span></span>
    any(Expression)

<span data-ttu-id="442a8-780">Randomly selects one row of the group and returns the value of the specified expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-780">Randomly selects one row of the group and returns the value of the specified expression.</span></span>

<span data-ttu-id="442a8-781">This is useful, for example, when some column has a large number of similar values (e.g., an "error text" column) and you want to sample that column once per a unique value of the compound group key.</span><span class="sxs-lookup"><span data-stu-id="442a8-781">This is useful, for example, when some column has a large number of similar values (e.g., an "error text" column) and you want to sample that column once per a unique value of the compound group key.</span></span> 

<span data-ttu-id="442a8-782">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-782">**Example**</span></span>  

```

traces 
| where timestamp > now(-15min)  
| summarize count(), any(message) by operation_Name 
| top 10 by count_level desc 
```

<a name="argmin"></a>
<a name="argmax"></a>

### <a name="argmin-argmax"></a><span data-ttu-id="442a8-783">argmin, argmax</span><span class="sxs-lookup"><span data-stu-id="442a8-783">argmin, argmax</span></span>
    argmin(ExprToMinimize, * | ExprToReturn  [ , ... ] )
    argmax(ExprToMaximize, * | ExprToReturn  [ , ... ] ) 

<span data-ttu-id="442a8-784">Finds a row in the group that minimizes/maximises *ExprToMaximize*, and returns the value of *ExprToReturn* (or `*` to return the entire row).</span><span class="sxs-lookup"><span data-stu-id="442a8-784">Finds a row in the group that minimizes/maximises *ExprToMaximize*, and returns the value of *ExprToReturn* (or `*` to return the entire row).</span></span>

<span data-ttu-id="442a8-785">**Tip**: The passed-through columns are automatically renamed.</span><span class="sxs-lookup"><span data-stu-id="442a8-785">**Tip**: The passed-through columns are automatically renamed.</span></span> <span data-ttu-id="442a8-786">To make sure you're using the right names, inspect the results using `take 5` before you pipe the results into another operator.</span><span class="sxs-lookup"><span data-stu-id="442a8-786">To make sure you're using the right names, inspect the results using `take 5` before you pipe the results into another operator.</span></span>

<span data-ttu-id="442a8-787">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-787">**Examples**</span></span>

<span data-ttu-id="442a8-788">For each request name, show when the longest request occurred:</span><span class="sxs-lookup"><span data-stu-id="442a8-788">For each request name, show when the longest request occurred:</span></span>

    requests | summarize argmax(duration, timestamp) by name

<span data-ttu-id="442a8-789">Show all the details of the longest request, not just the timestamp:</span><span class="sxs-lookup"><span data-stu-id="442a8-789">Show all the details of the longest request, not just the timestamp:</span></span>

    requests | summarize argmax(duration, *) by name


<span data-ttu-id="442a8-790">Find the lowest value of each metric, together with its timestamp and other data:</span><span class="sxs-lookup"><span data-stu-id="442a8-790">Find the lowest value of each metric, together with its timestamp and other data:</span></span>

    metrics 
    | summarize minValue=argmin(value, *) 
      by name


![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/argmin.png)

### <a name="avg"></a><span data-ttu-id="442a8-791">avg</span><span class="sxs-lookup"><span data-stu-id="442a8-791">avg</span></span>
    avg(Expression)

<span data-ttu-id="442a8-792">Calculates the average of *Expression* across the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-792">Calculates the average of *Expression* across the group.</span></span>

### <a name="buildschema"></a><span data-ttu-id="442a8-793">buildschema</span><span class="sxs-lookup"><span data-stu-id="442a8-793">buildschema</span></span>
    buildschema(DynamicExpression)

<span data-ttu-id="442a8-794">Returns the minimal schema that admits all values of *DynamicExpression*.</span><span class="sxs-lookup"><span data-stu-id="442a8-794">Returns the minimal schema that admits all values of *DynamicExpression*.</span></span> 

<span data-ttu-id="442a8-795">The parameter column type should be `dynamic` - an array or property bag.</span><span class="sxs-lookup"><span data-stu-id="442a8-795">The parameter column type should be `dynamic` - an array or property bag.</span></span> 

<span data-ttu-id="442a8-796">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-796">**Example**</span></span>

    exceptions | summarize buildschema(details)

<span data-ttu-id="442a8-797">Result:</span><span class="sxs-lookup"><span data-stu-id="442a8-797">Result:</span></span>

    { "indexer":
     {"id":"string",
       "parsedStack":
       { "indexer": 
         {  "level":"int",
            "assembly":"string",
            "fileName":"string",
            "method":"string",
            "line":"int"
         }},
      "outerId":"string",
      "message":"string",
      "type":"string",
      "rawStack":"string"
    }}

<span data-ttu-id="442a8-798">Notice that `indexer` is used to mark where you should use a numeric index.</span><span class="sxs-lookup"><span data-stu-id="442a8-798">Notice that `indexer` is used to mark where you should use a numeric index.</span></span> <span data-ttu-id="442a8-799">For this schema, some valid paths would be (assuming these example indexes are in range):</span><span class="sxs-lookup"><span data-stu-id="442a8-799">For this schema, some valid paths would be (assuming these example indexes are in range):</span></span>

    details[0].parsedStack[2].level
    details[0].message
    arraylength(details)
    arraylength(details[0].parsedStack)

<span data-ttu-id="442a8-800">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-800">**Example**</span></span>

<span data-ttu-id="442a8-801">Assume the input column has three dynamic values:</span><span class="sxs-lookup"><span data-stu-id="442a8-801">Assume the input column has three dynamic values:</span></span>

|  |
| --- |
| `{"x":1, "y":3.5}` |
| `{"x":"somevalue", "z":[1, 2, 3]}` |
| `{"y":{"w":"zzz"}, "t":["aa", "bb"], "z":["foo"]}` |

<span data-ttu-id="442a8-802">The resulting schema would be:</span><span class="sxs-lookup"><span data-stu-id="442a8-802">The resulting schema would be:</span></span>

    {
      "x":["int", "string"],
      "y":["double", {"w": "string"}],
      "z":{"indexer": ["int", "string"]},
      "t":{"indexer": "string"}
    }

<span data-ttu-id="442a8-803">The schema tells us that:</span><span class="sxs-lookup"><span data-stu-id="442a8-803">The schema tells us that:</span></span>

* <span data-ttu-id="442a8-804">The root object is a container with four properties named x, y, z and t.</span><span class="sxs-lookup"><span data-stu-id="442a8-804">The root object is a container with four properties named x, y, z and t.</span></span>
* <span data-ttu-id="442a8-805">The property called "x" that could be either of type "int" or of type "string".</span><span class="sxs-lookup"><span data-stu-id="442a8-805">The property called "x" that could be either of type "int" or of type "string".</span></span>
* <span data-ttu-id="442a8-806">The property called "y" that could of either of type "double", or another container with a property called "w" of type "string".</span><span class="sxs-lookup"><span data-stu-id="442a8-806">The property called "y" that could of either of type "double", or another container with a property called "w" of type "string".</span></span>
* <span data-ttu-id="442a8-807">The ``indexer`` keyword indicates that "z" and "t" are arrays.</span><span class="sxs-lookup"><span data-stu-id="442a8-807">The ``indexer`` keyword indicates that "z" and "t" are arrays.</span></span>
* <span data-ttu-id="442a8-808">Each item in the array "z" is either an int or a string.</span><span class="sxs-lookup"><span data-stu-id="442a8-808">Each item in the array "z" is either an int or a string.</span></span>
* <span data-ttu-id="442a8-809">"t" is an array of strings.</span><span class="sxs-lookup"><span data-stu-id="442a8-809">"t" is an array of strings.</span></span>
* <span data-ttu-id="442a8-810">Every property is implicitly optional, and any array may be empty.</span><span class="sxs-lookup"><span data-stu-id="442a8-810">Every property is implicitly optional, and any array may be empty.</span></span>

##### <a name="schema-model"></a><span data-ttu-id="442a8-811">Schema model</span><span class="sxs-lookup"><span data-stu-id="442a8-811">Schema model</span></span>
<span data-ttu-id="442a8-812">The syntax of the returned schema is:</span><span class="sxs-lookup"><span data-stu-id="442a8-812">The syntax of the returned schema is:</span></span>

    Container ::= '{' Named-type* '}';
    Named-type ::= (name | '"indexer"') ':' Type;
    Type ::= Primitive-type | Union-type | Container;
    Union-type ::= '[' Type* ']';
    Primitive-type ::= "int" | "string" | ...;

<span data-ttu-id="442a8-813">They are equivalent to a subset of the TypeScript type annotations, encoded as a dynamic value.</span><span class="sxs-lookup"><span data-stu-id="442a8-813">They are equivalent to a subset of the TypeScript type annotations, encoded as a dynamic value.</span></span> <span data-ttu-id="442a8-814">In Typescript, the example schema would be:</span><span class="sxs-lookup"><span data-stu-id="442a8-814">In Typescript, the example schema would be:</span></span>

    var someobject:
    {
      x?: (number | string),
      y?: (number | { w?: string}),
      z?: { [n:number] : (int | string)},
      t?: { [n:number]: string }
    }


### <a name="count"></a><span data-ttu-id="442a8-815">count</span><span class="sxs-lookup"><span data-stu-id="442a8-815">count</span></span>
    count([ Predicate ])

<span data-ttu-id="442a8-816">Returns a count of rows for which *Predicate* evaluates to `true`.</span><span class="sxs-lookup"><span data-stu-id="442a8-816">Returns a count of rows for which *Predicate* evaluates to `true`.</span></span> <span data-ttu-id="442a8-817">If no *Predicate* is specified, returns the total number of records in the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-817">If no *Predicate* is specified, returns the total number of records in the group.</span></span> 

<span data-ttu-id="442a8-818">**Perf tip**: use `summarize count(filter)` instead of `where filter | summarize count()`</span><span class="sxs-lookup"><span data-stu-id="442a8-818">**Perf tip**: use `summarize count(filter)` instead of `where filter | summarize count()`</span></span>

> [!NOTE]
> <span data-ttu-id="442a8-819">Avoid using count() to find the number of requests, exceptions or other events that have occurred.</span><span class="sxs-lookup"><span data-stu-id="442a8-819">Avoid using count() to find the number of requests, exceptions or other events that have occurred.</span></span> <span data-ttu-id="442a8-820">When [sampling](app-insights-sampling.md) is in operation, the number of data points retained in Application Insights will be less than the number of original events.</span><span class="sxs-lookup"><span data-stu-id="442a8-820">When [sampling](app-insights-sampling.md) is in operation, the number of data points retained in Application Insights will be less than the number of original events.</span></span> <span data-ttu-id="442a8-821">Instead, use `summarize sum(itemCount)...`.</span><span class="sxs-lookup"><span data-stu-id="442a8-821">Instead, use `summarize sum(itemCount)...`.</span></span> <span data-ttu-id="442a8-822">The itemCount property reflects the number of original events that are represented by each retained data point.</span><span class="sxs-lookup"><span data-stu-id="442a8-822">The itemCount property reflects the number of original events that are represented by each retained data point.</span></span>
> 
> 

### <a name="countif"></a><span data-ttu-id="442a8-823">countif</span><span class="sxs-lookup"><span data-stu-id="442a8-823">countif</span></span>
    countif(Predicate)

<span data-ttu-id="442a8-824">Returns a count of rows for which *Predicate* evaluates to `true`.</span><span class="sxs-lookup"><span data-stu-id="442a8-824">Returns a count of rows for which *Predicate* evaluates to `true`.</span></span>

<span data-ttu-id="442a8-825">**Perf tip**: use `summarize countif(filter)` instead of `where filter | summarize count()`</span><span class="sxs-lookup"><span data-stu-id="442a8-825">**Perf tip**: use `summarize countif(filter)` instead of `where filter | summarize count()`</span></span>

> [!NOTE]
> <span data-ttu-id="442a8-826">Avoid using countif() to find the number of requests, exceptions or other events that have occurred.</span><span class="sxs-lookup"><span data-stu-id="442a8-826">Avoid using countif() to find the number of requests, exceptions or other events that have occurred.</span></span> <span data-ttu-id="442a8-827">When [sampling](app-insights-sampling.md) is in operation, the number of data points will be less than the number of actual events.</span><span class="sxs-lookup"><span data-stu-id="442a8-827">When [sampling](app-insights-sampling.md) is in operation, the number of data points will be less than the number of actual events.</span></span> <span data-ttu-id="442a8-828">Instead, use `summarize sum(itemCount)...`.</span><span class="sxs-lookup"><span data-stu-id="442a8-828">Instead, use `summarize sum(itemCount)...`.</span></span> <span data-ttu-id="442a8-829">The itemCount property reflects the number of original events that are represented by each retained data point.</span><span class="sxs-lookup"><span data-stu-id="442a8-829">The itemCount property reflects the number of original events that are represented by each retained data point.</span></span>
> 
> 

### <a name="dcount"></a><span data-ttu-id="442a8-830">dcount</span><span class="sxs-lookup"><span data-stu-id="442a8-830">dcount</span></span>
    dcount( Expression [ ,  Accuracy ])

<span data-ttu-id="442a8-831">Returns an estimate of the number of distinct values of *Expr* in the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-831">Returns an estimate of the number of distinct values of *Expr* in the group.</span></span> <span data-ttu-id="442a8-832">(To list the distinct values, use [`makeset`](#makeset).)</span><span class="sxs-lookup"><span data-stu-id="442a8-832">(To list the distinct values, use [`makeset`](#makeset).)</span></span>

<span data-ttu-id="442a8-833">*Accuracy*, if specified, controls the balance between speed and accuracy.</span><span class="sxs-lookup"><span data-stu-id="442a8-833">*Accuracy*, if specified, controls the balance between speed and accuracy.</span></span>

* <span data-ttu-id="442a8-834">`0` = the least accurate and fastest calculation.</span><span class="sxs-lookup"><span data-stu-id="442a8-834">`0` = the least accurate and fastest calculation.</span></span>
* <span data-ttu-id="442a8-835">`1` the default, which balances accuracy and calculation time; about 0.8% error.</span><span class="sxs-lookup"><span data-stu-id="442a8-835">`1` the default, which balances accuracy and calculation time; about 0.8% error.</span></span>
* <span data-ttu-id="442a8-836">`2` = most accurate and slowest calculation; about 0.4% error.</span><span class="sxs-lookup"><span data-stu-id="442a8-836">`2` = most accurate and slowest calculation; about 0.4% error.</span></span>

<span data-ttu-id="442a8-837">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-837">**Example**</span></span>

    pageViews 
    | summarize cities=dcount(client_City) 
      by client_CountryOrRegion

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/dcount.png)

### <a name="dcountif"></a><span data-ttu-id="442a8-838">dcountif</span><span class="sxs-lookup"><span data-stu-id="442a8-838">dcountif</span></span>
    dcountif( Expression, Predicate [ ,  Accuracy ])

<span data-ttu-id="442a8-839">Returns an estimate of the number of distinct values of *Expr* of rows in the group for which *Predicate* is true.</span><span class="sxs-lookup"><span data-stu-id="442a8-839">Returns an estimate of the number of distinct values of *Expr* of rows in the group for which *Predicate* is true.</span></span> <span data-ttu-id="442a8-840">(To list the distinct values, use [`makeset`](#makeset).)</span><span class="sxs-lookup"><span data-stu-id="442a8-840">(To list the distinct values, use [`makeset`](#makeset).)</span></span>

<span data-ttu-id="442a8-841">*Accuracy*, if specified, controls the balance between speed and accuracy.</span><span class="sxs-lookup"><span data-stu-id="442a8-841">*Accuracy*, if specified, controls the balance between speed and accuracy.</span></span>

* <span data-ttu-id="442a8-842">`0` = the least accurate and fastest calculation.</span><span class="sxs-lookup"><span data-stu-id="442a8-842">`0` = the least accurate and fastest calculation.</span></span>
* <span data-ttu-id="442a8-843">`1` the default, which balances accuracy and calculation time; about 0.8% error.</span><span class="sxs-lookup"><span data-stu-id="442a8-843">`1` the default, which balances accuracy and calculation time; about 0.8% error.</span></span>
* <span data-ttu-id="442a8-844">`2` = most accurate and slowest calculation; about 0.4% error.</span><span class="sxs-lookup"><span data-stu-id="442a8-844">`2` = most accurate and slowest calculation; about 0.4% error.</span></span>

<span data-ttu-id="442a8-845">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-845">**Example**</span></span>

    pageViews 
    | summarize cities=dcountif(client_City, client_City startswith "St") 
      by client_CountryOrRegion


### <a name="makelist"></a><span data-ttu-id="442a8-846">makelist</span><span class="sxs-lookup"><span data-stu-id="442a8-846">makelist</span></span>
    makelist(Expr [ ,  MaxListSize ] )

<span data-ttu-id="442a8-847">Returns a `dynamic` (JSON) array of all the values of *Expr* in the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-847">Returns a `dynamic` (JSON) array of all the values of *Expr* in the group.</span></span> 

* <span data-ttu-id="442a8-848">*MaxListSize* is an optional integer limit on the maximum number of elements returned (default is *128*).</span><span class="sxs-lookup"><span data-stu-id="442a8-848">*MaxListSize* is an optional integer limit on the maximum number of elements returned (default is *128*).</span></span>

### <a name="makeset"></a><span data-ttu-id="442a8-849">makeset</span><span class="sxs-lookup"><span data-stu-id="442a8-849">makeset</span></span>
    makeset(Expression [ , MaxSetSize ] )

<span data-ttu-id="442a8-850">Returns a `dynamic` (JSON) array of the set of distinct values that *Expr* takes in the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-850">Returns a `dynamic` (JSON) array of the set of distinct values that *Expr* takes in the group.</span></span> <span data-ttu-id="442a8-851">(Tip: to just count the distinct values, use [`dcount`](#dcount).)</span><span class="sxs-lookup"><span data-stu-id="442a8-851">(Tip: to just count the distinct values, use [`dcount`](#dcount).)</span></span>

* <span data-ttu-id="442a8-852">*MaxSetSize* is an optional integer limit on the maximum number of elements returned (default is *128*).</span><span class="sxs-lookup"><span data-stu-id="442a8-852">*MaxSetSize* is an optional integer limit on the maximum number of elements returned (default is *128*).</span></span>

<span data-ttu-id="442a8-853">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-853">**Example**</span></span>

    pageViews 
    | summarize cities=makeset(client_City) 
      by client_CountryOrRegion

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/makeset.png)

<span data-ttu-id="442a8-854">See also the [`mvexpand` operator](#mvexpand-operator) for the opposite function.</span><span class="sxs-lookup"><span data-stu-id="442a8-854">See also the [`mvexpand` operator](#mvexpand-operator) for the opposite function.</span></span>

### <a name="max-min"></a><span data-ttu-id="442a8-855">max, min</span><span class="sxs-lookup"><span data-stu-id="442a8-855">max, min</span></span>
    max(Expr)

<span data-ttu-id="442a8-856">Calculates the maximum of *Expr*.</span><span class="sxs-lookup"><span data-stu-id="442a8-856">Calculates the maximum of *Expr*.</span></span>

    min(Expr)

<span data-ttu-id="442a8-857">Calculates the minimum of *Expr*.</span><span class="sxs-lookup"><span data-stu-id="442a8-857">Calculates the minimum of *Expr*.</span></span>

<span data-ttu-id="442a8-858">**Tip**: This gives you the min or max on its own - for example, the highest or lowest price.</span><span class="sxs-lookup"><span data-stu-id="442a8-858">**Tip**: This gives you the min or max on its own - for example, the highest or lowest price.</span></span> <span data-ttu-id="442a8-859">But if you want other columns in the row - for example, the name of the supplier with the lowest price - use [argmin or argmax](#argmin-argmax).</span><span class="sxs-lookup"><span data-stu-id="442a8-859">But if you want other columns in the row - for example, the name of the supplier with the lowest price - use [argmin or argmax](#argmin-argmax).</span></span>

<a name="percentile"></a>
<a name="percentiles"></a>
<a name="percentilew"></a>
<a name="percentilesw"></a>

### <a name="percentile-percentiles-percentilew-percentilesw"></a><span data-ttu-id="442a8-860">percentile, percentiles, percentilew, percentilesw</span><span class="sxs-lookup"><span data-stu-id="442a8-860">percentile, percentiles, percentilew, percentilesw</span></span>
    percentile(Expression, Percentile)

<span data-ttu-id="442a8-861">Returns an estimate for *Expression* of the specified percentile in the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-861">Returns an estimate for *Expression* of the specified percentile in the group.</span></span> <span data-ttu-id="442a8-862">The accuracy depends on the density of population in the region of the percentile.</span><span class="sxs-lookup"><span data-stu-id="442a8-862">The accuracy depends on the density of population in the region of the percentile.</span></span>

    percentiles(Expression, Percentile1 [ , Percentile2 ...] )

<span data-ttu-id="442a8-863">Like `percentile()`, but calculates a number of percentile values (which is faster than calculating each percentile individually).</span><span class="sxs-lookup"><span data-stu-id="442a8-863">Like `percentile()`, but calculates a number of percentile values (which is faster than calculating each percentile individually).</span></span>

    percentilew(Expression, WeightExpression, Percentile)

<span data-ttu-id="442a8-864">Weighted percentile.</span><span class="sxs-lookup"><span data-stu-id="442a8-864">Weighted percentile.</span></span> <span data-ttu-id="442a8-865">Use this for pre-aggregated data.</span><span class="sxs-lookup"><span data-stu-id="442a8-865">Use this for pre-aggregated data.</span></span>  <span data-ttu-id="442a8-866">`WeightExpression` is an integer that indicates how many original rows are represented by each aggregated row.</span><span class="sxs-lookup"><span data-stu-id="442a8-866">`WeightExpression` is an integer that indicates how many original rows are represented by each aggregated row.</span></span>

    percentilesw(Expression, WeightExpression, Percentile1, [, Percentile2 ...])

<span data-ttu-id="442a8-867">Like `percentilew()`, but calculates a number of percentile values.</span><span class="sxs-lookup"><span data-stu-id="442a8-867">Like `percentilew()`, but calculates a number of percentile values.</span></span>

<span data-ttu-id="442a8-868">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-868">**Examples**</span></span>

<span data-ttu-id="442a8-869">The value of `duration` that is larger than 95% of the sample set and smaller than 5% of the sample set, calculated for each request name:</span><span class="sxs-lookup"><span data-stu-id="442a8-869">The value of `duration` that is larger than 95% of the sample set and smaller than 5% of the sample set, calculated for each request name:</span></span>

    request 
    | summarize percentile(duration, 95)
      by name

<span data-ttu-id="442a8-870">Omit "by..." to calculate for the whole table.</span><span class="sxs-lookup"><span data-stu-id="442a8-870">Omit "by..." to calculate for the whole table.</span></span>

<span data-ttu-id="442a8-871">Simultaneously calculate several percentiles for different request names:</span><span class="sxs-lookup"><span data-stu-id="442a8-871">Simultaneously calculate several percentiles for different request names:</span></span>

    requests 
    | summarize 
        percentiles(duration, 5, 20, 50, 80, 95) 
      by name

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/percentiles.png)

<span data-ttu-id="442a8-872">The results show that for the request /Events/Index, 5% of requests are responded to in less than 2.44s,  half of them in 3.52s, and 5% are slower than 6.85s.</span><span class="sxs-lookup"><span data-stu-id="442a8-872">The results show that for the request /Events/Index, 5% of requests are responded to in less than 2.44s,  half of them in 3.52s, and 5% are slower than 6.85s.</span></span>

<span data-ttu-id="442a8-873">Calculate multiple statistics:</span><span class="sxs-lookup"><span data-stu-id="442a8-873">Calculate multiple statistics:</span></span>

    requests 
    | summarize 
        count(), 
        avg(Duration),
        percentiles(Duration, 5, 50, 95)
      by name

#### <a name="weighted-percentiles"></a><span data-ttu-id="442a8-874">Weighted percentiles</span><span class="sxs-lookup"><span data-stu-id="442a8-874">Weighted percentiles</span></span>
<span data-ttu-id="442a8-875">Use the weighted percentile functions in cases where the data has been pre-aggregated.</span><span class="sxs-lookup"><span data-stu-id="442a8-875">Use the weighted percentile functions in cases where the data has been pre-aggregated.</span></span> 

<span data-ttu-id="442a8-876">For example, suppose your app performs many thousands of operations per second, and you want to know their latency.</span><span class="sxs-lookup"><span data-stu-id="442a8-876">For example, suppose your app performs many thousands of operations per second, and you want to know their latency.</span></span> <span data-ttu-id="442a8-877">The simple solution would be to generate an Application Insights request or custom event for each operation.</span><span class="sxs-lookup"><span data-stu-id="442a8-877">The simple solution would be to generate an Application Insights request or custom event for each operation.</span></span> <span data-ttu-id="442a8-878">This would create a lot of traffic, although adaptive sampling would take effect to reduce it.</span><span class="sxs-lookup"><span data-stu-id="442a8-878">This would create a lot of traffic, although adaptive sampling would take effect to reduce it.</span></span> <span data-ttu-id="442a8-879">But you decide to implement an even better solution: you will write some code in your app to aggregate the data before sending it to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="442a8-879">But you decide to implement an even better solution: you will write some code in your app to aggregate the data before sending it to Application Insights.</span></span> <span data-ttu-id="442a8-880">The aggregated summary will be sent at regular intervals, reducing the data rate perhaps to a few points per minute.</span><span class="sxs-lookup"><span data-stu-id="442a8-880">The aggregated summary will be sent at regular intervals, reducing the data rate perhaps to a few points per minute.</span></span>

<span data-ttu-id="442a8-881">Your code takes a stream of latency measurements in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="442a8-881">Your code takes a stream of latency measurements in milliseconds.</span></span> <span data-ttu-id="442a8-882">For example:</span><span class="sxs-lookup"><span data-stu-id="442a8-882">For example:</span></span>

     { 15, 12, 2, 21, 2, 5, 35, 7, 12, 22, 1, 15, 18, 12, 26, 7 }

<span data-ttu-id="442a8-883">It counts the measurements in the following bins: `{ 10, 20, 30, 40, 50, 100 }`</span><span class="sxs-lookup"><span data-stu-id="442a8-883">It counts the measurements in the following bins: `{ 10, 20, 30, 40, 50, 100 }`</span></span>

<span data-ttu-id="442a8-884">Periodically, it makes a series of TrackEvent calls, one for each bucket, with custom measurements in each call:</span><span class="sxs-lookup"><span data-stu-id="442a8-884">Periodically, it makes a series of TrackEvent calls, one for each bucket, with custom measurements in each call:</span></span> 

    foreach (var latency in bins.Keys)
    { telemetry.TrackEvent("latency", null, 
         new Dictionary<string, double>
         ({"latency", latency}, {"opCount", bins[latency]}}); }

<span data-ttu-id="442a8-885">In Analytics, you see one such group of events like this:</span><span class="sxs-lookup"><span data-stu-id="442a8-885">In Analytics, you see one such group of events like this:</span></span>

| `opCount` | `latency` | <span data-ttu-id="442a8-886">meaning</span><span class="sxs-lookup"><span data-stu-id="442a8-886">meaning</span></span> |
| --- | --- | --- |
| <span data-ttu-id="442a8-887">8</span><span class="sxs-lookup"><span data-stu-id="442a8-887">8</span></span> |<span data-ttu-id="442a8-888">10</span><span class="sxs-lookup"><span data-stu-id="442a8-888">10</span></span> |<span data-ttu-id="442a8-889">= 8 operations in the 10ms bin</span><span class="sxs-lookup"><span data-stu-id="442a8-889">= 8 operations in the 10ms bin</span></span> |
| <span data-ttu-id="442a8-890">6</span><span class="sxs-lookup"><span data-stu-id="442a8-890">6</span></span> |<span data-ttu-id="442a8-891">20</span><span class="sxs-lookup"><span data-stu-id="442a8-891">20</span></span> |<span data-ttu-id="442a8-892">= 6 operations in the 20ms bin</span><span class="sxs-lookup"><span data-stu-id="442a8-892">= 6 operations in the 20ms bin</span></span> |
| <span data-ttu-id="442a8-893">3</span><span class="sxs-lookup"><span data-stu-id="442a8-893">3</span></span> |<span data-ttu-id="442a8-894">30</span><span class="sxs-lookup"><span data-stu-id="442a8-894">30</span></span> |<span data-ttu-id="442a8-895">= 3 operations in the 30ms bin</span><span class="sxs-lookup"><span data-stu-id="442a8-895">= 3 operations in the 30ms bin</span></span> |
| <span data-ttu-id="442a8-896">1</span><span class="sxs-lookup"><span data-stu-id="442a8-896">1</span></span> |<span data-ttu-id="442a8-897">40</span><span class="sxs-lookup"><span data-stu-id="442a8-897">40</span></span> |<span data-ttu-id="442a8-898">= 1 operations in the 40ms bin</span><span class="sxs-lookup"><span data-stu-id="442a8-898">= 1 operations in the 40ms bin</span></span> |

<span data-ttu-id="442a8-899">To get an accurate picture of the original distribution of event latencies, we use `percentilesw`:</span><span class="sxs-lookup"><span data-stu-id="442a8-899">To get an accurate picture of the original distribution of event latencies, we use `percentilesw`:</span></span>

    customEvents | summarize percentilesw(latency, opCount, 20, 50, 80)

<span data-ttu-id="442a8-900">The results are the same as if we had used plain `percentiles` on the original set of measurements.</span><span class="sxs-lookup"><span data-stu-id="442a8-900">The results are the same as if we had used plain `percentiles` on the original set of measurements.</span></span>

> [!NOTE]
> <span data-ttu-id="442a8-901">Weighted percentiles are not applicable to [sampled data](app-insights-sampling.md), where each sampled row represents a random sample of original rows, rather than a bin.</span><span class="sxs-lookup"><span data-stu-id="442a8-901">Weighted percentiles are not applicable to [sampled data](app-insights-sampling.md), where each sampled row represents a random sample of original rows, rather than a bin.</span></span> <span data-ttu-id="442a8-902">The plain percentile functions are appropriate for sampled data.</span><span class="sxs-lookup"><span data-stu-id="442a8-902">The plain percentile functions are appropriate for sampled data.</span></span>
> 
> 

#### <a name="estimation-error-in-percentiles"></a><span data-ttu-id="442a8-903">Estimation error in percentiles</span><span class="sxs-lookup"><span data-stu-id="442a8-903">Estimation error in percentiles</span></span>
<span data-ttu-id="442a8-904">The percentiles aggregate provides an approximate value using [T-Digest](https://github.com/tdunning/t-digest/blob/master/docs/t-digest-paper/histo.pdf).</span><span class="sxs-lookup"><span data-stu-id="442a8-904">The percentiles aggregate provides an approximate value using [T-Digest](https://github.com/tdunning/t-digest/blob/master/docs/t-digest-paper/histo.pdf).</span></span> 

<span data-ttu-id="442a8-905">A few important points:</span><span class="sxs-lookup"><span data-stu-id="442a8-905">A few important points:</span></span> 

* <span data-ttu-id="442a8-906">The bounds on the estimation error vary with the value of the requested percentile.</span><span class="sxs-lookup"><span data-stu-id="442a8-906">The bounds on the estimation error vary with the value of the requested percentile.</span></span> <span data-ttu-id="442a8-907">The best accuracy is at the ends of [0..100] scale, percentiles 0 and 100 are the exact minimum and maximum values of the distribution.</span><span class="sxs-lookup"><span data-stu-id="442a8-907">The best accuracy is at the ends of [0..100] scale, percentiles 0 and 100 are the exact minimum and maximum values of the distribution.</span></span> <span data-ttu-id="442a8-908">The accuracy gradually decreases towards the middle of the scale.</span><span class="sxs-lookup"><span data-stu-id="442a8-908">The accuracy gradually decreases towards the middle of the scale.</span></span> <span data-ttu-id="442a8-909">It is worst at the median and is capped at 1%.</span><span class="sxs-lookup"><span data-stu-id="442a8-909">It is worst at the median and is capped at 1%.</span></span> 
* <span data-ttu-id="442a8-910">Error bounds are observed on the rank, not on the value.</span><span class="sxs-lookup"><span data-stu-id="442a8-910">Error bounds are observed on the rank, not on the value.</span></span> <span data-ttu-id="442a8-911">Suppose percentile(X, 50) returned value of Xm.</span><span class="sxs-lookup"><span data-stu-id="442a8-911">Suppose percentile(X, 50) returned value of Xm.</span></span> <span data-ttu-id="442a8-912">The estimation guarantees that at least 49% and at most 51% of the values of X are less than Xm.</span><span class="sxs-lookup"><span data-stu-id="442a8-912">The estimation guarantees that at least 49% and at most 51% of the values of X are less than Xm.</span></span> <span data-ttu-id="442a8-913">There is no theoretical limit on the difference  between Xm and actual median value of X.</span><span class="sxs-lookup"><span data-stu-id="442a8-913">There is no theoretical limit on the difference  between Xm and actual median value of X.</span></span>

### <a name="stdev"></a><span data-ttu-id="442a8-914">stdev</span><span class="sxs-lookup"><span data-stu-id="442a8-914">stdev</span></span>
     stdev(Expr)

<span data-ttu-id="442a8-915">Returns the standard deviation of *Expr* over the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-915">Returns the standard deviation of *Expr* over the group.</span></span>

### <a name="variance"></a><span data-ttu-id="442a8-916">variance</span><span class="sxs-lookup"><span data-stu-id="442a8-916">variance</span></span>
    variance(Expr)

<span data-ttu-id="442a8-917">Returns the variance of *Expr* over the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-917">Returns the variance of *Expr* over the group.</span></span>

### <a name="sum"></a><span data-ttu-id="442a8-918">sum</span><span class="sxs-lookup"><span data-stu-id="442a8-918">sum</span></span>
    sum(Expr)

<span data-ttu-id="442a8-919">Returns the sum of *Expr* over the group.</span><span class="sxs-lookup"><span data-stu-id="442a8-919">Returns the sum of *Expr* over the group.</span></span>                      

## <a name="scalars"></a><span data-ttu-id="442a8-920">Scalars</span><span class="sxs-lookup"><span data-stu-id="442a8-920">Scalars</span></span>
<span data-ttu-id="442a8-921">[casts](#casts) | [comparisons](#scalar-comparisons)</span><span class="sxs-lookup"><span data-stu-id="442a8-921">[casts](#casts) | [comparisons](#scalar-comparisons)</span></span>
<br/>
<span data-ttu-id="442a8-922">[gettype](#gettype) | [hash](#hash) | [iff](#iff) |  [isnull](#isnull) | [isnotnull](#isnotnull) | [notnull](#notnull) | [toscalar](#toscalar)</span><span class="sxs-lookup"><span data-stu-id="442a8-922">[gettype](#gettype) | [hash](#hash) | [iff](#iff) |  [isnull](#isnull) | [isnotnull](#isnotnull) | [notnull](#notnull) | [toscalar](#toscalar)</span></span>

<span data-ttu-id="442a8-923">The supported types are:</span><span class="sxs-lookup"><span data-stu-id="442a8-923">The supported types are:</span></span>

| <span data-ttu-id="442a8-924">Type</span><span class="sxs-lookup"><span data-stu-id="442a8-924">Type</span></span> | <span data-ttu-id="442a8-925">Additional name(s)</span><span class="sxs-lookup"><span data-stu-id="442a8-925">Additional name(s)</span></span> | <span data-ttu-id="442a8-926">Equivalent .NET type</span><span class="sxs-lookup"><span data-stu-id="442a8-926">Equivalent .NET type</span></span> |
| --- | --- | --- |
| `bool` |`boolean` |`System.Boolean` |
| `datetime` |`date` |`System.DateTime` |
| `dynamic` | |`System.Object` |
| `guid` |<span data-ttu-id="442a8-927">`uuid`, `uniqueid`</span><span class="sxs-lookup"><span data-stu-id="442a8-927">`uuid`, `uniqueid`</span></span> |`System.Guid` |
| `int` | |`System.Int32` |
| `long` | |`System.Int64` |
| `double` |`real` |`System.Double` |
| `string` | |`System.String` |
| `timespan` |`time` |`System.TimeSpan` |

### <a name="casts"></a><span data-ttu-id="442a8-928">Casts</span><span class="sxs-lookup"><span data-stu-id="442a8-928">Casts</span></span>
<span data-ttu-id="442a8-929">You can cast from one type to another.</span><span class="sxs-lookup"><span data-stu-id="442a8-929">You can cast from one type to another.</span></span> <span data-ttu-id="442a8-930">In general, if the conversion makes sense, it will work:</span><span class="sxs-lookup"><span data-stu-id="442a8-930">In general, if the conversion makes sense, it will work:</span></span>

    todouble(10), todouble("10.6")
    toint(10.6) == 11
    floor(10.6) == 10
    toint("200")
    todatetime("2016-04-28 13:02")
    totimespan("1.5d"), totimespan("1.12:00:00")
    toguid("00000000-0000-0000-0000-000000000000")
    tostring(42.5)
    todynamic("{a:10, b:20}")

<span data-ttu-id="442a8-931">Check whether a string can be converted to a specific type:</span><span class="sxs-lookup"><span data-stu-id="442a8-931">Check whether a string can be converted to a specific type:</span></span>

    iff(notnull(todouble(customDimensions.myValue)),
       ..., ...)







### <a name="scalar-comparisons"></a><span data-ttu-id="442a8-932">Scalar comparisons</span><span class="sxs-lookup"><span data-stu-id="442a8-932">Scalar comparisons</span></span>
|  |  |
| --- | --- |
| `<` |<span data-ttu-id="442a8-933">Less</span><span class="sxs-lookup"><span data-stu-id="442a8-933">Less</span></span> |
| `<=` |<span data-ttu-id="442a8-934">Less or Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-934">Less or Equals</span></span> |
| `>` |<span data-ttu-id="442a8-935">Greater</span><span class="sxs-lookup"><span data-stu-id="442a8-935">Greater</span></span> |
| `>=` |<span data-ttu-id="442a8-936">Greater or Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-936">Greater or Equals</span></span> |
| `<>` |<span data-ttu-id="442a8-937">Not Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-937">Not Equals</span></span> |
| `!=` |<span data-ttu-id="442a8-938">Not Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-938">Not Equals</span></span> |
| `in` |<span data-ttu-id="442a8-939">Right operand is a (dynamic) array and left operand is equal to one of its elements.</span><span class="sxs-lookup"><span data-stu-id="442a8-939">Right operand is a (dynamic) array and left operand is equal to one of its elements.</span></span> |
| `!in` |<span data-ttu-id="442a8-940">Right operand is a (dynamic) array and left operand is not equal to any of its elements.</span><span class="sxs-lookup"><span data-stu-id="442a8-940">Right operand is a (dynamic) array and left operand is not equal to any of its elements.</span></span> |

### <a name="gettype"></a><span data-ttu-id="442a8-941">gettype</span><span class="sxs-lookup"><span data-stu-id="442a8-941">gettype</span></span>
<span data-ttu-id="442a8-942">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-942">**Returns**</span></span>

<span data-ttu-id="442a8-943">A string representing the underlying storage type of its single argument.</span><span class="sxs-lookup"><span data-stu-id="442a8-943">A string representing the underlying storage type of its single argument.</span></span> <span data-ttu-id="442a8-944">This is particularly useful when you have values of kind `dynamic`: in this case `gettype()` will reveal how a value is encoded.</span><span class="sxs-lookup"><span data-stu-id="442a8-944">This is particularly useful when you have values of kind `dynamic`: in this case `gettype()` will reveal how a value is encoded.</span></span>

<span data-ttu-id="442a8-945">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-945">**Examples**</span></span>

|  |  |
| --- | --- |
| `gettype("a")` |`"string" ` |
| `gettype(111)` |`"long" ` |
| `gettype(1==1)` |`"int8"` |
| `gettype(now())` |`"datetime" ` |
| `gettype(1s)` |`"timespan" ` |
| `gettype(parsejson('1'))` |`"int" ` |
| `gettype(parsejson(' "abc" '))` |`"string" ` |
| `gettype(parsejson(' {"abc":1} '))` |`"dictionary"` |
| `gettype(parsejson(' [1, 2, 3] '))` |`"array"` |
| `gettype(123.45)` |`"real" ` |
| `gettype(guid(12e8b78d-55b4-46ae-b068-26d7a0080254))` |`"guid"` |
| `gettype(parsejson(''))` |`"null"` |
| `gettype(1.2)==real` |`true` |

### <a name="hash"></a><span data-ttu-id="442a8-946">hash</span><span class="sxs-lookup"><span data-stu-id="442a8-946">hash</span></span>
<span data-ttu-id="442a8-947">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-947">**Syntax**</span></span>

    hash(source [, mod])

<span data-ttu-id="442a8-948">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-948">**Arguments**</span></span>

* <span data-ttu-id="442a8-949">*source*: The source scalar the hash is calculated on.</span><span class="sxs-lookup"><span data-stu-id="442a8-949">*source*: The source scalar the hash is calculated on.</span></span>
* <span data-ttu-id="442a8-950">*mod*: The modulo value to be applied on the hash result.</span><span class="sxs-lookup"><span data-stu-id="442a8-950">*mod*: The modulo value to be applied on the hash result.</span></span>

<span data-ttu-id="442a8-951">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-951">**Returns**</span></span>

<span data-ttu-id="442a8-952">The xxhash (long)value of the given scalar, modulo the given mod value (if specified).</span><span class="sxs-lookup"><span data-stu-id="442a8-952">The xxhash (long)value of the given scalar, modulo the given mod value (if specified).</span></span>

<span data-ttu-id="442a8-953">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-953">**Examples**</span></span>

```
hash("World")                   // 1846988464401551951
hash("World", 100)              // 51 (1846988464401551951 % 100)
hash(datetime("2015-01-01"))    // 1380966698541616202
```
### <a name="iff"></a><span data-ttu-id="442a8-954">iff</span><span class="sxs-lookup"><span data-stu-id="442a8-954">iff</span></span>
<span data-ttu-id="442a8-955">The `iff()` function evaluates the first argument (the predicate), and returns either the value of either the second or third arguments depending on whether the predicate is `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="442a8-955">The `iff()` function evaluates the first argument (the predicate), and returns either the value of either the second or third arguments depending on whether the predicate is `true` or `false`.</span></span> <span data-ttu-id="442a8-956">The second and third arguments must be of the same type.</span><span class="sxs-lookup"><span data-stu-id="442a8-956">The second and third arguments must be of the same type.</span></span>

<span data-ttu-id="442a8-957">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-957">**Syntax**</span></span>

    iff(predicate, ifTrue, ifFalse)


<span data-ttu-id="442a8-958">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-958">**Arguments**</span></span>

* <span data-ttu-id="442a8-959">*predicate:* An expression that evaluates to a `boolean` value.</span><span class="sxs-lookup"><span data-stu-id="442a8-959">*predicate:* An expression that evaluates to a `boolean` value.</span></span>
* <span data-ttu-id="442a8-960">*ifTrue:* An expression that gets evaluated and its value returned from the function if *predicate* evaluates to `true`.</span><span class="sxs-lookup"><span data-stu-id="442a8-960">*ifTrue:* An expression that gets evaluated and its value returned from the function if *predicate* evaluates to `true`.</span></span>
* <span data-ttu-id="442a8-961">*ifFalse:* An expression that gets evaluated and its value returned from the function if *predicate* evaluates to `false`.</span><span class="sxs-lookup"><span data-stu-id="442a8-961">*ifFalse:* An expression that gets evaluated and its value returned from the function if *predicate* evaluates to `false`.</span></span>

<span data-ttu-id="442a8-962">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-962">**Returns**</span></span>

<span data-ttu-id="442a8-963">This function returns the value of *ifTrue* if *predicate* evaluates to `true`, or the value of *ifFalse* otherwise.</span><span class="sxs-lookup"><span data-stu-id="442a8-963">This function returns the value of *ifTrue* if *predicate* evaluates to `true`, or the value of *ifFalse* otherwise.</span></span>

<span data-ttu-id="442a8-964">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-964">**Example**</span></span>

```
iff(floor(timestamp, 1d)==floor(now(), 1d), "today", "anotherday")
```

<a name="isnull"/></a>
<a name="isnotnull"/></a>
<a name="notnull"/></a>

### <a name="isnull-isnotnull-notnull"></a><span data-ttu-id="442a8-965">isnull, isnotnull, notnull</span><span class="sxs-lookup"><span data-stu-id="442a8-965">isnull, isnotnull, notnull</span></span>
    isnull(parsejson("")) == true

<span data-ttu-id="442a8-966">Takes a single argument and tells whether it is null.</span><span class="sxs-lookup"><span data-stu-id="442a8-966">Takes a single argument and tells whether it is null.</span></span>

<span data-ttu-id="442a8-967">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-967">**Syntax**</span></span>

    isnull([value])


    isnotnull([value])


    notnull([value])  // alias for isnotnull

<span data-ttu-id="442a8-968">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-968">**Returns**</span></span>

<span data-ttu-id="442a8-969">True or false depending on the whether the value is null or not null.</span><span class="sxs-lookup"><span data-stu-id="442a8-969">True or false depending on the whether the value is null or not null.</span></span>

| <span data-ttu-id="442a8-970">x</span><span class="sxs-lookup"><span data-stu-id="442a8-970">x</span></span> | <span data-ttu-id="442a8-971">isnull(x)</span><span class="sxs-lookup"><span data-stu-id="442a8-971">isnull(x)</span></span> |
| --- | --- |
| <span data-ttu-id="442a8-972">""</span><span class="sxs-lookup"><span data-stu-id="442a8-972">""</span></span> |<span data-ttu-id="442a8-973">false</span><span class="sxs-lookup"><span data-stu-id="442a8-973">false</span></span> |
| <span data-ttu-id="442a8-974">"x"</span><span class="sxs-lookup"><span data-stu-id="442a8-974">"x"</span></span> |<span data-ttu-id="442a8-975">false</span><span class="sxs-lookup"><span data-stu-id="442a8-975">false</span></span> |
| <span data-ttu-id="442a8-976">parsejson("")</span><span class="sxs-lookup"><span data-stu-id="442a8-976">parsejson("")</span></span> |<span data-ttu-id="442a8-977">true</span><span class="sxs-lookup"><span data-stu-id="442a8-977">true</span></span> |
| <span data-ttu-id="442a8-978">parsejson("[]")</span><span class="sxs-lookup"><span data-stu-id="442a8-978">parsejson("[]")</span></span> |<span data-ttu-id="442a8-979">false</span><span class="sxs-lookup"><span data-stu-id="442a8-979">false</span></span> |
| <span data-ttu-id="442a8-980">parsejson("{}")</span><span class="sxs-lookup"><span data-stu-id="442a8-980">parsejson("{}")</span></span> |<span data-ttu-id="442a8-981">false</span><span class="sxs-lookup"><span data-stu-id="442a8-981">false</span></span> |

<span data-ttu-id="442a8-982">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-982">**Example**</span></span>

    T | where isnotnull(PossiblyNull) | count

<span data-ttu-id="442a8-983">Notice that there are other ways of achieving this effect:</span><span class="sxs-lookup"><span data-stu-id="442a8-983">Notice that there are other ways of achieving this effect:</span></span>

    T | summarize count(PossiblyNull)

### <a name="toscalar"></a><span data-ttu-id="442a8-984">toscalar</span><span class="sxs-lookup"><span data-stu-id="442a8-984">toscalar</span></span>
<span data-ttu-id="442a8-985">Evaluates a query or an expression and returns the result as a single value.</span><span class="sxs-lookup"><span data-stu-id="442a8-985">Evaluates a query or an expression and returns the result as a single value.</span></span> <span data-ttu-id="442a8-986">This function is useful for staged calculations; for example, calculating a total count of events and then using that as a baseline.</span><span class="sxs-lookup"><span data-stu-id="442a8-986">This function is useful for staged calculations; for example, calculating a total count of events and then using that as a baseline.</span></span>

<span data-ttu-id="442a8-987">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-987">**Syntax**</span></span>

    toscalar(query)
    toscalar(scalar)

<span data-ttu-id="442a8-988">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-988">**Returns**</span></span>

<span data-ttu-id="442a8-989">The evaluated argument.</span><span class="sxs-lookup"><span data-stu-id="442a8-989">The evaluated argument.</span></span> <span data-ttu-id="442a8-990">If the argument is a table, returns the first column of the first row.</span><span class="sxs-lookup"><span data-stu-id="442a8-990">If the argument is a table, returns the first column of the first row.</span></span> <span data-ttu-id="442a8-991">(Good practice is to arrange that the argument has only one column and row.)</span><span class="sxs-lookup"><span data-stu-id="442a8-991">(Good practice is to arrange that the argument has only one column and row.)</span></span>

<span data-ttu-id="442a8-992">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-992">**Example**</span></span>

```AIQL

    // Get the count of requests 5 days ago:
    let baseline = toscalar(requests  
        | where floor(timestamp, 1d) == floor(ago(5d),1d) | count);
    // List the counts relative to that baseline:
    requests | summarize daycount = count() by floor(timestamp, 1d)  
    | extend relative = daycount - baseline
```




### <a name="boolean-literals"></a><span data-ttu-id="442a8-993">Boolean Literals</span><span class="sxs-lookup"><span data-stu-id="442a8-993">Boolean Literals</span></span>
    true == 1
    false == 0
    gettype(true) == "int8"
    typeof(bool) == typeof(int8)

### <a name="boolean-operators"></a><span data-ttu-id="442a8-994">Boolean operators</span><span class="sxs-lookup"><span data-stu-id="442a8-994">Boolean operators</span></span>
    and 
    or 

### <a name="convert-to-boolean"></a><span data-ttu-id="442a8-995">Convert to boolean</span><span class="sxs-lookup"><span data-stu-id="442a8-995">Convert to boolean</span></span>

<span data-ttu-id="442a8-996">If you have a string `aStringBoolean` that contains a value "true" or "false", you can convert it to Boolean as follows:</span><span class="sxs-lookup"><span data-stu-id="442a8-996">If you have a string `aStringBoolean` that contains a value "true" or "false", you can convert it to Boolean as follows:</span></span>

    booleanResult = aStringBoolean =~ "true"



## <a name="numbers"></a><span data-ttu-id="442a8-997">Numbers</span><span class="sxs-lookup"><span data-stu-id="442a8-997">Numbers</span></span>
<span data-ttu-id="442a8-998">[abs](#abs) | [bin](#bin) | [exp](#exp) | [floor](#floor) | [gamma](#gamma) |[log](#log) | [rand](#rand) | [range](#range) | [sqrt](#sqrt) 
| [todouble](#todouble) | [toint](#toint) | [tolong](#tolong)</span><span class="sxs-lookup"><span data-stu-id="442a8-998">[abs](#abs) | [bin](#bin) | [exp](#exp) | [floor](#floor) | [gamma](#gamma) |[log](#log) | [rand](#rand) | [range](#range) | [sqrt](#sqrt) 
| [todouble](#todouble) | [toint](#toint) | [tolong](#tolong)</span></span>

### <a name="numeric-literals"></a><span data-ttu-id="442a8-999">Numeric literals</span><span class="sxs-lookup"><span data-stu-id="442a8-999">Numeric literals</span></span>
|  |  |
| --- | --- |
| `42` |`long` |
| `42.0` |`real` |

### <a name="arithmetic-operators"></a><span data-ttu-id="442a8-1000">Arithmetic operators</span><span class="sxs-lookup"><span data-stu-id="442a8-1000">Arithmetic operators</span></span>
|  |  |
| --- | --- |
| + |<span data-ttu-id="442a8-1001">Add</span><span class="sxs-lookup"><span data-stu-id="442a8-1001">Add</span></span> |
| - |<span data-ttu-id="442a8-1002">Subtract</span><span class="sxs-lookup"><span data-stu-id="442a8-1002">Subtract</span></span> |
| * |<span data-ttu-id="442a8-1003">Multiply</span><span class="sxs-lookup"><span data-stu-id="442a8-1003">Multiply</span></span> |
| / |<span data-ttu-id="442a8-1004">Divide</span><span class="sxs-lookup"><span data-stu-id="442a8-1004">Divide</span></span> |
| % |<span data-ttu-id="442a8-1005">Modulo</span><span class="sxs-lookup"><span data-stu-id="442a8-1005">Modulo</span></span> |
| `<` |<span data-ttu-id="442a8-1006">Less</span><span class="sxs-lookup"><span data-stu-id="442a8-1006">Less</span></span> |
| `<=` |<span data-ttu-id="442a8-1007">Less or Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-1007">Less or Equals</span></span> |
| `>` |<span data-ttu-id="442a8-1008">Greater</span><span class="sxs-lookup"><span data-stu-id="442a8-1008">Greater</span></span> |
| `>=` |<span data-ttu-id="442a8-1009">Greater or Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-1009">Greater or Equals</span></span> |
| `<>` |<span data-ttu-id="442a8-1010">Not Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-1010">Not Equals</span></span> |
| `!=` |<span data-ttu-id="442a8-1011">Not Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-1011">Not Equals</span></span> |

### <a name="abs"></a><span data-ttu-id="442a8-1012">abs</span><span class="sxs-lookup"><span data-stu-id="442a8-1012">abs</span></span>
<span data-ttu-id="442a8-1013">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1013">**Syntax**</span></span>

    abs(x)

<span data-ttu-id="442a8-1014">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1014">**Arguments**</span></span>

* <span data-ttu-id="442a8-1015">x - an integer, real or timespan</span><span class="sxs-lookup"><span data-stu-id="442a8-1015">x - an integer, real or timespan</span></span>

<span data-ttu-id="442a8-1016">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1016">**Returns**</span></span>

    iff(x>0, x, -x)

<a name="bin"></a><a name="floor"></a>

### <a name="bin-floor"></a><span data-ttu-id="442a8-1017">bin, floor</span><span class="sxs-lookup"><span data-stu-id="442a8-1017">bin, floor</span></span>
<span data-ttu-id="442a8-1018">Rounds values down to an integer multiple of a given bin size.</span><span class="sxs-lookup"><span data-stu-id="442a8-1018">Rounds values down to an integer multiple of a given bin size.</span></span> <span data-ttu-id="442a8-1019">Used a lot in the [`summarize by`](#summarize-operator) query.</span><span class="sxs-lookup"><span data-stu-id="442a8-1019">Used a lot in the [`summarize by`](#summarize-operator) query.</span></span> <span data-ttu-id="442a8-1020">If you have a scattered set of values, they will be grouped into a smaller set of specific values.</span><span class="sxs-lookup"><span data-stu-id="442a8-1020">If you have a scattered set of values, they will be grouped into a smaller set of specific values.</span></span>

<span data-ttu-id="442a8-1021">Alias `floor`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1021">Alias `floor`.</span></span>

<span data-ttu-id="442a8-1022">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1022">**Syntax**</span></span>

     bin(value, roundTo)
     floor(value, roundTo)

<span data-ttu-id="442a8-1023">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1023">**Arguments**</span></span>

* <span data-ttu-id="442a8-1024">*value:* A number, date, or timespan.</span><span class="sxs-lookup"><span data-stu-id="442a8-1024">*value:* A number, date, or timespan.</span></span> 
* <span data-ttu-id="442a8-1025">*roundTo:* The "bin size".</span><span class="sxs-lookup"><span data-stu-id="442a8-1025">*roundTo:* The "bin size".</span></span> <span data-ttu-id="442a8-1026">A number, date or timespan that divides *value*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1026">A number, date or timespan that divides *value*.</span></span> 

<span data-ttu-id="442a8-1027">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1027">**Returns**</span></span>

<span data-ttu-id="442a8-1028">The nearest multiple of *roundTo* below *value*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1028">The nearest multiple of *roundTo* below *value*.</span></span>  

    (toint(value/roundTo)) * roundTo

<span data-ttu-id="442a8-1029">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1029">**Examples**</span></span>

| <span data-ttu-id="442a8-1030">Expression</span><span class="sxs-lookup"><span data-stu-id="442a8-1030">Expression</span></span> | <span data-ttu-id="442a8-1031">Result</span><span class="sxs-lookup"><span data-stu-id="442a8-1031">Result</span></span> |
| --- | --- |
| `bin(4.5, 1)` |`4.0` |
| `bin(time(16d), 7d)` |`14d` |
| `bin(datetime(1953-04-15 22:25:07), 1d)` |`datetime(1953-04-15)` |

<span data-ttu-id="442a8-1032">The following expression calculates a histogram of durations, with a bucket size of 1 second:</span><span class="sxs-lookup"><span data-stu-id="442a8-1032">The following expression calculates a histogram of durations, with a bucket size of 1 second:</span></span>

```AIQL

    T | summarize Hits=count() by bin(Duration, 1s)
```

### <a name="exp"></a><span data-ttu-id="442a8-1033">exp</span><span class="sxs-lookup"><span data-stu-id="442a8-1033">exp</span></span>
    exp(v)   // e raised to the power v
    exp2(v)  // 2 raised to the power v
    exp10(v) // 10 raised to the power v


### <a name="floor"></a><span data-ttu-id="442a8-1034">floor</span><span class="sxs-lookup"><span data-stu-id="442a8-1034">floor</span></span>
<span data-ttu-id="442a8-1035">An alias for [`bin()`](#bin).</span><span class="sxs-lookup"><span data-stu-id="442a8-1035">An alias for [`bin()`](#bin).</span></span>

### <a name="gamma"></a><span data-ttu-id="442a8-1036">gamma</span><span class="sxs-lookup"><span data-stu-id="442a8-1036">gamma</span></span>
<span data-ttu-id="442a8-1037">The [gamma function](https://en.wikipedia.org/wiki/Gamma_function)</span><span class="sxs-lookup"><span data-stu-id="442a8-1037">The [gamma function](https://en.wikipedia.org/wiki/Gamma_function)</span></span>

<span data-ttu-id="442a8-1038">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1038">**Syntax**</span></span>

    gamma(x)

<span data-ttu-id="442a8-1039">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1039">**Arguments**</span></span>

* <span data-ttu-id="442a8-1040">*x:* A real number</span><span class="sxs-lookup"><span data-stu-id="442a8-1040">*x:* A real number</span></span>

<span data-ttu-id="442a8-1041">For positive integers, `gamma(x) == (x-1)!` For example, `gamma(5) == 4 * 3 * 2 * 1`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1041">For positive integers, `gamma(x) == (x-1)!` For example, `gamma(5) == 4 * 3 * 2 * 1`.</span></span>

<span data-ttu-id="442a8-1042">See also [loggamma](#loggamma).</span><span class="sxs-lookup"><span data-stu-id="442a8-1042">See also [loggamma](#loggamma).</span></span>

### <a name="log"></a><span data-ttu-id="442a8-1043">log</span><span class="sxs-lookup"><span data-stu-id="442a8-1043">log</span></span>
    log(v)    // Natural logarithm of v
    log2(v)   // Logarithm base 2 of v
    log10(v)  // Logarithm base 10 of v


<span data-ttu-id="442a8-1044">`v` should be a real number > 0.</span><span class="sxs-lookup"><span data-stu-id="442a8-1044">`v` should be a real number > 0.</span></span> <span data-ttu-id="442a8-1045">Otherwise, null is returned.</span><span class="sxs-lookup"><span data-stu-id="442a8-1045">Otherwise, null is returned.</span></span>

### <a name="loggamma"></a><span data-ttu-id="442a8-1046">loggamma</span><span class="sxs-lookup"><span data-stu-id="442a8-1046">loggamma</span></span>
<span data-ttu-id="442a8-1047">The natural logarithm of the absolute value of the [gamma function](#gamma).</span><span class="sxs-lookup"><span data-stu-id="442a8-1047">The natural logarithm of the absolute value of the [gamma function](#gamma).</span></span>

<span data-ttu-id="442a8-1048">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1048">**Syntax**</span></span>

    loggamma(x)

<span data-ttu-id="442a8-1049">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1049">**Arguments**</span></span>

* <span data-ttu-id="442a8-1050">*x:* A real number</span><span class="sxs-lookup"><span data-stu-id="442a8-1050">*x:* A real number</span></span>

### <a name="rand"></a><span data-ttu-id="442a8-1051">rand</span><span class="sxs-lookup"><span data-stu-id="442a8-1051">rand</span></span>
<span data-ttu-id="442a8-1052">A random number generator.</span><span class="sxs-lookup"><span data-stu-id="442a8-1052">A random number generator.</span></span>

* <span data-ttu-id="442a8-1053">`rand()` - a real number between 0.0 and 1.0</span><span class="sxs-lookup"><span data-stu-id="442a8-1053">`rand()` - a real number between 0.0 and 1.0</span></span>
* <span data-ttu-id="442a8-1054">`rand(n)` - an integer between 0 and n-1</span><span class="sxs-lookup"><span data-stu-id="442a8-1054">`rand(n)` - an integer between 0 and n-1</span></span>

### <a name="sqrt"></a><span data-ttu-id="442a8-1055">sqrt</span><span class="sxs-lookup"><span data-stu-id="442a8-1055">sqrt</span></span>
<span data-ttu-id="442a8-1056">The square root function.</span><span class="sxs-lookup"><span data-stu-id="442a8-1056">The square root function.</span></span>  

<span data-ttu-id="442a8-1057">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1057">**Syntax**</span></span>

    sqrt(x)

<span data-ttu-id="442a8-1058">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1058">**Arguments**</span></span>

* <span data-ttu-id="442a8-1059">*x:* A real number >= 0.</span><span class="sxs-lookup"><span data-stu-id="442a8-1059">*x:* A real number >= 0.</span></span>

<span data-ttu-id="442a8-1060">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1060">**Returns**</span></span>

* <span data-ttu-id="442a8-1061">A positive number such that `sqrt(x) * sqrt(x) == x`</span><span class="sxs-lookup"><span data-stu-id="442a8-1061">A positive number such that `sqrt(x) * sqrt(x) == x`</span></span>
* <span data-ttu-id="442a8-1062">`null` if the argument is negative or cannot be converted to a `real` value.</span><span class="sxs-lookup"><span data-stu-id="442a8-1062">`null` if the argument is negative or cannot be converted to a `real` value.</span></span> 

### <a name="toint"></a><span data-ttu-id="442a8-1063">toint</span><span class="sxs-lookup"><span data-stu-id="442a8-1063">toint</span></span>
    toint(100)        // cast from long
    toint(20.7) == 20 // nearest int below double
    toint(20.4) == 20 // nearest int below double
    toint("  123  ")  // parse string
    toint(a[0])       // cast from dynamic
    toint(b.c)        // cast from dynamic


### <a name="todouble"></a><span data-ttu-id="442a8-1064">todouble</span><span class="sxs-lookup"><span data-stu-id="442a8-1064">todouble</span></span>
    todouble(20) == 20.0 // conversion from long or int
    todouble(" 12.34 ")  // parse string
    todouble(a[0])       // cast from dynamic
    todouble(b.c)        // cast from dynamic


### <a name="tolong"></a><span data-ttu-id="442a8-1065">tolong</span><span class="sxs-lookup"><span data-stu-id="442a8-1065">tolong</span></span>
    tolong(20.7) == 20 // conversion from double
    tolong(20.4) == 20 // conversion from double
    tolong("  123  ")  // parse string
    tolong(a[0])       // cast from dynamic
    tolong(b.c)        // cast from dynamic


## <a name="date-and-time"></a><span data-ttu-id="442a8-1066">Date and time</span><span class="sxs-lookup"><span data-stu-id="442a8-1066">Date and time</span></span>
<span data-ttu-id="442a8-1067">[ago](#ago) | [dayofmonth](#dayofmonth) | [dayofweek](#dayofweek) |  [dayofyear](#dayofyear) |[datepart](#datepart) | [endofday](#endofday) | [endofmonth](#endofmonth) | [endofweek](#endofweek) | [endofyear](#endofyear) | [getmonth](#getmonth)|  [getyear](#getyear) | [now](#now) | [startofday](#startofday) | [startofmonth](#startofmonth) | [startofweek](#startofweek) | [startofyear](#startofyear) | [todatetime](#todatetime) | [totimespan](#totimespan) | [weekofyear](#weekofyear)</span><span class="sxs-lookup"><span data-stu-id="442a8-1067">[ago](#ago) | [dayofmonth](#dayofmonth) | [dayofweek](#dayofweek) |  [dayofyear](#dayofyear) |[datepart](#datepart) | [endofday](#endofday) | [endofmonth](#endofmonth) | [endofweek](#endofweek) | [endofyear](#endofyear) | [getmonth](#getmonth)|  [getyear](#getyear) | [now](#now) | [startofday](#startofday) | [startofmonth](#startofmonth) | [startofweek](#startofweek) | [startofyear](#startofyear) | [todatetime](#todatetime) | [totimespan](#totimespan) | [weekofyear](#weekofyear)</span></span>

<span data-ttu-id="442a8-1068">A timespan represents an interval of time such as 3 hours or 1 year.</span><span class="sxs-lookup"><span data-stu-id="442a8-1068">A timespan represents an interval of time such as 3 hours or 1 year.</span></span>

<span data-ttu-id="442a8-1069">A datetime represents a specific calendar/clock date and time in UTC.</span><span class="sxs-lookup"><span data-stu-id="442a8-1069">A datetime represents a specific calendar/clock date and time in UTC.</span></span>

<span data-ttu-id="442a8-1070">There is no separate 'date' type.</span><span class="sxs-lookup"><span data-stu-id="442a8-1070">There is no separate 'date' type.</span></span> <span data-ttu-id="442a8-1071">To remove the time from a datetime, use an expression such as `bin(timestamp, 1d)`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1071">To remove the time from a datetime, use an expression such as `bin(timestamp, 1d)`.</span></span>

### <a name="date-and-time-literals"></a><span data-ttu-id="442a8-1072">Date and time literals</span><span class="sxs-lookup"><span data-stu-id="442a8-1072">Date and time literals</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="442a8-1073">**datetime**</span><span class="sxs-lookup"><span data-stu-id="442a8-1073">**datetime**</span></span> | |
| `datetime("2015-12-31 23:59:59.9")`<br/>`datetime("2015-12-31")` |<span data-ttu-id="442a8-1074">Times are always in UTC.</span><span class="sxs-lookup"><span data-stu-id="442a8-1074">Times are always in UTC.</span></span> <span data-ttu-id="442a8-1075">Omitting the date gives a time today.</span><span class="sxs-lookup"><span data-stu-id="442a8-1075">Omitting the date gives a time today.</span></span> |
| `now()` |<span data-ttu-id="442a8-1076">The current time.</span><span class="sxs-lookup"><span data-stu-id="442a8-1076">The current time.</span></span> |
| <span data-ttu-id="442a8-1077">`now(`-*timespan*`)`</span><span class="sxs-lookup"><span data-stu-id="442a8-1077">`now(`-*timespan*`)`</span></span> |<span data-ttu-id="442a8-1078">`now()-`*timespan*</span><span class="sxs-lookup"><span data-stu-id="442a8-1078">`now()-`*timespan*</span></span> |
| <span data-ttu-id="442a8-1079">`ago(`*timespan*`)`</span><span class="sxs-lookup"><span data-stu-id="442a8-1079">`ago(`*timespan*`)`</span></span> |<span data-ttu-id="442a8-1080">`now()-`*timespan*</span><span class="sxs-lookup"><span data-stu-id="442a8-1080">`now()-`*timespan*</span></span> |
| <span data-ttu-id="442a8-1081">**timespan**</span><span class="sxs-lookup"><span data-stu-id="442a8-1081">**timespan**</span></span> | |
| `2d` |<span data-ttu-id="442a8-1082">2 days</span><span class="sxs-lookup"><span data-stu-id="442a8-1082">2 days</span></span> |
| `1.5h` |<span data-ttu-id="442a8-1083">1.5 hour</span><span class="sxs-lookup"><span data-stu-id="442a8-1083">1.5 hour</span></span> |
| `30m` |<span data-ttu-id="442a8-1084">30 minutes</span><span class="sxs-lookup"><span data-stu-id="442a8-1084">30 minutes</span></span> |
| `10s` |<span data-ttu-id="442a8-1085">10 seconds</span><span class="sxs-lookup"><span data-stu-id="442a8-1085">10 seconds</span></span> |
| `0.1s` |<span data-ttu-id="442a8-1086">0.1 second</span><span class="sxs-lookup"><span data-stu-id="442a8-1086">0.1 second</span></span> |
| `100ms` |<span data-ttu-id="442a8-1087">100 millisecond</span><span class="sxs-lookup"><span data-stu-id="442a8-1087">100 millisecond</span></span> |
| `10microsecond` | |
| `1tick` |<span data-ttu-id="442a8-1088">100ns</span><span class="sxs-lookup"><span data-stu-id="442a8-1088">100ns</span></span> |
| `time("15 seconds")` | |
| `time("2")` |<span data-ttu-id="442a8-1089">2 days</span><span class="sxs-lookup"><span data-stu-id="442a8-1089">2 days</span></span> |
| `time("0.12:34:56.7")` |`0d+12h+34m+56.7s` |

### <a name="date-and-time-expressions"></a><span data-ttu-id="442a8-1090">Date and time expressions</span><span class="sxs-lookup"><span data-stu-id="442a8-1090">Date and time expressions</span></span>
| <span data-ttu-id="442a8-1091">Expression</span><span class="sxs-lookup"><span data-stu-id="442a8-1091">Expression</span></span> | <span data-ttu-id="442a8-1092">Result</span><span class="sxs-lookup"><span data-stu-id="442a8-1092">Result</span></span> |<span data-ttu-id="442a8-1093">Effect</span><span class="sxs-lookup"><span data-stu-id="442a8-1093">Effect</span></span>|
| --- | --- |---|
| `datetime("2015-01-02") - datetime("2015-01-01")` |`1d` | <span data-ttu-id="442a8-1094">Time difference</span><span class="sxs-lookup"><span data-stu-id="442a8-1094">Time difference</span></span>|
| `datetime("2015-01-01") + 1d` |`datetime("2015-01-02")` | <span data-ttu-id="442a8-1095">Add days</span><span class="sxs-lookup"><span data-stu-id="442a8-1095">Add days</span></span> |
| `datetime("2015-01-01") - 1d` |`datetime("2014-12-31")` | <span data-ttu-id="442a8-1096">Subtract days</span><span class="sxs-lookup"><span data-stu-id="442a8-1096">Subtract days</span></span>|
| `2h * 24` |`2d` |<span data-ttu-id="442a8-1097">Timespan multiples</span><span class="sxs-lookup"><span data-stu-id="442a8-1097">Timespan multiples</span></span>|
| `2d` / `2h` |`24` |<span data-ttu-id="442a8-1098">Timespan division</span><span class="sxs-lookup"><span data-stu-id="442a8-1098">Timespan division</span></span>|
| `datetime("2015-04-15T22:33") % 1d` |`timespan("22:33")` |<span data-ttu-id="442a8-1099">Time from a datetime</span><span class="sxs-lookup"><span data-stu-id="442a8-1099">Time from a datetime</span></span>|
| `bin(datetime("2015-04-15T22:33"), 1d)` |`datetime("2015-04-15T00:00")` |<span data-ttu-id="442a8-1100">Date from a datetime</span><span class="sxs-lookup"><span data-stu-id="442a8-1100">Date from a datetime</span></span>|
|  | ||
| `<` ||<span data-ttu-id="442a8-1101">Less</span><span class="sxs-lookup"><span data-stu-id="442a8-1101">Less</span></span> |
| `<=` ||<span data-ttu-id="442a8-1102">Less or Equal</span><span class="sxs-lookup"><span data-stu-id="442a8-1102">Less or Equal</span></span> |
| `>` ||<span data-ttu-id="442a8-1103">Greater</span><span class="sxs-lookup"><span data-stu-id="442a8-1103">Greater</span></span> |
| `>=` ||<span data-ttu-id="442a8-1104">Greater or Equal</span><span class="sxs-lookup"><span data-stu-id="442a8-1104">Greater or Equal</span></span> |
| `<>` ||<span data-ttu-id="442a8-1105">Not Equal</span><span class="sxs-lookup"><span data-stu-id="442a8-1105">Not Equal</span></span> |
| `!=` ||<span data-ttu-id="442a8-1106">Not Equal</span><span class="sxs-lookup"><span data-stu-id="442a8-1106">Not Equal</span></span> |

### <a name="ago"></a><span data-ttu-id="442a8-1107">ago</span><span class="sxs-lookup"><span data-stu-id="442a8-1107">ago</span></span>
<span data-ttu-id="442a8-1108">Subtracts the given timespan from the current UTC clock time.</span><span class="sxs-lookup"><span data-stu-id="442a8-1108">Subtracts the given timespan from the current UTC clock time.</span></span> <span data-ttu-id="442a8-1109">Like `now()`, this function can be used multiple times in a statement and the UTC clock time being referenced will be the same for all instantiations.</span><span class="sxs-lookup"><span data-stu-id="442a8-1109">Like `now()`, this function can be used multiple times in a statement and the UTC clock time being referenced will be the same for all instantiations.</span></span>

<span data-ttu-id="442a8-1110">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1110">**Syntax**</span></span>

    ago(a_timespan)

<span data-ttu-id="442a8-1111">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1111">**Arguments**</span></span>

* <span data-ttu-id="442a8-1112">*a_timespan*: Interval to subtract from the current UTC clock time (`now()`).</span><span class="sxs-lookup"><span data-stu-id="442a8-1112">*a_timespan*: Interval to subtract from the current UTC clock time (`now()`).</span></span>

<span data-ttu-id="442a8-1113">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1113">**Returns**</span></span>

    now() - a_timespan

<span data-ttu-id="442a8-1114">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1114">**Example**</span></span>

<span data-ttu-id="442a8-1115">All rows with a timestamp in the past hour:</span><span class="sxs-lookup"><span data-stu-id="442a8-1115">All rows with a timestamp in the past hour:</span></span>

```AIQL

    T | where timestamp > ago(1h)
```

### <a name="datepart"></a><span data-ttu-id="442a8-1116">datepart</span><span class="sxs-lookup"><span data-stu-id="442a8-1116">datepart</span></span>
    datepart("Day", datetime(2015-12-14)) == 14

<span data-ttu-id="442a8-1117">Extracts a specified part of a date as an integer.</span><span class="sxs-lookup"><span data-stu-id="442a8-1117">Extracts a specified part of a date as an integer.</span></span>

<span data-ttu-id="442a8-1118">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1118">**Syntax**</span></span>

    datepart(part, datetime)

<span data-ttu-id="442a8-1119">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1119">**Arguments**</span></span>

* <span data-ttu-id="442a8-1120">`part:String` - {"Year", "Month", "Day", "Hour", "Minute", "Second", "Millisecond", "Microsecond", "Nanosecond"}</span><span class="sxs-lookup"><span data-stu-id="442a8-1120">`part:String` - {"Year", "Month", "Day", "Hour", "Minute", "Second", "Millisecond", "Microsecond", "Nanosecond"}</span></span>
* `datetime`

<span data-ttu-id="442a8-1121">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1121">**Returns**</span></span>

<span data-ttu-id="442a8-1122">Long representing the specified part.</span><span class="sxs-lookup"><span data-stu-id="442a8-1122">Long representing the specified part.</span></span>

### <a name="dayofmonth"></a><span data-ttu-id="442a8-1123">dayofmonth</span><span class="sxs-lookup"><span data-stu-id="442a8-1123">dayofmonth</span></span>
    dayofmonth(datetime("2016-05-15")) == 15 

<span data-ttu-id="442a8-1124">The ordinal number of the day in the month.</span><span class="sxs-lookup"><span data-stu-id="442a8-1124">The ordinal number of the day in the month.</span></span>

<span data-ttu-id="442a8-1125">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1125">**Syntax**</span></span>

    dayofmonth(a_date)

<span data-ttu-id="442a8-1126">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1126">**Arguments**</span></span>

* <span data-ttu-id="442a8-1127">`a_date`: A `datetime`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1127">`a_date`: A `datetime`.</span></span>

### <a name="dayofweek"></a><span data-ttu-id="442a8-1128">dayofweek</span><span class="sxs-lookup"><span data-stu-id="442a8-1128">dayofweek</span></span>
    dayofweek(datetime("2015-12-14")) == 1d  // Monday

<span data-ttu-id="442a8-1129">The integer number of days since the preceding Sunday, as a `timespan`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1129">The integer number of days since the preceding Sunday, as a `timespan`.</span></span>

<span data-ttu-id="442a8-1130">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1130">**Syntax**</span></span>

    dayofweek(a_date)

<span data-ttu-id="442a8-1131">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1131">**Arguments**</span></span>

* <span data-ttu-id="442a8-1132">`a_date`: A `datetime`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1132">`a_date`: A `datetime`.</span></span>

<span data-ttu-id="442a8-1133">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1133">**Returns**</span></span>

<span data-ttu-id="442a8-1134">The `timespan` since midnight at the beginning of the preceding Sunday, rounded down to an integer number of days.</span><span class="sxs-lookup"><span data-stu-id="442a8-1134">The `timespan` since midnight at the beginning of the preceding Sunday, rounded down to an integer number of days.</span></span>

<span data-ttu-id="442a8-1135">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1135">**Examples**</span></span>

```AIQL
dayofweek(1947-11-29 10:00:05)  // time(6.00:00:00), indicating Saturday
dayofweek(1970-05-11)           // time(1.00:00:00), indicating Monday
```

### <a name="dayofyear"></a><span data-ttu-id="442a8-1136">dayofyear</span><span class="sxs-lookup"><span data-stu-id="442a8-1136">dayofyear</span></span>
    dayofyear(datetime("2016-05-31")) == 152 
    dayofyear(datetime("2016-01-01")) == 1 

<span data-ttu-id="442a8-1137">The ordinal number of the day in the year.</span><span class="sxs-lookup"><span data-stu-id="442a8-1137">The ordinal number of the day in the year.</span></span>

<span data-ttu-id="442a8-1138">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1138">**Syntax**</span></span>

    dayofyear(a_date)

<span data-ttu-id="442a8-1139">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1139">**Arguments**</span></span>

* <span data-ttu-id="442a8-1140">`a_date`: A `datetime`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1140">`a_date`: A `datetime`.</span></span>

<a name="endofday"></a><a name="endofweek"></a><a name="endofmonth"></a><a name="endofyear"></a>

### <a name="endofday-endofweek-endofmonth-endofyear"></a><span data-ttu-id="442a8-1141">endofday, endofweek, endofmonth, endofyear</span><span class="sxs-lookup"><span data-stu-id="442a8-1141">endofday, endofweek, endofmonth, endofyear</span></span>
    dt = datetime("2016-05-23 12:34")

    endofday(dt) == 2016-05-23T23:59:59.999
    endofweek(dt) == 2016-05-28T23:59:59.999 // Saturday
    endofmonth(dt) == 2016-05-31T23:59:59.999 
    endofyear(dt) == 2016-12-31T23:59:59.999 


### <a name="getmonth"></a><span data-ttu-id="442a8-1142">getmonth</span><span class="sxs-lookup"><span data-stu-id="442a8-1142">getmonth</span></span>
<span data-ttu-id="442a8-1143">Get the month number (1-12) from a datetime.</span><span class="sxs-lookup"><span data-stu-id="442a8-1143">Get the month number (1-12) from a datetime.</span></span>

<span data-ttu-id="442a8-1144">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1144">**Example**</span></span>

    ... | extend month = getmonth(datetime(2015-10-12))

    --> month == 10

### <a name="getyear"></a><span data-ttu-id="442a8-1145">getyear</span><span class="sxs-lookup"><span data-stu-id="442a8-1145">getyear</span></span>
<span data-ttu-id="442a8-1146">Get the year from a datetime.</span><span class="sxs-lookup"><span data-stu-id="442a8-1146">Get the year from a datetime.</span></span>

<span data-ttu-id="442a8-1147">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1147">**Example**</span></span>

    ... | extend year = getyear(datetime(2015-10-12))

    --> year == 2015

### <a name="now"></a><span data-ttu-id="442a8-1148">now</span><span class="sxs-lookup"><span data-stu-id="442a8-1148">now</span></span>
    now()
    now(-2d)

<span data-ttu-id="442a8-1149">The current UTC clock time, optionally offset by a given timespan.</span><span class="sxs-lookup"><span data-stu-id="442a8-1149">The current UTC clock time, optionally offset by a given timespan.</span></span> <span data-ttu-id="442a8-1150">This function can be used multiple times in a statement and the clock time being referenced will be the same for all instances.</span><span class="sxs-lookup"><span data-stu-id="442a8-1150">This function can be used multiple times in a statement and the clock time being referenced will be the same for all instances.</span></span>

<span data-ttu-id="442a8-1151">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1151">**Syntax**</span></span>

    now([offset])

<span data-ttu-id="442a8-1152">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1152">**Arguments**</span></span>

* <span data-ttu-id="442a8-1153">*offset:* A `timespan`, added to the current UTC clock time.</span><span class="sxs-lookup"><span data-stu-id="442a8-1153">*offset:* A `timespan`, added to the current UTC clock time.</span></span> <span data-ttu-id="442a8-1154">Default: 0.</span><span class="sxs-lookup"><span data-stu-id="442a8-1154">Default: 0.</span></span>

<span data-ttu-id="442a8-1155">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1155">**Returns**</span></span>

<span data-ttu-id="442a8-1156">The current UTC clock time as a `datetime`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1156">The current UTC clock time as a `datetime`.</span></span>

    now() + offset

<span data-ttu-id="442a8-1157">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1157">**Example**</span></span>

<span data-ttu-id="442a8-1158">Determines the interval since the event identified by the predicate:</span><span class="sxs-lookup"><span data-stu-id="442a8-1158">Determines the interval since the event identified by the predicate:</span></span>

```AIQL
T | where ... | extend Elapsed=now() - timestamp
```

<a name="startofday"></a><a name="startofweek"></a><a name="startofmonth"></a><a name="startofyear"></a>

### <a name="startofday-startofweek-startofmonth-startofyear"></a><span data-ttu-id="442a8-1159">startofday, startofweek, startofmonth, startofyear</span><span class="sxs-lookup"><span data-stu-id="442a8-1159">startofday, startofweek, startofmonth, startofyear</span></span>
    date=datetime("2016-05-23 12:34:56")

    startofday(date) == datetime("2016-05-23")
    startofweek(date) == datetime("2016-05-22") // Sunday
    startofmonth(date) == datetime("2016-05-01")
    startofyear(date) == datetime("2016-01-01")



### <a name="todatetime"></a><span data-ttu-id="442a8-1160">todatetime</span><span class="sxs-lookup"><span data-stu-id="442a8-1160">todatetime</span></span>
<span data-ttu-id="442a8-1161">Alias `datetime()`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1161">Alias `datetime()`.</span></span>

     todatetime("2016-03-28")
     todatetime("03/28/2016")
     todatetime("2016-03-28 14:34:00")
     todatetime("03/28/2016 2:34pm")
     todatetime("2016-03-28T14:34.5Z")
     todatetime(a[0]) 
     todatetime(b.c) 

<span data-ttu-id="442a8-1162">Check whether a string is a valid date:</span><span class="sxs-lookup"><span data-stu-id="442a8-1162">Check whether a string is a valid date:</span></span>

     iff(notnull(todatetime(customDimensions.myDate)),
         ..., ...)


### <a name="totimespan"></a><span data-ttu-id="442a8-1163">totimespan</span><span class="sxs-lookup"><span data-stu-id="442a8-1163">totimespan</span></span>
<span data-ttu-id="442a8-1164">Alias `timespan()`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1164">Alias `timespan()`.</span></span>

    totimespan("21d")
    totimespan("21h")
    totimespan(request.duration)

### <a name="weekofyear"></a><span data-ttu-id="442a8-1165">weekofyear</span><span class="sxs-lookup"><span data-stu-id="442a8-1165">weekofyear</span></span>
    weekofyear(datetime("2016-05-14")) == 21
    weekofyear(datetime("2016-01-03")) == 1
    weekofyear(datetime("2016-12-31")) == 53

<span data-ttu-id="442a8-1166">The integer result represents the week number by the ISO 8601 standard.</span><span class="sxs-lookup"><span data-stu-id="442a8-1166">The integer result represents the week number by the ISO 8601 standard.</span></span> <span data-ttu-id="442a8-1167">The first day of a week is Sunday, and the first week of the year is the week that contains that year's first Thursday.</span><span class="sxs-lookup"><span data-stu-id="442a8-1167">The first day of a week is Sunday, and the first week of the year is the week that contains that year's first Thursday.</span></span> <span data-ttu-id="442a8-1168">(The last days of a year can therefore contain some of the days of week 1 of the next year, or the first days can contain some of week 52 or 53 of the previous year.)</span><span class="sxs-lookup"><span data-stu-id="442a8-1168">(The last days of a year can therefore contain some of the days of week 1 of the next year, or the first days can contain some of week 52 or 53 of the previous year.)</span></span>

## <a name="string"></a><span data-ttu-id="442a8-1169">String</span><span class="sxs-lookup"><span data-stu-id="442a8-1169">String</span></span>
<span data-ttu-id="442a8-1170">[countof](#countof) | [extract](#extract) | [extractjson](#extractjson)  | [isempty](#isempty) | [isnotempty](#isnotempty) | [notempty](#notempty) | [parseurl](#parseurl) | [replace](#replace) | [split](#split) | [strcat](#strcat) | [strlen](#strlen) | [substring](#substring) | [tolower](#tolower) | [tostring](#tostring) | [toupper](#toupper)</span><span class="sxs-lookup"><span data-stu-id="442a8-1170">[countof](#countof) | [extract](#extract) | [extractjson](#extractjson)  | [isempty](#isempty) | [isnotempty](#isnotempty) | [notempty](#notempty) | [parseurl](#parseurl) | [replace](#replace) | [split](#split) | [strcat](#strcat) | [strlen](#strlen) | [substring](#substring) | [tolower](#tolower) | [tostring](#tostring) | [toupper](#toupper)</span></span>

### <a name="string-literals"></a><span data-ttu-id="442a8-1171">String Literals</span><span class="sxs-lookup"><span data-stu-id="442a8-1171">String Literals</span></span>
<span data-ttu-id="442a8-1172">The rules are the same as in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="442a8-1172">The rules are the same as in JavaScript.</span></span>

<span data-ttu-id="442a8-1173">Strings may be enclosed either in single or double quote characters.</span><span class="sxs-lookup"><span data-stu-id="442a8-1173">Strings may be enclosed either in single or double quote characters.</span></span> 

<span data-ttu-id="442a8-1174">Backslash (`\`) is used to escape characters such as `\t` (tab), `\n` (newline) and instances of the enclosing quote character.</span><span class="sxs-lookup"><span data-stu-id="442a8-1174">Backslash (`\`) is used to escape characters such as `\t` (tab), `\n` (newline) and instances of the enclosing quote character.</span></span>

* `'this is a "string" literal in single \' quotes'`
* `"this is a 'string' literal in double \" quotes"`
* `@"C:\backslash\not\escaped\with @ prefix"`

### <a name="obfuscated-string-literals"></a><span data-ttu-id="442a8-1175">Obfuscated String Literals</span><span class="sxs-lookup"><span data-stu-id="442a8-1175">Obfuscated String Literals</span></span>
<span data-ttu-id="442a8-1176">Obfuscated string literals are strings that Analytics will obscure when outputting the string (for example, when tracing).</span><span class="sxs-lookup"><span data-stu-id="442a8-1176">Obfuscated string literals are strings that Analytics will obscure when outputting the string (for example, when tracing).</span></span> <span data-ttu-id="442a8-1177">The obfuscation process replaces all obfuscated characters by a start (`*`) character.</span><span class="sxs-lookup"><span data-stu-id="442a8-1177">The obfuscation process replaces all obfuscated characters by a start (`*`) character.</span></span>

<span data-ttu-id="442a8-1178">To form an obfuscated string literal, prepend `h` or 'H'.</span><span class="sxs-lookup"><span data-stu-id="442a8-1178">To form an obfuscated string literal, prepend `h` or 'H'.</span></span> <span data-ttu-id="442a8-1179">For example:</span><span class="sxs-lookup"><span data-stu-id="442a8-1179">For example:</span></span>

```
h'hello'
h@'world' 
h"hello"
```

### <a name="string-comparisons"></a><span data-ttu-id="442a8-1180">String comparisons</span><span class="sxs-lookup"><span data-stu-id="442a8-1180">String comparisons</span></span>
| <span data-ttu-id="442a8-1181">Operator</span><span class="sxs-lookup"><span data-stu-id="442a8-1181">Operator</span></span> | <span data-ttu-id="442a8-1182">Description</span><span class="sxs-lookup"><span data-stu-id="442a8-1182">Description</span></span> | <span data-ttu-id="442a8-1183">Case-Sensitive</span><span class="sxs-lookup"><span data-stu-id="442a8-1183">Case-Sensitive</span></span> | <span data-ttu-id="442a8-1184">True example</span><span class="sxs-lookup"><span data-stu-id="442a8-1184">True example</span></span> |
| --- | --- | --- | --- |
| `==` |<span data-ttu-id="442a8-1185">Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-1185">Equals</span></span> |<span data-ttu-id="442a8-1186">Yes</span><span class="sxs-lookup"><span data-stu-id="442a8-1186">Yes</span></span> |`"aBc" == "aBc"` |
| <span data-ttu-id="442a8-1187">`<>` `!=`</span><span class="sxs-lookup"><span data-stu-id="442a8-1187">`<>` `!=`</span></span> |<span data-ttu-id="442a8-1188">Not equals</span><span class="sxs-lookup"><span data-stu-id="442a8-1188">Not equals</span></span> |<span data-ttu-id="442a8-1189">Yes</span><span class="sxs-lookup"><span data-stu-id="442a8-1189">Yes</span></span> |`"abc" <> "ABC"` |
| `=~` |<span data-ttu-id="442a8-1190">Equals</span><span class="sxs-lookup"><span data-stu-id="442a8-1190">Equals</span></span> |<span data-ttu-id="442a8-1191">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1191">No</span></span> |`"abc" =~ "ABC"` <br/>`boolAsString =~ "true"` |
| `!~` |<span data-ttu-id="442a8-1192">Not equals</span><span class="sxs-lookup"><span data-stu-id="442a8-1192">Not equals</span></span> |<span data-ttu-id="442a8-1193">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1193">No</span></span> |`"aBc" !~ "xyz"` |
| `has` |<span data-ttu-id="442a8-1194">Right-hand-side (RHS) is a whole term in left-hand-side (LHS)</span><span class="sxs-lookup"><span data-stu-id="442a8-1194">Right-hand-side (RHS) is a whole term in left-hand-side (LHS)</span></span> |<span data-ttu-id="442a8-1195">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1195">No</span></span> |`"North America" has "america"` |
| `!has` |<span data-ttu-id="442a8-1196">RHS is not a full term in LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1196">RHS is not a full term in LHS</span></span> |<span data-ttu-id="442a8-1197">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1197">No</span></span> |`"North America" !has "amer"` |
| `hasprefix` |<span data-ttu-id="442a8-1198">RHS is a prefix of a term in LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1198">RHS is a prefix of a term in LHS</span></span> |<span data-ttu-id="442a8-1199">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1199">No</span></span> |`"North America" hasprefix "ame"` |
| `!hasprefix` |<span data-ttu-id="442a8-1200">RHS is not a prefix of any term in LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1200">RHS is not a prefix of any term in LHS</span></span> |<span data-ttu-id="442a8-1201">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1201">No</span></span> |`"North America" !hasprefix "mer"` |
| `hassuffix` |<span data-ttu-id="442a8-1202">RHS is a suffix of a term in LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1202">RHS is a suffix of a term in LHS</span></span> |<span data-ttu-id="442a8-1203">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1203">No</span></span> |`"North America" hassuffix "rth"` |
| `!hassuffix` |<span data-ttu-id="442a8-1204">RHS is not a suffix of any term in LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1204">RHS is not a suffix of any term in LHS</span></span> |<span data-ttu-id="442a8-1205">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1205">No</span></span> |`"North America" !hassuffix "mer"` |
| `contains` |<span data-ttu-id="442a8-1206">RHS occurs as a substring of LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1206">RHS occurs as a substring of LHS</span></span> |<span data-ttu-id="442a8-1207">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1207">No</span></span> |`"FabriKam" contains "BRik"` |
| `!contains` |<span data-ttu-id="442a8-1208">RHS does not occur in LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1208">RHS does not occur in LHS</span></span> |<span data-ttu-id="442a8-1209">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1209">No</span></span> |`"Fabrikam" !contains "xyz"` |
| `containscs` |<span data-ttu-id="442a8-1210">RHS occurs as a substring of LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1210">RHS occurs as a substring of LHS</span></span> |<span data-ttu-id="442a8-1211">Yes</span><span class="sxs-lookup"><span data-stu-id="442a8-1211">Yes</span></span> |`"FabriKam" contains "Kam"` |
| `!containscs` |<span data-ttu-id="442a8-1212">RHS does not occur in LHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1212">RHS does not occur in LHS</span></span> |<span data-ttu-id="442a8-1213">Yes</span><span class="sxs-lookup"><span data-stu-id="442a8-1213">Yes</span></span> |`"Fabrikam" !contains "Kam"` |
| `startswith` |<span data-ttu-id="442a8-1214">RHS is an initial substring of LHS.</span><span class="sxs-lookup"><span data-stu-id="442a8-1214">RHS is an initial substring of LHS.</span></span> |<span data-ttu-id="442a8-1215">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1215">No</span></span> |`"Fabrikam" startswith "fab"` |
| `!startswith` |<span data-ttu-id="442a8-1216">RHS is not an initial substring of LHS.</span><span class="sxs-lookup"><span data-stu-id="442a8-1216">RHS is not an initial substring of LHS.</span></span> |<span data-ttu-id="442a8-1217">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1217">No</span></span> |`"Fabrikam" !startswith "abr"` |
| `endswith` |<span data-ttu-id="442a8-1218">RHS is a terminal substring of LHS.</span><span class="sxs-lookup"><span data-stu-id="442a8-1218">RHS is a terminal substring of LHS.</span></span> |<span data-ttu-id="442a8-1219">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1219">No</span></span> |`"Fabrikam" endswith "kam"` |
| `!endswith` |<span data-ttu-id="442a8-1220">RHS is not a terminal substring of LHS.</span><span class="sxs-lookup"><span data-stu-id="442a8-1220">RHS is not a terminal substring of LHS.</span></span> |<span data-ttu-id="442a8-1221">No</span><span class="sxs-lookup"><span data-stu-id="442a8-1221">No</span></span> |`"Fabrikam" !endswith "ka"` |
| `matches regex` |<span data-ttu-id="442a8-1222">LHS contains a match for RHS</span><span class="sxs-lookup"><span data-stu-id="442a8-1222">LHS contains a match for RHS</span></span> |<span data-ttu-id="442a8-1223">Yes</span><span class="sxs-lookup"><span data-stu-id="442a8-1223">Yes</span></span> |`"Fabrikam" matches regex "b.*k"` |
| [`in`](#in) |<span data-ttu-id="442a8-1224">Equal to any of the elements</span><span class="sxs-lookup"><span data-stu-id="442a8-1224">Equal to any of the elements</span></span> |<span data-ttu-id="442a8-1225">Yes</span><span class="sxs-lookup"><span data-stu-id="442a8-1225">Yes</span></span> |`"abc" in ("123", "345", "abc")` |
| [`!in`](#in) |<span data-ttu-id="442a8-1226">Not equal to any of the elements</span><span class="sxs-lookup"><span data-stu-id="442a8-1226">Not equal to any of the elements</span></span> |<span data-ttu-id="442a8-1227">Yes</span><span class="sxs-lookup"><span data-stu-id="442a8-1227">Yes</span></span> |`"bc" !in ("123", "345", "abc")` |

<span data-ttu-id="442a8-1228">Use `has` or `in` if you're testing for the presence of a whole lexical term - that is, a symbol or an alphanumeric word bounded by non-alphanumeric characters or start or end of field.</span><span class="sxs-lookup"><span data-stu-id="442a8-1228">Use `has` or `in` if you're testing for the presence of a whole lexical term - that is, a symbol or an alphanumeric word bounded by non-alphanumeric characters or start or end of field.</span></span> <span data-ttu-id="442a8-1229">`has` performs faster than `contains`, `startswith` or `endswith`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1229">`has` performs faster than `contains`, `startswith` or `endswith`.</span></span> <span data-ttu-id="442a8-1230">The first of these queries runs faster:</span><span class="sxs-lookup"><span data-stu-id="442a8-1230">The first of these queries runs faster:</span></span>

    EventLog | where continent has "North" | count;
    EventLog | where continent contains "nor" | count





### <a name="countof"></a><span data-ttu-id="442a8-1231">countof</span><span class="sxs-lookup"><span data-stu-id="442a8-1231">countof</span></span>
    countof("The cat sat on the mat", "at") == 3
    countof("The cat sat on the mat", @"\b.at\b", "regex") == 3

<span data-ttu-id="442a8-1232">Counts occurrences of a substring in a string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1232">Counts occurrences of a substring in a string.</span></span> <span data-ttu-id="442a8-1233">Plain string matches may overlap; regex matches do not.</span><span class="sxs-lookup"><span data-stu-id="442a8-1233">Plain string matches may overlap; regex matches do not.</span></span>

<span data-ttu-id="442a8-1234">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1234">**Syntax**</span></span>

    countof(text, search [, kind])

<span data-ttu-id="442a8-1235">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1235">**Arguments**</span></span>

* <span data-ttu-id="442a8-1236">*text:* A string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1236">*text:* A string.</span></span>
* <span data-ttu-id="442a8-1237">*search:* The plain string or regular expression to match inside *text*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1237">*search:* The plain string or regular expression to match inside *text*.</span></span>
* <span data-ttu-id="442a8-1238">*kind:* `"normal"|"regex"` Default `normal`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1238">*kind:* `"normal"|"regex"` Default `normal`.</span></span> 

<span data-ttu-id="442a8-1239">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1239">**Returns**</span></span>

<span data-ttu-id="442a8-1240">The number of times that the search string can be matched in the container.</span><span class="sxs-lookup"><span data-stu-id="442a8-1240">The number of times that the search string can be matched in the container.</span></span> <span data-ttu-id="442a8-1241">Plain string matches may overlap; regex matches do not.</span><span class="sxs-lookup"><span data-stu-id="442a8-1241">Plain string matches may overlap; regex matches do not.</span></span>

<span data-ttu-id="442a8-1242">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1242">**Examples**</span></span>

|  |  |
| --- | --- |
| `countof("aaa", "a")` |<span data-ttu-id="442a8-1243">3</span><span class="sxs-lookup"><span data-stu-id="442a8-1243">3</span></span> |
| `countof("aaaa", "aa")` |<span data-ttu-id="442a8-1244">3 (not 2!)</span><span class="sxs-lookup"><span data-stu-id="442a8-1244">3 (not 2!)</span></span> |
| `countof("ababa", "ab", "normal")` |<span data-ttu-id="442a8-1245">2</span><span class="sxs-lookup"><span data-stu-id="442a8-1245">2</span></span> |
| `countof("ababa", "aba")` |<span data-ttu-id="442a8-1246">2</span><span class="sxs-lookup"><span data-stu-id="442a8-1246">2</span></span> |
| `countof("ababa", "aba", "regex")` |<span data-ttu-id="442a8-1247">1</span><span class="sxs-lookup"><span data-stu-id="442a8-1247">1</span></span> |
| `countof("abcabc", "a.c", "regex")` |<span data-ttu-id="442a8-1248">2</span><span class="sxs-lookup"><span data-stu-id="442a8-1248">2</span></span> |

### <a name="extract"></a><span data-ttu-id="442a8-1249">extract</span><span class="sxs-lookup"><span data-stu-id="442a8-1249">extract</span></span>
    extract("x=([0-9.]+)", 1, "hello x=45.6|wo") == "45.6"

<span data-ttu-id="442a8-1250">Get a match for a [regular expression](#regular-expressions) from a text string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1250">Get a match for a [regular expression](#regular-expressions) from a text string.</span></span> <span data-ttu-id="442a8-1251">Optionally, it then converts the extracted substring to the indicated type.</span><span class="sxs-lookup"><span data-stu-id="442a8-1251">Optionally, it then converts the extracted substring to the indicated type.</span></span>

<span data-ttu-id="442a8-1252">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1252">**Syntax**</span></span>

    extract(regex, captureGroup, text [, typeLiteral])

<span data-ttu-id="442a8-1253">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1253">**Arguments**</span></span>

* <span data-ttu-id="442a8-1254">*regex:* A [regular expression](#regular-expressions).</span><span class="sxs-lookup"><span data-stu-id="442a8-1254">*regex:* A [regular expression](#regular-expressions).</span></span>
* <span data-ttu-id="442a8-1255">*captureGroup:* A positive `int` constant indicating the capture group to extract.</span><span class="sxs-lookup"><span data-stu-id="442a8-1255">*captureGroup:* A positive `int` constant indicating the capture group to extract.</span></span> <span data-ttu-id="442a8-1256">0 stands for the entire match, 1 for the value matched by the first '('parenthesis')' in the regular expression, 2 or more for subsequent parentheses.</span><span class="sxs-lookup"><span data-stu-id="442a8-1256">0 stands for the entire match, 1 for the value matched by the first '('parenthesis')' in the regular expression, 2 or more for subsequent parentheses.</span></span>
* <span data-ttu-id="442a8-1257">*text:* A `string` to search.</span><span class="sxs-lookup"><span data-stu-id="442a8-1257">*text:* A `string` to search.</span></span>
* <span data-ttu-id="442a8-1258">*typeLiteral:* An optional type literal (e.g., `typeof(long)`).</span><span class="sxs-lookup"><span data-stu-id="442a8-1258">*typeLiteral:* An optional type literal (e.g., `typeof(long)`).</span></span> <span data-ttu-id="442a8-1259">If provided, the extracted substring is converted to this type.</span><span class="sxs-lookup"><span data-stu-id="442a8-1259">If provided, the extracted substring is converted to this type.</span></span> 

<span data-ttu-id="442a8-1260">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1260">**Returns**</span></span>

<span data-ttu-id="442a8-1261">If *regex* finds a match in *text*: the substring matched against the indicated capture group *captureGroup*, optionally converted to *typeLiteral*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1261">If *regex* finds a match in *text*: the substring matched against the indicated capture group *captureGroup*, optionally converted to *typeLiteral*.</span></span>

<span data-ttu-id="442a8-1262">If there's no match, or the type conversion fails: `null`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1262">If there's no match, or the type conversion fails: `null`.</span></span> 

<span data-ttu-id="442a8-1263">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1263">**Examples**</span></span>

<span data-ttu-id="442a8-1264">The example string `Trace` is searched for a definition for `Duration`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1264">The example string `Trace` is searched for a definition for `Duration`.</span></span> <span data-ttu-id="442a8-1265">The match is converted to `real`, then multiplied it by a time constant (`1s`) so that `Duration` is of type `timespan`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1265">The match is converted to `real`, then multiplied it by a time constant (`1s`) so that `Duration` is of type `timespan`.</span></span> <span data-ttu-id="442a8-1266">In this example, it is equal to 123.45 seconds:</span><span class="sxs-lookup"><span data-stu-id="442a8-1266">In this example, it is equal to 123.45 seconds:</span></span>

```AIQL
...
| extend Trace="A=1, B=2, Duration=123.45, ..."
| extend Duration = extract("Duration=([0-9.]+)", 1, Trace, typeof(real)) * time(1s) 
```

<span data-ttu-id="442a8-1267">This example is equivalent to `substring(Text, 2, 4)`:</span><span class="sxs-lookup"><span data-stu-id="442a8-1267">This example is equivalent to `substring(Text, 2, 4)`:</span></span>

```AIQL
extract("^.{2,2}(.{4,4})", 1, Text)
```

<a name="notempty"></a>
<a name="isnotempty"></a>
<a name="isempty"></a>



### <a name="isempty-isnotempty-notempty"></a><span data-ttu-id="442a8-1268">isempty, isnotempty, notempty</span><span class="sxs-lookup"><span data-stu-id="442a8-1268">isempty, isnotempty, notempty</span></span>
    isempty("") == true

<span data-ttu-id="442a8-1269">True if the argument is an empty string or is null.</span><span class="sxs-lookup"><span data-stu-id="442a8-1269">True if the argument is an empty string or is null.</span></span>
<span data-ttu-id="442a8-1270">See also [isnull](#isnull).</span><span class="sxs-lookup"><span data-stu-id="442a8-1270">See also [isnull](#isnull).</span></span>

<span data-ttu-id="442a8-1271">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1271">**Syntax**</span></span>

    isempty([value])


    isnotempty([value])


    notempty([value]) // alias of isnotempty

<span data-ttu-id="442a8-1272">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1272">**Returns**</span></span>

<span data-ttu-id="442a8-1273">Indicates whether the argument is an empty string or isnull.</span><span class="sxs-lookup"><span data-stu-id="442a8-1273">Indicates whether the argument is an empty string or isnull.</span></span>

| <span data-ttu-id="442a8-1274">x</span><span class="sxs-lookup"><span data-stu-id="442a8-1274">x</span></span> | <span data-ttu-id="442a8-1275">isempty(x)</span><span class="sxs-lookup"><span data-stu-id="442a8-1275">isempty(x)</span></span> |
| --- | --- |
| <span data-ttu-id="442a8-1276">""</span><span class="sxs-lookup"><span data-stu-id="442a8-1276">""</span></span> |<span data-ttu-id="442a8-1277">true</span><span class="sxs-lookup"><span data-stu-id="442a8-1277">true</span></span> |
| <span data-ttu-id="442a8-1278">"x"</span><span class="sxs-lookup"><span data-stu-id="442a8-1278">"x"</span></span> |<span data-ttu-id="442a8-1279">false</span><span class="sxs-lookup"><span data-stu-id="442a8-1279">false</span></span> |
| <span data-ttu-id="442a8-1280">parsejson("")</span><span class="sxs-lookup"><span data-stu-id="442a8-1280">parsejson("")</span></span> |<span data-ttu-id="442a8-1281">true</span><span class="sxs-lookup"><span data-stu-id="442a8-1281">true</span></span> |
| <span data-ttu-id="442a8-1282">parsejson("[]")</span><span class="sxs-lookup"><span data-stu-id="442a8-1282">parsejson("[]")</span></span> |<span data-ttu-id="442a8-1283">false</span><span class="sxs-lookup"><span data-stu-id="442a8-1283">false</span></span> |
| <span data-ttu-id="442a8-1284">parsejson("{}")</span><span class="sxs-lookup"><span data-stu-id="442a8-1284">parsejson("{}")</span></span> |<span data-ttu-id="442a8-1285">false</span><span class="sxs-lookup"><span data-stu-id="442a8-1285">false</span></span> |

<span data-ttu-id="442a8-1286">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1286">**Example**</span></span>

    T | where isempty(fieldName) | count


### <a name="parseurl"></a><span data-ttu-id="442a8-1287">parseurl</span><span class="sxs-lookup"><span data-stu-id="442a8-1287">parseurl</span></span>
<span data-ttu-id="442a8-1288">Split a URL into its parts.</span><span class="sxs-lookup"><span data-stu-id="442a8-1288">Split a URL into its parts.</span></span>

<span data-ttu-id="442a8-1289">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1289">**Syntax**</span></span>

    parseurl(urlstring)

<span data-ttu-id="442a8-1290">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1290">**Arguments**</span></span>

* <span data-ttu-id="442a8-1291">*urlstring:* A URL.</span><span class="sxs-lookup"><span data-stu-id="442a8-1291">*urlstring:* A URL.</span></span>

<span data-ttu-id="442a8-1292">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1292">**Returns**</span></span>

<span data-ttu-id="442a8-1293">An object containing the parts as strings.</span><span class="sxs-lookup"><span data-stu-id="442a8-1293">An object containing the parts as strings.</span></span>

<span data-ttu-id="442a8-1294">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1294">**Example**</span></span>

    parseurl("http://user:pass@contoso.com/icecream/buy.aspx?a=1&b=2#tag")

    {
    "Scheme" : "http",
    "Host" : "contoso.com",
    "Port" : "80",
    "Path" : "/icecream/buy.aspx",
    "Username" : "user",
    "Password" : "pass",
    "Query Parameters" : {"a":"1","b":"2"},
    "Fragment" : "tag"
    }

### <a name="replace"></a><span data-ttu-id="442a8-1295">replace</span><span class="sxs-lookup"><span data-stu-id="442a8-1295">replace</span></span>
<span data-ttu-id="442a8-1296">Replace all regex matches with another string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1296">Replace all regex matches with another string.</span></span>

<span data-ttu-id="442a8-1297">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1297">**Syntax**</span></span>

    replace(regex, rewrite, text)

<span data-ttu-id="442a8-1298">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1298">**Arguments**</span></span>

* <span data-ttu-id="442a8-1299">*regex:* The [regular expression](https://github.com/google/re2/wiki/Syntax) to search *text*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1299">*regex:* The [regular expression](https://github.com/google/re2/wiki/Syntax) to search *text*.</span></span> <span data-ttu-id="442a8-1300">It can contain capture groups in '('parentheses')'.</span><span class="sxs-lookup"><span data-stu-id="442a8-1300">It can contain capture groups in '('parentheses')'.</span></span> 
* <span data-ttu-id="442a8-1301">*rewrite:* The replacement regex for any match made by *matchingRegex*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1301">*rewrite:* The replacement regex for any match made by *matchingRegex*.</span></span> <span data-ttu-id="442a8-1302">Use `\0` to refer to the whole match, `\1` for the first capture group, `\2` and so on for subsequent capture groups.</span><span class="sxs-lookup"><span data-stu-id="442a8-1302">Use `\0` to refer to the whole match, `\1` for the first capture group, `\2` and so on for subsequent capture groups.</span></span>
* <span data-ttu-id="442a8-1303">*text:* A string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1303">*text:* A string.</span></span>

<span data-ttu-id="442a8-1304">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1304">**Returns**</span></span>

<span data-ttu-id="442a8-1305">*text* after replacing all matches of *regex* with evaluations of *rewrite*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1305">*text* after replacing all matches of *regex* with evaluations of *rewrite*.</span></span> <span data-ttu-id="442a8-1306">Matches do not overlap.</span><span class="sxs-lookup"><span data-stu-id="442a8-1306">Matches do not overlap.</span></span>

<span data-ttu-id="442a8-1307">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1307">**Example**</span></span>

<span data-ttu-id="442a8-1308">This statement:</span><span class="sxs-lookup"><span data-stu-id="442a8-1308">This statement:</span></span>

```AIQL
range x from 1 to 5 step 1
| extend str=strcat('Number is ', tostring(x))
| extend replaced=replace(@'is (\d+)', @'was: \1', str)
```

<span data-ttu-id="442a8-1309">Has the following results:</span><span class="sxs-lookup"><span data-stu-id="442a8-1309">Has the following results:</span></span>

| <span data-ttu-id="442a8-1310">x</span><span class="sxs-lookup"><span data-stu-id="442a8-1310">x</span></span> | <span data-ttu-id="442a8-1311">str</span><span class="sxs-lookup"><span data-stu-id="442a8-1311">str</span></span> | <span data-ttu-id="442a8-1312">replaced</span><span class="sxs-lookup"><span data-stu-id="442a8-1312">replaced</span></span> |
| --- | --- | --- |
| <span data-ttu-id="442a8-1313">1</span><span class="sxs-lookup"><span data-stu-id="442a8-1313">1</span></span> |<span data-ttu-id="442a8-1314">Number is 1.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1314">Number is 1.000000</span></span> |<span data-ttu-id="442a8-1315">Number was: 1.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1315">Number was: 1.000000</span></span> |
| <span data-ttu-id="442a8-1316">2</span><span class="sxs-lookup"><span data-stu-id="442a8-1316">2</span></span> |<span data-ttu-id="442a8-1317">Number is 2.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1317">Number is 2.000000</span></span> |<span data-ttu-id="442a8-1318">Number was: 2.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1318">Number was: 2.000000</span></span> |
| <span data-ttu-id="442a8-1319">3</span><span class="sxs-lookup"><span data-stu-id="442a8-1319">3</span></span> |<span data-ttu-id="442a8-1320">Number is 3.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1320">Number is 3.000000</span></span> |<span data-ttu-id="442a8-1321">Number was: 3.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1321">Number was: 3.000000</span></span> |
| <span data-ttu-id="442a8-1322">4</span><span class="sxs-lookup"><span data-stu-id="442a8-1322">4</span></span> |<span data-ttu-id="442a8-1323">Number is 4.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1323">Number is 4.000000</span></span> |<span data-ttu-id="442a8-1324">Number was: 4.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1324">Number was: 4.000000</span></span> |
| <span data-ttu-id="442a8-1325">5</span><span class="sxs-lookup"><span data-stu-id="442a8-1325">5</span></span> |<span data-ttu-id="442a8-1326">Number is 5.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1326">Number is 5.000000</span></span> |<span data-ttu-id="442a8-1327">Number was: 5.000000</span><span class="sxs-lookup"><span data-stu-id="442a8-1327">Number was: 5.000000</span></span> |

### <a name="split"></a><span data-ttu-id="442a8-1328">split</span><span class="sxs-lookup"><span data-stu-id="442a8-1328">split</span></span>
    split("aaa_bbb_ccc", "_") == ["aaa","bbb","ccc"]

<span data-ttu-id="442a8-1329">Splits a given string according to a given delimiter and returns a string array with the conatined substrings.</span><span class="sxs-lookup"><span data-stu-id="442a8-1329">Splits a given string according to a given delimiter and returns a string array with the conatined substrings.</span></span> <span data-ttu-id="442a8-1330">Optionally, a specific substring can be returned if exists.</span><span class="sxs-lookup"><span data-stu-id="442a8-1330">Optionally, a specific substring can be returned if exists.</span></span>

<span data-ttu-id="442a8-1331">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1331">**Syntax**</span></span>

    split(source, delimiter [, requestedIndex])

<span data-ttu-id="442a8-1332">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1332">**Arguments**</span></span>

* <span data-ttu-id="442a8-1333">*source*: The source string that will be splitted according to the given delimiter.</span><span class="sxs-lookup"><span data-stu-id="442a8-1333">*source*: The source string that will be splitted according to the given delimiter.</span></span>
* <span data-ttu-id="442a8-1334">*delimiter*: The delimiter that will be used in order to split the source string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1334">*delimiter*: The delimiter that will be used in order to split the source string.</span></span>
* <span data-ttu-id="442a8-1335">*requestedIndex*: An optional zero-based index `int`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1335">*requestedIndex*: An optional zero-based index `int`.</span></span> <span data-ttu-id="442a8-1336">If provided, the returned string array will contain the requested substring if exists.</span><span class="sxs-lookup"><span data-stu-id="442a8-1336">If provided, the returned string array will contain the requested substring if exists.</span></span> 

<span data-ttu-id="442a8-1337">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1337">**Returns**</span></span>

<span data-ttu-id="442a8-1338">A string array that contains the substrings of the given source string that are delimited by the given delimiter.</span><span class="sxs-lookup"><span data-stu-id="442a8-1338">A string array that contains the substrings of the given source string that are delimited by the given delimiter.</span></span>

<span data-ttu-id="442a8-1339">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1339">**Examples**</span></span>

```
split("aa_bb", "_")           // ["aa","bb"]
split("aaa_bbb_ccc", "_", 1)  // ["bbb"]
split("", "_")                // [""]
split("a__b")                 // ["a","","b"]
split("aabbcc", "bb")         // ["aa","cc"]
```




### <a name="strcat"></a><span data-ttu-id="442a8-1340">strcat</span><span class="sxs-lookup"><span data-stu-id="442a8-1340">strcat</span></span>
    strcat("hello", " ", "world")

<span data-ttu-id="442a8-1341">Concatenates between 1 and 16 arguments, which must be strings.</span><span class="sxs-lookup"><span data-stu-id="442a8-1341">Concatenates between 1 and 16 arguments, which must be strings.</span></span>

### <a name="strlen"></a><span data-ttu-id="442a8-1342">strlen</span><span class="sxs-lookup"><span data-stu-id="442a8-1342">strlen</span></span>
    strlen("hello") == 5

<span data-ttu-id="442a8-1343">Length of a string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1343">Length of a string.</span></span>

### <a name="substring"></a><span data-ttu-id="442a8-1344">substring</span><span class="sxs-lookup"><span data-stu-id="442a8-1344">substring</span></span>
    substring("abcdefg", 1, 2) == "bc"

<span data-ttu-id="442a8-1345">Extract a substring from a given source string starting from a given index.</span><span class="sxs-lookup"><span data-stu-id="442a8-1345">Extract a substring from a given source string starting from a given index.</span></span> <span data-ttu-id="442a8-1346">Optionally, the length of the requested substring can be specified.</span><span class="sxs-lookup"><span data-stu-id="442a8-1346">Optionally, the length of the requested substring can be specified.</span></span>

<span data-ttu-id="442a8-1347">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1347">**Syntax**</span></span>

    substring(source, startingIndex [, length])

<span data-ttu-id="442a8-1348">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1348">**Arguments**</span></span>

* <span data-ttu-id="442a8-1349">*source:* The source string that the substring will be taken from.</span><span class="sxs-lookup"><span data-stu-id="442a8-1349">*source:* The source string that the substring will be taken from.</span></span>
* <span data-ttu-id="442a8-1350">*startingIndex:* The zero-based starting character position of the requested substring.</span><span class="sxs-lookup"><span data-stu-id="442a8-1350">*startingIndex:* The zero-based starting character position of the requested substring.</span></span>
* <span data-ttu-id="442a8-1351">*length:* An optional parameter that can be used to specify the requested number of characters in the substring.</span><span class="sxs-lookup"><span data-stu-id="442a8-1351">*length:* An optional parameter that can be used to specify the requested number of characters in the substring.</span></span> 

<span data-ttu-id="442a8-1352">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1352">**Returns**</span></span>

<span data-ttu-id="442a8-1353">A substring from the given string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1353">A substring from the given string.</span></span> <span data-ttu-id="442a8-1354">The substring starts at startingIndex (zero-based) character position and continues to the end of the string or length characters if specified.</span><span class="sxs-lookup"><span data-stu-id="442a8-1354">The substring starts at startingIndex (zero-based) character position and continues to the end of the string or length characters if specified.</span></span>

<span data-ttu-id="442a8-1355">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1355">**Examples**</span></span>

```
substring("123456", 1)        // 23456
substring("123456", 2, 2)     // 34
substring("ABCD", 0, 2)       // AB
```

### <a name="tolower"></a><span data-ttu-id="442a8-1356">tolower</span><span class="sxs-lookup"><span data-stu-id="442a8-1356">tolower</span></span>
    tolower("HELLO") == "hello"

<span data-ttu-id="442a8-1357">Converts a string to lower case.</span><span class="sxs-lookup"><span data-stu-id="442a8-1357">Converts a string to lower case.</span></span>

### <a name="toupper"></a><span data-ttu-id="442a8-1358">toupper</span><span class="sxs-lookup"><span data-stu-id="442a8-1358">toupper</span></span>
    toupper("hello") == "HELLO"

<span data-ttu-id="442a8-1359">Converts a string to upper case.</span><span class="sxs-lookup"><span data-stu-id="442a8-1359">Converts a string to upper case.</span></span>

### <a name="guids"></a><span data-ttu-id="442a8-1360">GUIDs</span><span class="sxs-lookup"><span data-stu-id="442a8-1360">GUIDs</span></span>
    guid(00000000-1111-2222-3333-055567f333de)


## <a name="arrays-objects-and-dynamic"></a><span data-ttu-id="442a8-1361">Arrays, objects and dynamic</span><span class="sxs-lookup"><span data-stu-id="442a8-1361">Arrays, objects and dynamic</span></span>
<span data-ttu-id="442a8-1362">[literals](#dynamic-literals) | [casting](#casting-dynamic-objects) | [operators](#operators) | [let clauses](#dynamic-objects-in-let-clauses)</span><span class="sxs-lookup"><span data-stu-id="442a8-1362">[literals](#dynamic-literals) | [casting](#casting-dynamic-objects) | [operators](#operators) | [let clauses](#dynamic-objects-in-let-clauses)</span></span>
<br/>
<span data-ttu-id="442a8-1363">[arraylength](#arraylength) | [extractjson](#extractjson) | [parsejson](#parsejson) | [range](#range) | [treepath](#treepath) | [todynamic](#todynamic) | [zip](#zip)</span><span class="sxs-lookup"><span data-stu-id="442a8-1363">[arraylength](#arraylength) | [extractjson](#extractjson) | [parsejson](#parsejson) | [range](#range) | [treepath](#treepath) | [todynamic](#todynamic) | [zip](#zip)</span></span>

<span data-ttu-id="442a8-1364">Here's the result of a query on an Application Insights exception.</span><span class="sxs-lookup"><span data-stu-id="442a8-1364">Here's the result of a query on an Application Insights exception.</span></span> <span data-ttu-id="442a8-1365">The value in `details` is an array.</span><span class="sxs-lookup"><span data-stu-id="442a8-1365">The value in `details` is an array.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/310.png)

<span data-ttu-id="442a8-1366">**Indexing:** Index arrays and objects just as in JavaScript:</span><span class="sxs-lookup"><span data-stu-id="442a8-1366">**Indexing:** Index arrays and objects just as in JavaScript:</span></span>

    exceptions | take 1
    | extend 
        line = details[0].parsedStack[0].line,
        stackdepth = arraylength(details[0].parsedStack)

* <span data-ttu-id="442a8-1367">But use `arraylength` and other Analytics functions (not ".length"!)</span><span class="sxs-lookup"><span data-stu-id="442a8-1367">But use `arraylength` and other Analytics functions (not ".length"!)</span></span>

<span data-ttu-id="442a8-1368">**Casting** In some cases it's necessary to cast an element that you extract from an object, because its type could vary.</span><span class="sxs-lookup"><span data-stu-id="442a8-1368">**Casting** In some cases it's necessary to cast an element that you extract from an object, because its type could vary.</span></span> <span data-ttu-id="442a8-1369">For example, `summarize...to` needs a specific type:</span><span class="sxs-lookup"><span data-stu-id="442a8-1369">For example, `summarize...to` needs a specific type:</span></span>

    exceptions 
    | summarize count() 
      by toint(details[0].parsedStack[0].line)

    exceptions
    | summarize count()
      by tostring(details[0].parsedStack[0].assembly)

<span data-ttu-id="442a8-1370">**Literals** To create an explicit array or property-bag object, write it as a JSON string and cast:</span><span class="sxs-lookup"><span data-stu-id="442a8-1370">**Literals** To create an explicit array or property-bag object, write it as a JSON string and cast:</span></span>

    todynamic('[{"x":"1", "y":"32"}, {"x":"6", "y":"44"}]')


<span data-ttu-id="442a8-1371">**mvexpand:** To pull apart the properties of an object into separate rows, use mvexpand:</span><span class="sxs-lookup"><span data-stu-id="442a8-1371">**mvexpand:** To pull apart the properties of an object into separate rows, use mvexpand:</span></span>

    exceptions | take 1
    | mvexpand details[0].parsedStack[0]


![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/410.png)

<span data-ttu-id="442a8-1372">**treepath:** To find all the paths in a complex object:</span><span class="sxs-lookup"><span data-stu-id="442a8-1372">**treepath:** To find all the paths in a complex object:</span></span>

    exceptions | take 1 | project timestamp, details
    | extend path = treepath(details)
    | mvexpand path


![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-reference/420.png)

<span data-ttu-id="442a8-1373">**buildschema:** To find the minimum schema that admits all values of the expression in the table:</span><span class="sxs-lookup"><span data-stu-id="442a8-1373">**buildschema:** To find the minimum schema that admits all values of the expression in the table:</span></span>

    exceptions | summarize buildschema(details)

<span data-ttu-id="442a8-1374">Result:</span><span class="sxs-lookup"><span data-stu-id="442a8-1374">Result:</span></span>

    { "indexer":
     {"id":"string",
       "parsedStack":
       { "indexer":
         {  "level":"int",
            "assembly":"string",
            "fileName":"string",
            "method":"string",
            "line":"int"
         }},
      "outerId":"string",
      "message":"string",
      "type":"string",
      "rawStack":"string"
    }}

<span data-ttu-id="442a8-1375">Notice that `indexer` is used to mark where you should use a numeric index.</span><span class="sxs-lookup"><span data-stu-id="442a8-1375">Notice that `indexer` is used to mark where you should use a numeric index.</span></span> <span data-ttu-id="442a8-1376">For this schema, some valid paths would be (assuming these example indexes are in range):</span><span class="sxs-lookup"><span data-stu-id="442a8-1376">For this schema, some valid paths would be (assuming these example indexes are in range):</span></span>

    details[0].parsedStack[2].level
    details[0].message
    arraylength(details)
    arraylength(details[0].parsedStack)



### <a name="array-and-object-literals"></a><span data-ttu-id="442a8-1377">Array and object literals</span><span class="sxs-lookup"><span data-stu-id="442a8-1377">Array and object literals</span></span>
<span data-ttu-id="442a8-1378">To create a dynamic literal, use `parsejson` (alias `todynamic`) with a JSON string argument:</span><span class="sxs-lookup"><span data-stu-id="442a8-1378">To create a dynamic literal, use `parsejson` (alias `todynamic`) with a JSON string argument:</span></span>

* <span data-ttu-id="442a8-1379">`parsejson('[43, 21, 65]')` - an array of numbers</span><span class="sxs-lookup"><span data-stu-id="442a8-1379">`parsejson('[43, 21, 65]')` - an array of numbers</span></span>
* `parsejson('{"name":"Alan", "age":21, "address":{"street":432,"postcode":"JLK32P"}}')`
* <span data-ttu-id="442a8-1380">`parsejson('21')` - a single value of dynamic type containing a number</span><span class="sxs-lookup"><span data-stu-id="442a8-1380">`parsejson('21')` - a single value of dynamic type containing a number</span></span>
* <span data-ttu-id="442a8-1381">`parsejson('"21"')` - a single value of dynamic type containing a string</span><span class="sxs-lookup"><span data-stu-id="442a8-1381">`parsejson('"21"')` - a single value of dynamic type containing a string</span></span>

<span data-ttu-id="442a8-1382">Note that, unlike JavaScript, JSON mandates the use of double-quotes (`"`) around strings.</span><span class="sxs-lookup"><span data-stu-id="442a8-1382">Note that, unlike JavaScript, JSON mandates the use of double-quotes (`"`) around strings.</span></span> <span data-ttu-id="442a8-1383">Therefore, it is generally easier to quote a JSON-encoded string literals using single-quotes (`'`).</span><span class="sxs-lookup"><span data-stu-id="442a8-1383">Therefore, it is generally easier to quote a JSON-encoded string literals using single-quotes (`'`).</span></span>

<span data-ttu-id="442a8-1384">This example creates a dynamic value and then uses its fields:</span><span class="sxs-lookup"><span data-stu-id="442a8-1384">This example creates a dynamic value and then uses its fields:</span></span>

```

T
| extend person = parsejson('{"name":"Alan", "age":21, "address":{"street":432,"postcode":"JLK32P"}}')
| extend n = person.name, add = person.address.street
```


### <a name="dynamic-object-functions"></a><span data-ttu-id="442a8-1385">Dynamic object functions</span><span class="sxs-lookup"><span data-stu-id="442a8-1385">Dynamic object functions</span></span>
|  |  |
| --- | --- |
| [<span data-ttu-id="442a8-1386">*value* `in` *array*</span><span class="sxs-lookup"><span data-stu-id="442a8-1386">*value* `in` *array*</span></span>](#in) |<span data-ttu-id="442a8-1387">*array* contains *value*</span><span class="sxs-lookup"><span data-stu-id="442a8-1387">*array* contains *value*</span></span> |
| [<span data-ttu-id="442a8-1388">*value* `!in` *array*</span><span class="sxs-lookup"><span data-stu-id="442a8-1388">*value* `!in` *array*</span></span>](#in) |<span data-ttu-id="442a8-1389">*array* does not contain *value*</span><span class="sxs-lookup"><span data-stu-id="442a8-1389">*array* does not contain *value*</span></span> |
| [<span data-ttu-id="442a8-1390">`arraylength(`array`)`</span><span class="sxs-lookup"><span data-stu-id="442a8-1390">`arraylength(`array`)`</span></span>](#arraylength) |<span data-ttu-id="442a8-1391">Null if it isn't an array</span><span class="sxs-lookup"><span data-stu-id="442a8-1391">Null if it isn't an array</span></span> |
| [<span data-ttu-id="442a8-1392">`extractjson(`path,object`)`</span><span class="sxs-lookup"><span data-stu-id="442a8-1392">`extractjson(`path,object`)`</span></span>](#extractjson) |<span data-ttu-id="442a8-1393">Uses path to navigate into object.</span><span class="sxs-lookup"><span data-stu-id="442a8-1393">Uses path to navigate into object.</span></span> |
| [<span data-ttu-id="442a8-1394">`parsejson(`source`)`</span><span class="sxs-lookup"><span data-stu-id="442a8-1394">`parsejson(`source`)`</span></span>](#parsejson) |<span data-ttu-id="442a8-1395">Turns a JSON string into a dynamic object.</span><span class="sxs-lookup"><span data-stu-id="442a8-1395">Turns a JSON string into a dynamic object.</span></span> |
| [<span data-ttu-id="442a8-1396">`range(`from,to,step`)`</span><span class="sxs-lookup"><span data-stu-id="442a8-1396">`range(`from,to,step`)`</span></span>](#range) |<span data-ttu-id="442a8-1397">An array of values</span><span class="sxs-lookup"><span data-stu-id="442a8-1397">An array of values</span></span> |
| [<span data-ttu-id="442a8-1398">`mvexpand` listColumn</span><span class="sxs-lookup"><span data-stu-id="442a8-1398">`mvexpand` listColumn</span></span>](#mvexpand-operator) |<span data-ttu-id="442a8-1399">Replicates a row for each value in a list in a specified cell.</span><span class="sxs-lookup"><span data-stu-id="442a8-1399">Replicates a row for each value in a list in a specified cell.</span></span> |
| [<span data-ttu-id="442a8-1400">`summarize buildschema(`column`)`</span><span class="sxs-lookup"><span data-stu-id="442a8-1400">`summarize buildschema(`column`)`</span></span>](#buildschema) |<span data-ttu-id="442a8-1401">Infers the type schema from column content</span><span class="sxs-lookup"><span data-stu-id="442a8-1401">Infers the type schema from column content</span></span> |
| [<span data-ttu-id="442a8-1402">`summarize makelist(`column`)` </span><span class="sxs-lookup"><span data-stu-id="442a8-1402">`summarize makelist(`column`)` </span></span>](#makelist) |<span data-ttu-id="442a8-1403">Flattens groups of rows and puts the values of the column in an array.</span><span class="sxs-lookup"><span data-stu-id="442a8-1403">Flattens groups of rows and puts the values of the column in an array.</span></span> |
| [<span data-ttu-id="442a8-1404">`summarize makeset(`column`)`</span><span class="sxs-lookup"><span data-stu-id="442a8-1404">`summarize makeset(`column`)`</span></span>](#makeset) |<span data-ttu-id="442a8-1405">Flattens groups of rows and puts the values of the column in an array, without duplication.</span><span class="sxs-lookup"><span data-stu-id="442a8-1405">Flattens groups of rows and puts the values of the column in an array, without duplication.</span></span> |

### <a name="dynamic-objects-in-let-clauses"></a><span data-ttu-id="442a8-1406">Dynamic objects in let clauses</span><span class="sxs-lookup"><span data-stu-id="442a8-1406">Dynamic objects in let clauses</span></span>
<span data-ttu-id="442a8-1407">[Let clauses](#let-clause) store dynamic values as strings, so these two clauses are equivalent, and both need the `parsejson` (or `todynamic`) before being used:</span><span class="sxs-lookup"><span data-stu-id="442a8-1407">[Let clauses](#let-clause) store dynamic values as strings, so these two clauses are equivalent, and both need the `parsejson` (or `todynamic`) before being used:</span></span>

    let list1 = '{"a" : "somevalue"}';
    let list2 = parsejson('{"a" : "somevalue"}');

    T | project parsejson(list1).a, parsejson(list2).a


### <a name="in"></a><span data-ttu-id="442a8-1408">in</span><span class="sxs-lookup"><span data-stu-id="442a8-1408">in</span></span>
    value in (listExpression)
    value !in (listExpression)

<span data-ttu-id="442a8-1409">Determines whether there is (not) an item in the list that is equal to the value.</span><span class="sxs-lookup"><span data-stu-id="442a8-1409">Determines whether there is (not) an item in the list that is equal to the value.</span></span> <span data-ttu-id="442a8-1410">Case-sensitive, where the value is a string.</span><span class="sxs-lookup"><span data-stu-id="442a8-1410">Case-sensitive, where the value is a string.</span></span>

<span data-ttu-id="442a8-1411">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1411">**Arguments**</span></span>

* <span data-ttu-id="442a8-1412">`value`: A scalar expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-1412">`value`: A scalar expression.</span></span>
* <span data-ttu-id="442a8-1413">`listExpression`...: A list of scalar expressions, or an expression that evaluates to a list.</span><span class="sxs-lookup"><span data-stu-id="442a8-1413">`listExpression`...: A list of scalar expressions, or an expression that evaluates to a list.</span></span> 

<span data-ttu-id="442a8-1414">A nested array is flattened into a single list - for example, `where x in (dynamic([1,[2,3]]))` becomes `where x in (1,2,3)`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1414">A nested array is flattened into a single list - for example, `where x in (dynamic([1,[2,3]]))` becomes `where x in (1,2,3)`.</span></span>  

<span data-ttu-id="442a8-1415">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1415">**Examples**</span></span>

```AIQL
    requests | where client_City in ("London", "Paris", "Rome")
```

```AIQL
let cities = dynamic(['Dublin','Redmond','Amsterdam']);
requests | where client_City in (cities) 
|  summarize count() by client_City
```

<span data-ttu-id="442a8-1416">Computed list:</span><span class="sxs-lookup"><span data-stu-id="442a8-1416">Computed list:</span></span>

```AIQL
let topCities =  toscalar ( // convert single column to value
   requests
   | summarize count() by client_City 
   | top 4 by count_ 
   | summarize makeset(client_City)) ;
requests
| where client_City in (topCities) 
| summarize count() by client_City;
```

<span data-ttu-id="442a8-1417">Using a function call as the list expression:</span><span class="sxs-lookup"><span data-stu-id="442a8-1417">Using a function call as the list expression:</span></span>

```AIQL
let topCities =  (n:int) {toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City)) };
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```
 

### <a name="arraylength"></a><span data-ttu-id="442a8-1418">arraylength</span><span class="sxs-lookup"><span data-stu-id="442a8-1418">arraylength</span></span>
<span data-ttu-id="442a8-1419">The number of elements in a dynamic array.</span><span class="sxs-lookup"><span data-stu-id="442a8-1419">The number of elements in a dynamic array.</span></span>

<span data-ttu-id="442a8-1420">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1420">**Syntax**</span></span>

    arraylength(array)

<span data-ttu-id="442a8-1421">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1421">**Arguments**</span></span>

* <span data-ttu-id="442a8-1422">*array:* A `dynamic` value.</span><span class="sxs-lookup"><span data-stu-id="442a8-1422">*array:* A `dynamic` value.</span></span>

<span data-ttu-id="442a8-1423">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1423">**Returns**</span></span>

<span data-ttu-id="442a8-1424">The number of elements in *array*, or `null` if *array* is not an array.</span><span class="sxs-lookup"><span data-stu-id="442a8-1424">The number of elements in *array*, or `null` if *array* is not an array.</span></span>

<span data-ttu-id="442a8-1425">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1425">**Examples**</span></span>

```
arraylength(parsejson('[1, 2, 3, "four"]')) == 4
arraylength(parsejson('[8]')) == 1
arraylength(parsejson('[{}]')) == 1
arraylength(parsejson('[]')) == 0
arraylength(parsejson('{}')) == null
arraylength(parsejson('21')) == null
```



### <a name="extractjson"></a><span data-ttu-id="442a8-1426">extractjson</span><span class="sxs-lookup"><span data-stu-id="442a8-1426">extractjson</span></span>
    extractjson("$.hosts[1].AvailableMB", EventText, typeof(int))

<span data-ttu-id="442a8-1427">Get a specified element out of a JSON text using a path expression.</span><span class="sxs-lookup"><span data-stu-id="442a8-1427">Get a specified element out of a JSON text using a path expression.</span></span> <span data-ttu-id="442a8-1428">Optionally convert the extracted string to a specific type.</span><span class="sxs-lookup"><span data-stu-id="442a8-1428">Optionally convert the extracted string to a specific type.</span></span>

<span data-ttu-id="442a8-1429">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1429">**Syntax**</span></span>

```

    string extractjson(jsonPath, dataSource) 
    resulttype extractjson(jsonPath, dataSource, typeof(resulttype))
```


<span data-ttu-id="442a8-1430">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1430">**Returns**</span></span>

<span data-ttu-id="442a8-1431">This function performs a JsonPath query into dataSource which contains a valid JSON string, optionally converting that value to another type depending on the third argument.</span><span class="sxs-lookup"><span data-stu-id="442a8-1431">This function performs a JsonPath query into dataSource which contains a valid JSON string, optionally converting that value to another type depending on the third argument.</span></span>

<span data-ttu-id="442a8-1432">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1432">**Example**</span></span>

<span data-ttu-id="442a8-1433">The [bracket] notation and dot notation are equivalent:</span><span class="sxs-lookup"><span data-stu-id="442a8-1433">The [bracket] notation and dot notation are equivalent:</span></span>

    ... | extend AvailableMB = extractjson("$.hosts[1].AvailableMB", EventText, typeof(int)) | ...

    ... | extend AvailableMD = extractjson("$['hosts'][1]['AvailableMB']", EventText, typeof(int)) | ...



<span data-ttu-id="442a8-1434">**Performance tips**</span><span class="sxs-lookup"><span data-stu-id="442a8-1434">**Performance tips**</span></span>

* <span data-ttu-id="442a8-1435">Apply where-clauses before using `extractjson()`</span><span class="sxs-lookup"><span data-stu-id="442a8-1435">Apply where-clauses before using `extractjson()`</span></span>
* <span data-ttu-id="442a8-1436">Consider using a regular expression match with [extract](#extract) instead.</span><span class="sxs-lookup"><span data-stu-id="442a8-1436">Consider using a regular expression match with [extract](#extract) instead.</span></span> <span data-ttu-id="442a8-1437">This can run very much faster, and is effective if the JSON is produced from a template.</span><span class="sxs-lookup"><span data-stu-id="442a8-1437">This can run very much faster, and is effective if the JSON is produced from a template.</span></span>
* <span data-ttu-id="442a8-1438">Use `parsejson()` if you need to extract more than one value from the JSON.</span><span class="sxs-lookup"><span data-stu-id="442a8-1438">Use `parsejson()` if you need to extract more than one value from the JSON.</span></span>
* <span data-ttu-id="442a8-1439">Consider having the JSON parsed at ingestion by declaring the type of the column to be dynamic.</span><span class="sxs-lookup"><span data-stu-id="442a8-1439">Consider having the JSON parsed at ingestion by declaring the type of the column to be dynamic.</span></span>

### <a name="json-path-expressions"></a><span data-ttu-id="442a8-1440">JSON Path expressions</span><span class="sxs-lookup"><span data-stu-id="442a8-1440">JSON Path expressions</span></span>
|  |  |
| --- | --- |
| `$` |<span data-ttu-id="442a8-1441">Root object</span><span class="sxs-lookup"><span data-stu-id="442a8-1441">Root object</span></span> |
| `@` |<span data-ttu-id="442a8-1442">Current object</span><span class="sxs-lookup"><span data-stu-id="442a8-1442">Current object</span></span> |
| `[0]` |<span data-ttu-id="442a8-1443">Array subscript</span><span class="sxs-lookup"><span data-stu-id="442a8-1443">Array subscript</span></span> |
| <span data-ttu-id="442a8-1444">`.` or `[0]`</span><span class="sxs-lookup"><span data-stu-id="442a8-1444">`.` or `[0]`</span></span> |<span data-ttu-id="442a8-1445">Child</span><span class="sxs-lookup"><span data-stu-id="442a8-1445">Child</span></span> |

<span data-ttu-id="442a8-1446">*(We don't currently implement wildcards, recursion, union, or slices.)*</span><span class="sxs-lookup"><span data-stu-id="442a8-1446">*(We don't currently implement wildcards, recursion, union, or slices.)*</span></span>

### <a name="parsejson"></a><span data-ttu-id="442a8-1447">parsejson</span><span class="sxs-lookup"><span data-stu-id="442a8-1447">parsejson</span></span>
<span data-ttu-id="442a8-1448">Interprets a `string` as a [JSON value](http://json.org/)) and returns the value as `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="442a8-1448">Interprets a `string` as a [JSON value](http://json.org/)) and returns the value as `dynamic`.</span></span> <span data-ttu-id="442a8-1449">It is superior to using `extractjson()` when you need to extract more than one element of a JSON compound object.</span><span class="sxs-lookup"><span data-stu-id="442a8-1449">It is superior to using `extractjson()` when you need to extract more than one element of a JSON compound object.</span></span>

<span data-ttu-id="442a8-1450">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1450">**Syntax**</span></span>

    parsejson(json)

<span data-ttu-id="442a8-1451">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1451">**Arguments**</span></span>

* <span data-ttu-id="442a8-1452">*json:* A JSON document.</span><span class="sxs-lookup"><span data-stu-id="442a8-1452">*json:* A JSON document.</span></span>

<span data-ttu-id="442a8-1453">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1453">**Returns**</span></span>

<span data-ttu-id="442a8-1454">An object of type `dynamic` specified by *json*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1454">An object of type `dynamic` specified by *json*.</span></span>

<span data-ttu-id="442a8-1455">**Example**</span><span class="sxs-lookup"><span data-stu-id="442a8-1455">**Example**</span></span>

<span data-ttu-id="442a8-1456">In the following example, when `context_custom_metrics` is a `string` that looks like this:</span><span class="sxs-lookup"><span data-stu-id="442a8-1456">In the following example, when `context_custom_metrics` is a `string` that looks like this:</span></span> 

```
{"duration":{"value":118.0,"count":5.0,"min":100.0,"max":150.0,"stdDev":0.0,"sampledValue":118.0,"sum":118.0}}
```

<span data-ttu-id="442a8-1457">then the following fragment retrieves the value of the `duration` slot in the object, and from that it retrieves two slots, `duration.value` and `duration.min` (`118.0` and `110.0`, respectively).</span><span class="sxs-lookup"><span data-stu-id="442a8-1457">then the following fragment retrieves the value of the `duration` slot in the object, and from that it retrieves two slots, `duration.value` and `duration.min` (`118.0` and `110.0`, respectively).</span></span>

```AIQL
T
| ...
| extend d=parsejson(context_custom_metrics) 
| extend duration_value=d.duration.value, duration_min=d["duration"]["min"]
```



### <a name="range"></a><span data-ttu-id="442a8-1458">range</span><span class="sxs-lookup"><span data-stu-id="442a8-1458">range</span></span>
<span data-ttu-id="442a8-1459">The `range()` function (not to be confused with the `range` operator) generates a dynamic array holding a series of equally-spaced values.</span><span class="sxs-lookup"><span data-stu-id="442a8-1459">The `range()` function (not to be confused with the `range` operator) generates a dynamic array holding a series of equally-spaced values.</span></span>

<span data-ttu-id="442a8-1460">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="442a8-1460">**Syntax**</span></span>

    range(start, stop, step)

<span data-ttu-id="442a8-1461">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="442a8-1461">**Arguments**</span></span>

* <span data-ttu-id="442a8-1462">*start:* The value of the first element in the resulting array.</span><span class="sxs-lookup"><span data-stu-id="442a8-1462">*start:* The value of the first element in the resulting array.</span></span> 
* <span data-ttu-id="442a8-1463">*stop:* The value of the last element in the resulting array, or the least value that is greater than the last element in the resulting array and within an integer multiple of *step* from *start*.</span><span class="sxs-lookup"><span data-stu-id="442a8-1463">*stop:* The value of the last element in the resulting array, or the least value that is greater than the last element in the resulting array and within an integer multiple of *step* from *start*.</span></span>
* <span data-ttu-id="442a8-1464">*step:* The difference between two consecutive elements of the array.</span><span class="sxs-lookup"><span data-stu-id="442a8-1464">*step:* The difference between two consecutive elements of the array.</span></span>

<span data-ttu-id="442a8-1465">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1465">**Examples**</span></span>

<span data-ttu-id="442a8-1466">The following example returns `[1, 4, 7]`:</span><span class="sxs-lookup"><span data-stu-id="442a8-1466">The following example returns `[1, 4, 7]`:</span></span>

```AIQL
range(1, 8, 3)
```

<span data-ttu-id="442a8-1467">The following example returns an array holding all days in the year 2015:</span><span class="sxs-lookup"><span data-stu-id="442a8-1467">The following example returns an array holding all days in the year 2015:</span></span>

```AIQL

    range(datetime(2015-01-01), datetime(2015-12-31), 1d)
```

### <a name="todynamic"></a><span data-ttu-id="442a8-1468">todynamic</span><span class="sxs-lookup"><span data-stu-id="442a8-1468">todynamic</span></span>
    todynamic('{"a":"a1", "b":["b1", "b2"]}')

<span data-ttu-id="442a8-1469">Converts a string to a dynamic value.</span><span class="sxs-lookup"><span data-stu-id="442a8-1469">Converts a string to a dynamic value.</span></span>

### <a name="treepath"></a><span data-ttu-id="442a8-1470">treepath</span><span class="sxs-lookup"><span data-stu-id="442a8-1470">treepath</span></span>
    treepath(dynamic_object)

<span data-ttu-id="442a8-1471">Enumerates all the path expressions that identify leaves in a dynamic object.</span><span class="sxs-lookup"><span data-stu-id="442a8-1471">Enumerates all the path expressions that identify leaves in a dynamic object.</span></span> 

<span data-ttu-id="442a8-1472">**Returns**</span><span class="sxs-lookup"><span data-stu-id="442a8-1472">**Returns**</span></span>

<span data-ttu-id="442a8-1473">An array of path expressions.</span><span class="sxs-lookup"><span data-stu-id="442a8-1473">An array of path expressions.</span></span>

<span data-ttu-id="442a8-1474">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1474">**Examples**</span></span>

    treepath(parsejson('{"a":"b", "c":123}')) 
    =>       ["['a']","['c']"]
    treepath(parsejson('{"prop1":[1,2,3,4], "prop2":"value2"}'))
    =>       ["['prop1']","['prop1'][0]","['prop2']"]
    treepath(parsejson('{"listProperty":[100,200,300,"abcde",{"x":"y"}]}'))
    =>       ["['listProperty']","['listProperty'][0]","['listProperty'][0]['x']"]

<span data-ttu-id="442a8-1475">Note that "[0]" indicates the presence of an array, but does not specify the index used by a specific path.</span><span class="sxs-lookup"><span data-stu-id="442a8-1475">Note that "[0]" indicates the presence of an array, but does not specify the index used by a specific path.</span></span>

### <a name="zip"></a><span data-ttu-id="442a8-1476">zip</span><span class="sxs-lookup"><span data-stu-id="442a8-1476">zip</span></span>
    zip(list1, list2, ...)

<span data-ttu-id="442a8-1477">Combines a set of lists into one list of tuples.</span><span class="sxs-lookup"><span data-stu-id="442a8-1477">Combines a set of lists into one list of tuples.</span></span>

* <span data-ttu-id="442a8-1478">`list1...`: A list of values</span><span class="sxs-lookup"><span data-stu-id="442a8-1478">`list1...`: A list of values</span></span>

<span data-ttu-id="442a8-1479">**Examples**</span><span class="sxs-lookup"><span data-stu-id="442a8-1479">**Examples**</span></span>

    zip(parsejson('[1,3,5]'), parsejson('[2,4,6]'))
    => [ [1,2], [3,4], [5,6] ]


    zip(parsejson('[1,3,5]'), parsejson('[2,4]'))
    => [ [1,2], [3,4], [5,null] ]


### <a name="names"></a><span data-ttu-id="442a8-1480">Names</span><span class="sxs-lookup"><span data-stu-id="442a8-1480">Names</span></span>
<span data-ttu-id="442a8-1481">Names can be up to 1024 characters long.</span><span class="sxs-lookup"><span data-stu-id="442a8-1481">Names can be up to 1024 characters long.</span></span> <span data-ttu-id="442a8-1482">They are case-sensitive and may contain letters, digits and underscores (`_`).</span><span class="sxs-lookup"><span data-stu-id="442a8-1482">They are case-sensitive and may contain letters, digits and underscores (`_`).</span></span> 

<span data-ttu-id="442a8-1483">Quote a name using [' ... '] or [" ... "] to include other characters or use a keyword as a name.</span><span class="sxs-lookup"><span data-stu-id="442a8-1483">Quote a name using [' ... '] or [" ... "] to include other characters or use a keyword as a name.</span></span> <span data-ttu-id="442a8-1484">For example:</span><span class="sxs-lookup"><span data-stu-id="442a8-1484">For example:</span></span>

```AIQL

    requests | 
    summarize  ["distinct urls"] = dcount(name) // non-alphanumerics
    by  ['where'] = client_City, // using a keyword as a name
        ['outcome!'] = success // non-alphanumerics
```


|  |  |
| --- | --- |
| <span data-ttu-id="442a8-1485">['path\\file\n\'x\'']</span><span class="sxs-lookup"><span data-stu-id="442a8-1485">['path\\file\n\'x\'']</span></span> |<span data-ttu-id="442a8-1486">Use \ to escape characters</span><span class="sxs-lookup"><span data-stu-id="442a8-1486">Use \ to escape characters</span></span> |
| <span data-ttu-id="442a8-1487">["d-e.=/f#\n"]</span><span class="sxs-lookup"><span data-stu-id="442a8-1487">["d-e.=/f#\n"]</span></span> | |
| <span data-ttu-id="442a8-1488">[@'path\file']</span><span class="sxs-lookup"><span data-stu-id="442a8-1488">[@'path\file']</span></span> |<span data-ttu-id="442a8-1489">No escapes - \ is literal</span><span class="sxs-lookup"><span data-stu-id="442a8-1489">No escapes - \ is literal</span></span> |
| <span data-ttu-id="442a8-1490">[@"\now & then\"]</span><span class="sxs-lookup"><span data-stu-id="442a8-1490">[@"\now & then\"]</span></span> | |
| <span data-ttu-id="442a8-1491">[where]</span><span class="sxs-lookup"><span data-stu-id="442a8-1491">[where]</span></span> |<span data-ttu-id="442a8-1492">Using a language keyword as a name</span><span class="sxs-lookup"><span data-stu-id="442a8-1492">Using a language keyword as a name</span></span> |

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]











