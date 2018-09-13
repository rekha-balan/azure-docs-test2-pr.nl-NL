---
title: View or analyze Azure Log Analytics data collected | Microsoft Docs
description: This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics resource using the Log Search portal.  The tutorial includes running some simple queries to return different types of data and analyzing results.
services: log-analytics
documentationcenter: log-analytics
author: mgoedtel
manager: carmonm
editor: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 07/31/2018
ms.author: magoedte
ms.custom: mvc
ms.component: na
ms.openlocfilehash: 31e9e6b173a578b09f656850271ed5a8f0f2baa8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855720"
---
# <a name="view-or-analyze-data-collected-with-log-analytics-log-search"></a><span data-ttu-id="1ec9a-104">View or analyze data collected with Log Analytics log search</span><span class="sxs-lookup"><span data-stu-id="1ec9a-104">View or analyze data collected with Log Analytics log search</span></span>

<span data-ttu-id="1ec9a-105">In Log Analytics you can leverage log searches by constructing queries to analyze the collected data, use pre-existing dashboards which you can customize with graphical views of your most valuable searches.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-105">In Log Analytics you can leverage log searches by constructing queries to analyze the collected data, use pre-existing dashboards which you can customize with graphical views of your most valuable searches.</span></span>  <span data-ttu-id="1ec9a-106">Now that you have defined collection of operational data from your Azure VMs and Activity Logs, in this tutorial you learn how to:</span><span class="sxs-lookup"><span data-stu-id="1ec9a-106">Now that you have defined collection of operational data from your Azure VMs and Activity Logs, in this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ec9a-107">Perform a simple search of event data and use features to modify and filter the results</span><span class="sxs-lookup"><span data-stu-id="1ec9a-107">Perform a simple search of event data and use features to modify and filter the results</span></span> 
> * <span data-ttu-id="1ec9a-108">Learn how to work with performance data</span><span class="sxs-lookup"><span data-stu-id="1ec9a-108">Learn how to work with performance data</span></span>

<span data-ttu-id="1ec9a-109">To complete the example in this tutorial, you must have an existing virtual machine [connected to the Log Analytics workspace](log-analytics-quick-collect-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="1ec9a-109">To complete the example in this tutorial, you must have an existing virtual machine [connected to the Log Analytics workspace](log-analytics-quick-collect-azurevm.md).</span></span>  

<span data-ttu-id="1ec9a-110">Creating and editing queries, in addition to working interactively with returned data, can be accomplished one of two ways.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-110">Creating and editing queries, in addition to working interactively with returned data, can be accomplished one of two ways.</span></span>  <span data-ttu-id="1ec9a-111">For basic queries, use the Log Search page in the Azure portal, or for advanced querying, you can use the Advanced Analytics portal.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-111">For basic queries, use the Log Search page in the Azure portal, or for advanced querying, you can use the Advanced Analytics portal.</span></span> <span data-ttu-id="1ec9a-112">To learn more about the difference in functionality between the two portals, see [Portals for creating and editing log queries in Azure Log Analytics](log-analytics-log-search-portals.md)</span><span class="sxs-lookup"><span data-stu-id="1ec9a-112">To learn more about the difference in functionality between the two portals, see [Portals for creating and editing log queries in Azure Log Analytics](log-analytics-log-search-portals.md)</span></span>

<span data-ttu-id="1ec9a-113">In this tutorial, we will be working with Log Search in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-113">In this tutorial, we will be working with Log Search in the Azure portal.</span></span> 

## <a name="log-in-to-azure-portal"></a><span data-ttu-id="1ec9a-114">Log in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="1ec9a-114">Log in to Azure portal</span></span>
<span data-ttu-id="1ec9a-115">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ec9a-115">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span> 

## <a name="open-the-log-search-portal"></a><span data-ttu-id="1ec9a-116">Open the Log Search portal</span><span class="sxs-lookup"><span data-stu-id="1ec9a-116">Open the Log Search portal</span></span> 
<span data-ttu-id="1ec9a-117">Start by opening the Log Search portal.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-117">Start by opening the Log Search portal.</span></span>   

1. <span data-ttu-id="1ec9a-118">In the Azure portal, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-118">In the Azure portal, click **All services**.</span></span> <span data-ttu-id="1ec9a-119">In the list of resources, type **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-119">In the list of resources, type **Monitor**.</span></span> <span data-ttu-id="1ec9a-120">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-120">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="1ec9a-121">Select **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-121">Select **Monitor**.</span></span>
2. <span data-ttu-id="1ec9a-122">On the Monitor navigation menu, select **Log Analytics** and then select a workspace.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-122">On the Monitor navigation menu, select **Log Analytics** and then select a workspace.</span></span>

## <a name="create-a-simple-search"></a><span data-ttu-id="1ec9a-123">Create a simple search</span><span class="sxs-lookup"><span data-stu-id="1ec9a-123">Create a simple search</span></span>
<span data-ttu-id="1ec9a-124">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-124">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="1ec9a-125">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-125">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="1ec9a-126">Type one the following queries in the search box and click the search button.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-126">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="1ec9a-127">Data is returned in the default list view, and you can see how many total records were returned.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-127">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Simple query](media/log-analytics-tutorial-viewdata/log-analytics-portal-eventlist-01.png)

<span data-ttu-id="1ec9a-129">Only the first few properties of each record are displayed.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-129">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="1ec9a-130">Click **show more** to display all properties for a particular record.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-130">Click **show more** to display all properties for a particular record.</span></span>

