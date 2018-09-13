---
title: Log searches in Azure Log Analytics| Microsoft Docs
description: You require a log search to retrieve any data from Log Analytics.  This article describes how new log searches are used in Log Analytics and provides concepts that you need to understand before creating one.
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
ms.date: 09/29/2017
ms.author: bwren
ms.component: na
ms.openlocfilehash: d1cd4f938092c6a1312bd0c0ec9240d459d67e83
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869813"
---
# <a name="understanding-log-searches-in-log-analytics"></a><span data-ttu-id="735ad-104">Understanding log searches in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="735ad-104">Understanding log searches in Log Analytics</span></span>

<span data-ttu-id="735ad-105">You require a log search to retrieve any data from Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="735ad-105">You require a log search to retrieve any data from Log Analytics.</span></span>  <span data-ttu-id="735ad-106">Whether you're analyzing data in the portal, configuring an alert rule to be notified of a particular condition, or retrieving data using the Log Analytics API, you will use a log search to specify the data you want.</span><span class="sxs-lookup"><span data-stu-id="735ad-106">Whether you're analyzing data in the portal, configuring an alert rule to be notified of a particular condition, or retrieving data using the Log Analytics API, you will use a log search to specify the data you want.</span></span>  <span data-ttu-id="735ad-107">This article describes how log searches are used in Log Analytics and provides concepts that should understand before creating one.</span><span class="sxs-lookup"><span data-stu-id="735ad-107">This article describes how log searches are used in Log Analytics and provides concepts that should understand before creating one.</span></span> <span data-ttu-id="735ad-108">See the [Next steps](#next-steps) section for details on creating and editing log searches and for references on the query language.</span><span class="sxs-lookup"><span data-stu-id="735ad-108">See the [Next steps](#next-steps) section for details on creating and editing log searches and for references on the query language.</span></span>

## <a name="where-log-searches-are-used"></a><span data-ttu-id="735ad-109">Where log searches are used</span><span class="sxs-lookup"><span data-stu-id="735ad-109">Where log searches are used</span></span>

<span data-ttu-id="735ad-110">The different ways that you will use log searches in Log Analytics include the following:</span><span class="sxs-lookup"><span data-stu-id="735ad-110">The different ways that you will use log searches in Log Analytics include the following:</span></span>

- <span data-ttu-id="735ad-111">**Portals.**</span><span class="sxs-lookup"><span data-stu-id="735ad-111">**Portals.**</span></span> <span data-ttu-id="735ad-112">You can perform interactive analysis of data in the repository in the Azure portal or the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="735ad-112">You can perform interactive analysis of data in the repository in the Azure portal or the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="735ad-113">This allows you to edit your query and analyze the results in a variety of formats and visualizations.</span><span class="sxs-lookup"><span data-stu-id="735ad-113">This allows you to edit your query and analyze the results in a variety of formats and visualizations.</span></span>  <span data-ttu-id="735ad-114">Most queries that you create will start in one of the portals and then copied once you verify that it works as expected.</span><span class="sxs-lookup"><span data-stu-id="735ad-114">Most queries that you create will start in one of the portals and then copied once you verify that it works as expected.</span></span>
- <span data-ttu-id="735ad-115">**Alert rules.**</span><span class="sxs-lookup"><span data-stu-id="735ad-115">**Alert rules.**</span></span> <span data-ttu-id="735ad-116">[Alert rules](log-analytics-alerts.md) proactively identify issues from data in your workspace.</span><span class="sxs-lookup"><span data-stu-id="735ad-116">[Alert rules](log-analytics-alerts.md) proactively identify issues from data in your workspace.</span></span>  <span data-ttu-id="735ad-117">Each alert rule is based on a log search that is automatically run at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="735ad-117">Each alert rule is based on a log search that is automatically run at regular intervals.</span></span>  <span data-ttu-id="735ad-118">The results are inspected to determine if an alert should be created.</span><span class="sxs-lookup"><span data-stu-id="735ad-118">The results are inspected to determine if an alert should be created.</span></span>
- <span data-ttu-id="735ad-119">**Views.**</span><span class="sxs-lookup"><span data-stu-id="735ad-119">**Views.**</span></span>  <span data-ttu-id="735ad-120">You can create visualizations of data to be included in user dashboards with [View Designer](log-analytics-view-designer.md).</span><span class="sxs-lookup"><span data-stu-id="735ad-120">You can create visualizations of data to be included in user dashboards with [View Designer](log-analytics-view-designer.md).</span></span>  <span data-ttu-id="735ad-121">Log searches provide the data used by [tiles](log-analytics-view-designer-tiles.md) and [visualization parts](log-analytics-view-designer-parts.md) in each view.</span><span class="sxs-lookup"><span data-stu-id="735ad-121">Log searches provide the data used by [tiles](log-analytics-view-designer-tiles.md) and [visualization parts](log-analytics-view-designer-parts.md) in each view.</span></span>  <span data-ttu-id="735ad-122">You can drill down from visualization parts into the Log Search page to perform further analysis on the data.</span><span class="sxs-lookup"><span data-stu-id="735ad-122">You can drill down from visualization parts into the Log Search page to perform further analysis on the data.</span></span>
- <span data-ttu-id="735ad-123">**Export.**</span><span class="sxs-lookup"><span data-stu-id="735ad-123">**Export.**</span></span>  <span data-ttu-id="735ad-124">When you export data from the Log Analytics workspace to Excel or [Power BI](log-analytics-powerbi.md), you create a log search to define the data to export.</span><span class="sxs-lookup"><span data-stu-id="735ad-124">When you export data from the Log Analytics workspace to Excel or [Power BI](log-analytics-powerbi.md), you create a log search to define the data to export.</span></span>
- <span data-ttu-id="735ad-125">**PowerShell.**</span><span class="sxs-lookup"><span data-stu-id="735ad-125">**PowerShell.**</span></span> <span data-ttu-id="735ad-126">You can run a PowerShell script from a command line or an Azure Automation runbook that uses [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) to retrieve data from Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="735ad-126">You can run a PowerShell script from a command line or an Azure Automation runbook that uses [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) to retrieve data from Log Analytics.</span></span>  <span data-ttu-id="735ad-127">This cmdlet requires a query to determine the data to retrieve.</span><span class="sxs-lookup"><span data-stu-id="735ad-127">This cmdlet requires a query to determine the data to retrieve.</span></span>
- <span data-ttu-id="735ad-128">**Log Analytics API.**</span><span class="sxs-lookup"><span data-stu-id="735ad-128">**Log Analytics API.**</span></span>  <span data-ttu-id="735ad-129">The [Log Analytics log search API](log-analytics-log-search-api.md) allows any REST API client to retrieve data from the workspace.</span><span class="sxs-lookup"><span data-stu-id="735ad-129">The [Log Analytics log search API](log-analytics-log-search-api.md) allows any REST API client to retrieve data from the workspace.</span></span>  <span data-ttu-id="735ad-130">The API request includes a query that is run against Log Analytics to determine the data to retrieve.</span><span class="sxs-lookup"><span data-stu-id="735ad-130">The API request includes a query that is run against Log Analytics to determine the data to retrieve.</span></span>

![Log searches](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a><span data-ttu-id="735ad-132">How Log Analytics data is organized</span><span class="sxs-lookup"><span data-stu-id="735ad-132">How Log Analytics data is organized</span></span>
<span data-ttu-id="735ad-133">When you build a query, you start by determining which tables have the data that you're looking for.</span><span class="sxs-lookup"><span data-stu-id="735ad-133">When you build a query, you start by determining which tables have the data that you're looking for.</span></span> <span data-ttu-id="735ad-134">Each [data source](log-analytics-data-sources.md) and [solution](../operations-management-suite/operations-management-suite-solutions.md) stores its data in dedicated tables in the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="735ad-134">Each [data source](log-analytics-data-sources.md) and [solution](../operations-management-suite/operations-management-suite-solutions.md) stores its data in dedicated tables in the Log Analytics workspace.</span></span>  <span data-ttu-id="735ad-135">Documentation for each data source and solution includes the name of the data type that it creates and a description of each of its properties.</span><span class="sxs-lookup"><span data-stu-id="735ad-135">Documentation for each data source and solution includes the name of the data type that it creates and a description of each of its properties.</span></span>  <span data-ttu-id="735ad-136">Many queries will only require data from a single tables, but others may use a variety of options to include data from multiple tables.</span><span class="sxs-lookup"><span data-stu-id="735ad-136">Many queries will only require data from a single tables, but others may use a variety of options to include data from multiple tables.</span></span>

![Tables](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a><span data-ttu-id="735ad-138">Writing a query</span><span class="sxs-lookup"><span data-stu-id="735ad-138">Writing a query</span></span>
<span data-ttu-id="735ad-139">At the core of log searches in Log Analytics is [an extensive query language](https://docs.loganalytics.io/) that lets you retrieve and analyze data from the repository in a variety of ways.</span><span class="sxs-lookup"><span data-stu-id="735ad-139">At the core of log searches in Log Analytics is [an extensive query language](https://docs.loganalytics.io/) that lets you retrieve and analyze data from the repository in a variety of ways.</span></span>  <span data-ttu-id="735ad-140">This same query language is used for [Application Insights](../application-insights/app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="735ad-140">This same query language is used for [Application Insights](../application-insights/app-insights-analytics.md).</span></span>  <span data-ttu-id="735ad-141">Learning how to write a query is critical to creating log searches in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="735ad-141">Learning how to write a query is critical to creating log searches in Log Analytics.</span></span>  <span data-ttu-id="735ad-142">You'll typically start with basic queries and then progress to use more advanced functions as your requirements become more complex.</span><span class="sxs-lookup"><span data-stu-id="735ad-142">You'll typically start with basic queries and then progress to use more advanced functions as your requirements become more complex.</span></span>

<span data-ttu-id="735ad-143">The basic structure of a query is a source table followed by a series of operators separated by a pipe character `|`.</span><span class="sxs-lookup"><span data-stu-id="735ad-143">The basic structure of a query is a source table followed by a series of operators separated by a pipe character `|`.</span></span>  <span data-ttu-id="735ad-144">You can chain together multiple operators to refine the data and perform advanced functions.</span><span class="sxs-lookup"><span data-stu-id="735ad-144">You can chain together multiple operators to refine the data and perform advanced functions.</span></span>

<span data-ttu-id="735ad-145">For example, suppose you wanted to find the top ten computers with the most error events over the past day.</span><span class="sxs-lookup"><span data-stu-id="735ad-145">For example, suppose you wanted to find the top ten computers with the most error events over the past day.</span></span>

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

<span data-ttu-id="735ad-146">Or maybe you want to find computers that haven't had a heartbeat in the last day.</span><span class="sxs-lookup"><span data-stu-id="735ad-146">Or maybe you want to find computers that haven't had a heartbeat in the last day.</span></span>

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

<span data-ttu-id="735ad-147">How about a line chart with the processor utilization for each computer from last week?</span><span class="sxs-lookup"><span data-stu-id="735ad-147">How about a line chart with the processor utilization for each computer from last week?</span></span>

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

<span data-ttu-id="735ad-148">You can see from these quick samples that regardless of the kind of data that you're working with, the structure of the query is similar.</span><span class="sxs-lookup"><span data-stu-id="735ad-148">You can see from these quick samples that regardless of the kind of data that you're working with, the structure of the query is similar.</span></span>  <span data-ttu-id="735ad-149">You can break it down into distinct steps where the resulting data from one command is sent through the pipeline to the next command.</span><span class="sxs-lookup"><span data-stu-id="735ad-149">You can break it down into distinct steps where the resulting data from one command is sent through the pipeline to the next command.</span></span>

<span data-ttu-id="735ad-150">You can also query data across Log Analytics workspaces within your subscription.</span><span class="sxs-lookup"><span data-stu-id="735ad-150">You can also query data across Log Analytics workspaces within your subscription.</span></span>

    union Update, workspace("contoso-workspace").Update
    | where TimeGenerated >= ago(1h)
    | summarize dcount(Computer) by Classification 


<span data-ttu-id="735ad-151">For complete documentation on the Azure Log Analytics query language including tutorials and language reference, see the [Azure Log Analytics query language documentation](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="735ad-151">For complete documentation on the Azure Log Analytics query language including tutorials and language reference, see the [Azure Log Analytics query language documentation](https://docs.loganalytics.io/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="735ad-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="735ad-152">Next steps</span></span>

- <span data-ttu-id="735ad-153">Learn about the [portals that you use to create and edit log searches](log-analytics-log-search-portals.md).</span><span class="sxs-lookup"><span data-stu-id="735ad-153">Learn about the [portals that you use to create and edit log searches](log-analytics-log-search-portals.md).</span></span>
- <span data-ttu-id="735ad-154">Check out a [tutorial on writing queries](log-analytics-tutorial-viewdata.md) using the new query language.</span><span class="sxs-lookup"><span data-stu-id="735ad-154">Check out a [tutorial on writing queries](log-analytics-tutorial-viewdata.md) using the new query language.</span></span>
