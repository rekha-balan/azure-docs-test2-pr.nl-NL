---
title: Use Azure Database Migration Service to monitor migration activity | Microsoft Docs
description: Learn to use the Azure Database Migration Service to monitor migration activity.
services: database-migration
author: HJToland3
ms.author: jtoland
manager: ''
ms.reviewer: ''
ms.service: database-migration
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 08/27/2018
ms.openlocfilehash: 78ad7a503cb2c99b9dac19a5500a01c8f7b7bfc3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855846"
---
# <a name="monitor-migration-activity"></a><span data-ttu-id="22d01-103">Monitor migration activity</span><span class="sxs-lookup"><span data-stu-id="22d01-103">Monitor migration activity</span></span>
<span data-ttu-id="22d01-104">In this article, you learn how to monitor the progress of a migration at both a database level and a table level.</span><span class="sxs-lookup"><span data-stu-id="22d01-104">In this article, you learn how to monitor the progress of a migration at both a database level and a table level.</span></span>

## <a name="monitor-at-the-database-level"></a><span data-ttu-id="22d01-105">Monitor at the database level</span><span class="sxs-lookup"><span data-stu-id="22d01-105">Monitor at the database level</span></span>
<span data-ttu-id="22d01-106">To monitor activity at the database level, view the database-level blade:</span><span class="sxs-lookup"><span data-stu-id="22d01-106">To monitor activity at the database level, view the database-level blade:</span></span>

![Database-level blade](media\how-to-monitor-migration-activity\dms-database-level-blade.png)

> [!NOTE]
> <span data-ttu-id="22d01-108">Selecting the database hyperlink will show you the list of tables and their migration progress.</span><span class="sxs-lookup"><span data-stu-id="22d01-108">Selecting the database hyperlink will show you the list of tables and their migration progress.</span></span>

<span data-ttu-id="22d01-109">The following table lists the fields on the database-level blade and describes the various status values associated with each.</span><span class="sxs-lookup"><span data-stu-id="22d01-109">The following table lists the fields on the database-level blade and describes the various status values associated with each.</span></span>