## <a name="filter-results-of-the-query"></a><span data-ttu-id="1ec9a-131">Filter results of the query</span><span class="sxs-lookup"><span data-stu-id="1ec9a-131">Filter results of the query</span></span>
<span data-ttu-id="1ec9a-132">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-132">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="1ec9a-133">Several record properties are displayed for that record type, and you can select one or more property values to narrow your search results.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-133">Several record properties are displayed for that record type, and you can select one or more property values to narrow your search results.</span></span>

<span data-ttu-id="1ec9a-134">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-134">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="1ec9a-135">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-135">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="1ec9a-136">This changes the query to one of the following to limit the results to error events.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-136">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/log-analytics-tutorial-viewdata/log-analytics-portal-eventlist-02.png)

<span data-ttu-id="1ec9a-138">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-138">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Add to filter menu](media/log-analytics-tutorial-viewdata/log-analytics-portal-eventlist-03.png)

<span data-ttu-id="1ec9a-140">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-140">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="1ec9a-141">You only have the **Filter** option for properties with their name in blue when you hover over them.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-141">You only have the **Filter** option for properties with their name in blue when you hover over them.</span></span>  <span data-ttu-id="1ec9a-142">These are *searchable* fields which are indexed for search conditions.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-142">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="1ec9a-143">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-143">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="1ec9a-144">This option returns records that have that value in any property.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-144">This option returns records that have that value in any property.</span></span>

<span data-ttu-id="1ec9a-145">You can group the results on a single property by selecting the **Group by** option in the record menu.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-145">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="1ec9a-146">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-146">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="1ec9a-147">You can group on more than one property, but you would need to edit the query directly.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-147">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="1ec9a-148">Select the record menu next the **Computer** property and select **Group by 'Computer'**.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-148">Select the record menu next the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Group by computer](media/log-analytics-tutorial-viewdata/log-analytics-portal-eventlist-04.png)

## <a name="work-with-results"></a><span data-ttu-id="1ec9a-150">Work with results</span><span class="sxs-lookup"><span data-stu-id="1ec9a-150">Work with results</span></span>
<span data-ttu-id="1ec9a-151">The Log Search portal has a variety of features for working with the results of a query.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-151">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="1ec9a-152">You can sort, filter, and group results to analyze the data without modifying the actual query.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-152">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="1ec9a-153">Results of a query are not sorted by default.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-153">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="1ec9a-154">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-154">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Table view](media/log-analytics-tutorial-viewdata/log-search-portal-table-01.png)

<span data-ttu-id="1ec9a-156">Click the arrow by a record to view the details for that record.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-156">Click the arrow by a record to view the details for that record.</span></span>

![Sort results](media/log-analytics-tutorial-viewdata/log-search-portal-table-02.png)

<span data-ttu-id="1ec9a-158">Sort on any field by clicking on its column header.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-158">Sort on any field by clicking on its column header.</span></span>

![Sort results](media/log-analytics-tutorial-viewdata/log-search-portal-table-03.png)

<span data-ttu-id="1ec9a-160">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-160">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Filter results](media/log-analytics-tutorial-viewdata/log-search-portal-table-04.png)

<span data-ttu-id="1ec9a-162">Group on a column by dragging its column header to the top of the results.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-162">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="1ec9a-163">You can group on multiple fields by dragging multiple columns to the top.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-163">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Group results](media/log-analytics-tutorial-viewdata/log-search-portal-table-05.png)


## <a name="work-with-performance-data"></a><span data-ttu-id="1ec9a-165">Work with performance data</span><span class="sxs-lookup"><span data-stu-id="1ec9a-165">Work with performance data</span></span>
<span data-ttu-id="1ec9a-166">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-166">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="1ec9a-167">Performance records look just like any other record, and we are going to write a simple query that returns all performance records just like with events.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-167">Performance records look just like any other record, and we are going to write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Performance data](media/log-analytics-tutorial-viewdata/log-analytics-portal-perfsearch-01.png)

<span data-ttu-id="1ec9a-169">Returning millions of records for all performance objects and counters though isn't very useful.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-169">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="1ec9a-170">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-170">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="1ec9a-171">This returns only processor utilization records for both Windows and Linux computers.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-171">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where ObjectName == "Processor"  | where CounterName == "% Processor Time"
```

![Processor utilization](media/log-analytics-tutorial-viewdata/log-analytics-portal-perfsearch-02.png)

<span data-ttu-id="1ec9a-173">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-173">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="1ec9a-174">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-174">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="1ec9a-175">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-175">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="1ec9a-176">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-176">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  
| where ObjectName == "Processor"  | where CounterName == "% Processor Time"
| summarize avg(CounterValue) by Computer, TimeGenerated
```

![Performance data chart](media/log-analytics-tutorial-viewdata/log-analytics-portal-perfsearch-03.png)

<span data-ttu-id="1ec9a-178">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-178">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  
| where ObjectName == "Processor" | where CounterName == "% Processor Time" 
| summarize avg(CounterValue) by Computer, TimeGenerated 
| render timechart
```

![Line chart](media/log-analytics-tutorial-viewdata/log-analytics-portal-linechart-01.png)

## <a name="next-steps"></a><span data-ttu-id="1ec9a-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ec9a-180">Next steps</span></span>
<span data-ttu-id="1ec9a-181">In this tutorial, you learned how to create basic log searches to analyze event and performance data.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-181">In this tutorial, you learned how to create basic log searches to analyze event and performance data.</span></span>  <span data-ttu-id="1ec9a-182">Advance to the next tutorial to learn how to visualize the data by creating a dashboard.</span><span class="sxs-lookup"><span data-stu-id="1ec9a-182">Advance to the next tutorial to learn how to visualize the data by creating a dashboard.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ec9a-183">Create and share Log Analytics dashboards</span><span class="sxs-lookup"><span data-stu-id="1ec9a-183">Create and share Log Analytics dashboards</span></span>](log-analytics-tutorial-dashboards.md)
