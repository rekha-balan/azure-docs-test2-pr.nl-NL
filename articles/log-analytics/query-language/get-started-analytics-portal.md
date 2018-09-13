---
title: Get started with the Log Analytics page in the Azure portal | Microsoft Docs
description: This article provides a tutorial for using the Log Analytics page to write queries.
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
ms.date: 08/20/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 493497476fdfe7d96d6f2dde735bab0147e547a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864409"
---
# <a name="get-started-with-the-log-analytics-page-in-the-azure-portal"></a><span data-ttu-id="a3d4b-103">Get started with the Log Analytics page in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a3d4b-103">Get started with the Log Analytics page in the Azure portal</span></span>

<span data-ttu-id="a3d4b-104">In this tutorial you will learn how to use the Log Analytics page in the Azure portal (currently in preview) to write Log Analytics queries.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-104">In this tutorial you will learn how to use the Log Analytics page in the Azure portal (currently in preview) to write Log Analytics queries.</span></span> <span data-ttu-id="a3d4b-105">It will teach you how to:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-105">It will teach you how to:</span></span>

- <span data-ttu-id="a3d4b-106">Write simple queries</span><span class="sxs-lookup"><span data-stu-id="a3d4b-106">Write simple queries</span></span>
- <span data-ttu-id="a3d4b-107">Understand the schema of your data</span><span class="sxs-lookup"><span data-stu-id="a3d4b-107">Understand the schema of your data</span></span>
- <span data-ttu-id="a3d4b-108">Filter, sort, and group results</span><span class="sxs-lookup"><span data-stu-id="a3d4b-108">Filter, sort, and group results</span></span>
- <span data-ttu-id="a3d4b-109">Apply a time range</span><span class="sxs-lookup"><span data-stu-id="a3d4b-109">Apply a time range</span></span>
- <span data-ttu-id="a3d4b-110">Create charts</span><span class="sxs-lookup"><span data-stu-id="a3d4b-110">Create charts</span></span>
- <span data-ttu-id="a3d4b-111">Save and load queries</span><span class="sxs-lookup"><span data-stu-id="a3d4b-111">Save and load queries</span></span>
- <span data-ttu-id="a3d4b-112">Export and share queries</span><span class="sxs-lookup"><span data-stu-id="a3d4b-112">Export and share queries</span></span>


## <a name="meet-the-log-analytics-page"></a><span data-ttu-id="a3d4b-113">Meet the Log Analytics page</span><span class="sxs-lookup"><span data-stu-id="a3d4b-113">Meet the Log Analytics page</span></span> 
<span data-ttu-id="a3d4b-114">The Log Analytics page is a web tool used to write and execute Azure Log Analytics queries.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-114">The Log Analytics page is a web tool used to write and execute Azure Log Analytics queries.</span></span> <span data-ttu-id="a3d4b-115">Open it by selecting **Logs (preview)** in the Log Analytics menu.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-115">Open it by selecting **Logs (preview)** in the Log Analytics menu.</span></span> <span data-ttu-id="a3d4b-116">It starts with a new blank query.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-116">It starts with a new blank query.</span></span>

![Home page](media/get-started-analytics-portal/homepage.png)



## <a name="basic-queries"></a><span data-ttu-id="a3d4b-118">Basic queries</span><span class="sxs-lookup"><span data-stu-id="a3d4b-118">Basic queries</span></span>
<span data-ttu-id="a3d4b-119">Queries can be used to search terms, identify trends, analyze patterns, and provide many other insights based on your data.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-119">Queries can be used to search terms, identify trends, analyze patterns, and provide many other insights based on your data.</span></span> <span data-ttu-id="a3d4b-120">Start with a basic query:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-120">Start with a basic query:</span></span>

```OQL
Event | search "error"
```

<span data-ttu-id="a3d4b-121">This query searches the _Event_ table for records that contain the term "error" in any property.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-121">This query searches the _Event_ table for records that contain the term "error" in any property.</span></span>