<table id='overview' class='overview'>
  <thead>
    <tr>
      <th class="x-hidden-focus"><span data-ttu-id="22d01-110"><strong>Field name</strong></span><span class="sxs-lookup"><span data-stu-id="22d01-110"><strong>Field name</strong></span></span></th>
      <th><span data-ttu-id="22d01-111"><strong>Field substatus</strong></span><span class="sxs-lookup"><span data-stu-id="22d01-111"><strong>Field substatus</strong></span></span></th>
      <th><span data-ttu-id="22d01-112"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="22d01-112"><strong>Description</strong></span></span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3" class="ActivityStatus"><span data-ttu-id="22d01-113"><strong>Activity status</strong></span><span class="sxs-lookup"><span data-stu-id="22d01-113"><strong>Activity status</strong></span></span></td>
      <td><span data-ttu-id="22d01-114">Running</span><span class="sxs-lookup"><span data-stu-id="22d01-114">Running</span></span></td>
      <td><span data-ttu-id="22d01-115">Migration activity is running.</span><span class="sxs-lookup"><span data-stu-id="22d01-115">Migration activity is running.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-116">Succeeded</span><span class="sxs-lookup"><span data-stu-id="22d01-116">Succeeded</span></span></td>
      <td><span data-ttu-id="22d01-117">Migration activity succeeded without issues.</span><span class="sxs-lookup"><span data-stu-id="22d01-117">Migration activity succeeded without issues.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-118">Faulted</span><span class="sxs-lookup"><span data-stu-id="22d01-118">Faulted</span></span></td>
      <td><span data-ttu-id="22d01-119">Migration failed.</span><span class="sxs-lookup"><span data-stu-id="22d01-119">Migration failed.</span></span> <span data-ttu-id="22d01-120">Select the ‘See error details’ link under migration details for the complete error message.</span><span class="sxs-lookup"><span data-stu-id="22d01-120">Select the ‘See error details’ link under migration details for the complete error message.</span></span></td>
    </tr>
    <tr>
      <td rowspan="4" class="Status"><span data-ttu-id="22d01-121"><strong>Status</strong></span><span class="sxs-lookup"><span data-stu-id="22d01-121"><strong>Status</strong></span></span></td>
      <td><span data-ttu-id="22d01-122">Initializing</span><span class="sxs-lookup"><span data-stu-id="22d01-122">Initializing</span></span></td>
      <td><span data-ttu-id="22d01-123">DMS is setting up the migration pipeline.</span><span class="sxs-lookup"><span data-stu-id="22d01-123">DMS is setting up the migration pipeline.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-124">Running</span><span class="sxs-lookup"><span data-stu-id="22d01-124">Running</span></span></td>
      <td><span data-ttu-id="22d01-125">DMS pipeline is running and performing migration.</span><span class="sxs-lookup"><span data-stu-id="22d01-125">DMS pipeline is running and performing migration.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-126">Complete</span><span class="sxs-lookup"><span data-stu-id="22d01-126">Complete</span></span></td>
      <td><span data-ttu-id="22d01-127">Migration completed.</span><span class="sxs-lookup"><span data-stu-id="22d01-127">Migration completed.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-128">Failed</span><span class="sxs-lookup"><span data-stu-id="22d01-128">Failed</span></span></td>
      <td><span data-ttu-id="22d01-129">Migration failed.</span><span class="sxs-lookup"><span data-stu-id="22d01-129">Migration failed.</span></span> <span data-ttu-id="22d01-130">Click on migration details to see migration errors.</span><span class="sxs-lookup"><span data-stu-id="22d01-130">Click on migration details to see migration errors.</span></span></td>
    </tr>
    <tr>
      <td rowspan="5" class="migration-details"><span data-ttu-id="22d01-131"><strong>Migration details</strong></span><span class="sxs-lookup"><span data-stu-id="22d01-131"><strong>Migration details</strong></span></span></td>
      <td><span data-ttu-id="22d01-132">Initiating the migration pipeline</span><span class="sxs-lookup"><span data-stu-id="22d01-132">Initiating the migration pipeline</span></span></td>
      <td><span data-ttu-id="22d01-133">DMS is setting up the migration pipeline.</span><span class="sxs-lookup"><span data-stu-id="22d01-133">DMS is setting up the migration pipeline.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-134">Full data load in progress</span><span class="sxs-lookup"><span data-stu-id="22d01-134">Full data load in progress</span></span></td>
      <td><span data-ttu-id="22d01-135">DMS is performing initial load.</span><span class="sxs-lookup"><span data-stu-id="22d01-135">DMS is performing initial load.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-136">Ready for Cutover</span><span class="sxs-lookup"><span data-stu-id="22d01-136">Ready for Cutover</span></span></td>
      <td><span data-ttu-id="22d01-137">After initial load is completed, DMS will mark database as ready for cutover.</span><span class="sxs-lookup"><span data-stu-id="22d01-137">After initial load is completed, DMS will mark database as ready for cutover.</span></span> <span data-ttu-id="22d01-138">User should check if data has caught up on continuous sync.</span><span class="sxs-lookup"><span data-stu-id="22d01-138">User should check if data has caught up on continuous sync.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-139">All changes applied</span><span class="sxs-lookup"><span data-stu-id="22d01-139">All changes applied</span></span></td>
      <td><span data-ttu-id="22d01-140">Initial load and continuous sync are complete.</span><span class="sxs-lookup"><span data-stu-id="22d01-140">Initial load and continuous sync are complete.</span></span> <span data-ttu-id="22d01-141">This status also occurs after the database is cutover successfully.</span><span class="sxs-lookup"><span data-stu-id="22d01-141">This status also occurs after the database is cutover successfully.</span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="22d01-142">See error details</span><span class="sxs-lookup"><span data-stu-id="22d01-142">See error details</span></span></td>
      <td><span data-ttu-id="22d01-143">Click on the link to show error details.</span><span class="sxs-lookup"><span data-stu-id="22d01-143">Click on the link to show error details.</span></span></td>
    </tr>
    <tr>
      <td rowspan="1" class="duration"><span data-ttu-id="22d01-144"><strong>Duration</strong></span><span class="sxs-lookup"><span data-stu-id="22d01-144"><strong>Duration</strong></span></span></td>
      <td><span data-ttu-id="22d01-145">N/A</span><span class="sxs-lookup"><span data-stu-id="22d01-145">N/A</span></span></td>
      <td><span data-ttu-id="22d01-146">Total time from migration activity being initialized to migration completed or migration faulted.</span><span class="sxs-lookup"><span data-stu-id="22d01-146">Total time from migration activity being initialized to migration completed or migration faulted.</span></span></td>
    </tr>
     </tbody>
</table>

## <a name="monitor-at-table-level--quick-summary"></a><span data-ttu-id="22d01-147">Monitor at table level – Quick Summary</span><span class="sxs-lookup"><span data-stu-id="22d01-147">Monitor at table level – Quick Summary</span></span>
<span data-ttu-id="22d01-148">To monitor activity at the table level, view the table-level blade.</span><span class="sxs-lookup"><span data-stu-id="22d01-148">To monitor activity at the table level, view the table-level blade.</span></span> <span data-ttu-id="22d01-149">The top portion of the blade shows the detailed number of rows migrated in full load and incremental updates.</span><span class="sxs-lookup"><span data-stu-id="22d01-149">The top portion of the blade shows the detailed number of rows migrated in full load and incremental updates.</span></span> 

