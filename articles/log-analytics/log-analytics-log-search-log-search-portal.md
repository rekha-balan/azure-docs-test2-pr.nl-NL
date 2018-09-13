---
title: Using the Log Search portal in Azure Log Analytics | Microsoft Docs
description: This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.  The tutorial includes running some simple queries to return different types of data and analyzing results.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/15/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 532df20a7639f42d8ba1c840a5fd19f0ad0e4042
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870917"
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="0927e-104">Create log searches in Azure Log Analytics using the Log search portal</span><span class="sxs-lookup"><span data-stu-id="0927e-104">Create log searches in Azure Log Analytics using the Log search portal</span></span>

<span data-ttu-id="0927e-105">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span><span class="sxs-lookup"><span data-stu-id="0927e-105">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="0927e-106">The tutorial includes running some simple queries to return different types of data and analyzing results.</span><span class="sxs-lookup"><span data-stu-id="0927e-106">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="0927e-107">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span><span class="sxs-lookup"><span data-stu-id="0927e-107">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="0927e-108">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="0927e-108">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="0927e-109">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="0927e-109">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="0927e-110">Both portals use the same query language to access the same data in the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="0927e-110">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0927e-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0927e-111">Prerequisites</span></span>
<span data-ttu-id="0927e-112">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span><span class="sxs-lookup"><span data-stu-id="0927e-112">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="0927e-113">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0927e-113">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="0927e-114">Connect least one [Windows agent](log-analytics-windows-agent.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span><span class="sxs-lookup"><span data-stu-id="0927e-114">Connect least one [Windows agent](log-analytics-windows-agent.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="0927e-115">Open the Log Search portal</span><span class="sxs-lookup"><span data-stu-id="0927e-115">Open the Log Search portal</span></span>
<span data-ttu-id="0927e-116">Start by opening the Log Search portal.</span><span class="sxs-lookup"><span data-stu-id="0927e-116">Start by opening the Log Search portal.</span></span> 

1. <span data-ttu-id="0927e-117">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0927e-117">Open the Azure portal.</span></span>
2. <span data-ttu-id="0927e-118">Navigate to Log Analytics and select your workspace.</span><span class="sxs-lookup"><span data-stu-id="0927e-118">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="0927e-119">Select **Logs**.</span><span class="sxs-lookup"><span data-stu-id="0927e-119">Select **Logs**.</span></span>


