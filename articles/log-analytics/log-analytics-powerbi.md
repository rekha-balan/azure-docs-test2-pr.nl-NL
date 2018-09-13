---
title: Export Log Analytics data to Power BI | Microsoft Docs
description: Power BI is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.  Log Analytics can continuously export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.  This article describes how to configure queries in Log Analytics that automatically export to Power BI at regular intervals.
services: log-analytics
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 64eb6939ebe5e5dd834d97f94455d36a51f0fc17
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669511"
---
# <a name="export-log-analytics-data-to-power-bi"></a><span data-ttu-id="8bebf-105">Export Log Analytics data to Power BI</span><span class="sxs-lookup"><span data-stu-id="8bebf-105">Export Log Analytics data to Power BI</span></span>
<span data-ttu-id="8bebf-106">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span><span class="sxs-lookup"><span data-stu-id="8bebf-106">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="8bebf-107">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span><span class="sxs-lookup"><span data-stu-id="8bebf-107">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="8bebf-108">When you configure Power BI with Log Analytics, you create log queries that export their results to corresponding datasets in Power BI.</span><span class="sxs-lookup"><span data-stu-id="8bebf-108">When you configure Power BI with Log Analytics, you create log queries that export their results to corresponding datasets in Power BI.</span></span>  <span data-ttu-id="8bebf-109">The query and export continues to automatically run on a schedule that you define to keep the dataset up to date with the latest data collected by Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8bebf-109">The query and export continues to automatically run on a schedule that you define to keep the dataset up to date with the latest data collected by Log Analytics.</span></span>