<span data-ttu-id="22d01-150">The bottom portion of the blade lists the tables and shows a quick summary of migration progress.</span><span class="sxs-lookup"><span data-stu-id="22d01-150">The bottom portion of the blade lists the tables and shows a quick summary of migration progress.</span></span>

![Table-level blade - quick summary](media\how-to-monitor-migration-activity\dms-table-level-blade-summary.png)

<span data-ttu-id="22d01-152">The following table describes the fields shown in the table-level details.</span><span class="sxs-lookup"><span data-stu-id="22d01-152">The following table describes the fields shown in the table-level details.</span></span>

| <span data-ttu-id="22d01-153">Field name</span><span class="sxs-lookup"><span data-stu-id="22d01-153">Field name</span></span>        | <span data-ttu-id="22d01-154">Description</span><span class="sxs-lookup"><span data-stu-id="22d01-154">Description</span></span>       |
| ------------- | ------------- |
| <span data-ttu-id="22d01-155">**Full load completed**</span><span class="sxs-lookup"><span data-stu-id="22d01-155">**Full load completed**</span></span>      | <span data-ttu-id="22d01-156">Number of tables completed full data load.</span><span class="sxs-lookup"><span data-stu-id="22d01-156">Number of tables completed full data load.</span></span> |
| <span data-ttu-id="22d01-157">**Full load queued**</span><span class="sxs-lookup"><span data-stu-id="22d01-157">**Full load queued**</span></span>      | <span data-ttu-id="22d01-158">Number of tables being queued for full load.</span><span class="sxs-lookup"><span data-stu-id="22d01-158">Number of tables being queued for full load.</span></span>      |
| <span data-ttu-id="22d01-159">**Full load loading**</span><span class="sxs-lookup"><span data-stu-id="22d01-159">**Full load loading**</span></span> | <span data-ttu-id="22d01-160">Number of tables failed.</span><span class="sxs-lookup"><span data-stu-id="22d01-160">Number of tables failed.</span></span>      |
| <span data-ttu-id="22d01-161">**Incremental updates**</span><span class="sxs-lookup"><span data-stu-id="22d01-161">**Incremental updates**</span></span>      | <span data-ttu-id="22d01-162">Number of change data capture (CDC) updates in rows applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-162">Number of change data capture (CDC) updates in rows applied to target.</span></span> |
| <span data-ttu-id="22d01-163">**Incremental inserts**</span><span class="sxs-lookup"><span data-stu-id="22d01-163">**Incremental inserts**</span></span>      | <span data-ttu-id="22d01-164">Number of CDC inserts in rows applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-164">Number of CDC inserts in rows applied to target.</span></span>      |
| <span data-ttu-id="22d01-165">**Incremental deletes**</span><span class="sxs-lookup"><span data-stu-id="22d01-165">**Incremental deletes**</span></span> | <span data-ttu-id="22d01-166">Number of CDC deletes in rows applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-166">Number of CDC deletes in rows applied to target.</span></span>      |
| <span data-ttu-id="22d01-167">**Pending changes**</span><span class="sxs-lookup"><span data-stu-id="22d01-167">**Pending changes**</span></span>      | <span data-ttu-id="22d01-168">Number of CDC in rows that are still waiting to get applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-168">Number of CDC in rows that are still waiting to get applied to target.</span></span> |
| <span data-ttu-id="22d01-169">**Applied changes**</span><span class="sxs-lookup"><span data-stu-id="22d01-169">**Applied changes**</span></span>      | <span data-ttu-id="22d01-170">Total of CDC updates, inserts, and deletes in rows applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-170">Total of CDC updates, inserts, and deletes in rows applied to target.</span></span>      |
| <span data-ttu-id="22d01-171">**Tables in error state**</span><span class="sxs-lookup"><span data-stu-id="22d01-171">**Tables in error state**</span></span> | <span data-ttu-id="22d01-172">Number of tables that are in ‘error’ state during migration.</span><span class="sxs-lookup"><span data-stu-id="22d01-172">Number of tables that are in ‘error’ state during migration.</span></span> <span data-ttu-id="22d01-173">Some examples that tables can go into error state are when there are duplicates identified in the target or data isn't compatible loading in the target table.</span><span class="sxs-lookup"><span data-stu-id="22d01-173">Some examples that tables can go into error state are when there are duplicates identified in the target or data isn't compatible loading in the target table.</span></span>      |

