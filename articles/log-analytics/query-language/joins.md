---
title: Joins in Azure Log Analytics queries | Microsoft Docs
description: This article includes a lesson on using joins in the Log Analytics query language.
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
ms.openlocfilehash: 823e8694b574acdde122f8d5224b04d3872b6820
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870490"
---
# <a name="joins-in-log-analytics-queries"></a><span data-ttu-id="22a16-103">Joins in Log Analytics queries</span><span class="sxs-lookup"><span data-stu-id="22a16-103">Joins in Log Analytics queries</span></span>

> [!NOTE]
> <span data-ttu-id="22a16-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span><span class="sxs-lookup"><span data-stu-id="22a16-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span></span>

<span data-ttu-id="22a16-105">Joins allow you to analyze data from multiple tables, in the same query.</span><span class="sxs-lookup"><span data-stu-id="22a16-105">Joins allow you to analyze data from multiple tables, in the same query.</span></span> <span data-ttu-id="22a16-106">They merge the rows of two data sets by matching values of specified columns.</span><span class="sxs-lookup"><span data-stu-id="22a16-106">They merge the rows of two data sets by matching values of specified columns.</span></span>


```OQL
SecurityEvent 
| where EventID == 4624     // sign-in events
| project Computer, Account, TargetLogonId, LogonTime=TimeGenerated
| join kind= inner (
    SecurityEvent 
    | where EventID == 4634     // sign-out events
    | project TargetLogonId, LogoffTime=TimeGenerated
) on TargetLogonId
| extend Duration = LogoffTime-LogonTime
| project-away TargetLogonId1 
| top 10 by Duration desc
```

<span data-ttu-id="22a16-107">In this example, the first dataset filters for all sign-in events.</span><span class="sxs-lookup"><span data-stu-id="22a16-107">In this example, the first dataset filters for all sign-in events.</span></span> <span data-ttu-id="22a16-108">This is joined with a second dataset that filters for all sign-out events.</span><span class="sxs-lookup"><span data-stu-id="22a16-108">This is joined with a second dataset that filters for all sign-out events.</span></span> <span data-ttu-id="22a16-109">The projected columns are _Computer_, _Account_, _TargetLogonId_, and _TimeGenerated_.</span><span class="sxs-lookup"><span data-stu-id="22a16-109">The projected columns are _Computer_, _Account_, _TargetLogonId_, and _TimeGenerated_.</span></span> <span data-ttu-id="22a16-110">The datasets are correlated by a shared column, _TargetLogonId_.</span><span class="sxs-lookup"><span data-stu-id="22a16-110">The datasets are correlated by a shared column, _TargetLogonId_.</span></span> <span data-ttu-id="22a16-111">The output is a single record per correlation, which has both the sign-in and sign-out time.</span><span class="sxs-lookup"><span data-stu-id="22a16-111">The output is a single record per correlation, which has both the sign-in and sign-out time.</span></span>

<span data-ttu-id="22a16-112">If both datasets have columns with the same names, the columns of the right-side dataset would be given an index number, so in this example the results would show _TargetLogonId_ with values from the left-side table and _TargetLogonId1_  with values from the right-side table.</span><span class="sxs-lookup"><span data-stu-id="22a16-112">If both datasets have columns with the same names, the columns of the right-side dataset would be given an index number, so in this example the results would show _TargetLogonId_ with values from the left-side table and _TargetLogonId1_  with values from the right-side table.</span></span> <span data-ttu-id="22a16-113">In this case, the second _TargetLogonId1_ column was removed by using the `project-away` operator.</span><span class="sxs-lookup"><span data-stu-id="22a16-113">In this case, the second _TargetLogonId1_ column was removed by using the `project-away` operator.</span></span>

> [!NOTE]
> <span data-ttu-id="22a16-114">To improve performance, keep only the relevant columns of the joined data-sets, using the `project` operator.</span><span class="sxs-lookup"><span data-stu-id="22a16-114">To improve performance, keep only the relevant columns of the joined data-sets, using the `project` operator.</span></span>


