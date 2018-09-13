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
# <a name="working-with-date-time-values-in-log-analytics-queries"></a>Working with date time values in Log Analytics queries

> [!NOTE]
> You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.

This article describes how to work with date and time data in Log Analytics queries.


## <a name="date-time-basics"></a>Date time basics
The Log Analytics query language has two main data types associated with dates and times: datetime and timespan. All dates are expressed in UTC. While multiple datetime formats are supported, the ISO8601 format is preferred. 

Timespans are expressed as a decimal followed by a time unit:

|shorthand   | time unit    |
|:---|:---|
|d           | day          |
|h           | hour         |
|m           | minute       |
|s           | second       |
|ms          | millisecond  |
|microsecond | microsecond  |
|tick        | nanosecond   |

Datetimes can be created by casting a string using the `todatetime` operator. For example, to review the VM heartbeats sent in a specific timeframe, you can make use of the [between operator](https://docs.loganalytics.io/docs/Language-Reference/Scalar-operators/between-operator) which is convenient to specify a time range..

```OQL
Heartbeat
| where TimeGenerated between(datetime("2018-06-30 22:46:42") .. datetime("2018-07-01 00:57:27"))
```

Another common scenario is comparing a datetime to the present. For example, to see all heartbeats over the last two minutes, you can use the `now` operator together with a timespan that represents two minutes:

```OQL
Heartbeat
| where TimeGenerated > now() - 2m
```

A shortcut is also available for this function:
```OQL
Heartbeat
| where TimeGenerated > now(-2m)
```

The shortest and most readable method though is using the `ago` operator:
```OQL
Heartbeat
| where TimeGenerated > ago(2m)
```

Suppose that instead of knowing the start and end time, you know the start time and the duration. You can rewrite the query as follows:

```OQL
let startDatetime = todatetime("2018-06-30 20:12:42.9");
let duration = totimespan(25m);
Heartbeat
| where TimeGenerated between(startDatetime .. (startDatetime+duration) )
| extend timeFromStart = TimeGenerated - startDatetime
```

## <a name="converting-time-units"></a>Converting time units
It can be useful to express a datetime or timespan in a time unit other than the default one. For example, suppose you're reviewing error events from the last 30 minutes, and need a calculated column that shows how long ago the event happened:

```OQL
Event
| where TimeGenerated > ago(30m)
| where EventLevelName == "Error"
| extend timeAgo = now() - TimeGenerated 
```

You can see the _timeAgo_ column holds values such as: "00:09:31.5118992", meaning they are formatted as hh:mm:ss.fffffff. If you'd like to format these values to the _numver_ of minutes since the start time, simply divide that value by "1 minute":

```OQL
Event
| where TimeGenerated > ago(30m)
| where EventLevelName == "Error"
| extend timeAgo = now() - TimeGenerated
| extend timeAgoMinutes = timeAgo/1m 
```


## <a name="aggregations-and-bucketing-by-time-intervals"></a>Aggregations and bucketing by time intervals
Another very common scenario is the need to obtain statistics over a certain time period in a particular time grain. For this, a `bin` operator can be used as part of a summarize clause.

Use the following query to get the number of events that occurred every 5 minutes during the last half hour:

```OQL
Event
| where TimeGenerated > ago(30m)
| summarize events_count=count() by bin(TimeGenerated, 5m) 
```

This produces the following table:  
|TimeGenerated(UTC)|events_count|
|--|--|
|2018-08-01T09:30:00.000|54|
|2018-08-01T09:35:00.000|41|
|2018-08-01T09:40:00.000|42|
|2018-08-01T09:45:00.000|41|
|2018-08-01T09:50:00.000|41|
|2018-08-01T09:55:00.000|16|

Another way to create buckets of results is to use functions, such as `startofday`:

```OQL
Event
| where TimeGenerated > ago(4d)
| summarize events_count=count() by startofday(TimeGenerated) 
```

This produces the following results:

|timestamp|count_|
|--|--|
|2018-07-28T00:00:00.000|7,136|
|2018-07-29T00:00:00.000|12,315|
|2018-07-30T00:00:00.000|16,847|
|2018-07-31T00:00:00.000|12,616|
|2018-08-01T00:00:00.000|5,416  |


## <a name="time-zones"></a>Time zones
Since all datetime values are expressed in UTC, it's often useful to convert these into the local timezone. For example, use this calculation to convert UTC to PST times:

```OQL
Event
| extend localTimestamp = TimeGenerated - 8h
```

## <a name="related-functions"></a>Related functions

| Category | Function |
|:---|:---|
| Convert data types | [todatetime](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/todatetime())  [totimespan](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/totimespan())  |
| Round value to bin size | [bin](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/bin()) |
| Get a specific date or time | [ago](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/ago()) [now](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/now())   |
| Get part of value | [datetime_part](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/datetime_part()) [getmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/getmonth()) [monthofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/monthofyear()) [getyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/getyear()) [dayofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofmonth()) [dayofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofweek()) [dayofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/dayofyear()) [weekofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/weekofyear()) |
| Get a date relative to value  | [endofday](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofday()) [endofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofweek()) [endofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofmonth()) [endofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/endofyear()) [startofday](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofday()) [startofweek](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofweek()) [startofmonth](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofmonth()) [startofyear](https://docs.loganalytics.io/docs/Language-Reference/Scalar-functions/startofyear()) |

## <a name="next-steps"></a>Next steps
See other lessons for using the Log Analytics query language:

- [String operations](string-operations.md)
- [Aggregation functions](aggregations.md)
- [Advanced aggregations](advanced-aggregations.md)
- [JSON and data structures](json-data-structures.md)
- [Advanced query writing](advanced-query-writing.md)
- [Joins](joins.md)
- [Charts](charts.md)