---
title: Aggregations in Azure Log Analytics queries| Microsoft Docs
description: Describes aggregation functions in Log Analytics queries that offer useful ways to analyze your data.
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
ms.openlocfilehash: 562fdc82e0b814fc759bda7b853492b47d073925
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857518"
---
# <a name="aggregations-in-log-analytics-queries"></a><span data-ttu-id="b6160-103">Aggregations in Log Analytics queries</span><span class="sxs-lookup"><span data-stu-id="b6160-103">Aggregations in Log Analytics queries</span></span>

> [!NOTE]
> <span data-ttu-id="b6160-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span><span class="sxs-lookup"><span data-stu-id="b6160-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span></span>

<span data-ttu-id="b6160-105">This article describes aggregation functions in Log Analytics queries that offer useful ways to analyze your data.</span><span class="sxs-lookup"><span data-stu-id="b6160-105">This article describes aggregation functions in Log Analytics queries that offer useful ways to analyze your data.</span></span> <span data-ttu-id="b6160-106">These functions all work with the `summarize` operator that produces a  table with aggregated results of the input table.</span><span class="sxs-lookup"><span data-stu-id="b6160-106">These functions all work with the `summarize` operator that produces a  table with aggregated results of the input table.</span></span>

## <a name="counts"></a><span data-ttu-id="b6160-107">Counts</span><span class="sxs-lookup"><span data-stu-id="b6160-107">Counts</span></span>

### <a name="count"></a><span data-ttu-id="b6160-108">count</span><span class="sxs-lookup"><span data-stu-id="b6160-108">count</span></span>
<span data-ttu-id="b6160-109">Count the number of rows in the result set after any filters are applied.</span><span class="sxs-lookup"><span data-stu-id="b6160-109">Count the number of rows in the result set after any filters are applied.</span></span> <span data-ttu-id="b6160-110">The following example returns the total number of rows in the _Perf_ table from the last 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="b6160-110">The following example returns the total number of rows in the _Perf_ table from the last 30 minutes.</span></span> <span data-ttu-id="b6160-111">The result is returned in a column named *count_* unless you assign it a specific name:</span><span class="sxs-lookup"><span data-stu-id="b6160-111">The result is returned in a column named *count_* unless you assign it a specific name:</span></span>


```OQL
Perf
| where TimeGenerated > ago(30m) 
| summarize count()
```

```OQL
Perf
| where TimeGenerated > ago(30m) 
| summarize num_of_records=count() 
```

<span data-ttu-id="b6160-112">A timechart visualization can be useful to see a trend over time:</span><span class="sxs-lookup"><span data-stu-id="b6160-112">A timechart visualization can be useful to see a trend over time:</span></span>

```OQL
Perf 
| where TimeGenerated > ago(30m) 
| summarize count() by bin(TimeGenerated, 5m)
| render timechart
```

<span data-ttu-id="b6160-113">The output from this example shows the perf record count trendline in 5 minutes' intervals:</span><span class="sxs-lookup"><span data-stu-id="b6160-113">The output from this example shows the perf record count trendline in 5 minutes' intervals:</span></span>

![Count trend](media/aggregations/count-trend.png)


### <a name="dcount-dcountif"></a><span data-ttu-id="b6160-115">dcount, dcountif</span><span class="sxs-lookup"><span data-stu-id="b6160-115">dcount, dcountif</span></span>
<span data-ttu-id="b6160-116">Use `dcount` and `dcountif` to count distinct values in a specific column.</span><span class="sxs-lookup"><span data-stu-id="b6160-116">Use `dcount` and `dcountif` to count distinct values in a specific column.</span></span> <span data-ttu-id="b6160-117">The following query evaluates how many distinct computers sent heartbeats in the last hour:</span><span class="sxs-lookup"><span data-stu-id="b6160-117">The following query evaluates how many distinct computers sent heartbeats in the last hour:</span></span>

```OQL
Heartbeat 
| where TimeGenerated > ago(1h) 
| summarize dcount(Computer)
```

<span data-ttu-id="b6160-118">To count only the Linux computers that sent heartbeats, use `dcountif`:</span><span class="sxs-lookup"><span data-stu-id="b6160-118">To count only the Linux computers that sent heartbeats, use `dcountif`:</span></span>

