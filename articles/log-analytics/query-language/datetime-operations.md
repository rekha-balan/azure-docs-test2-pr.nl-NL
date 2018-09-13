---
title: Working with date time values in Azure Log Analytics queries| Microsoft Docs
description: Describes how to work with date and time data in Log Analytics queries.
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
ms.openlocfilehash: 833548a4bfca83a8ee6971f05a4f308cc54d5b5d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868071"
---
# <a name="working-with-date-time-values-in-log-analytics-queries"></a><span data-ttu-id="b020f-103">Working with date time values in Log Analytics queries</span><span class="sxs-lookup"><span data-stu-id="b020f-103">Working with date time values in Log Analytics queries</span></span>

> [!NOTE]
> <span data-ttu-id="b020f-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span><span class="sxs-lookup"><span data-stu-id="b020f-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span></span>

<span data-ttu-id="b020f-105">This article describes how to work with date and time data in Log Analytics queries.</span><span class="sxs-lookup"><span data-stu-id="b020f-105">This article describes how to work with date and time data in Log Analytics queries.</span></span>


## <a name="date-time-basics"></a><span data-ttu-id="b020f-106">Date time basics</span><span class="sxs-lookup"><span data-stu-id="b020f-106">Date time basics</span></span>
<span data-ttu-id="b020f-107">The Log Analytics query language has two main data types associated with dates and times: datetime and timespan.</span><span class="sxs-lookup"><span data-stu-id="b020f-107">The Log Analytics query language has two main data types associated with dates and times: datetime and timespan.</span></span> <span data-ttu-id="b020f-108">All dates are expressed in UTC.</span><span class="sxs-lookup"><span data-stu-id="b020f-108">All dates are expressed in UTC.</span></span> <span data-ttu-id="b020f-109">While multiple datetime formats are supported, the ISO8601 format is preferred.</span><span class="sxs-lookup"><span data-stu-id="b020f-109">While multiple datetime formats are supported, the ISO8601 format is preferred.</span></span> 

<span data-ttu-id="b020f-110">Timespans are expressed as a decimal followed by a time unit:</span><span class="sxs-lookup"><span data-stu-id="b020f-110">Timespans are expressed as a decimal followed by a time unit:</span></span>

|<span data-ttu-id="b020f-111">shorthand</span><span class="sxs-lookup"><span data-stu-id="b020f-111">shorthand</span></span>   | <span data-ttu-id="b020f-112">time unit</span><span class="sxs-lookup"><span data-stu-id="b020f-112">time unit</span></span>    |
|:---|:---|
|<span data-ttu-id="b020f-113">d</span><span class="sxs-lookup"><span data-stu-id="b020f-113">d</span></span>           | <span data-ttu-id="b020f-114">day</span><span class="sxs-lookup"><span data-stu-id="b020f-114">day</span></span>          |
|<span data-ttu-id="b020f-115">h</span><span class="sxs-lookup"><span data-stu-id="b020f-115">h</span></span>           | <span data-ttu-id="b020f-116">hour</span><span class="sxs-lookup"><span data-stu-id="b020f-116">hour</span></span>         |
|<span data-ttu-id="b020f-117">m</span><span class="sxs-lookup"><span data-stu-id="b020f-117">m</span></span>           | <span data-ttu-id="b020f-118">minute</span><span class="sxs-lookup"><span data-stu-id="b020f-118">minute</span></span>       |
|<span data-ttu-id="b020f-119">s</span><span class="sxs-lookup"><span data-stu-id="b020f-119">s</span></span>           | <span data-ttu-id="b020f-120">second</span><span class="sxs-lookup"><span data-stu-id="b020f-120">second</span></span>       |
|<span data-ttu-id="b020f-121">ms</span><span class="sxs-lookup"><span data-stu-id="b020f-121">ms</span></span>          | <span data-ttu-id="b020f-122">millisecond</span><span class="sxs-lookup"><span data-stu-id="b020f-122">millisecond</span></span>  |
|<span data-ttu-id="b020f-123">microsecond</span><span class="sxs-lookup"><span data-stu-id="b020f-123">microsecond</span></span> | <span data-ttu-id="b020f-124">microsecond</span><span class="sxs-lookup"><span data-stu-id="b020f-124">microsecond</span></span>  |
|<span data-ttu-id="b020f-125">tick</span><span class="sxs-lookup"><span data-stu-id="b020f-125">tick</span></span>        | <span data-ttu-id="b020f-126">nanosecond</span><span class="sxs-lookup"><span data-stu-id="b020f-126">nanosecond</span></span>   |