<span data-ttu-id="a3d4b-122">Queries can start with either a table name or a **search** command.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-122">Queries can start with either a table name or a **search** command.</span></span> <span data-ttu-id="a3d4b-123">The above example starts with the table name _Event_, which defines the scope of the query.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-123">The above example starts with the table name _Event_, which defines the scope of the query.</span></span> <span data-ttu-id="a3d4b-124">The pipe (|) character separates commands, so the output of the first one in the input of the following command.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-124">The pipe (|) character separates commands, so the output of the first one in the input of the following command.</span></span> <span data-ttu-id="a3d4b-125">You can add any number of commands to a single query.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-125">You can add any number of commands to a single query.</span></span>

<span data-ttu-id="a3d4b-126">Another way to write that same query would be:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-126">Another way to write that same query would be:</span></span>

```OQL
search in (Event) "error"
```

<span data-ttu-id="a3d4b-127">In this example, **search** is scoped to the _Event_ table, and all records in that table are searched for the term "error".</span><span class="sxs-lookup"><span data-stu-id="a3d4b-127">In this example, **search** is scoped to the _Event_ table, and all records in that table are searched for the term "error".</span></span>

## <a name="running-a-query"></a><span data-ttu-id="a3d4b-128">Running a query</span><span class="sxs-lookup"><span data-stu-id="a3d4b-128">Running a query</span></span>
<span data-ttu-id="a3d4b-129">Run a query by clicking the **Run** button or pressing **Shift+Enter**.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-129">Run a query by clicking the **Run** button or pressing **Shift+Enter**.</span></span> <span data-ttu-id="a3d4b-130">Consider the following details which determine the code that will be run and the data that's returned:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-130">Consider the following details which determine the code that will be run and the data that's returned:</span></span>

- <span data-ttu-id="a3d4b-131">Line breaks: A single break makes your query clearer.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-131">Line breaks: A single break makes your query clearer.</span></span> <span data-ttu-id="a3d4b-132">Multiple line breaks split it into separate queries.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-132">Multiple line breaks split it into separate queries.</span></span>
- <span data-ttu-id="a3d4b-133">Cursor: Place your cursor somewhere inside the query to execute it.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-133">Cursor: Place your cursor somewhere inside the query to execute it.</span></span> <span data-ttu-id="a3d4b-134">The current query is considered to be the code up until a blank line is found.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-134">The current query is considered to be the code up until a blank line is found.</span></span>
- <span data-ttu-id="a3d4b-135">Time range - A time range of _last 24 hours_ is set by default.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-135">Time range - A time range of _last 24 hours_ is set by default.</span></span> <span data-ttu-id="a3d4b-136">To use a different range, use the time-picker or add an explicit time range filter to your query.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-136">To use a different range, use the time-picker or add an explicit time range filter to your query.</span></span>


## <a name="understand-the-schema"></a><span data-ttu-id="a3d4b-137">Understand the schema</span><span class="sxs-lookup"><span data-stu-id="a3d4b-137">Understand the schema</span></span>
<span data-ttu-id="a3d4b-138">The schema is a collection of tables visually grouped under a logical category.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-138">The schema is a collection of tables visually grouped under a logical category.</span></span> <span data-ttu-id="a3d4b-139">Several of the categories are from monitoring solutions.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-139">Several of the categories are from monitoring solutions.</span></span> <span data-ttu-id="a3d4b-140">The _LogManagement_ category contains common data such as Windows and Syslog events, performance data, and client heartbeats.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-140">The _LogManagement_ category contains common data such as Windows and Syslog events, performance data, and client heartbeats.</span></span>

![Schema](media/get-started-analytics-portal/schema.png)

<span data-ttu-id="a3d4b-142">In each table, data is organized in columns with different data types as indicated by icons next to the column name.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-142">In each table, data is organized in columns with different data types as indicated by icons next to the column name.</span></span> <span data-ttu-id="a3d4b-143">For example, the _Event_ table shown in the screenshot contains columns such as _Computer_ which is text, _EventCategory_ which is a number, and _TimeGenerated_ which is date/time.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-143">For example, the _Event_ table shown in the screenshot contains columns such as _Computer_ which is text, _EventCategory_ which is a number, and _TimeGenerated_ which is date/time.</span></span>

