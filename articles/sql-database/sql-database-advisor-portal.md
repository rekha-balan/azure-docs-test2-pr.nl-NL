---
title: Azure SQL Database Advisor using the Azure portal | Microsoft Docs
description: You can use the Azure SQL Database Advisor in the Azure portal to review and implement recommendations for your existing SQL Databases that can improve current query performance.
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor and tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: 46479e84dcebef86c72fcef9ce1fef2edf066885
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554148"
---
# <a name="sql-database-advisor-using-the-azure-portal"></a><span data-ttu-id="4e03b-103">SQL Database Advisor using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4e03b-103">SQL Database Advisor using the Azure portal</span></span>

<span data-ttu-id="4e03b-104">You can use the Azure SQL Database Advisor in the Azure portal to review and implement recommendations for your existing SQL Databases that can improve current query performance.</span><span class="sxs-lookup"><span data-stu-id="4e03b-104">You can use the Azure SQL Database Advisor in the Azure portal to review and implement recommendations for your existing SQL Databases that can improve current query performance.</span></span>

## <a name="viewing-recommendations"></a><span data-ttu-id="4e03b-105">Viewing recommendations</span><span class="sxs-lookup"><span data-stu-id="4e03b-105">Viewing recommendations</span></span>
<span data-ttu-id="4e03b-106">The recommendations page is where you view the top recommendations based on their potential impact to improve performance.</span><span class="sxs-lookup"><span data-stu-id="4e03b-106">The recommendations page is where you view the top recommendations based on their potential impact to improve performance.</span></span> <span data-ttu-id="4e03b-107">You can also view the status of the historical operations.</span><span class="sxs-lookup"><span data-stu-id="4e03b-107">You can also view the status of the historical operations.</span></span> <span data-ttu-id="4e03b-108">Select a recommendation or status to see  more details.</span><span class="sxs-lookup"><span data-stu-id="4e03b-108">Select a recommendation or status to see  more details.</span></span>

<span data-ttu-id="4e03b-109">To view and apply recommendations, you need the correct [role-based access control](../active-directory/role-based-access-control-configure.md) permissions in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e03b-109">To view and apply recommendations, you need the correct [role-based access control](../active-directory/role-based-access-control-configure.md) permissions in Azure.</span></span> <span data-ttu-id="4e03b-110">**Reader**, **SQL DB Contributor** permissions are required to view recommendations, and **Owner**, **SQL DB Contributor** permissions are required to execute any actions; create or drop indexes and cancel index creation.</span><span class="sxs-lookup"><span data-stu-id="4e03b-110">**Reader**, **SQL DB Contributor** permissions are required to view recommendations, and **Owner**, **SQL DB Contributor** permissions are required to execute any actions; create or drop indexes and cancel index creation.</span></span>

1. <span data-ttu-id="4e03b-111">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4e03b-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4e03b-112">Click **More services** > **SQL databases**, and select your database.</span><span class="sxs-lookup"><span data-stu-id="4e03b-112">Click **More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="4e03b-113">Click **Performance recommendation** to view available recommendations for the selected database.</span><span class="sxs-lookup"><span data-stu-id="4e03b-113">Click **Performance recommendation** to view available recommendations for the selected database.</span></span>

> [!NOTE]
> <span data-ttu-id="4e03b-114">To get recommendations a database needs to have about a day of usage, and there needs to be some activity.</span><span class="sxs-lookup"><span data-stu-id="4e03b-114">To get recommendations a database needs to have about a day of usage, and there needs to be some activity.</span></span> <span data-ttu-id="4e03b-115">There also needs to be some consistent activity.</span><span class="sxs-lookup"><span data-stu-id="4e03b-115">There also needs to be some consistent activity.</span></span> <span data-ttu-id="4e03b-116">The SQL Database Advisor can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span><span class="sxs-lookup"><span data-stu-id="4e03b-116">The SQL Database Advisor can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="4e03b-117">If recommendations are not available, the **Performance recommendation** page should provide a message explaining why.</span><span class="sxs-lookup"><span data-stu-id="4e03b-117">If recommendations are not available, the **Performance recommendation** page should provide a message explaining why.</span></span>
> 
> 

![Recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="4e03b-119">Here is an example of "Fix schema issue" recommendation in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4e03b-119">Here is an example of "Fix schema issue" recommendation in the Azure portal.</span></span>

![Fix Schema Issue](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-advisor-portal/sql-database-advisor-schema-issue.png)

<span data-ttu-id="4e03b-121">Recommendations are sorted by their potential impact on performance into the following four categories:</span><span class="sxs-lookup"><span data-stu-id="4e03b-121">Recommendations are sorted by their potential impact on performance into the following four categories:</span></span>

| <span data-ttu-id="4e03b-122">Impact</span><span class="sxs-lookup"><span data-stu-id="4e03b-122">Impact</span></span> | <span data-ttu-id="4e03b-123">Description</span><span class="sxs-lookup"><span data-stu-id="4e03b-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e03b-124">High</span><span class="sxs-lookup"><span data-stu-id="4e03b-124">High</span></span> |<span data-ttu-id="4e03b-125">High impact recommendations should provide the most significant performance impact.</span><span class="sxs-lookup"><span data-stu-id="4e03b-125">High impact recommendations should provide the most significant performance impact.</span></span> |
| <span data-ttu-id="4e03b-126">Medium</span><span class="sxs-lookup"><span data-stu-id="4e03b-126">Medium</span></span> |<span data-ttu-id="4e03b-127">Medium impact recommendations should improve performance, but not substantially.</span><span class="sxs-lookup"><span data-stu-id="4e03b-127">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="4e03b-128">Low</span><span class="sxs-lookup"><span data-stu-id="4e03b-128">Low</span></span> |<span data-ttu-id="4e03b-129">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span><span class="sxs-lookup"><span data-stu-id="4e03b-129">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |

### <a name="removing-recommendations-from-the-list"></a><span data-ttu-id="4e03b-130">Removing recommendations from the list</span><span class="sxs-lookup"><span data-stu-id="4e03b-130">Removing recommendations from the list</span></span>
<span data-ttu-id="4e03b-131">If your list of recommendations contains items that you want to remove from the list, you can discard the recommendation:</span><span class="sxs-lookup"><span data-stu-id="4e03b-131">If your list of recommendations contains items that you want to remove from the list, you can discard the recommendation:</span></span>

1. <span data-ttu-id="4e03b-132">Select a recommendation in the list of **Recommendations**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-132">Select a recommendation in the list of **Recommendations**.</span></span>
2. <span data-ttu-id="4e03b-133">Click **Discard** on the **Details** blade.</span><span class="sxs-lookup"><span data-stu-id="4e03b-133">Click **Discard** on the **Details** blade.</span></span>

<span data-ttu-id="4e03b-134">If desired, you can add discarded items back to the **Recommendations** list:</span><span class="sxs-lookup"><span data-stu-id="4e03b-134">If desired, you can add discarded items back to the **Recommendations** list:</span></span>

1. <span data-ttu-id="4e03b-135">On the **Recommendations** blade click **View discarded**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-135">On the **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="4e03b-136">Select a discarded item from the list to view its details.</span><span class="sxs-lookup"><span data-stu-id="4e03b-136">Select a discarded item from the list to view its details.</span></span>
3. <span data-ttu-id="4e03b-137">Optionally, click **Undo Discard** to add the index back to the main list of **Recommendations**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-137">Optionally, click **Undo Discard** to add the index back to the main list of **Recommendations**.</span></span>

## <a name="applying-recommendations"></a><span data-ttu-id="4e03b-138">Applying recommendations</span><span class="sxs-lookup"><span data-stu-id="4e03b-138">Applying recommendations</span></span>
<span data-ttu-id="4e03b-139">SQL Database Advisor gives you full control over how recommendations are enabled using any of the following three options:</span><span class="sxs-lookup"><span data-stu-id="4e03b-139">SQL Database Advisor gives you full control over how recommendations are enabled using any of the following three options:</span></span> 

* <span data-ttu-id="4e03b-140">Apply individual recommendations one at a time.</span><span class="sxs-lookup"><span data-stu-id="4e03b-140">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="4e03b-141">Enable the advisor to automatically apply recommendations (currently applies to index recommendations only).</span><span class="sxs-lookup"><span data-stu-id="4e03b-141">Enable the advisor to automatically apply recommendations (currently applies to index recommendations only).</span></span>
* <span data-ttu-id="4e03b-142">To implement a recommendation manually, run the recommended T-SQL script against your database .</span><span class="sxs-lookup"><span data-stu-id="4e03b-142">To implement a recommendation manually, run the recommended T-SQL script against your database .</span></span>

<span data-ttu-id="4e03b-143">Select any recommendation to view its details and then click **View script** to review the exact details of how the recommendation is created.</span><span class="sxs-lookup"><span data-stu-id="4e03b-143">Select any recommendation to view its details and then click **View script** to review the exact details of how the recommendation is created.</span></span>

<span data-ttu-id="4e03b-144">The database remains online while the advisor applies the recommendation -- using SQL Database Advisor never takes a database offline.</span><span class="sxs-lookup"><span data-stu-id="4e03b-144">The database remains online while the advisor applies the recommendation -- using SQL Database Advisor never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="4e03b-145">Apply an individual recommendation</span><span class="sxs-lookup"><span data-stu-id="4e03b-145">Apply an individual recommendation</span></span>
<span data-ttu-id="4e03b-146">You can review and accept recommendations one at a time.</span><span class="sxs-lookup"><span data-stu-id="4e03b-146">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="4e03b-147">On the **Recommendations** blade, click a recommendation.</span><span class="sxs-lookup"><span data-stu-id="4e03b-147">On the **Recommendations** blade, click a recommendation.</span></span>
2. <span data-ttu-id="4e03b-148">On the **Details** blade click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-148">On the **Details** blade click **Apply**.</span></span>
   
    ![Apply recommendation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-advisor-portal/apply.png)

### <a name="enable-automatic-index-management"></a><span data-ttu-id="4e03b-150">Enable automatic index management</span><span class="sxs-lookup"><span data-stu-id="4e03b-150">Enable automatic index management</span></span>
<span data-ttu-id="4e03b-151">You can set the SQL Database Advisor to implement recommendations automatically.</span><span class="sxs-lookup"><span data-stu-id="4e03b-151">You can set the SQL Database Advisor to implement recommendations automatically.</span></span> <span data-ttu-id="4e03b-152">As recommendations become available they will automatically be applied.</span><span class="sxs-lookup"><span data-stu-id="4e03b-152">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="4e03b-153">As with all index operations managed by the service if the performance impact is negative the recommendation will be reverted.</span><span class="sxs-lookup"><span data-stu-id="4e03b-153">As with all index operations managed by the service if the performance impact is negative the recommendation will be reverted.</span></span>

1. <span data-ttu-id="4e03b-154">On the **Recommendations** blade, click **Automate**:</span><span class="sxs-lookup"><span data-stu-id="4e03b-154">On the **Recommendations** blade, click **Automate**:</span></span>
   
    ![Advisor settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="4e03b-156">Set the advisor to automatically **Create** or **Drop** indexes:</span><span class="sxs-lookup"><span data-stu-id="4e03b-156">Set the advisor to automatically **Create** or **Drop** indexes:</span></span>
   
    ![Recommended Indexes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-the-recommended-t-sql-script"></a><span data-ttu-id="4e03b-158">Manually run the recommended T-SQL script</span><span class="sxs-lookup"><span data-stu-id="4e03b-158">Manually run the recommended T-SQL script</span></span>
<span data-ttu-id="4e03b-159">Select any recommendation and then click **View script**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-159">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="4e03b-160">Run this script against your database to manually apply the recommendation.</span><span class="sxs-lookup"><span data-stu-id="4e03b-160">Run this script against your database to manually apply the recommendation.</span></span>

<span data-ttu-id="4e03b-161">*Indexes that are manually executed are not monitored and validated for performance impact by the service* so it is suggested that you monitor these indexes after creation to verify they provide performance gains and adjust or delete them if necessary.</span><span class="sxs-lookup"><span data-stu-id="4e03b-161">*Indexes that are manually executed are not monitored and validated for performance impact by the service* so it is suggested that you monitor these indexes after creation to verify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="4e03b-162">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e03b-162">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="4e03b-163">Canceling recommendations</span><span class="sxs-lookup"><span data-stu-id="4e03b-163">Canceling recommendations</span></span>
<span data-ttu-id="4e03b-164">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span><span class="sxs-lookup"><span data-stu-id="4e03b-164">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="4e03b-165">Recommendations with a status of **Executing** cannot be canceled.</span><span class="sxs-lookup"><span data-stu-id="4e03b-165">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="4e03b-166">Select a recommendation in the **Tuning History** area to open the **recommendations details** blade.</span><span class="sxs-lookup"><span data-stu-id="4e03b-166">Select a recommendation in the **Tuning History** area to open the **recommendations details** blade.</span></span>
2. <span data-ttu-id="4e03b-167">Click **Cancel** to abort the process of applying the recommendation.</span><span class="sxs-lookup"><span data-stu-id="4e03b-167">Click **Cancel** to abort the process of applying the recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="4e03b-168">Monitoring operations</span><span class="sxs-lookup"><span data-stu-id="4e03b-168">Monitoring operations</span></span>
<span data-ttu-id="4e03b-169">Applying a recommendation might not happen instantaneously.</span><span class="sxs-lookup"><span data-stu-id="4e03b-169">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="4e03b-170">The portal provides details regarding the status of recommendation operations.</span><span class="sxs-lookup"><span data-stu-id="4e03b-170">The portal provides details regarding the status of recommendation operations.</span></span> <span data-ttu-id="4e03b-171">The following are possible states that an index can be in:</span><span class="sxs-lookup"><span data-stu-id="4e03b-171">The following are possible states that an index can be in:</span></span>

| <span data-ttu-id="4e03b-172">Status</span><span class="sxs-lookup"><span data-stu-id="4e03b-172">Status</span></span> | <span data-ttu-id="4e03b-173">Description</span><span class="sxs-lookup"><span data-stu-id="4e03b-173">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e03b-174">Pending</span><span class="sxs-lookup"><span data-stu-id="4e03b-174">Pending</span></span> |<span data-ttu-id="4e03b-175">Apply recommendation command has been received and is scheduled for execution.</span><span class="sxs-lookup"><span data-stu-id="4e03b-175">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="4e03b-176">Executing</span><span class="sxs-lookup"><span data-stu-id="4e03b-176">Executing</span></span> |<span data-ttu-id="4e03b-177">The recommendation is being applied.</span><span class="sxs-lookup"><span data-stu-id="4e03b-177">The recommendation is being applied.</span></span> |
| <span data-ttu-id="4e03b-178">Success</span><span class="sxs-lookup"><span data-stu-id="4e03b-178">Success</span></span> |<span data-ttu-id="4e03b-179">Recommendation was successfully applied.</span><span class="sxs-lookup"><span data-stu-id="4e03b-179">Recommendation was successfully applied.</span></span> |
| <span data-ttu-id="4e03b-180">Error</span><span class="sxs-lookup"><span data-stu-id="4e03b-180">Error</span></span> |<span data-ttu-id="4e03b-181">An error occurred during the process of applying the recommendation.</span><span class="sxs-lookup"><span data-stu-id="4e03b-181">An error occurred during the process of applying the recommendation.</span></span> <span data-ttu-id="4e03b-182">This can be a transient issue, or possibly a schema change to the table and the script is no longer valid.</span><span class="sxs-lookup"><span data-stu-id="4e03b-182">This can be a transient issue, or possibly a schema change to the table and the script is no longer valid.</span></span> |
| <span data-ttu-id="4e03b-183">Reverting</span><span class="sxs-lookup"><span data-stu-id="4e03b-183">Reverting</span></span> |<span data-ttu-id="4e03b-184">The recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span><span class="sxs-lookup"><span data-stu-id="4e03b-184">The recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="4e03b-185">Reverted</span><span class="sxs-lookup"><span data-stu-id="4e03b-185">Reverted</span></span> |<span data-ttu-id="4e03b-186">The recommendation was reverted.</span><span class="sxs-lookup"><span data-stu-id="4e03b-186">The recommendation was reverted.</span></span> |

<span data-ttu-id="4e03b-187">Click an in-process recommendation from the list to see more details:</span><span class="sxs-lookup"><span data-stu-id="4e03b-187">Click an in-process recommendation from the list to see more details:</span></span>

![Recommended Indexes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="4e03b-189">Reverting a recommendation</span><span class="sxs-lookup"><span data-stu-id="4e03b-189">Reverting a recommendation</span></span>
<span data-ttu-id="4e03b-190">If you used the advisor to apply the recommendation (meaning you did not manually run the T-SQL script) it will automatically revert it if it finds the performance impact to be negative.</span><span class="sxs-lookup"><span data-stu-id="4e03b-190">If you used the advisor to apply the recommendation (meaning you did not manually run the T-SQL script) it will automatically revert it if it finds the performance impact to be negative.</span></span> <span data-ttu-id="4e03b-191">If for any reason you simply want to revert a recommendation you can do the following:</span><span class="sxs-lookup"><span data-stu-id="4e03b-191">If for any reason you simply want to revert a recommendation you can do the following:</span></span>

1. <span data-ttu-id="4e03b-192">Select a successfully applied recommendation in the **Tuning history** area.</span><span class="sxs-lookup"><span data-stu-id="4e03b-192">Select a successfully applied recommendation in the **Tuning history** area.</span></span>
2. <span data-ttu-id="4e03b-193">Click **Revert** on the **recommendation details** blade.</span><span class="sxs-lookup"><span data-stu-id="4e03b-193">Click **Revert** on the **recommendation details** blade.</span></span>

![Recommended Indexes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="4e03b-195">Monitoring performance impact of index recommendations</span><span class="sxs-lookup"><span data-stu-id="4e03b-195">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="4e03b-196">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on the recommendation details blade to open [Query Performance Insights](sql-database-query-performance.md) and see the performance impact of your top queries.</span><span class="sxs-lookup"><span data-stu-id="4e03b-196">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on the recommendation details blade to open [Query Performance Insights](sql-database-query-performance.md) and see the performance impact of your top queries.</span></span>

![Monitor performance impact](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="4e03b-198">Summary</span><span class="sxs-lookup"><span data-stu-id="4e03b-198">Summary</span></span>
<span data-ttu-id="4e03b-199">SQL Database Advisor provides recommendations for improving SQL database performance.</span><span class="sxs-lookup"><span data-stu-id="4e03b-199">SQL Database Advisor provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="4e03b-200">By providing T-SQL scripts, as well as individual and fully-automatic (currently index only), the advisor provides helpful assistance in optimizing your database and ultimately improving query performance.</span><span class="sxs-lookup"><span data-stu-id="4e03b-200">By providing T-SQL scripts, as well as individual and fully-automatic (currently index only), the advisor provides helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e03b-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e03b-201">Next steps</span></span>
<span data-ttu-id="4e03b-202">Monitor your recommendations and continue to apply them to refine performance.</span><span class="sxs-lookup"><span data-stu-id="4e03b-202">Monitor your recommendations and continue to apply them to refine performance.</span></span> <span data-ttu-id="4e03b-203">Database workloads are dynamic and change continuously.</span><span class="sxs-lookup"><span data-stu-id="4e03b-203">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="4e03b-204">SQL Database advisor will continue to monitor and provide recommendations that can potentially improve your database's performance.</span><span class="sxs-lookup"><span data-stu-id="4e03b-204">SQL Database advisor will continue to monitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="4e03b-205">See [SQL Database Advisor](sql-database-advisor.md) for an overview of SQL Database Advisor.</span><span class="sxs-lookup"><span data-stu-id="4e03b-205">See [SQL Database Advisor](sql-database-advisor.md) for an overview of SQL Database Advisor.</span></span>
* <span data-ttu-id="4e03b-206">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span><span class="sxs-lookup"><span data-stu-id="4e03b-206">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e03b-207">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4e03b-207">Additional resources</span></span>
* [<span data-ttu-id="4e03b-208">Query Store</span><span class="sxs-lookup"><span data-stu-id="4e03b-208">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="4e03b-209">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="4e03b-209">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="4e03b-210">Role-based access control</span><span class="sxs-lookup"><span data-stu-id="4e03b-210">Role-based access control</span></span>](../active-directory/role-based-access-control-configure.md)









