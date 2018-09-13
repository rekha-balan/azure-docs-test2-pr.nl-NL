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
# <a name="writing-advanced-queries-in-log-analytics"></a><span data-ttu-id="cbaac-103">Writing advanced queries in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="cbaac-103">Writing advanced queries in Log Analytics</span></span>

> [!NOTE]
> <span data-ttu-id="cbaac-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span><span class="sxs-lookup"><span data-stu-id="cbaac-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span></span>

## <a name="reusing-code-with-let"></a><span data-ttu-id="cbaac-105">Reusing code with let</span><span class="sxs-lookup"><span data-stu-id="cbaac-105">Reusing code with let</span></span>
<span data-ttu-id="cbaac-106">Use `let` to assign results to a variable, and refer to it later in the query:</span><span class="sxs-lookup"><span data-stu-id="cbaac-106">Use `let` to assign results to a variable, and refer to it later in the query:</span></span>

```OQL
// get all events that have level 2 (indicates warning level)
let warning_events=
Event
| where EventLevel == 2;
// count the number of warning events per computer
warning_events
| summarize count() by Computer 
```

<span data-ttu-id="cbaac-107">You can also assign constant values to variables.</span><span class="sxs-lookup"><span data-stu-id="cbaac-107">You can also assign constant values to variables.</span></span> <span data-ttu-id="cbaac-108">This supports a method to set up parameters for the fields that you need to change every time you execute the query.</span><span class="sxs-lookup"><span data-stu-id="cbaac-108">This supports a method to set up parameters for the fields that you need to change every time you execute the query.</span></span> <span data-ttu-id="cbaac-109">Modify those parameters as needed.</span><span class="sxs-lookup"><span data-stu-id="cbaac-109">Modify those parameters as needed.</span></span> <span data-ttu-id="cbaac-110">For example, to calculate the free disk space and free memory (in percentiles), in a given time window:</span><span class="sxs-lookup"><span data-stu-id="cbaac-110">For example, to calculate the free disk space and free memory (in percentiles), in a given time window:</span></span>

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

<span data-ttu-id="cbaac-111">This makes it easy to change the start of end time the next time you run the query.</span><span class="sxs-lookup"><span data-stu-id="cbaac-111">This makes it easy to change the start of end time the next time you run the query.</span></span>

### <a name="local-functions-and-parameters"></a><span data-ttu-id="cbaac-112">Local functions and parameters</span><span class="sxs-lookup"><span data-stu-id="cbaac-112">Local functions and parameters</span></span>
<span data-ttu-id="cbaac-113">Use `let` statements to create functions that can be used in the same query.</span><span class="sxs-lookup"><span data-stu-id="cbaac-113">Use `let` statements to create functions that can be used in the same query.</span></span> <span data-ttu-id="cbaac-114">For example, define a function that takes a datetime field (in the UTC format) and converts it to a standard US format.</span><span class="sxs-lookup"><span data-stu-id="cbaac-114">For example, define a function that takes a datetime field (in the UTC format) and converts it to a standard US format.</span></span> 

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

## <a name="functions"></a><span data-ttu-id="cbaac-115">Functions</span><span class="sxs-lookup"><span data-stu-id="cbaac-115">Functions</span></span>
<span data-ttu-id="cbaac-116">You can save a query with a function alias so it can be referenced by other queries.</span><span class="sxs-lookup"><span data-stu-id="cbaac-116">You can save a query with a function alias so it can be referenced by other queries.</span></span> <span data-ttu-id="cbaac-117">For example, the following standard query returns all missing security updates reported in the last day:</span><span class="sxs-lookup"><span data-stu-id="cbaac-117">For example, the following standard query returns all missing security updates reported in the last day:</span></span>

```OQL
Update
| where TimeGenerated > ago(1d) 
| where Classification == "Security Updates" 
| where UpdateState == "Needed"
```

<span data-ttu-id="cbaac-118">You can save this query as a function and give it an alias such as _security_updates_last_day_.</span><span class="sxs-lookup"><span data-stu-id="cbaac-118">You can save this query as a function and give it an alias such as _security_updates_last_day_.</span></span> <span data-ttu-id="cbaac-119">Then you can use it in another query to search for SQL-related needed security updates:</span><span class="sxs-lookup"><span data-stu-id="cbaac-119">Then you can use it in another query to search for SQL-related needed security updates:</span></span>

```OQL
security_updates_last_day | where Title contains "SQL"
```

<span data-ttu-id="cbaac-120">To save a query as a function, select the **Save** button in the portal and change **Save as** to _Function_.</span><span class="sxs-lookup"><span data-stu-id="cbaac-120">To save a query as a function, select the **Save** button in the portal and change **Save as** to _Function_.</span></span> <span data-ttu-id="cbaac-121">The function alias can contain letters, digits, or underscores but must start with a letter or an underscore.</span><span class="sxs-lookup"><span data-stu-id="cbaac-121">The function alias can contain letters, digits, or underscores but must start with a letter or an underscore.</span></span>

