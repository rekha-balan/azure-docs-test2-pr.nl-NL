---
title: Advanced queries in Azure Log Analytics | Microsoft Docs
description: This article provides a tutorial for using the Analytics portal to write queries in Log Analytics.
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
ms.openlocfilehash: 72c151fec0637822411f8cac44f4e13a8df96445
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866724"
---
# <a name="writing-advanced-queries-in-log-analytics"></a>Writing advanced queries in Log Analytics

> [!NOTE]
> You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.

## <a name="reusing-code-with-let"></a>Reusing code with let
Use `let` to assign results to a variable, and refer to it later in the query:

```OQL
// get all events that have level 2 (indicates warning level)
let warning_events=
Event
| where EventLevel == 2;
// count the number of warning events per computer
warning_events
| summarize count() by Computer 
```

You can also assign constant values to variables. This supports a method to set up parameters for the fields that you need to change every time you execute the query. Modify those parameters as needed. For example, to calculate the free disk space and free memory (in percentiles), in a given time window:

```OQL
let startDate = datetime(2018-08-01T12:55:02);
let endDate = datetime(2018-08-02T13:21:35);
let FreeDiskSpace =
Perf
| where TimeGenerated between (startDate .. endDate)
| where ObjectName=="Logical Disk" and CounterName=="Free Megabytes"
| summarize percentiles(CounterValue, 50, 75, 90, 99);
let FreeMemory =
Perf
| where TimeGenerated between (startDate .. endDate)
| where ObjectName=="Memory" and CounterName=="Available MBytes Memory"
| summarize percentiles(CounterValue, 50, 75, 90, 99);
union FreeDiskSpace, FreeMemory
```

This makes it easy to change the start of end time the next time you run the query.

### <a name="local-functions-and-parameters"></a>Local functions and parameters
Use `let` statements to create functions that can be used in the same query. For example, define a function that takes a datetime field (in the UTC format) and converts it to a standard US format. 

```OQL
let utc_to_us_date_format = (t:datetime)
{
  strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
  bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
};
Event 
| where TimeGenerated > ago(1h) 
| extend USTimeGenerated = utc_to_us_date_format(TimeGenerated)
| project TimeGenerated, USTimeGenerated, Source, Computer, EventLevel, EventData 
```

## <a name="functions"></a>Functions
You can save a query with a function alias so it can be referenced by other queries. For example, the following standard query returns all missing security updates reported in the last day:

```OQL
Update
| where TimeGenerated > ago(1d) 
| where Classification == "Security Updates" 
| where UpdateState == "Needed"
```

You can save this query as a function and give it an alias such as _security_updates_last_day_. Then you can use it in another query to search for SQL-related needed security updates:

```OQL
security_updates_last_day | where Title contains "SQL"
```

To save a query as a function, select the **Save** button in the portal and change **Save as** to _Function_. The function alias can contain letters, digits, or underscores but must start with a letter or an underscore.

> [!NOTE]
> Saving a function is possible in Log Analytics queries, but currently not for Application Insights queries.


## <a name="print"></a>Print
`print` will return a table with a single column and a single row, showing the result of a calculation. This is often used in cases where you need a simple calcuation. For example, to find the current time in PST and add a column with EST:

```OQL
print nowPst = now()-8h
| extend nowEst = nowPst+3h
```

## <a name="datatable"></a>Datatable
`datatable` allows you to define a set of data. You provide a schema and a set of values and then pipe the table into any other query elements. For example to create a table of RAM usage and calculate their average value per hour:

```OQL
datatable (TimeGenerated: datetime, usage_percent: double)
[
  "2018-06-02T15:15:46.3418323Z", 15.5,
  "2018-06-02T15:45:43.1561235Z", 20.2,
  "2018-06-02T16:16:49.2354895Z", 17.3,
  "2018-06-02T16:46:44.9813459Z", 45.7,
  "2018-06-02T17:15:41.7895423Z", 10.9,
  "2018-06-02T17:44:23.9813459Z", 24.7,
  "2018-06-02T18:14:59.7283023Z", 22.3,
  "2018-06-02T18:45:12.1895483Z", 25.4
]
| summarize avg(usage_percent) by bin(TimeGenerated, 1h)
```

Datatable constructs are also very useful when creating a lookup table. For example, to map table data such as event IDs from the _SecurityEvent_ table, to event types listed elsewhere, create a lookup table with the event types using `datatable` and join this datatable with _SecurityEvent_ data:

```OQL
let eventCodes = datatable (EventID: int, EventType:string)
[
    4625, "Account activity",
    4688, "Process action",
    4634, "Account activity",
    4672, "Access",
    4624, "Account activity",
    4799, "Access management",
    4798, "Access management",
    5059, "Key operation",
    4648, "A logon was attempted using explicit credentials",
    4768, "Access management",
    4662, "Other",
    8002, "Process action",
    4904, "Security event management",
    4905, "Security event management",
];
SecurityEvent
| where TimeGenerated > ago(1h) 
| join kind=leftouter (
  eventCodes
) on EventID
| project TimeGenerated, Account, AccountType, Computer, EventType
```

## <a name="next-steps"></a>Next steps
See other lessons for using the Log Analytics query language:

- [String operations](string-operations.md)
- [Date and time operations](datetime-operations.md)
- [Aggregation functions](aggregations.md)
- [Advanced aggregations](advanced-aggregations.md)
- [JSON and data structures](json-data-structures.md)
- [Joins](joins.md)
- [Charts](charts.md)