## <a name="create-a-simple-search"></a><span data-ttu-id="0927e-120">Create a simple search</span><span class="sxs-lookup"><span data-stu-id="0927e-120">Create a simple search</span></span>
<span data-ttu-id="0927e-121">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span><span class="sxs-lookup"><span data-stu-id="0927e-121">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="0927e-122">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span><span class="sxs-lookup"><span data-stu-id="0927e-122">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="0927e-123">Type one the following queries in the search box and click the search button.</span><span class="sxs-lookup"><span data-stu-id="0927e-123">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="0927e-124">Data is returned in the default list view, and you can see how many total records were returned.</span><span class="sxs-lookup"><span data-stu-id="0927e-124">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Simple query](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="0927e-126">Only the first few properties of each record are displayed.</span><span class="sxs-lookup"><span data-stu-id="0927e-126">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="0927e-127">Click **show more** to display all properties for a particular record.</span><span class="sxs-lookup"><span data-stu-id="0927e-127">Click **show more** to display all properties for a particular record.</span></span>

![Record details](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="0927e-129">Set the time scope</span><span class="sxs-lookup"><span data-stu-id="0927e-129">Set the time scope</span></span>
<span data-ttu-id="0927e-130">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span><span class="sxs-lookup"><span data-stu-id="0927e-130">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="0927e-131">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span><span class="sxs-lookup"><span data-stu-id="0927e-131">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="0927e-132">You can change the time filter either by selecting the dropdown or by modifying the slider.</span><span class="sxs-lookup"><span data-stu-id="0927e-132">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="0927e-133">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span><span class="sxs-lookup"><span data-stu-id="0927e-133">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="0927e-134">This segment will vary depending on the range.</span><span class="sxs-lookup"><span data-stu-id="0927e-134">This segment will vary depending on the range.</span></span>

<span data-ttu-id="0927e-135">The default time scope is **1 day**.</span><span class="sxs-lookup"><span data-stu-id="0927e-135">The default time scope is **1 day**.</span></span>  <span data-ttu-id="0927e-136">Change this value to **7 days**, and the total number of records should increase.</span><span class="sxs-lookup"><span data-stu-id="0927e-136">Change this value to **7 days**, and the total number of records should increase.</span></span>

![Date time scope](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="0927e-138">Filter results of the query</span><span class="sxs-lookup"><span data-stu-id="0927e-138">Filter results of the query</span></span>
<span data-ttu-id="0927e-139">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span><span class="sxs-lookup"><span data-stu-id="0927e-139">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="0927e-140">Several properties of the records returned are displayed with their top ten values with their record count.</span><span class="sxs-lookup"><span data-stu-id="0927e-140">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="0927e-141">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="0927e-141">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="0927e-142">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="0927e-142">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="0927e-143">This changes the query to one of the following to limit the results to error events.</span><span class="sxs-lookup"><span data-stu-id="0927e-143">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="0927e-145">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span><span class="sxs-lookup"><span data-stu-id="0927e-145">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Add to filter menu](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="0927e-147">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span><span class="sxs-lookup"><span data-stu-id="0927e-147">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="0927e-148">You only have the **Filter** option for properties with their name in blue.</span><span class="sxs-lookup"><span data-stu-id="0927e-148">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="0927e-149">These are *searchable* fields which are indexed for search conditions.</span><span class="sxs-lookup"><span data-stu-id="0927e-149">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="0927e-150">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span><span class="sxs-lookup"><span data-stu-id="0927e-150">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="0927e-151">This option returns records that have that value in any property.</span><span class="sxs-lookup"><span data-stu-id="0927e-151">This option returns records that have that value in any property.</span></span>

![Filter menu](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="0927e-153">You can group the results on a single property by selecting the **Group by** option in the record menu.</span><span class="sxs-lookup"><span data-stu-id="0927e-153">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="0927e-154">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span><span class="sxs-lookup"><span data-stu-id="0927e-154">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="0927e-155">You can group on more than one property, but you would need to edit the query directly.</span><span class="sxs-lookup"><span data-stu-id="0927e-155">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="0927e-156">Select the record menu next the **Computer** property and select **Group by 'Computer'**.</span><span class="sxs-lookup"><span data-stu-id="0927e-156">Select the record menu next the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Group by computer](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="0927e-158">Work with results</span><span class="sxs-lookup"><span data-stu-id="0927e-158">Work with results</span></span>
<span data-ttu-id="0927e-159">The Log Search portal has a variety of features for working with the results of a query.</span><span class="sxs-lookup"><span data-stu-id="0927e-159">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="0927e-160">You can sort, filter, and group results to analyze the data without modifying the actual query.</span><span class="sxs-lookup"><span data-stu-id="0927e-160">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="0927e-161">Results of a query are not sorted by default.</span><span class="sxs-lookup"><span data-stu-id="0927e-161">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="0927e-162">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span><span class="sxs-lookup"><span data-stu-id="0927e-162">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Table view](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="0927e-164">Click the arrow by a record to view the details for that record.</span><span class="sxs-lookup"><span data-stu-id="0927e-164">Click the arrow by a record to view the details for that record.</span></span>

![Sort results](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="0927e-166">Sort on any field by clicking on its column header.</span><span class="sxs-lookup"><span data-stu-id="0927e-166">Sort on any field by clicking on its column header.</span></span>

![Sort results](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="0927e-168">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span><span class="sxs-lookup"><span data-stu-id="0927e-168">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Filter results](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="0927e-170">Group on a column by dragging its column header to the top of the results.</span><span class="sxs-lookup"><span data-stu-id="0927e-170">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="0927e-171">You can group on multiple fields by dragging multiple columns to the top.</span><span class="sxs-lookup"><span data-stu-id="0927e-171">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Group results](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="0927e-173">Work with performance data</span><span class="sxs-lookup"><span data-stu-id="0927e-173">Work with performance data</span></span>
<span data-ttu-id="0927e-174">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span><span class="sxs-lookup"><span data-stu-id="0927e-174">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="0927e-175">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span><span class="sxs-lookup"><span data-stu-id="0927e-175">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Performance data](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="0927e-177">Returning millions of records for all performance objects and counters though isn't very useful.</span><span class="sxs-lookup"><span data-stu-id="0927e-177">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="0927e-178">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span><span class="sxs-lookup"><span data-stu-id="0927e-178">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="0927e-179">This returns only processor utilization records for both Windows and Linux computers.</span><span class="sxs-lookup"><span data-stu-id="0927e-179">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Processor utilization](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="0927e-181">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span><span class="sxs-lookup"><span data-stu-id="0927e-181">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="0927e-182">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="0927e-182">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="0927e-183">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span><span class="sxs-lookup"><span data-stu-id="0927e-183">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="0927e-184">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span><span class="sxs-lookup"><span data-stu-id="0927e-184">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Performance data chart](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="0927e-186">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span><span class="sxs-lookup"><span data-stu-id="0927e-186">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Line chart](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="0927e-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="0927e-188">Next steps</span></span>

- <span data-ttu-id="0927e-189">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="0927e-189">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="0927e-190">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span><span class="sxs-lookup"><span data-stu-id="0927e-190">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>