## <a name="filter-the-results"></a><span data-ttu-id="a3d4b-144">Filter the results</span><span class="sxs-lookup"><span data-stu-id="a3d4b-144">Filter the results</span></span>
<span data-ttu-id="a3d4b-145">Start by getting everything in the _Event_ table.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-145">Start by getting everything in the _Event_ table.</span></span>

```OQL
Event
```

<span data-ttu-id="a3d4b-146">The Log Analytics page automatically scopes results by:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-146">The Log Analytics page automatically scopes results by:</span></span>

- <span data-ttu-id="a3d4b-147">Time range:  By default, queries are limited to the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-147">Time range:  By default, queries are limited to the last 24 hours.</span></span>
- <span data-ttu-id="a3d4b-148">Number of results: Results are limited to maximum of 10,000 records.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-148">Number of results: Results are limited to maximum of 10,000 records.</span></span>

<span data-ttu-id="a3d4b-149">This query is very general, and it returns too many results to be useful.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-149">This query is very general, and it returns too many results to be useful.</span></span> <span data-ttu-id="a3d4b-150">You can filter the results either through the table elements, or by explicitly adding a filter to the query.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-150">You can filter the results either through the table elements, or by explicitly adding a filter to the query.</span></span> <span data-ttu-id="a3d4b-151">Filtering results through the table elements applies to the existing result set, while a filter to the query itself will return a new filtered result set and could therefore produce more accurate results.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-151">Filtering results through the table elements applies to the existing result set, while a filter to the query itself will return a new filtered result set and could therefore produce more accurate results.</span></span>

### <a name="add-a-filter-to-the-query"></a><span data-ttu-id="a3d4b-152">Add a filter to the query</span><span class="sxs-lookup"><span data-stu-id="a3d4b-152">Add a filter to the query</span></span>
<span data-ttu-id="a3d4b-153">There is an arrow to the left of each record.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-153">There is an arrow to the left of each record.</span></span> <span data-ttu-id="a3d4b-154">Click this arrow to open the details for a specific record.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-154">Click this arrow to open the details for a specific record.</span></span>

<span data-ttu-id="a3d4b-155">Hover above a column name for the "+" and "-" icons to display.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-155">Hover above a column name for the "+" and "-" icons to display.</span></span> <span data-ttu-id="a3d4b-156">To add a filter that will return only records with the same value, click the "+" sign.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-156">To add a filter that will return only records with the same value, click the "+" sign.</span></span> <span data-ttu-id="a3d4b-157">Click "-" to exclude records with this value and then click **Run** to run the query again.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-157">Click "-" to exclude records with this value and then click **Run** to run the query again.</span></span>

![Add filter to query](media/get-started-analytics-portal/add-filter.png)

### <a name="filter-through-the-table-elements"></a><span data-ttu-id="a3d4b-159">Filter through the table elements</span><span class="sxs-lookup"><span data-stu-id="a3d4b-159">Filter through the table elements</span></span>
<span data-ttu-id="a3d4b-160">Now let's focus on events with a severity of _Error_.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-160">Now let's focus on events with a severity of _Error_.</span></span> <span data-ttu-id="a3d4b-161">This is specified in a column named _EventLevelName_.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-161">This is specified in a column named _EventLevelName_.</span></span> <span data-ttu-id="a3d4b-162">You'll need to scroll to the right to see this column.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-162">You'll need to scroll to the right to see this column.</span></span>

<span data-ttu-id="a3d4b-163">Click the Filter icon next to the column title, and in the pop-up window select values that _Starts with_ the text _error_:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-163">Click the Filter icon next to the column title, and in the pop-up window select values that _Starts with_ the text _error_:</span></span>

![Filter](media/get-started-analytics-portal/filter.png)


