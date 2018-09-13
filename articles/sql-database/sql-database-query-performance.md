---
title: Query performance insights for Azure SQL Database  | Microsoft Docs
description: Query performance monitoring identifies the most CPU-consuming queries for an Azure SQL Database.
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor and tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/09/2016
ms.author: sstein
ms.openlocfilehash: 7516c82a55d3a09c8c0e78e05adac1dd8fa17ecc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663070"
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="167a9-103">Azure SQL Database Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="167a9-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="167a9-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span><span class="sxs-lookup"><span data-stu-id="167a9-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="167a9-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span><span class="sxs-lookup"><span data-stu-id="167a9-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span></span>

* <span data-ttu-id="167a9-106">Deeper insight into your databases resource (DTU) consumption.</span><span class="sxs-lookup"><span data-stu-id="167a9-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="167a9-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span><span class="sxs-lookup"><span data-stu-id="167a9-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="167a9-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span><span class="sxs-lookup"><span data-stu-id="167a9-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="167a9-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="167a9-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="167a9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="167a9-110">Prerequisites</span></span>
* <span data-ttu-id="167a9-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span><span class="sxs-lookup"><span data-stu-id="167a9-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="167a9-112">If Query Store is not running, the portal prompts you to turn it on.</span><span class="sxs-lookup"><span data-stu-id="167a9-112">If Query Store is not running, the portal prompts you to turn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="167a9-113">Permissions</span><span class="sxs-lookup"><span data-stu-id="167a9-113">Permissions</span></span>
<span data-ttu-id="167a9-114">The following [role-based access control](../active-directory/role-based-access-control-configure.md) permissions are required to use Query Performance Insight:</span><span class="sxs-lookup"><span data-stu-id="167a9-114">The following [role-based access control](../active-directory/role-based-access-control-configure.md) permissions are required to use Query Performance Insight:</span></span> 

* <span data-ttu-id="167a9-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span><span class="sxs-lookup"><span data-stu-id="167a9-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="167a9-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span><span class="sxs-lookup"><span data-stu-id="167a9-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="167a9-117">Using Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="167a9-117">Using Query Performance Insight</span></span>
<span data-ttu-id="167a9-118">Query Performance Insight is easy to use:</span><span class="sxs-lookup"><span data-stu-id="167a9-118">Query Performance Insight is easy to use:</span></span>

* <span data-ttu-id="167a9-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span><span class="sxs-lookup"><span data-stu-id="167a9-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span></span> 
  * <span data-ttu-id="167a9-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span><span class="sxs-lookup"><span data-stu-id="167a9-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="167a9-121">On the first tab, review the list of top resource-consuming queries.</span><span class="sxs-lookup"><span data-stu-id="167a9-121">On the first tab, review the list of top resource-consuming queries.</span></span>