## <a name="monitor-at-table-level--detailed-summary"></a><span data-ttu-id="22d01-174">Monitor at table level – Detailed Summary</span><span class="sxs-lookup"><span data-stu-id="22d01-174">Monitor at table level – Detailed Summary</span></span>
<span data-ttu-id="22d01-175">There are two tabs that show migration progress in Full load and Incremental data sync.</span><span class="sxs-lookup"><span data-stu-id="22d01-175">There are two tabs that show migration progress in Full load and Incremental data sync.</span></span>
    
![Full load tab](media\how-to-monitor-migration-activity\dms-full-load-tab.png)

![Incremental data sync tab](media\how-to-monitor-migration-activity\dms-incremental-data-sync-tab.png)

<span data-ttu-id="22d01-178">The following table describes the fields shown in table level migration progress.</span><span class="sxs-lookup"><span data-stu-id="22d01-178">The following table describes the fields shown in table level migration progress.</span></span>

| <span data-ttu-id="22d01-179">Field name</span><span class="sxs-lookup"><span data-stu-id="22d01-179">Field name</span></span>        | <span data-ttu-id="22d01-180">Description</span><span class="sxs-lookup"><span data-stu-id="22d01-180">Description</span></span>       |
| ------------- | ------------- |
| <span data-ttu-id="22d01-181">**Status - Syncing**</span><span class="sxs-lookup"><span data-stu-id="22d01-181">**Status - Syncing**</span></span>      | <span data-ttu-id="22d01-182">Continuous sync is running.</span><span class="sxs-lookup"><span data-stu-id="22d01-182">Continuous sync is running.</span></span> |
| <span data-ttu-id="22d01-183">**Insert**</span><span class="sxs-lookup"><span data-stu-id="22d01-183">**Insert**</span></span>      | <span data-ttu-id="22d01-184">Number of CDC inserts in rows applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-184">Number of CDC inserts in rows applied to target.</span></span>      |
| <span data-ttu-id="22d01-185">**Update**</span><span class="sxs-lookup"><span data-stu-id="22d01-185">**Update**</span></span> | <span data-ttu-id="22d01-186">Number of CDC updates in rows applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-186">Number of CDC updates in rows applied to target.</span></span>      |
| <span data-ttu-id="22d01-187">**Delete**</span><span class="sxs-lookup"><span data-stu-id="22d01-187">**Delete**</span></span>      | <span data-ttu-id="22d01-188">Number of CDC deletes in rows applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-188">Number of CDC deletes in rows applied to target.</span></span> |
| <span data-ttu-id="22d01-189">**Total Applied**</span><span class="sxs-lookup"><span data-stu-id="22d01-189">**Total Applied**</span></span>      | <span data-ttu-id="22d01-190">Total of CDC updates, inserts, and deletes in rows applied to target.</span><span class="sxs-lookup"><span data-stu-id="22d01-190">Total of CDC updates, inserts, and deletes in rows applied to target.</span></span> |
| <span data-ttu-id="22d01-191">**Data Errors**</span><span class="sxs-lookup"><span data-stu-id="22d01-191">**Data Errors**</span></span> | <span data-ttu-id="22d01-192">Number of data errors happened in this table.</span><span class="sxs-lookup"><span data-stu-id="22d01-192">Number of data errors happened in this table.</span></span> <span data-ttu-id="22d01-193">Some examples of the errors are *511: Cannot create a row of size %d which is greater than the allowable maximum row size of %d, 8114: Error converting data type %ls to %ls.*</span><span class="sxs-lookup"><span data-stu-id="22d01-193">Some examples of the errors are *511: Cannot create a row of size %d which is greater than the allowable maximum row size of %d, 8114: Error converting data type %ls to %ls.*</span></span>  <span data-ttu-id="22d01-194">Customer should query from attms_apply_exceptions table in Azure target to see the error details.</span><span class="sxs-lookup"><span data-stu-id="22d01-194">Customer should query from attms_apply_exceptions table in Azure target to see the error details.</span></span>    |

> [!NOTE]
> <span data-ttu-id="22d01-195">CDC values of Insert, Update and Delete and Total Applied may decrease when database is cutover or migration is restarted.</span><span class="sxs-lookup"><span data-stu-id="22d01-195">CDC values of Insert, Update and Delete and Total Applied may decrease when database is cutover or migration is restarted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22d01-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="22d01-196">Next steps</span></span>
- <span data-ttu-id="22d01-197">Review the migration guidance in the Microsoft [Database Migration Guide](https://datamigration.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="22d01-197">Review the migration guidance in the Microsoft [Database Migration Guide](https://datamigration.microsoft.com/).</span></span>