## <a name="sort-and-group-results"></a><span data-ttu-id="a3d4b-165">Sort and group results</span><span class="sxs-lookup"><span data-stu-id="a3d4b-165">Sort and group results</span></span>
<span data-ttu-id="a3d4b-166">The results are now narrowed down to include only error events from SQL Server, created in the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-166">The results are now narrowed down to include only error events from SQL Server, created in the last 24 hours.</span></span> <span data-ttu-id="a3d4b-167">However, the results are not sorted in any way.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-167">However, the results are not sorted in any way.</span></span> <span data-ttu-id="a3d4b-168">To sort the results by a specific column, such as _timestamp_ for example, click the column title.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-168">To sort the results by a specific column, such as _timestamp_ for example, click the column title.</span></span> <span data-ttu-id="a3d4b-169">One click sorts in ascending order while a second click will sort in descending.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-169">One click sorts in ascending order while a second click will sort in descending.</span></span>

![Sort column](media/get-started-analytics-portal/sort-column.png)

<span data-ttu-id="a3d4b-171">Another way to organize results is by groups.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-171">Another way to organize results is by groups.</span></span> <span data-ttu-id="a3d4b-172">To group results by a specific column, simply drag the column header above the other columns.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-172">To group results by a specific column, simply drag the column header above the other columns.</span></span> <span data-ttu-id="a3d4b-173">To create subgroups, drag other columns the upper bar as well.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-173">To create subgroups, drag other columns the upper bar as well.</span></span>

![Groups](media/get-started-analytics-portal/groups.png)

## <a name="select-columns-to-display"></a><span data-ttu-id="a3d4b-175">Select columns to display</span><span class="sxs-lookup"><span data-stu-id="a3d4b-175">Select columns to display</span></span>
<span data-ttu-id="a3d4b-176">The results table often includes a lot of columns.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-176">The results table often includes a lot of columns.</span></span> <span data-ttu-id="a3d4b-177">You might find that some of the returned columns are not displayed by default, or you may want to remove some the columns that are displayed.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-177">You might find that some of the returned columns are not displayed by default, or you may want to remove some the columns that are displayed.</span></span> <span data-ttu-id="a3d4b-178">To select the columns to show, click the Columns button:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-178">To select the columns to show, click the Columns button:</span></span>

![Select columns](media/get-started-analytics-portal/select-columns.png)


## <a name="select-a-time-range"></a><span data-ttu-id="a3d4b-180">Select a time range</span><span class="sxs-lookup"><span data-stu-id="a3d4b-180">Select a time range</span></span>
<span data-ttu-id="a3d4b-181">By default, the Log Analytics page applies the _last 24 hours_ time range.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-181">By default, the Log Analytics page applies the _last 24 hours_ time range.</span></span> <span data-ttu-id="a3d4b-182">To use a different range, select another value through the time picker and click **Run**.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-182">To use a different range, select another value through the time picker and click **Run**.</span></span> <span data-ttu-id="a3d4b-183">In addition to the preset values, you can use the _Custom time range_ option to select an absolute range for your query.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-183">In addition to the preset values, you can use the _Custom time range_ option to select an absolute range for your query.</span></span>

![Time picker](media/get-started-analytics-portal/time-picker.png)

<span data-ttu-id="a3d4b-185">When selecting a custom time range, the selected values are in UTC, which could be different than your local time zone.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-185">When selecting a custom time range, the selected values are in UTC, which could be different than your local time zone.</span></span>

<span data-ttu-id="a3d4b-186">If the query explicitly contains a filter for _TimeGenerated_, the time picker title will show _Set in query_.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-186">If the query explicitly contains a filter for _TimeGenerated_, the time picker title will show _Set in query_.</span></span> <span data-ttu-id="a3d4b-187">Manual selection will be disabled to prevent a conflict.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-187">Manual selection will be disabled to prevent a conflict.</span></span>


