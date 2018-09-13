---
title: Creating charts and diagrams from Azure Log Analytics queries | Microsoft Docs
description: Describes various visualizations in Azure Log Analytics to display your data in different ways.
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
ms.openlocfilehash: 359e5e671287c4d330deeb2d3573877d9ee5d1c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857487"
---
# <a name="creating-charts-and-diagrams-from-log-analytics-queries"></a><span data-ttu-id="a0793-103">Creating charts and diagrams from Log Analytics queries</span><span class="sxs-lookup"><span data-stu-id="a0793-103">Creating charts and diagrams from Log Analytics queries</span></span>

> [!NOTE]
> <span data-ttu-id="a0793-104">You should complete [Advanced aggregations in Log Analytics queries](advanced-aggregations.md) before completing this lesson.</span><span class="sxs-lookup"><span data-stu-id="a0793-104">You should complete [Advanced aggregations in Log Analytics queries](advanced-aggregations.md) before completing this lesson.</span></span>

<span data-ttu-id="a0793-105">This article describes various visualizations in Azure Log Analytics to display your data in different ways.</span><span class="sxs-lookup"><span data-stu-id="a0793-105">This article describes various visualizations in Azure Log Analytics to display your data in different ways.</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="a0793-106">Charting the results</span><span class="sxs-lookup"><span data-stu-id="a0793-106">Charting the results</span></span>
<span data-ttu-id="a0793-107">Start by reviewing how many computers there are per operating system, during the past hour:</span><span class="sxs-lookup"><span data-stu-id="a0793-107">Start by reviewing how many computers there are per operating system, during the past hour:</span></span>

```OQL
Heartbeat
| where TimeGenerated > ago(1h)
| summarize count(Computer) by OSType  
```

<span data-ttu-id="a0793-108">By default, results display as a table:</span><span class="sxs-lookup"><span data-stu-id="a0793-108">By default, results display as a table:</span></span>

![Table](media/charts/table-display.png)

<span data-ttu-id="a0793-110">To get a better view, select **Chart**, and choose the **Pie** option to visualize the results:</span><span class="sxs-lookup"><span data-stu-id="a0793-110">To get a better view, select **Chart**, and choose the **Pie** option to visualize the results:</span></span>

![Pie chart](media/charts/charts-and-diagrams-pie.png)


## <a name="timecharts"></a><span data-ttu-id="a0793-112">Timecharts</span><span class="sxs-lookup"><span data-stu-id="a0793-112">Timecharts</span></span>
<span data-ttu-id="a0793-113">Show the average, 50th and 95th percentiles of processor time in bins of 1 hour.</span><span class="sxs-lookup"><span data-stu-id="a0793-113">Show the average, 50th and 95th percentiles of processor time in bins of 1 hour.</span></span> <span data-ttu-id="a0793-114">The query generates multiple series and you can then select which series to show in the time chart:</span><span class="sxs-lookup"><span data-stu-id="a0793-114">The query generates multiple series and you can then select which series to show in the time chart:</span></span>

```OQL
Perf
| where TimeGenerated > ago(1d) 
| where CounterName == "% Processor Time" 
| summarize avg(CounterValue), percentiles(CounterValue, 50, 95)  by bin(TimeGenerated, 1h)
```

<span data-ttu-id="a0793-115">Select the **Line** chart display option:</span><span class="sxs-lookup"><span data-stu-id="a0793-115">Select the **Line** chart display option:</span></span>

![Line chart](media/charts/charts-and-diagrams-multiSeries.png)

### <a name="reference-line"></a><span data-ttu-id="a0793-117">Reference line</span><span class="sxs-lookup"><span data-stu-id="a0793-117">Reference line</span></span>

<span data-ttu-id="a0793-118">A reference line can help you easily identifying if the metric exceeded a specific threshold.</span><span class="sxs-lookup"><span data-stu-id="a0793-118">A reference line can help you easily identifying if the metric exceeded a specific threshold.</span></span> <span data-ttu-id="a0793-119">To add a line to a chart, extend the dataset with a constant column:</span><span class="sxs-lookup"><span data-stu-id="a0793-119">To add a line to a chart, extend the dataset with a constant column:</span></span>