```OQL
Heartbeat 
| where TimeGenerated > ago(1h) 
| summarize dcountif(Computer, OSType=="Linux")
```

### <a name="evaluating-subgroups"></a><span data-ttu-id="b6160-119">Evaluating subgroups</span><span class="sxs-lookup"><span data-stu-id="b6160-119">Evaluating subgroups</span></span>
<span data-ttu-id="b6160-120">To perform a count or other aggregations on subgroups in your data, use the `by` keyword.</span><span class="sxs-lookup"><span data-stu-id="b6160-120">To perform a count or other aggregations on subgroups in your data, use the `by` keyword.</span></span> <span data-ttu-id="b6160-121">For example, to count the number of distinct Linux computers that sent heartbeats in each country:</span><span class="sxs-lookup"><span data-stu-id="b6160-121">For example, to count the number of distinct Linux computers that sent heartbeats in each country:</span></span>

```OQL
Heartbeat 
| where TimeGenerated > ago(1h) 
| summarize distinct_computers=dcountif(Computer, OSType=="Linux") by RemoteIPCountry
```

|<span data-ttu-id="b6160-122">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="b6160-122">RemoteIPCountry</span></span>  | <span data-ttu-id="b6160-123">distinct_computers</span><span class="sxs-lookup"><span data-stu-id="b6160-123">distinct_computers</span></span>  |
------------------|---------------------|
|<span data-ttu-id="b6160-124">United States</span><span class="sxs-lookup"><span data-stu-id="b6160-124">United States</span></span>    | <span data-ttu-id="b6160-125">19</span><span class="sxs-lookup"><span data-stu-id="b6160-125">19</span></span>                  |
|<span data-ttu-id="b6160-126">Canada</span><span class="sxs-lookup"><span data-stu-id="b6160-126">Canada</span></span>           | <span data-ttu-id="b6160-127">3</span><span class="sxs-lookup"><span data-stu-id="b6160-127">3</span></span>                   |
|<span data-ttu-id="b6160-128">Ireland</span><span class="sxs-lookup"><span data-stu-id="b6160-128">Ireland</span></span>          | <span data-ttu-id="b6160-129">0</span><span class="sxs-lookup"><span data-stu-id="b6160-129">0</span></span>                   |
|<span data-ttu-id="b6160-130">United Kingdom</span><span class="sxs-lookup"><span data-stu-id="b6160-130">United Kingdom</span></span>   | <span data-ttu-id="b6160-131">0</span><span class="sxs-lookup"><span data-stu-id="b6160-131">0</span></span>                   |
|<span data-ttu-id="b6160-132">Netherlands</span><span class="sxs-lookup"><span data-stu-id="b6160-132">Netherlands</span></span>      | <span data-ttu-id="b6160-133">2</span><span class="sxs-lookup"><span data-stu-id="b6160-133">2</span></span>                   |


<span data-ttu-id="b6160-134">To analyze even smaller subgroups of your data, add additional column names to the `by` section.</span><span class="sxs-lookup"><span data-stu-id="b6160-134">To analyze even smaller subgroups of your data, add additional column names to the `by` section.</span></span> <span data-ttu-id="b6160-135">For example, you might want to count the distinct computers from each country per OSType:</span><span class="sxs-lookup"><span data-stu-id="b6160-135">For example, you might want to count the distinct computers from each country per OSType:</span></span>

```OQL
Heartbeat 
| where TimeGenerated > ago(1h) 
| summarize distinct_computers=dcountif(Computer, OSType=="Linux") by RemoteIPCountry, OSType
```

## <a name="percentiles-and-variance"></a><span data-ttu-id="b6160-136">Percentiles and Variance</span><span class="sxs-lookup"><span data-stu-id="b6160-136">Percentiles and Variance</span></span>
<span data-ttu-id="b6160-137">When evaluating numerical values, a common practice is to average them using `summarize avg(expression)`.</span><span class="sxs-lookup"><span data-stu-id="b6160-137">When evaluating numerical values, a common practice is to average them using `summarize avg(expression)`.</span></span> <span data-ttu-id="b6160-138">Averages are affected by extreme values that characterize only a few cases.</span><span class="sxs-lookup"><span data-stu-id="b6160-138">Averages are affected by extreme values that characterize only a few cases.</span></span> <span data-ttu-id="b6160-139">To address that issue, you can use less sensitive functions such as `median` or `variance`.</span><span class="sxs-lookup"><span data-stu-id="b6160-139">To address that issue, you can use less sensitive functions such as `median` or `variance`.</span></span>