* <span data-ttu-id="167a9-122">Select an individual query to view its details.</span><span class="sxs-lookup"><span data-stu-id="167a9-122">Select an individual query to view its details.</span></span>
* <span data-ttu-id="167a9-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span><span class="sxs-lookup"><span data-stu-id="167a9-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="167a9-124">Use sliders or zoom icons to change observed interval.</span><span class="sxs-lookup"><span data-stu-id="167a9-124">Use sliders or zoom icons to change observed interval.</span></span>
  
    ![performance dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="167a9-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span><span class="sxs-lookup"><span data-stu-id="167a9-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span></span> <span data-ttu-id="167a9-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span><span class="sxs-lookup"><span data-stu-id="167a9-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span></span> <span data-ttu-id="167a9-128">You may enable Query Store at any time if it is not running.</span><span class="sxs-lookup"><span data-stu-id="167a9-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="167a9-129">Review top CPU consuming queries</span><span class="sxs-lookup"><span data-stu-id="167a9-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="167a9-130">In the [portal](http://portal.azure.com) do the following:</span><span class="sxs-lookup"><span data-stu-id="167a9-130">In the [portal](http://portal.azure.com) do the following:</span></span>

1. <span data-ttu-id="167a9-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span><span class="sxs-lookup"><span data-stu-id="167a9-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Query Performance Insight][1]
   
    <span data-ttu-id="167a9-133">The top queries view opens and the top CPU consuming queries are listed.</span><span class="sxs-lookup"><span data-stu-id="167a9-133">The top queries view opens and the top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="167a9-134">Click around the chart for details.</span><span class="sxs-lookup"><span data-stu-id="167a9-134">Click around the chart for details.</span></span><br><span data-ttu-id="167a9-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span><span class="sxs-lookup"><span data-stu-id="167a9-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![top queries][2]
   
    <span data-ttu-id="167a9-137">The bottom grid represents aggregated information for the visible queries.</span><span class="sxs-lookup"><span data-stu-id="167a9-137">The bottom grid represents aggregated information for the visible queries.</span></span>
   
   * <span data-ttu-id="167a9-138">Query ID - unique identifier of query inside database.</span><span class="sxs-lookup"><span data-stu-id="167a9-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="167a9-139">CPU per query during observable interval (depends on aggregation function).</span><span class="sxs-lookup"><span data-stu-id="167a9-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="167a9-140">Duration per query (depends on aggregation function).</span><span class="sxs-lookup"><span data-stu-id="167a9-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="167a9-141">Total number of executions for a particular query.</span><span class="sxs-lookup"><span data-stu-id="167a9-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="167a9-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span><span class="sxs-lookup"><span data-stu-id="167a9-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span></span>
3. <span data-ttu-id="167a9-143">If your data becomes stale, click the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="167a9-143">If your data becomes stale, click the **Refresh** button.</span></span>
4. <span data-ttu-id="167a9-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="167a9-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="167a9-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span><span class="sxs-lookup"><span data-stu-id="167a9-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="167a9-146">Metric (CPU, duration, execution count)</span><span class="sxs-lookup"><span data-stu-id="167a9-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="167a9-147">Time interval (Last 24 hours, Past week, Past month).</span><span class="sxs-lookup"><span data-stu-id="167a9-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="167a9-148">Number of queries.</span><span class="sxs-lookup"><span data-stu-id="167a9-148">Number of queries.</span></span>
   * <span data-ttu-id="167a9-149">Aggregation function.</span><span class="sxs-lookup"><span data-stu-id="167a9-149">Aggregation function.</span></span>
     
     ![settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="167a9-151">Viewing individual query details</span><span class="sxs-lookup"><span data-stu-id="167a9-151">Viewing individual query details</span></span>
<span data-ttu-id="167a9-152">To view query details:</span><span class="sxs-lookup"><span data-stu-id="167a9-152">To view query details:</span></span>

1. <span data-ttu-id="167a9-153">Click any query in the list of top queries.</span><span class="sxs-lookup"><span data-stu-id="167a9-153">Click any query in the list of top queries.</span></span>
   
    ![details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/details.png)
2. <span data-ttu-id="167a9-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span><span class="sxs-lookup"><span data-stu-id="167a9-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="167a9-156">Click around the chart for details.</span><span class="sxs-lookup"><span data-stu-id="167a9-156">Click around the chart for details.</span></span>
   
   * <span data-ttu-id="167a9-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span><span class="sxs-lookup"><span data-stu-id="167a9-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span></span>
   * <span data-ttu-id="167a9-158">Second chart shows total duration by the selected query.</span><span class="sxs-lookup"><span data-stu-id="167a9-158">Second chart shows total duration by the selected query.</span></span>
   * <span data-ttu-id="167a9-159">Bottom chart shows total number of executions by the selected query.</span><span class="sxs-lookup"><span data-stu-id="167a9-159">Bottom chart shows total number of executions by the selected query.</span></span>
     
     ![query details][3]
4. <span data-ttu-id="167a9-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span><span class="sxs-lookup"><span data-stu-id="167a9-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="167a9-162">Review top queries per duration</span><span class="sxs-lookup"><span data-stu-id="167a9-162">Review top queries per duration</span></span>
<span data-ttu-id="167a9-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span><span class="sxs-lookup"><span data-stu-id="167a9-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="167a9-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span><span class="sxs-lookup"><span data-stu-id="167a9-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="167a9-165">They are also the best candidates for optimization.</span><span class="sxs-lookup"><span data-stu-id="167a9-165">They are also the best candidates for optimization.</span></span><br>

<span data-ttu-id="167a9-166">To identify long running queries:</span><span class="sxs-lookup"><span data-stu-id="167a9-166">To identify long running queries:</span></span>

1. <span data-ttu-id="167a9-167">Open **Custom** tab in Query Performance Insight for selected database</span><span class="sxs-lookup"><span data-stu-id="167a9-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="167a9-168">Change metrics to be **duration**</span><span class="sxs-lookup"><span data-stu-id="167a9-168">Change metrics to be **duration**</span></span>
3. <span data-ttu-id="167a9-169">Select number of queries and observation interval</span><span class="sxs-lookup"><span data-stu-id="167a9-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="167a9-170">Select aggregation function</span><span class="sxs-lookup"><span data-stu-id="167a9-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="167a9-171">**Sum** adds up all query execution time during whole observation interval.</span><span class="sxs-lookup"><span data-stu-id="167a9-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="167a9-172">**Max** finds queries which execution time was maximum at whole observation interval.</span><span class="sxs-lookup"><span data-stu-id="167a9-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="167a9-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span><span class="sxs-lookup"><span data-stu-id="167a9-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span></span> 
     
     ![query duration][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="167a9-175">Review top queries per execution count</span><span class="sxs-lookup"><span data-stu-id="167a9-175">Review top queries per execution count</span></span>
<span data-ttu-id="167a9-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span><span class="sxs-lookup"><span data-stu-id="167a9-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="167a9-177">In some cases, very high execution count may lead to increase of network round trips.</span><span class="sxs-lookup"><span data-stu-id="167a9-177">In some cases, very high execution count may lead to increase of network round trips.</span></span> <span data-ttu-id="167a9-178">Round trips significantly affect performance.</span><span class="sxs-lookup"><span data-stu-id="167a9-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="167a9-179">They are subject to network latency and to downstream server latency.</span><span class="sxs-lookup"><span data-stu-id="167a9-179">They are subject to network latency and to downstream server latency.</span></span> 

<span data-ttu-id="167a9-180">For example, many data-driven Web sites heavily access the database for every user request.</span><span class="sxs-lookup"><span data-stu-id="167a9-180">For example, many data-driven Web sites heavily access the database for every user request.</span></span> <span data-ttu-id="167a9-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span><span class="sxs-lookup"><span data-stu-id="167a9-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span></span>  <span data-ttu-id="167a9-182">General advice is to keep round trips to an absolute minimum.</span><span class="sxs-lookup"><span data-stu-id="167a9-182">General advice is to keep round trips to an absolute minimum.</span></span>

<span data-ttu-id="167a9-183">To identify frequently executed queries (“chatty”) queries:</span><span class="sxs-lookup"><span data-stu-id="167a9-183">To identify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="167a9-184">Open **Custom** tab in Query Performance Insight for selected database</span><span class="sxs-lookup"><span data-stu-id="167a9-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="167a9-185">Change metrics to be **execution count**</span><span class="sxs-lookup"><span data-stu-id="167a9-185">Change metrics to be **execution count**</span></span>
3. <span data-ttu-id="167a9-186">Select number of queries and observation interval</span><span class="sxs-lookup"><span data-stu-id="167a9-186">Select number of queries and observation interval</span></span>
   
    ![query execution count][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="167a9-188">Understanding performance tuning annotations</span><span class="sxs-lookup"><span data-stu-id="167a9-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="167a9-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span><span class="sxs-lookup"><span data-stu-id="167a9-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span></span><br>

<span data-ttu-id="167a9-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="167a9-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="167a9-191">By hovering annotation, you get basic information about the action:</span><span class="sxs-lookup"><span data-stu-id="167a9-191">By hovering annotation, you get basic information about the action:</span></span>

![query annotation][6]

<span data-ttu-id="167a9-193">If you want to know more or apply advisor recommendation, click the icon.</span><span class="sxs-lookup"><span data-stu-id="167a9-193">If you want to know more or apply advisor recommendation, click the icon.</span></span> <span data-ttu-id="167a9-194">It will open details of action.</span><span class="sxs-lookup"><span data-stu-id="167a9-194">It will open details of action.</span></span> <span data-ttu-id="167a9-195">If it’s an active recommendation you can apply it straight away using command.</span><span class="sxs-lookup"><span data-stu-id="167a9-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![query annotation details][7]

### <a name="multiple-annotations"></a><span data-ttu-id="167a9-197">Multiple annotations.</span><span class="sxs-lookup"><span data-stu-id="167a9-197">Multiple annotations.</span></span>
<span data-ttu-id="167a9-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span><span class="sxs-lookup"><span data-stu-id="167a9-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span></span> <span data-ttu-id="167a9-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span><span class="sxs-lookup"><span data-stu-id="167a9-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="167a9-200">Correlating queries and performance tuning actions can help to better understand your workload.</span><span class="sxs-lookup"><span data-stu-id="167a9-200">Correlating queries and performance tuning actions can help to better understand your workload.</span></span> 

## <a name="optimizing-the-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="167a9-201">Optimizing the Query Store configuration for Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="167a9-201">Optimizing the Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="167a9-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span><span class="sxs-lookup"><span data-stu-id="167a9-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span></span>

* <span data-ttu-id="167a9-203">"Query Store is not properly configured on this database.</span><span class="sxs-lookup"><span data-stu-id="167a9-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="167a9-204">Click here to learn more."</span><span class="sxs-lookup"><span data-stu-id="167a9-204">Click here to learn more."</span></span>
* <span data-ttu-id="167a9-205">"Query Store is not properly configured on this database.</span><span class="sxs-lookup"><span data-stu-id="167a9-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="167a9-206">Click here to change settings."</span><span class="sxs-lookup"><span data-stu-id="167a9-206">Click here to change settings."</span></span> 

<span data-ttu-id="167a9-207">These messages usually appear when Query Store is not able to collect new data.</span><span class="sxs-lookup"><span data-stu-id="167a9-207">These messages usually appear when Query Store is not able to collect new data.</span></span> 

<span data-ttu-id="167a9-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span><span class="sxs-lookup"><span data-stu-id="167a9-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="167a9-209">You can fix this by increasing size of Query Store or clearing Query Store.</span><span class="sxs-lookup"><span data-stu-id="167a9-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![qds button][8]

<span data-ttu-id="167a9-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span><span class="sxs-lookup"><span data-stu-id="167a9-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="167a9-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span><span class="sxs-lookup"><span data-stu-id="167a9-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![qds button][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="167a9-214">Recommended retention and capture policy</span><span class="sxs-lookup"><span data-stu-id="167a9-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="167a9-215">There are two types of retention policies:</span><span class="sxs-lookup"><span data-stu-id="167a9-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="167a9-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span><span class="sxs-lookup"><span data-stu-id="167a9-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="167a9-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span><span class="sxs-lookup"><span data-stu-id="167a9-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="167a9-218">Capture policy could be set to:</span><span class="sxs-lookup"><span data-stu-id="167a9-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="167a9-219">**All** - Captures all queries.</span><span class="sxs-lookup"><span data-stu-id="167a9-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="167a9-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span><span class="sxs-lookup"><span data-stu-id="167a9-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="167a9-221">Thresholds for execution count, compile and runtime duration are internally determined.</span><span class="sxs-lookup"><span data-stu-id="167a9-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="167a9-222">This is the default option.</span><span class="sxs-lookup"><span data-stu-id="167a9-222">This is the default option.</span></span>
* <span data-ttu-id="167a9-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span><span class="sxs-lookup"><span data-stu-id="167a9-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="167a9-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span><span class="sxs-lookup"><span data-stu-id="167a9-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="167a9-225">Increase size of Query Store.</span><span class="sxs-lookup"><span data-stu-id="167a9-225">Increase size of Query Store.</span></span> <span data-ttu-id="167a9-226">This could be performed by connecting to a database and issuing following query:</span><span class="sxs-lookup"><span data-stu-id="167a9-226">This could be performed by connecting to a database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="167a9-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span><span class="sxs-lookup"><span data-stu-id="167a9-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="167a9-228">Executing following query will delete all current information in the Query Store.</span><span class="sxs-lookup"><span data-stu-id="167a9-228">Executing following query will delete all current information in the Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="167a9-229">Summary</span><span class="sxs-lookup"><span data-stu-id="167a9-229">Summary</span></span>
<span data-ttu-id="167a9-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span><span class="sxs-lookup"><span data-stu-id="167a9-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span></span> <span data-ttu-id="167a9-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span><span class="sxs-lookup"><span data-stu-id="167a9-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="167a9-232">Next steps</span><span class="sxs-lookup"><span data-stu-id="167a9-232">Next steps</span></span>
<span data-ttu-id="167a9-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span><span class="sxs-lookup"><span data-stu-id="167a9-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span></span>

![Performance Advisor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/tile.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/top-queries.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/query-details.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/top-duration.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/top-execution.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/annotation.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/annotation-details.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/qds-off.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-query-performance/qds-button.png