```OQL
Perf
| where TimeGenerated > ago(1d) 
| where CounterName == "% Processor Time" 
| summarize avg(CounterValue), percentiles(CounterValue, 50, 95)  by bin(TimeGenerated, 1h)
| extend Threshold = 20
```

![Reference line](media/charts/charts-and-diagrams-multiSeriesThreshold.png)

## <a name="multiple-dimensions"></a><span data-ttu-id="a0793-121">Multiple dimensions</span><span class="sxs-lookup"><span data-stu-id="a0793-121">Multiple dimensions</span></span>
<span data-ttu-id="a0793-122">Multiple expressions in the `by` clause of `summarize` create multiple rows in the results, one for each combination of values.</span><span class="sxs-lookup"><span data-stu-id="a0793-122">Multiple expressions in the `by` clause of `summarize` create multiple rows in the results, one for each combination of values.</span></span>

```OQL
SecurityEvent
| where TimeGenerated > ago(1d)
| summarize count() by tostring(EventID), AccountType, bin(TimeGenerated, 1h)
```

<span data-ttu-id="a0793-123">When you view the results as a chart, it uses the first column from the `by` clause.</span><span class="sxs-lookup"><span data-stu-id="a0793-123">When you view the results as a chart, it uses the first column from the `by` clause.</span></span> <span data-ttu-id="a0793-124">The following example shows a stacked column chart using the _EventID._</span><span class="sxs-lookup"><span data-stu-id="a0793-124">The following example shows a stacked column chart using the _EventID._</span></span> <span data-ttu-id="a0793-125">Dimensions must be of `string` type, so in this example the _EventID_ is being cast to string.</span><span class="sxs-lookup"><span data-stu-id="a0793-125">Dimensions must be of `string` type, so in this example the _EventID_ is being cast to string.</span></span> 

![Bar chart EventID](media/charts/charts-and-diagrams-multiDimension1.png)

<span data-ttu-id="a0793-127">You can switch between by selecting the dropdown with the column name.</span><span class="sxs-lookup"><span data-stu-id="a0793-127">You can switch between by selecting the dropdown with the column name.</span></span> 

![Bar chart AccountType](media/charts/charts-and-diagrams-multiDimension2.png)

## <a name="next-steps"></a><span data-ttu-id="a0793-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0793-129">Next steps</span></span>
<span data-ttu-id="a0793-130">See other lessons for using the Log Analytics query language:</span><span class="sxs-lookup"><span data-stu-id="a0793-130">See other lessons for using the Log Analytics query language:</span></span>

- [<span data-ttu-id="a0793-131">String operations</span><span class="sxs-lookup"><span data-stu-id="a0793-131">String operations</span></span>](string-operations.md)
- [<span data-ttu-id="a0793-132">Date and time operations</span><span class="sxs-lookup"><span data-stu-id="a0793-132">Date and time operations</span></span>](datetime-operations.md)
- [<span data-ttu-id="a0793-133">Aggregation functions</span><span class="sxs-lookup"><span data-stu-id="a0793-133">Aggregation functions</span></span>](aggregations.md)
- [<span data-ttu-id="a0793-134">Advanced aggregations</span><span class="sxs-lookup"><span data-stu-id="a0793-134">Advanced aggregations</span></span>](advanced-aggregations.md)
- [<span data-ttu-id="a0793-135">JSON and data structures</span><span class="sxs-lookup"><span data-stu-id="a0793-135">JSON and data structures</span></span>](json-data-structures.md)
- [<span data-ttu-id="a0793-136">Advanced query writing</span><span class="sxs-lookup"><span data-stu-id="a0793-136">Advanced query writing</span></span>](advanced-query-writing.md)
- [<span data-ttu-id="a0793-137">Joins</span><span class="sxs-lookup"><span data-stu-id="a0793-137">Joins</span></span>](joins.md)