## <a name="charts"></a><span data-ttu-id="a3d4b-188">Charts</span><span class="sxs-lookup"><span data-stu-id="a3d4b-188">Charts</span></span>
<span data-ttu-id="a3d4b-189">In addition to returning results in a table, query results can be presented in visual formats.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-189">In addition to returning results in a table, query results can be presented in visual formats.</span></span> <span data-ttu-id="a3d4b-190">Use the following query as an example:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-190">Use the following query as an example:</span></span>

```OQL
Event 
| where EventLevelName == "Error" 
| where TimeGenerated > ago(1d) 
| summarize count() by Source 
```

<span data-ttu-id="a3d4b-191">By default, results are displayed in a table.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-191">By default, results are displayed in a table.</span></span> <span data-ttu-id="a3d4b-192">Click _Chart_ to see the results in a graphic view:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-192">Click _Chart_ to see the results in a graphic view:</span></span>

![Bar chart](media/get-started-analytics-portal/bar-chart.png)

<span data-ttu-id="a3d4b-194">The results are shown in a stacked bar chart.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-194">The results are shown in a stacked bar chart.</span></span> <span data-ttu-id="a3d4b-195">Click _Stacked Column_ and select _Pie_ to show another view of the results:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-195">Click _Stacked Column_ and select _Pie_ to show another view of the results:</span></span>

![Pie chart](media/get-started-analytics-portal/pie-chart.png)

<span data-ttu-id="a3d4b-197">Different properties of the view, such as x and y axes, or grouping and splitting preferences, can be changed manually from the control bar.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-197">Different properties of the view, such as x and y axes, or grouping and splitting preferences, can be changed manually from the control bar.</span></span>

<span data-ttu-id="a3d4b-198">You can also set the preferred view in the query itself, using the render operator.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-198">You can also set the preferred view in the query itself, using the render operator.</span></span>

### <a name="smart-diagnostics"></a><span data-ttu-id="a3d4b-199">Smart diagnostics</span><span class="sxs-lookup"><span data-stu-id="a3d4b-199">Smart diagnostics</span></span>
<span data-ttu-id="a3d4b-200">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-200">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="a3d4b-201">This indicates that _Smart Diagnostics_ has identified a combination of properties that filter out the sudden change.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-201">This indicates that _Smart Diagnostics_ has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="a3d4b-202">Click the point to get more detail on the filter, and to see the filtered version.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-202">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="a3d4b-203">This may help you identify what caused the change:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-203">This may help you identify what caused the change:</span></span>