### <a name="percentile"></a><span data-ttu-id="b6160-140">Percentile</span><span class="sxs-lookup"><span data-stu-id="b6160-140">Percentile</span></span>
<span data-ttu-id="b6160-141">To find the median value, use the `percentile` function with a value to specify the percentile:</span><span class="sxs-lookup"><span data-stu-id="b6160-141">To find the median value, use the `percentile` function with a value to specify the percentile:</span></span>

```OQL
Perf
| where TimeGenerated > ago(30m) 
| where CounterName == "% Processor Time" and InstanceName == "_Total" 
| summarize percentiles(CounterValue, 50) by Computer
```

<span data-ttu-id="b6160-142">You can also specify different percentiles to get an aggregated result for each:</span><span class="sxs-lookup"><span data-stu-id="b6160-142">You can also specify different percentiles to get an aggregated result for each:</span></span>

```OQL
Perf
| where TimeGenerated > ago(30m) 
| where CounterName == "% Processor Time" and InstanceName == "_Total" 
| summarize percentiles(CounterValue, 25, 50, 75, 90) by Computer
```

<span data-ttu-id="b6160-143">This might show that some computer CPUs have similar median values, but while some are steady around the median, other computers have reported much lower and higher CPU values meaning they experienced spikes.</span><span class="sxs-lookup"><span data-stu-id="b6160-143">This might show that some computer CPUs have similar median values, but while some are steady around the median, other computers have reported much lower and higher CPU values meaning they experienced spikes.</span></span>

### <a name="variance"></a><span data-ttu-id="b6160-144">Variance</span><span class="sxs-lookup"><span data-stu-id="b6160-144">Variance</span></span>
<span data-ttu-id="b6160-145">To directly evaluate the variance of a value, use the standard deviation and variance methods:</span><span class="sxs-lookup"><span data-stu-id="b6160-145">To directly evaluate the variance of a value, use the standard deviation and variance methods:</span></span>

```OQL
Perf
| where TimeGenerated > ago(30m) 
| where CounterName == "% Processor Time" and InstanceName == "_Total" 
| summarize stdev(CounterValue), variance(CounterValue) by Computer
```

<span data-ttu-id="b6160-146">A good way to analyze the stability of the CPU usage is to combine stdev with the median calculation:</span><span class="sxs-lookup"><span data-stu-id="b6160-146">A good way to analyze the stability of the CPU usage is to combine stdev with the median calculation:</span></span>

```OQL
Perf
| where TimeGenerated > ago(130m) 
| where CounterName == "% Processor Time" and InstanceName == "_Total" 
| summarize stdev(CounterValue), percentiles(CounterValue, 50) by Computer
```

<span data-ttu-id="b6160-147">See other lessons for using the Log Analytics query language:</span><span class="sxs-lookup"><span data-stu-id="b6160-147">See other lessons for using the Log Analytics query language:</span></span>

- [<span data-ttu-id="b6160-148">String operations</span><span class="sxs-lookup"><span data-stu-id="b6160-148">String operations</span></span>](string-operations.md)
- [<span data-ttu-id="b6160-149">Date and time operations</span><span class="sxs-lookup"><span data-stu-id="b6160-149">Date and time operations</span></span>](datetime-operations.md)
- [<span data-ttu-id="b6160-150">Advanced aggregations</span><span class="sxs-lookup"><span data-stu-id="b6160-150">Advanced aggregations</span></span>](advanced-aggregations.md)
- [<span data-ttu-id="b6160-151">JSON and data structures</span><span class="sxs-lookup"><span data-stu-id="b6160-151">JSON and data structures</span></span>](json-data-structures.md)
- [<span data-ttu-id="b6160-152">Advanced query writing</span><span class="sxs-lookup"><span data-stu-id="b6160-152">Advanced query writing</span></span>](advanced-query-writing.md)
- [<span data-ttu-id="b6160-153">Joins</span><span class="sxs-lookup"><span data-stu-id="b6160-153">Joins</span></span>](joins.md)
- [<span data-ttu-id="b6160-154">Charts</span><span class="sxs-lookup"><span data-stu-id="b6160-154">Charts</span></span>](charts.md)