> [!NOTE]
> <span data-ttu-id="cbaac-122">Saving a function is possible in Log Analytics queries, but currently not for Application Insights queries.</span><span class="sxs-lookup"><span data-stu-id="cbaac-122">Saving a function is possible in Log Analytics queries, but currently not for Application Insights queries.</span></span>


## <a name="print"></a><span data-ttu-id="cbaac-123">Print</span><span class="sxs-lookup"><span data-stu-id="cbaac-123">Print</span></span>
<span data-ttu-id="cbaac-124">`print` will return a table with a single column and a single row, showing the result of a calculation.</span><span class="sxs-lookup"><span data-stu-id="cbaac-124">`print` will return a table with a single column and a single row, showing the result of a calculation.</span></span> <span data-ttu-id="cbaac-125">This is often used in cases where you need a simple calcuation.</span><span class="sxs-lookup"><span data-stu-id="cbaac-125">This is often used in cases where you need a simple calcuation.</span></span> <span data-ttu-id="cbaac-126">For example, to find the current time in PST and add a column with EST:</span><span class="sxs-lookup"><span data-stu-id="cbaac-126">For example, to find the current time in PST and add a column with EST:</span></span>

```OQL
print nowPst = now()-8h
| extend nowEst = nowPst+3h
```

## <a name="datatable"></a><span data-ttu-id="cbaac-127">Datatable</span><span class="sxs-lookup"><span data-stu-id="cbaac-127">Datatable</span></span>
<span data-ttu-id="cbaac-128">`datatable` allows you to define a set of data.</span><span class="sxs-lookup"><span data-stu-id="cbaac-128">`datatable` allows you to define a set of data.</span></span> <span data-ttu-id="cbaac-129">You provide a schema and a set of values and then pipe the table into any other query elements.</span><span class="sxs-lookup"><span data-stu-id="cbaac-129">You provide a schema and a set of values and then pipe the table into any other query elements.</span></span> <span data-ttu-id="cbaac-130">For example to create a table of RAM usage and calculate their average value per hour:</span><span class="sxs-lookup"><span data-stu-id="cbaac-130">For example to create a table of RAM usage and calculate their average value per hour:</span></span>

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

<span data-ttu-id="cbaac-131">Datatable constructs are also very useful when creating a lookup table.</span><span class="sxs-lookup"><span data-stu-id="cbaac-131">Datatable constructs are also very useful when creating a lookup table.</span></span> <span data-ttu-id="cbaac-132">For example, to map table data such as event IDs from the _SecurityEvent_ table, to event types listed elsewhere, create a lookup table with the event types using `datatable` and join this datatable with _SecurityEvent_ data:</span><span class="sxs-lookup"><span data-stu-id="cbaac-132">For example, to map table data such as event IDs from the _SecurityEvent_ table, to event types listed elsewhere, create a lookup table with the event types using `datatable` and join this datatable with _SecurityEvent_ data:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cbaac-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="cbaac-133">Next steps</span></span>
<span data-ttu-id="cbaac-134">See other lessons for using the Log Analytics query language:</span><span class="sxs-lookup"><span data-stu-id="cbaac-134">See other lessons for using the Log Analytics query language:</span></span>

- [<span data-ttu-id="cbaac-135">String operations</span><span class="sxs-lookup"><span data-stu-id="cbaac-135">String operations</span></span>](string-operations.md)
- [<span data-ttu-id="cbaac-136">Date and time operations</span><span class="sxs-lookup"><span data-stu-id="cbaac-136">Date and time operations</span></span>](datetime-operations.md)
- [<span data-ttu-id="cbaac-137">Aggregation functions</span><span class="sxs-lookup"><span data-stu-id="cbaac-137">Aggregation functions</span></span>](aggregations.md)
- [<span data-ttu-id="cbaac-138">Advanced aggregations</span><span class="sxs-lookup"><span data-stu-id="cbaac-138">Advanced aggregations</span></span>](advanced-aggregations.md)
- [<span data-ttu-id="cbaac-139">JSON and data structures</span><span class="sxs-lookup"><span data-stu-id="cbaac-139">JSON and data structures</span></span>](json-data-structures.md)
- [<span data-ttu-id="cbaac-140">Joins</span><span class="sxs-lookup"><span data-stu-id="cbaac-140">Joins</span></span>](joins.md)
- [<span data-ttu-id="cbaac-141">Charts</span><span class="sxs-lookup"><span data-stu-id="cbaac-141">Charts</span></span>](charts.md)