![Smart diagnostics](media/get-started-analytics-portal/smart-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="a3d4b-205">Pin to dashboard</span><span class="sxs-lookup"><span data-stu-id="a3d4b-205">Pin to dashboard</span></span>
<span data-ttu-id="a3d4b-206">To pin a diagram or table to one of your shared Azure dashboards, click the pin icon.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-206">To pin a diagram or table to one of your shared Azure dashboards, click the pin icon.</span></span>

![Pin to dashboard](media/get-started-analytics-portal/pin-dashboard.png)

<span data-ttu-id="a3d4b-208">Certain simplifications are applied to a chart when you pin it to a dashboard:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-208">Certain simplifications are applied to a chart when you pin it to a dashboard:</span></span>

- <span data-ttu-id="a3d4b-209">Table columns and rows: In order to pin a table to the dashboard, it must have four or fewer columns.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-209">Table columns and rows: In order to pin a table to the dashboard, it must have four or fewer columns.</span></span> <span data-ttu-id="a3d4b-210">Only the top seven rows are displayed.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-210">Only the top seven rows are displayed.</span></span>
- <span data-ttu-id="a3d4b-211">Time restriction: Queries are automatically limited to the past 14 days.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-211">Time restriction: Queries are automatically limited to the past 14 days.</span></span>
- <span data-ttu-id="a3d4b-212">Bin count restriction: If you display a chart that has a lot of discrete bins, less populated bins are automatically grouped into a single _others_ bin.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-212">Bin count restriction: If you display a chart that has a lot of discrete bins, less populated bins are automatically grouped into a single _others_ bin.</span></span>

## <a name="save-queries"></a><span data-ttu-id="a3d4b-213">Save queries</span><span class="sxs-lookup"><span data-stu-id="a3d4b-213">Save queries</span></span>
<span data-ttu-id="a3d4b-214">Once you've created a useful query, you might want to save it or share with others.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-214">Once you've created a useful query, you might want to save it or share with others.</span></span> <span data-ttu-id="a3d4b-215">The **Save** icon is on the top bar.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-215">The **Save** icon is on the top bar.</span></span>

<span data-ttu-id="a3d4b-216">You can save either the entire query page, or a single query as a function.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-216">You can save either the entire query page, or a single query as a function.</span></span> <span data-ttu-id="a3d4b-217">Functions are queries that can also be referenced by other queries.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-217">Functions are queries that can also be referenced by other queries.</span></span> <span data-ttu-id="a3d4b-218">In order to save a query as a function, you must provide a function alias, which is the name used to call this query when referenced by other queries.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-218">In order to save a query as a function, you must provide a function alias, which is the name used to call this query when referenced by other queries.</span></span>

![Save function](media/get-started-analytics-portal/save-function.png)

<span data-ttu-id="a3d4b-220">Log Analytics queries are always saved to a selected workspace, and shared with other users of that workspace.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-220">Log Analytics queries are always saved to a selected workspace, and shared with other users of that workspace.</span></span>

## <a name="load-queries"></a><span data-ttu-id="a3d4b-221">Load queries</span><span class="sxs-lookup"><span data-stu-id="a3d4b-221">Load queries</span></span>
<span data-ttu-id="a3d4b-222">The Query Explorer icon is at the top-right area.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-222">The Query Explorer icon is at the top-right area.</span></span> <span data-ttu-id="a3d4b-223">This lists all saved queries by category.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-223">This lists all saved queries by category.</span></span> <span data-ttu-id="a3d4b-224">It also enables you to mark specific queries as Favorites to quickly find them in the future.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-224">It also enables you to mark specific queries as Favorites to quickly find them in the future.</span></span> <span data-ttu-id="a3d4b-225">Double-click a saved query to add it to the current window.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-225">Double-click a saved query to add it to the current window.</span></span>

![Query explorer](media/get-started-analytics-portal/query-explorer.png)

## <a name="export-and-share-as-link"></a><span data-ttu-id="a3d4b-227">Export and share as link</span><span class="sxs-lookup"><span data-stu-id="a3d4b-227">Export and share as link</span></span>
<span data-ttu-id="a3d4b-228">The Log Analytics page supports several exporting methods:</span><span class="sxs-lookup"><span data-stu-id="a3d4b-228">The Log Analytics page supports several exporting methods:</span></span>

- <span data-ttu-id="a3d4b-229">Excel: Save the results as a CSV file.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-229">Excel: Save the results as a CSV file.</span></span>
- <span data-ttu-id="a3d4b-230">Power BI: Export the results to power BI.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-230">Power BI: Export the results to power BI.</span></span> <span data-ttu-id="a3d4b-231">See [Import Azure Log Analytics data into Power BI](../log-analytics-powerbi.md) for details.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-231">See [Import Azure Log Analytics data into Power BI](../log-analytics-powerbi.md) for details.</span></span>
- <span data-ttu-id="a3d4b-232">Share a link: The query itself can be shared as a link which can then be sent and executed by other users that have access to the same workspace.</span><span class="sxs-lookup"><span data-stu-id="a3d4b-232">Share a link: The query itself can be shared as a link which can then be sent and executed by other users that have access to the same workspace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3d4b-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3d4b-233">Next steps</span></span>

- <span data-ttu-id="a3d4b-234">Learn more about [writing Log Analytics queries](get-started-queries.md).</span><span class="sxs-lookup"><span data-stu-id="a3d4b-234">Learn more about [writing Log Analytics queries](get-started-queries.md).</span></span>