<span data-ttu-id="b020f-127">Datetimes can be created by casting a string using the `todatetime` operator.</span><span class="sxs-lookup"><span data-stu-id="b020f-127">Datetimes can be created by casting a string using the `todatetime` operator.</span></span> <span data-ttu-id="b020f-128">For example, to review the VM heartbeats sent in a specific timeframe, you can make use of the [between operator](https://docs.loganalytics.io/docs/Language-Reference/Scalar-operators/between-operator) which is convenient to specify a time range..</span><span class="sxs-lookup"><span data-stu-id="b020f-128">For example, to review the VM heartbeats sent in a specific timeframe, you can make use of the [between operator](https://docs.loganalytics.io/docs/Language-Reference/Scalar-operators/between-operator) which is convenient to specify a time range..</span></span>

```OQL
Heartbeat
| where TimeGenerated between(datetime("2018-06-30 22:46:42") .. datetime("2018-07-01 00:57:27"))
```

<span data-ttu-id="b020f-129">Another common scenario is comparing a datetime to the present.</span><span class="sxs-lookup"><span data-stu-id="b020f-129">Another common scenario is comparing a datetime to the present.</span></span> <span data-ttu-id="b020f-130">For example, to see all heartbeats over the last two minutes, you can use the `now` operator together with a timespan that represents two minutes:</span><span class="sxs-lookup"><span data-stu-id="b020f-130">For example, to see all heartbeats over the last two minutes, you can use the `now` operator together with a timespan that represents two minutes:</span></span>

```OQL
Heartbeat
| where TimeGenerated > now() - 2m
```

<span data-ttu-id="b020f-131">A shortcut is also available for this function:</span><span class="sxs-lookup"><span data-stu-id="b020f-131">A shortcut is also available for this function:</span></span>
```OQL
Heartbeat
| where TimeGenerated > now(-2m)
```

<span data-ttu-id="b020f-132">The shortest and most readable method though is using the `ago` operator:</span><span class="sxs-lookup"><span data-stu-id="b020f-132">The shortest and most readable method though is using the `ago` operator:</span></span>
```OQL
Heartbeat
| where TimeGenerated > ago(2m)
```

<span data-ttu-id="b020f-133">Suppose that instead of knowing the start and end time, you know the start time and the duration.</span><span class="sxs-lookup"><span data-stu-id="b020f-133">Suppose that instead of knowing the start and end time, you know the start time and the duration.</span></span> <span data-ttu-id="b020f-134">You can rewrite the query as follows:</span><span class="sxs-lookup"><span data-stu-id="b020f-134">You can rewrite the query as follows:</span></span>

```OQL
let startDatetime = todatetime("2018-06-30 20:12:42.9");
let duration = totimespan(25m);
Heartbeat
| where TimeGenerated between(startDatetime .. (startDatetime+duration) )
| extend timeFromStart = TimeGenerated - startDatetime
```

## <a name="converting-time-units"></a><span data-ttu-id="b020f-135">Converting time units</span><span class="sxs-lookup"><span data-stu-id="b020f-135">Converting time units</span></span>
<span data-ttu-id="b020f-136">It can be useful to express a datetime or timespan in a time unit other than the default one.</span><span class="sxs-lookup"><span data-stu-id="b020f-136">It can be useful to express a datetime or timespan in a time unit other than the default one.</span></span> <span data-ttu-id="b020f-137">For example, suppose you're reviewing error events from the last 30 minutes, and need a calculated column that shows how long ago the event happened:</span><span class="sxs-lookup"><span data-stu-id="b020f-137">For example, suppose you're reviewing error events from the last 30 minutes, and need a calculated column that shows how long ago the event happened:</span></span>

```OQL
Event
| where TimeGenerated > ago(30m)
| where EventLevelName == "Error"
| extend timeAgo = now() - TimeGenerated 
```

<span data-ttu-id="b020f-138">You can see the _timeAgo_ column holds values such as: "00:09:31.5118992", meaning they are formatted as hh:mm:ss.fffffff.</span><span class="sxs-lookup"><span data-stu-id="b020f-138">You can see the _timeAgo_ column holds values such as: "00:09:31.5118992", meaning they are formatted as hh:mm:ss.fffffff.</span></span> <span data-ttu-id="b020f-139">If you'd like to format these values to the _numver_ of minutes since the start time, simply divide that value by "1 minute":</span><span class="sxs-lookup"><span data-stu-id="b020f-139">If you'd like to format these values to the _numver_ of minutes since the start time, simply divide that value by "1 minute":</span></span>

```OQL
Event
| where TimeGenerated > ago(30m)
| where EventLevelName == "Error"
| extend timeAgo = now() - TimeGenerated
| extend timeAgoMinutes = timeAgo/1m 
```


## <a name="aggregations-and-bucketing-by-time-intervals"></a><span data-ttu-id="b020f-140">Aggregations and bucketing by time intervals</span><span class="sxs-lookup"><span data-stu-id="b020f-140">Aggregations and bucketing by time intervals</span></span>
<span data-ttu-id="b020f-141">Another very common scenario is the need to obtain statistics over a certain time period in a particular time grain.</span><span class="sxs-lookup"><span data-stu-id="b020f-141">Another very common scenario is the need to obtain statistics over a certain time period in a particular time grain.</span></span> <span data-ttu-id="b020f-142">For this, a `bin` operator can be used as part of a summarize clause.</span><span class="sxs-lookup"><span data-stu-id="b020f-142">For this, a `bin` operator can be used as part of a summarize clause.</span></span>

<span data-ttu-id="b020f-143">Use the following query to get the number of events that occurred every 5 minutes during the last half hour:</span><span class="sxs-lookup"><span data-stu-id="b020f-143">Use the following query to get the number of events that occurred every 5 minutes during the last half hour:</span></span>

```OQL
Event
| where TimeGenerated > ago(30m)
| summarize events_count=count() by bin(TimeGenerated, 5m) 
```

<span data-ttu-id="b020f-144">This produces the following table:</span><span class="sxs-lookup"><span data-stu-id="b020f-144">This produces the following table:</span></span>  
|<span data-ttu-id="b020f-145">TimeGenerated(UTC)</span><span class="sxs-lookup"><span data-stu-id="b020f-145">TimeGenerated(UTC)</span></span>|<span data-ttu-id="b020f-146">events_count</span><span class="sxs-lookup"><span data-stu-id="b020f-146">events_count</span></span>|
|--|--|
|<span data-ttu-id="b020f-147">2018-08-01T09:30:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-147">2018-08-01T09:30:00.000</span></span>|<span data-ttu-id="b020f-148">54</span><span class="sxs-lookup"><span data-stu-id="b020f-148">54</span></span>|
|<span data-ttu-id="b020f-149">2018-08-01T09:35:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-149">2018-08-01T09:35:00.000</span></span>|<span data-ttu-id="b020f-150">41</span><span class="sxs-lookup"><span data-stu-id="b020f-150">41</span></span>|
|<span data-ttu-id="b020f-151">2018-08-01T09:40:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-151">2018-08-01T09:40:00.000</span></span>|<span data-ttu-id="b020f-152">42</span><span class="sxs-lookup"><span data-stu-id="b020f-152">42</span></span>|
|<span data-ttu-id="b020f-153">2018-08-01T09:45:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-153">2018-08-01T09:45:00.000</span></span>|<span data-ttu-id="b020f-154">41</span><span class="sxs-lookup"><span data-stu-id="b020f-154">41</span></span>|
|<span data-ttu-id="b020f-155">2018-08-01T09:50:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-155">2018-08-01T09:50:00.000</span></span>|<span data-ttu-id="b020f-156">41</span><span class="sxs-lookup"><span data-stu-id="b020f-156">41</span></span>|
|<span data-ttu-id="b020f-157">2018-08-01T09:55:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-157">2018-08-01T09:55:00.000</span></span>|<span data-ttu-id="b020f-158">16</span><span class="sxs-lookup"><span data-stu-id="b020f-158">16</span></span>|

<span data-ttu-id="b020f-159">Another way to create buckets of results is to use functions, such as `startofday`:</span><span class="sxs-lookup"><span data-stu-id="b020f-159">Another way to create buckets of results is to use functions, such as `startofday`:</span></span>

```OQL
Event
| where TimeGenerated > ago(4d)
| summarize events_count=count() by startofday(TimeGenerated) 
```

<span data-ttu-id="b020f-160">This produces the following results:</span><span class="sxs-lookup"><span data-stu-id="b020f-160">This produces the following results:</span></span>

|<span data-ttu-id="b020f-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="b020f-161">timestamp</span></span>|<span data-ttu-id="b020f-162">count_</span><span class="sxs-lookup"><span data-stu-id="b020f-162">count_</span></span>|
|--|--|
|<span data-ttu-id="b020f-163">2018-07-28T00:00:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-163">2018-07-28T00:00:00.000</span></span>|<span data-ttu-id="b020f-164">7,136</span><span class="sxs-lookup"><span data-stu-id="b020f-164">7,136</span></span>|
|<span data-ttu-id="b020f-165">2018-07-29T00:00:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-165">2018-07-29T00:00:00.000</span></span>|<span data-ttu-id="b020f-166">12,315</span><span class="sxs-lookup"><span data-stu-id="b020f-166">12,315</span></span>|
|<span data-ttu-id="b020f-167">2018-07-30T00:00:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-167">2018-07-30T00:00:00.000</span></span>|<span data-ttu-id="b020f-168">16,847</span><span class="sxs-lookup"><span data-stu-id="b020f-168">16,847</span></span>|
|<span data-ttu-id="b020f-169">2018-07-31T00:00:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-169">2018-07-31T00:00:00.000</span></span>|<span data-ttu-id="b020f-170">12,616</span><span class="sxs-lookup"><span data-stu-id="b020f-170">12,616</span></span>|
|<span data-ttu-id="b020f-171">2018-08-01T00:00:00.000</span><span class="sxs-lookup"><span data-stu-id="b020f-171">2018-08-01T00:00:00.000</span></span>|<span data-ttu-id="b020f-172">5,416</span><span class="sxs-lookup"><span data-stu-id="b020f-172">5,416</span></span>  |


## <a name="time-zones"></a><span data-ttu-id="b020f-173">Time zones</span><span class="sxs-lookup"><span data-stu-id="b020f-173">Time zones</span></span>
<span data-ttu-id="b020f-174">Since all datetime values are expressed in UTC, it's often useful to convert these into the local timezone.</span><span class="sxs-lookup"><span data-stu-id="b020f-174">Since all datetime values are expressed in UTC, it's often useful to convert these into the local timezone.</span></span> <span data-ttu-id="b020f-175">For example, use this calculation to convert UTC to PST times:</span><span class="sxs-lookup"><span data-stu-id="b020f-175">For example, use this calculation to convert UTC to PST times:</span></span>

```OQL
Event
| extend localTimestamp = TimeGenerated - 8h
```

## <a name="related-functions"></a><span data-ttu-id="b020f-176">Related functions</span><span class="sxs-lookup"><span data-stu-id="b020f-176">Related functions</span></span>

| <span data-ttu-id="b020f-177">Category</span><span class="sxs-lookup"><span data-stu-id="b020f-177">Category</span></span> | <span data-ttu-id="b020f-178">Function</span><span class="sxs-lookup"><span data-stu-id="b020f-178">Function</span></span> |
|:---|:---|
| <span data-ttu-id="b020f-179">Convert data types</span><span class="sxs-lookup"><span data-stu-id="b020f-179">Convert data types</span></span> | <span data-ttu-id="b020f-180">[todatetime](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/todatetime())  [totimespan](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/totimespan())</span><span class="sxs-lookup"><span data-stu-id="b020f-180">[todatetime](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/todatetime())  [totimespan](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/totimespan())</span></span>  |
| <span data-ttu-id="b020f-181">Round value to bin size</span><span class="sxs-lookup"><span data-stu-id="b020f-181">Round value to bin size</span></span> | <span data-ttu-id="b020f-182">[bin](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/bin())</span><span class="sxs-lookup"><span data-stu-id="b020f-182">[bin](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/bin())</span></span> |
| <span data-ttu-id="b020f-183">Get a specific date or time</span><span class="sxs-lookup"><span data-stu-id="b020f-183">Get a specific date or time</span></span> | <span data-ttu-id="b020f-184">[ago](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/ago()) [now](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/now())</span><span class="sxs-lookup"><span data-stu-id="b020f-184">[ago](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/ago()) [now](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/now())</span></span>   |
| <span data-ttu-id="b020f-185">Get part of value</span><span class="sxs-lookup"><span data-stu-id="b020f-185">Get part of value</span></span> | <span data-ttu-id="b020f-186">[datetime_part](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/datetime_part()) [getmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/getmonth()) [monthofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/monthofyear()) [getyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/getyear()) [dayofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofmonth()) [dayofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofweek()) [dayofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofyear()) [weekofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/weekofyear())</span><span class="sxs-lookup"><span data-stu-id="b020f-186">[datetime_part](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/datetime_part()) [getmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/getmonth()) [monthofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/monthofyear()) [getyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/getyear()) [dayofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofmonth()) [dayofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofweek()) [dayofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofyear()) [weekofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/weekofyear())</span></span> |
| <span data-ttu-id="b020f-187">Get a date relative to value</span><span class="sxs-lookup"><span data-stu-id="b020f-187">Get a date relative to value</span></span>  | <span data-ttu-id="b020f-188">[endofday](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofday()) [endofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofweek()) [endofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofmonth()) [endofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofyear()) [startofday](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofday()) [startofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofweek()) [startofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofmonth()) [startofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofyear())</span><span class="sxs-lookup"><span data-stu-id="b020f-188">[endofday](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofday()) [endofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofweek()) [endofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofmonth()) [endofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofyear()) [startofday](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofday()) [startofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofweek()) [startofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofmonth()) [startofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofyear())</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b020f-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="b020f-189">Next steps</span></span>
<span data-ttu-id="b020f-190">See other lessons for using the Log Analytics query language:</span><span class="sxs-lookup"><span data-stu-id="b020f-190">See other lessons for using the Log Analytics query language:</span></span>

- [<span data-ttu-id="b020f-191">String operations</span><span class="sxs-lookup"><span data-stu-id="b020f-191">String operations</span></span>](string-operations.md)
- [<span data-ttu-id="b020f-192">Aggregation functions</span><span class="sxs-lookup"><span data-stu-id="b020f-192">Aggregation functions</span></span>](aggregations.md)
- [<span data-ttu-id="b020f-193">Advanced aggregations</span><span class="sxs-lookup"><span data-stu-id="b020f-193">Advanced aggregations</span></span>](advanced-aggregations.md)
- [<span data-ttu-id="b020f-194">JSON and data structures</span><span class="sxs-lookup"><span data-stu-id="b020f-194">JSON and data structures</span></span>](json-data-structures.md)
- [<span data-ttu-id="b020f-195">Advanced query writing</span><span class="sxs-lookup"><span data-stu-id="b020f-195">Advanced query writing</span></span>](advanced-query-writing.md)
- [<span data-ttu-id="b020f-196">Joins</span><span class="sxs-lookup"><span data-stu-id="b020f-196">Joins</span></span>](joins.md)
- [<span data-ttu-id="b020f-197">Charts</span><span class="sxs-lookup"><span data-stu-id="b020f-197">Charts</span></span>](charts.md)