![Log Analytics to Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="8bebf-111">Power BI Schedules</span><span class="sxs-lookup"><span data-stu-id="8bebf-111">Power BI Schedules</span></span>
<span data-ttu-id="8bebf-112">A *Power BI Schedule* includes a log search that exports a set of data from the OMS repository to a corresponding dataset in Power BI and a schedule that defines how often this search is run to keep the dataset current.</span><span class="sxs-lookup"><span data-stu-id="8bebf-112">A *Power BI Schedule* includes a log search that exports a set of data from the OMS repository to a corresponding dataset in Power BI and a schedule that defines how often this search is run to keep the dataset current.</span></span>

<span data-ttu-id="8bebf-113">The fields in the dataset will match the properties of the records returned by the log search.</span><span class="sxs-lookup"><span data-stu-id="8bebf-113">The fields in the dataset will match the properties of the records returned by the log search.</span></span>  <span data-ttu-id="8bebf-114">If the search returns records of different types then the dataset will include all of the properties from each of the included record types.</span><span class="sxs-lookup"><span data-stu-id="8bebf-114">If the search returns records of different types then the dataset will include all of the properties from each of the included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="8bebf-115">It is a best practice to use a log search query that returns raw data as opposed to performing any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span><span class="sxs-lookup"><span data-stu-id="8bebf-115">It is a best practice to use a log search query that returns raw data as opposed to performing any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="8bebf-116">You can perform any aggregation and calculations in Power BI from the raw data.</span><span class="sxs-lookup"><span data-stu-id="8bebf-116">You can perform any aggregation and calculations in Power BI from the raw data.</span></span>
> 
> 

## <a name="connecting-oms-workspace-to-power-bi"></a><span data-ttu-id="8bebf-117">Connecting OMS workspace to Power BI</span><span class="sxs-lookup"><span data-stu-id="8bebf-117">Connecting OMS workspace to Power BI</span></span>
<span data-ttu-id="8bebf-118">Before you can export from Log Analytics to Power BI, you must connect your OMS workspace to your Power BI account using the following procedure.</span><span class="sxs-lookup"><span data-stu-id="8bebf-118">Before you can export from Log Analytics to Power BI, you must connect your OMS workspace to your Power BI account using the following procedure.</span></span>  

1. <span data-ttu-id="8bebf-119">In the OMS console click the **Settings** tile.</span><span class="sxs-lookup"><span data-stu-id="8bebf-119">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="8bebf-120">Select **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-120">Select **Accounts**.</span></span>
3. <span data-ttu-id="8bebf-121">In the **Workspace Information** section click **Connect to Power BI Account**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-121">In the **Workspace Information** section click **Connect to Power BI Account**.</span></span>
4. <span data-ttu-id="8bebf-122">Enter the credentials for your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="8bebf-122">Enter the credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="8bebf-123">Create a Power BI Schedule</span><span class="sxs-lookup"><span data-stu-id="8bebf-123">Create a Power BI Schedule</span></span>
<span data-ttu-id="8bebf-124">Create a Power BI Schedule for each dataset using the following procedure.</span><span class="sxs-lookup"><span data-stu-id="8bebf-124">Create a Power BI Schedule for each dataset using the following procedure.</span></span>

1. <span data-ttu-id="8bebf-125">In the OMS console click the **Log Search** tile.</span><span class="sxs-lookup"><span data-stu-id="8bebf-125">In the OMS console click the **Log Search** tile.</span></span>
2. <span data-ttu-id="8bebf-126">Type in a new query or select a saved search that returns the data that you want to export to **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-126">Type in a new query or select a saved search that returns the data that you want to export to **Power BI**.</span></span>  
3. <span data-ttu-id="8bebf-127">Click the **Power BI** button at the top of the page to open the **Power BI** dialog.</span><span class="sxs-lookup"><span data-stu-id="8bebf-127">Click the **Power BI** button at the top of the page to open the **Power BI** dialog.</span></span>
4. <span data-ttu-id="8bebf-128">Provide the information in the following table and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-128">Provide the information in the following table and click **Save**.</span></span>

| <span data-ttu-id="8bebf-129">Property</span><span class="sxs-lookup"><span data-stu-id="8bebf-129">Property</span></span> | <span data-ttu-id="8bebf-130">Description</span><span class="sxs-lookup"><span data-stu-id="8bebf-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8bebf-131">Name</span><span class="sxs-lookup"><span data-stu-id="8bebf-131">Name</span></span> |<span data-ttu-id="8bebf-132">Name to identify the schedule when you view the list of Power BI schedules.</span><span class="sxs-lookup"><span data-stu-id="8bebf-132">Name to identify the schedule when you view the list of Power BI schedules.</span></span> |
| <span data-ttu-id="8bebf-133">Saved Search</span><span class="sxs-lookup"><span data-stu-id="8bebf-133">Saved Search</span></span> |<span data-ttu-id="8bebf-134">The log search to run.</span><span class="sxs-lookup"><span data-stu-id="8bebf-134">The log search to run.</span></span>  <span data-ttu-id="8bebf-135">You can either select the current query or select an existing saved search from the dropdown box.</span><span class="sxs-lookup"><span data-stu-id="8bebf-135">You can either select the current query or select an existing saved search from the dropdown box.</span></span> |
| <span data-ttu-id="8bebf-136">Schedule</span><span class="sxs-lookup"><span data-stu-id="8bebf-136">Schedule</span></span> |<span data-ttu-id="8bebf-137">How often to run the saved search and export to the Power BI dataset.</span><span class="sxs-lookup"><span data-stu-id="8bebf-137">How often to run the saved search and export to the Power BI dataset.</span></span>  <span data-ttu-id="8bebf-138">The value must be between 15 minutes and 24 hours.</span><span class="sxs-lookup"><span data-stu-id="8bebf-138">The value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="8bebf-139">Dataset Name</span><span class="sxs-lookup"><span data-stu-id="8bebf-139">Dataset Name</span></span> |<span data-ttu-id="8bebf-140">The name of the dataset in Power BI.</span><span class="sxs-lookup"><span data-stu-id="8bebf-140">The name of the dataset in Power BI.</span></span>  <span data-ttu-id="8bebf-141">It will be created if it doesn’t exist and updated if it does exist.</span><span class="sxs-lookup"><span data-stu-id="8bebf-141">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="8bebf-142">Viewing and Removing Power BI Schedules</span><span class="sxs-lookup"><span data-stu-id="8bebf-142">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="8bebf-143">View the list of existing Power BI Schedules with the following procedure.</span><span class="sxs-lookup"><span data-stu-id="8bebf-143">View the list of existing Power BI Schedules with the following procedure.</span></span>

1. <span data-ttu-id="8bebf-144">In the OMS console click the **Settings** tile.</span><span class="sxs-lookup"><span data-stu-id="8bebf-144">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="8bebf-145">Select **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-145">Select **Power BI**.</span></span>

<span data-ttu-id="8bebf-146">In addition to the details of the schedule, the number of times that the schedule has run in the past week and the status of the last sync are displayed.</span><span class="sxs-lookup"><span data-stu-id="8bebf-146">In addition to the details of the schedule, the number of times that the schedule has run in the past week and the status of the last sync are displayed.</span></span>  <span data-ttu-id="8bebf-147">If the sync encountered errors, you can click the link to run a log search for records with details of the error.</span><span class="sxs-lookup"><span data-stu-id="8bebf-147">If the sync encountered errors, you can click the link to run a log search for records with details of the error.</span></span>

<span data-ttu-id="8bebf-148">You can remove a schedule by clicking on the **X** in the **Remove column**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-148">You can remove a schedule by clicking on the **X** in the **Remove column**.</span></span>  <span data-ttu-id="8bebf-149">You can disable a schedule by selecting **Off**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-149">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="8bebf-150">To modify a schedule you must remove it and recreate it with the new settings.</span><span class="sxs-lookup"><span data-stu-id="8bebf-150">To modify a schedule you must remove it and recreate it with the new settings.</span></span>

![Power BI Schedules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="8bebf-152">Sample walkthrough</span><span class="sxs-lookup"><span data-stu-id="8bebf-152">Sample walkthrough</span></span>
<span data-ttu-id="8bebf-153">The following section walks through an example of creating a Power BI Schedule and using its dataset to create a simple report.</span><span class="sxs-lookup"><span data-stu-id="8bebf-153">The following section walks through an example of creating a Power BI Schedule and using its dataset to create a simple report.</span></span>  <span data-ttu-id="8bebf-154">In this example, all performance data for a set of computers is exported to Power BI and then a line graph is created to display processor utilization.</span><span class="sxs-lookup"><span data-stu-id="8bebf-154">In this example, all performance data for a set of computers is exported to Power BI and then a line graph is created to display processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="8bebf-155">Create log search</span><span class="sxs-lookup"><span data-stu-id="8bebf-155">Create log search</span></span>
<span data-ttu-id="8bebf-156">We start by creating a log search for the data that we want to send to the dataset.</span><span class="sxs-lookup"><span data-stu-id="8bebf-156">We start by creating a log search for the data that we want to send to the dataset.</span></span>  <span data-ttu-id="8bebf-157">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span><span class="sxs-lookup"><span data-stu-id="8bebf-157">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Power BI Schedules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="8bebf-159">Create Power BI Search</span><span class="sxs-lookup"><span data-stu-id="8bebf-159">Create Power BI Search</span></span>
<span data-ttu-id="8bebf-160">We click the **Power BI** button to open the Power BI dialog and provide the required information.</span><span class="sxs-lookup"><span data-stu-id="8bebf-160">We click the **Power BI** button to open the Power BI dialog and provide the required information.</span></span>  <span data-ttu-id="8bebf-161">We want this search to run once per hour and create a dataset called *Contoso Perf*.</span><span class="sxs-lookup"><span data-stu-id="8bebf-161">We want this search to run once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="8bebf-162">Since we already have the search open that creates the data we want, we keep the default of *Use current search query* for **Saved Search**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-162">Since we already have the search open that creates the data we want, we keep the default of *Use current search query* for **Saved Search**.</span></span>

![Power BI search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="8bebf-164">Verify Power BI Search</span><span class="sxs-lookup"><span data-stu-id="8bebf-164">Verify Power BI Search</span></span>
<span data-ttu-id="8bebf-165">To verify that we created the schedule correctly, we view the list of Power BI Searches under the **Settings** tile in the OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="8bebf-165">To verify that we created the schedule correctly, we view the list of Power BI Searches under the **Settings** tile in the OMS dashboard.</span></span>  <span data-ttu-id="8bebf-166">We wait several minutes and refresh this view until it reports that the sync has been run.</span><span class="sxs-lookup"><span data-stu-id="8bebf-166">We wait several minutes and refresh this view until it reports that the sync has been run.</span></span>

![Power BI search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-the-dataset-in-power-bi"></a><span data-ttu-id="8bebf-168">Verify the dataset in Power BI</span><span class="sxs-lookup"><span data-stu-id="8bebf-168">Verify the dataset in Power BI</span></span>
<span data-ttu-id="8bebf-169">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll to **Datasets** at the bottom of the left pane.</span><span class="sxs-lookup"><span data-stu-id="8bebf-169">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll to **Datasets** at the bottom of the left pane.</span></span>  <span data-ttu-id="8bebf-170">We can see that the *Contoso Perf* dataset is listed indicating that our export has run successfully.</span><span class="sxs-lookup"><span data-stu-id="8bebf-170">We can see that the *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Power BI dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="8bebf-172">Create report based on dataset</span><span class="sxs-lookup"><span data-stu-id="8bebf-172">Create report based on dataset</span></span>
<span data-ttu-id="8bebf-173">We select the **Contoso Perf** dataset and then click on **Results** in the **Fields** pane on the right to view the fields that are part of this dataset.</span><span class="sxs-lookup"><span data-stu-id="8bebf-173">We select the **Contoso Perf** dataset and then click on **Results** in the **Fields** pane on the right to view the fields that are part of this dataset.</span></span>  <span data-ttu-id="8bebf-174">To create a line graph showing processor utilization for each computer, we perform the following actions.</span><span class="sxs-lookup"><span data-stu-id="8bebf-174">To create a line graph showing processor utilization for each computer, we perform the following actions.</span></span>

1. <span data-ttu-id="8bebf-175">Select the Line chart visualization.</span><span class="sxs-lookup"><span data-stu-id="8bebf-175">Select the Line chart visualization.</span></span>
2. <span data-ttu-id="8bebf-176">Drag **ObjectName** to **Report level filter** and check **Processor**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-176">Drag **ObjectName** to **Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="8bebf-177">Drag **CounterName** to **Report level filter** and check **% Processor Time**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-177">Drag **CounterName** to **Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="8bebf-178">Drag **CounterValue** to **Values**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-178">Drag **CounterValue** to **Values**.</span></span>
5. <span data-ttu-id="8bebf-179">Drag **Computer** to **Legend**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-179">Drag **Computer** to **Legend**.</span></span>
6. <span data-ttu-id="8bebf-180">Drag **TimeGenerated** to **Axis**.</span><span class="sxs-lookup"><span data-stu-id="8bebf-180">Drag **TimeGenerated** to **Axis**.</span></span>

<span data-ttu-id="8bebf-181">We can see that the resulting line graph is displayed with the data from our dataset.</span><span class="sxs-lookup"><span data-stu-id="8bebf-181">We can see that the resulting line graph is displayed with the data from our dataset.</span></span>

![Power BI line graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-the-report"></a><span data-ttu-id="8bebf-183">Save the report</span><span class="sxs-lookup"><span data-stu-id="8bebf-183">Save the report</span></span>
<span data-ttu-id="8bebf-184">We save the report by clicking on the Save button at the top of the screen and validate that it is now listed in the Reports section in the left pane.</span><span class="sxs-lookup"><span data-stu-id="8bebf-184">We save the report by clicking on the Save button at the top of the screen and validate that it is now listed in the Reports section in the left pane.</span></span>

![Power BI reports](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="8bebf-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bebf-186">Next steps</span></span>
* <span data-ttu-id="8bebf-187">Learn about [log searches](log-analytics-log-searches.md) to build queries that can be exported to Power BI.</span><span class="sxs-lookup"><span data-stu-id="8bebf-187">Learn about [log searches](log-analytics-log-searches.md) to build queries that can be exported to Power BI.</span></span>
* <span data-ttu-id="8bebf-188">Learn more about [Power BI](http://powerbi.microsoft.com) to build visualizations based on Log Analytics exports.</span><span class="sxs-lookup"><span data-stu-id="8bebf-188">Learn more about [Power BI](http://powerbi.microsoft.com) to build visualizations based on Log Analytics exports.</span></span>