<span data-ttu-id="22a16-115">Use the following syntax to join two datasets and the joined key has a different name between the two tables:</span><span class="sxs-lookup"><span data-stu-id="22a16-115">Use the following syntax to join two datasets and the joined key has a different name between the two tables:</span></span>
```
Table1
| join ( Table2 ) 
on $left.key1 == $right.key2
```

## <a name="lookup-tables"></a><span data-ttu-id="22a16-116">Lookup Tables</span><span class="sxs-lookup"><span data-stu-id="22a16-116">Lookup Tables</span></span>
<span data-ttu-id="22a16-117">A common use of joins is using static mapping of values using `datatable` that can help in transforming the results into more presentable way.</span><span class="sxs-lookup"><span data-stu-id="22a16-117">A common use of joins is using static mapping of values using `datatable` that can help in transforming the results into more presentable way.</span></span> <span data-ttu-id="22a16-118">For example, to enrich the security event data with the event name for each event ID.</span><span class="sxs-lookup"><span data-stu-id="22a16-118">For example, to enrich the security event data with the event name for each event ID.</span></span>

```OQL
let DimTable = datatable(EventID:int, eventName:string)
  [
    4625, "Account activity",
    4688, "Process action",
    4634, "Account activity",
    4658, "The handle to an object was closed",
    4656, "A handle to an object was requested",
    4690, "An attempt was made to duplicate a handle to an object",
    4663, "An attempt was made to access an object",
    5061, "Cryptographic operation",
    5058, "Key file operation"
  ];
SecurityEvent
| join kind = inner
 DimTable on EventID
| summarize count() by eventName
```

![Join with a datatable](media/joins/dim-table.png)

## <a name="join-kinds"></a><span data-ttu-id="22a16-120">Join kinds</span><span class="sxs-lookup"><span data-stu-id="22a16-120">Join kinds</span></span>
<span data-ttu-id="22a16-121">Specify the type of join with the _kind_ argument.</span><span class="sxs-lookup"><span data-stu-id="22a16-121">Specify the type of join with the _kind_ argument.</span></span> <span data-ttu-id="22a16-122">Each type performs a different match between the records of the given tables as described in the following table.</span><span class="sxs-lookup"><span data-stu-id="22a16-122">Each type performs a different match between the records of the given tables as described in the following table.</span></span>

| <span data-ttu-id="22a16-123">Join type</span><span class="sxs-lookup"><span data-stu-id="22a16-123">Join type</span></span> | <span data-ttu-id="22a16-124">Description</span><span class="sxs-lookup"><span data-stu-id="22a16-124">Description</span></span> |
|:---|:---|
| <span data-ttu-id="22a16-125">innerunique</span><span class="sxs-lookup"><span data-stu-id="22a16-125">innerunique</span></span> | <span data-ttu-id="22a16-126">This is the default join mode.</span><span class="sxs-lookup"><span data-stu-id="22a16-126">This is the default join mode.</span></span> <span data-ttu-id="22a16-127">First the values of the matched column on the left table are found, and duplicate values are removed.</span><span class="sxs-lookup"><span data-stu-id="22a16-127">First the values of the matched column on the left table are found, and duplicate values are removed.</span></span>  <span data-ttu-id="22a16-128">Then the set of unique values is matched against the right table.</span><span class="sxs-lookup"><span data-stu-id="22a16-128">Then the set of unique values is matched against the right table.</span></span> |
| <span data-ttu-id="22a16-129">inner</span><span class="sxs-lookup"><span data-stu-id="22a16-129">inner</span></span> | <span data-ttu-id="22a16-130">Only matching records in both tables are included in the results.</span><span class="sxs-lookup"><span data-stu-id="22a16-130">Only matching records in both tables are included in the results.</span></span> |
| <span data-ttu-id="22a16-131">leftouter</span><span class="sxs-lookup"><span data-stu-id="22a16-131">leftouter</span></span> | <span data-ttu-id="22a16-132">All records in the left table and matching records in the right table are included in the results.</span><span class="sxs-lookup"><span data-stu-id="22a16-132">All records in the left table and matching records in the right table are included in the results.</span></span> <span data-ttu-id="22a16-133">Unmatched output properties contain nulls.</span><span class="sxs-lookup"><span data-stu-id="22a16-133">Unmatched output properties contain nulls.</span></span>  |
| <span data-ttu-id="22a16-134">leftanti</span><span class="sxs-lookup"><span data-stu-id="22a16-134">leftanti</span></span> | <span data-ttu-id="22a16-135">Records from the left side that do not have matches from the right are included in the results.</span><span class="sxs-lookup"><span data-stu-id="22a16-135">Records from the left side that do not have matches from the right are included in the results.</span></span> <span data-ttu-id="22a16-136">The results table has only columns from the left table.</span><span class="sxs-lookup"><span data-stu-id="22a16-136">The results table has only columns from the left table.</span></span> |
| <span data-ttu-id="22a16-137">leftsemi</span><span class="sxs-lookup"><span data-stu-id="22a16-137">leftsemi</span></span> | <span data-ttu-id="22a16-138">Records from the left side that have matches from the right are included in the results.</span><span class="sxs-lookup"><span data-stu-id="22a16-138">Records from the left side that have matches from the right are included in the results.</span></span> <span data-ttu-id="22a16-139">The results table has only columns from the left table.</span><span class="sxs-lookup"><span data-stu-id="22a16-139">The results table has only columns from the left table.</span></span> |


## <a name="best-practices"></a><span data-ttu-id="22a16-140">Best practices</span><span class="sxs-lookup"><span data-stu-id="22a16-140">Best practices</span></span>

<span data-ttu-id="22a16-141">Consider the following points for optimal performance:</span><span class="sxs-lookup"><span data-stu-id="22a16-141">Consider the following points for optimal performance:</span></span>

- <span data-ttu-id="22a16-142">Use a time filter on each table to reduce the records that must be evaluated for the join.</span><span class="sxs-lookup"><span data-stu-id="22a16-142">Use a time filter on each table to reduce the records that must be evaluated for the join.</span></span>
- <span data-ttu-id="22a16-143">Use `where` and `project` to reduce the numbers of rows and columns in the input tables before the join.</span><span class="sxs-lookup"><span data-stu-id="22a16-143">Use `where` and `project` to reduce the numbers of rows and columns in the input tables before the join.</span></span>
* <span data-ttu-id="22a16-144">If one table is always smaller than the other, use it as the left side of the join.</span><span class="sxs-lookup"><span data-stu-id="22a16-144">If one table is always smaller than the other, use it as the left side of the join.</span></span>


## <a name="next-steps"></a><span data-ttu-id="22a16-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="22a16-145">Next steps</span></span>
<span data-ttu-id="22a16-146">See other lessons for using the Log Analytics query language:</span><span class="sxs-lookup"><span data-stu-id="22a16-146">See other lessons for using the Log Analytics query language:</span></span>

- [<span data-ttu-id="22a16-147">String operations</span><span class="sxs-lookup"><span data-stu-id="22a16-147">String operations</span></span>](string-operations.md)
- [<span data-ttu-id="22a16-148">Aggregation functions</span><span class="sxs-lookup"><span data-stu-id="22a16-148">Aggregation functions</span></span>](aggregations.md)
- [<span data-ttu-id="22a16-149">Advanced aggregations</span><span class="sxs-lookup"><span data-stu-id="22a16-149">Advanced aggregations</span></span>](advanced-aggregations.md)
- [<span data-ttu-id="22a16-150">JSON and data structures</span><span class="sxs-lookup"><span data-stu-id="22a16-150">JSON and data structures</span></span>](json-data-structures.md)
- [<span data-ttu-id="22a16-151">Advanced query writing</span><span class="sxs-lookup"><span data-stu-id="22a16-151">Advanced query writing</span></span>](advanced-query-writing.md)
- [<span data-ttu-id="22a16-152">Charts</span><span class="sxs-lookup"><span data-stu-id="22a16-152">Charts</span></span>](charts.md)