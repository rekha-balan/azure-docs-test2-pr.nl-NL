---
title: Migrate your existing Azure data warehouse to premium storage | Microsoft Docs
description: Instructions for migrating an existing data warehouse to premium storage
services: sql-data-warehouse
documentationcenter: NA
author: happynicolle
manager: barbkess
editor: ''
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 213d35ed0c16ae22ece5aa09f6bfe193f40d0e69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550428"
---
# <a name="migrate-your-data-warehouse-to-premium-storage"></a><span data-ttu-id="96504-103">Migrate your data warehouse to premium storage</span><span class="sxs-lookup"><span data-stu-id="96504-103">Migrate your data warehouse to premium storage</span></span>
<span data-ttu-id="96504-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="96504-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="96504-105">Existing data warehouses currently on standard storage can now be migrated to premium storage.</span><span class="sxs-lookup"><span data-stu-id="96504-105">Existing data warehouses currently on standard storage can now be migrated to premium storage.</span></span> <span data-ttu-id="96504-106">You can take advantage of automatic migration, or if you prefer to control when to migrate (which does involve some downtime), you can do the migration yourself.</span><span class="sxs-lookup"><span data-stu-id="96504-106">You can take advantage of automatic migration, or if you prefer to control when to migrate (which does involve some downtime), you can do the migration yourself.</span></span>

<span data-ttu-id="96504-107">If you have more than one data warehouse, use the [automatic migration schedule][automatic migration schedule] to determine when it will also be migrated.</span><span class="sxs-lookup"><span data-stu-id="96504-107">If you have more than one data warehouse, use the [automatic migration schedule][automatic migration schedule] to determine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="96504-108">Determine storage type</span><span class="sxs-lookup"><span data-stu-id="96504-108">Determine storage type</span></span>
<span data-ttu-id="96504-109">If you created a data warehouse before the following dates, you are currently using standard storage.</span><span class="sxs-lookup"><span data-stu-id="96504-109">If you created a data warehouse before the following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="96504-110">**Region**</span><span class="sxs-lookup"><span data-stu-id="96504-110">**Region**</span></span> | <span data-ttu-id="96504-111">**Data warehouse created before this date**</span><span class="sxs-lookup"><span data-stu-id="96504-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="96504-112">Australia East</span><span class="sxs-lookup"><span data-stu-id="96504-112">Australia East</span></span> |<span data-ttu-id="96504-113">Premium storage not yet available</span><span class="sxs-lookup"><span data-stu-id="96504-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="96504-114">China East</span><span class="sxs-lookup"><span data-stu-id="96504-114">China East</span></span> |<span data-ttu-id="96504-115">November 1, 2016</span><span class="sxs-lookup"><span data-stu-id="96504-115">November 1, 2016</span></span> |
| <span data-ttu-id="96504-116">China North</span><span class="sxs-lookup"><span data-stu-id="96504-116">China North</span></span> |<span data-ttu-id="96504-117">November 1, 2016</span><span class="sxs-lookup"><span data-stu-id="96504-117">November 1, 2016</span></span> |
| <span data-ttu-id="96504-118">Germany Central</span><span class="sxs-lookup"><span data-stu-id="96504-118">Germany Central</span></span> |<span data-ttu-id="96504-119">November 1, 2016</span><span class="sxs-lookup"><span data-stu-id="96504-119">November 1, 2016</span></span> |
| <span data-ttu-id="96504-120">Germany Northeast</span><span class="sxs-lookup"><span data-stu-id="96504-120">Germany Northeast</span></span> |<span data-ttu-id="96504-121">November 1, 2016</span><span class="sxs-lookup"><span data-stu-id="96504-121">November 1, 2016</span></span> |
| <span data-ttu-id="96504-122">India West</span><span class="sxs-lookup"><span data-stu-id="96504-122">India West</span></span> |<span data-ttu-id="96504-123">Premium storage not yet available</span><span class="sxs-lookup"><span data-stu-id="96504-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="96504-124">Japan West</span><span class="sxs-lookup"><span data-stu-id="96504-124">Japan West</span></span> |<span data-ttu-id="96504-125">Premium storage not yet available</span><span class="sxs-lookup"><span data-stu-id="96504-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="96504-126">North Central US</span><span class="sxs-lookup"><span data-stu-id="96504-126">North Central US</span></span> |<span data-ttu-id="96504-127">November 10, 2016</span><span class="sxs-lookup"><span data-stu-id="96504-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="96504-128">Automatic migration details</span><span class="sxs-lookup"><span data-stu-id="96504-128">Automatic migration details</span></span>
<span data-ttu-id="96504-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during the [automatic migration schedule][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="96504-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during the [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="96504-130">Your existing data warehouse will be unusable during the migration.</span><span class="sxs-lookup"><span data-stu-id="96504-130">Your existing data warehouse will be unusable during the migration.</span></span> <span data-ttu-id="96504-131">The migration will take approximately one hour per terabyte of storage per data warehouse.</span><span class="sxs-lookup"><span data-stu-id="96504-131">The migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="96504-132">You will not be charged during any portion of the automatic migration.</span><span class="sxs-lookup"><span data-stu-id="96504-132">You will not be charged during any portion of the automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="96504-133">When the migration is complete, your data warehouse will be back online and usable.</span><span class="sxs-lookup"><span data-stu-id="96504-133">When the migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="96504-134">Microsoft is taking the following steps to complete the migration (these do not require any involvement on your part).</span><span class="sxs-lookup"><span data-stu-id="96504-134">Microsoft is taking the following steps to complete the migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="96504-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span><span class="sxs-lookup"><span data-stu-id="96504-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="96504-136">Microsoft renames “MyDW” to “MyDW_DO_NOT_USE_[Timestamp].”</span><span class="sxs-lookup"><span data-stu-id="96504-136">Microsoft renames “MyDW” to “MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="96504-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span><span class="sxs-lookup"><span data-stu-id="96504-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="96504-138">During this time, a backup is taken.</span><span class="sxs-lookup"><span data-stu-id="96504-138">During this time, a backup is taken.</span></span> <span data-ttu-id="96504-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span><span class="sxs-lookup"><span data-stu-id="96504-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="96504-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from the backup taken in step 2.</span><span class="sxs-lookup"><span data-stu-id="96504-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from the backup taken in step 2.</span></span> <span data-ttu-id="96504-141">“MyDW” will not appear until after the restore is complete.</span><span class="sxs-lookup"><span data-stu-id="96504-141">“MyDW” will not appear until after the restore is complete.</span></span>
4. <span data-ttu-id="96504-142">After the restore is complete, “MyDW” returns to the same data warehouse units and state (paused or active) that it was before the migration.</span><span class="sxs-lookup"><span data-stu-id="96504-142">After the restore is complete, “MyDW” returns to the same data warehouse units and state (paused or active) that it was before the migration.</span></span>
5. <span data-ttu-id="96504-143">After the migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span><span class="sxs-lookup"><span data-stu-id="96504-143">After the migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="96504-144">The following settings do not carry over as part of the migration:</span><span class="sxs-lookup"><span data-stu-id="96504-144">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="96504-145">Auditing at the database level needs to be re-enabled.</span><span class="sxs-lookup"><span data-stu-id="96504-145">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="96504-146">Firewall rules at the database level need to be re-added.</span><span class="sxs-lookup"><span data-stu-id="96504-146">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="96504-147">Firewall rules at the server level are not affected.</span><span class="sxs-lookup"><span data-stu-id="96504-147">Firewall rules at the server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="96504-148">Automatic migration schedule</span><span class="sxs-lookup"><span data-stu-id="96504-148">Automatic migration schedule</span></span>
<span data-ttu-id="96504-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during the following outage schedule.</span><span class="sxs-lookup"><span data-stu-id="96504-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during the following outage schedule.</span></span>

| <span data-ttu-id="96504-150">**Region**</span><span class="sxs-lookup"><span data-stu-id="96504-150">**Region**</span></span> | <span data-ttu-id="96504-151">**Estimated start date**</span><span class="sxs-lookup"><span data-stu-id="96504-151">**Estimated start date**</span></span> | <span data-ttu-id="96504-152">**Estimated end date**</span><span class="sxs-lookup"><span data-stu-id="96504-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="96504-153">Australia East</span><span class="sxs-lookup"><span data-stu-id="96504-153">Australia East</span></span> |<span data-ttu-id="96504-154">Not determined yet</span><span class="sxs-lookup"><span data-stu-id="96504-154">Not determined yet</span></span> |<span data-ttu-id="96504-155">Not determined yet</span><span class="sxs-lookup"><span data-stu-id="96504-155">Not determined yet</span></span> |
| <span data-ttu-id="96504-156">China East</span><span class="sxs-lookup"><span data-stu-id="96504-156">China East</span></span> |<span data-ttu-id="96504-157">January 9, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-157">January 9, 2017</span></span> |<span data-ttu-id="96504-158">January 13, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-158">January 13, 2017</span></span> |
| <span data-ttu-id="96504-159">China North</span><span class="sxs-lookup"><span data-stu-id="96504-159">China North</span></span> |<span data-ttu-id="96504-160">January 9, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-160">January 9, 2017</span></span> |<span data-ttu-id="96504-161">January 13, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-161">January 13, 2017</span></span> |
| <span data-ttu-id="96504-162">Germany Central</span><span class="sxs-lookup"><span data-stu-id="96504-162">Germany Central</span></span> |<span data-ttu-id="96504-163">January 9, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-163">January 9, 2017</span></span> |<span data-ttu-id="96504-164">January 13, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-164">January 13, 2017</span></span> |
| <span data-ttu-id="96504-165">Germany Northeast</span><span class="sxs-lookup"><span data-stu-id="96504-165">Germany Northeast</span></span> |<span data-ttu-id="96504-166">January 9, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-166">January 9, 2017</span></span> |<span data-ttu-id="96504-167">January 13, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-167">January 13, 2017</span></span> |
| <span data-ttu-id="96504-168">India West</span><span class="sxs-lookup"><span data-stu-id="96504-168">India West</span></span> |<span data-ttu-id="96504-169">Not determined yet</span><span class="sxs-lookup"><span data-stu-id="96504-169">Not determined yet</span></span> |<span data-ttu-id="96504-170">Not determined yet</span><span class="sxs-lookup"><span data-stu-id="96504-170">Not determined yet</span></span> |
| <span data-ttu-id="96504-171">Japan West</span><span class="sxs-lookup"><span data-stu-id="96504-171">Japan West</span></span> |<span data-ttu-id="96504-172">Not determined yet</span><span class="sxs-lookup"><span data-stu-id="96504-172">Not determined yet</span></span> |<span data-ttu-id="96504-173">Not determined yet</span><span class="sxs-lookup"><span data-stu-id="96504-173">Not determined yet</span></span> |
| <span data-ttu-id="96504-174">North Central US</span><span class="sxs-lookup"><span data-stu-id="96504-174">North Central US</span></span> |<span data-ttu-id="96504-175">January 9, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-175">January 9, 2017</span></span> |<span data-ttu-id="96504-176">January 13, 2017</span><span class="sxs-lookup"><span data-stu-id="96504-176">January 13, 2017</span></span> |

## <a name="self-migration-to-premium-storage"></a><span data-ttu-id="96504-177">Self-migration to premium storage</span><span class="sxs-lookup"><span data-stu-id="96504-177">Self-migration to premium storage</span></span>
<span data-ttu-id="96504-178">If you want to control when your downtime will occur, you can use the following steps to migrate an existing data warehouse on standard storage to premium storage.</span><span class="sxs-lookup"><span data-stu-id="96504-178">If you want to control when your downtime will occur, you can use the following steps to migrate an existing data warehouse on standard storage to premium storage.</span></span> <span data-ttu-id="96504-179">If you choose this option, you must complete the self-migration before the automatic migration begins in that region.</span><span class="sxs-lookup"><span data-stu-id="96504-179">If you choose this option, you must complete the self-migration before the automatic migration begins in that region.</span></span> <span data-ttu-id="96504-180">This ensures that you avoid any risk of the automatic migration causing a conflict (refer to the [automatic migration schedule][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="96504-180">This ensures that you avoid any risk of the automatic migration causing a conflict (refer to the [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="96504-181">Self-migration instructions</span><span class="sxs-lookup"><span data-stu-id="96504-181">Self-migration instructions</span></span>
<span data-ttu-id="96504-182">To migrate your data warehouse yourself, use the backup and restore features.</span><span class="sxs-lookup"><span data-stu-id="96504-182">To migrate your data warehouse yourself, use the backup and restore features.</span></span> <span data-ttu-id="96504-183">The restore portion of the migration is expected to take around one hour per terabyte of storage per data warehouse.</span><span class="sxs-lookup"><span data-stu-id="96504-183">The restore portion of the migration is expected to take around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="96504-184">If you want to keep the same name after migration is complete, follow the [steps to rename during migration][steps to rename during migration].</span><span class="sxs-lookup"><span data-stu-id="96504-184">If you want to keep the same name after migration is complete, follow the [steps to rename during migration][steps to rename during migration].</span></span>

1. <span data-ttu-id="96504-185">[Pause][Pause] your data warehouse.</span><span class="sxs-lookup"><span data-stu-id="96504-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="96504-186">This takes an automatic backup.</span><span class="sxs-lookup"><span data-stu-id="96504-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="96504-187">[Restore][Restore] from your most recent snapshot.</span><span class="sxs-lookup"><span data-stu-id="96504-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="96504-188">Delete your existing data warehouse on standard storage.</span><span class="sxs-lookup"><span data-stu-id="96504-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="96504-189">**If you fail to do this step, you will be charged for both data warehouses.**</span><span class="sxs-lookup"><span data-stu-id="96504-189">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="96504-190">The following settings do not carry over as part of the migration:</span><span class="sxs-lookup"><span data-stu-id="96504-190">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="96504-191">Auditing at the database level needs to be re-enabled.</span><span class="sxs-lookup"><span data-stu-id="96504-191">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="96504-192">Firewall rules at the database level need to be re-added.</span><span class="sxs-lookup"><span data-stu-id="96504-192">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="96504-193">Firewall rules at the server level are not affected.</span><span class="sxs-lookup"><span data-stu-id="96504-193">Firewall rules at the server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="96504-194">Rename data warehouse during migration (optional)</span><span class="sxs-lookup"><span data-stu-id="96504-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="96504-195">Two databases on the same logical server cannot have the same name.</span><span class="sxs-lookup"><span data-stu-id="96504-195">Two databases on the same logical server cannot have the same name.</span></span> <span data-ttu-id="96504-196">SQL Data Warehouse now supports the ability to rename a data warehouse.</span><span class="sxs-lookup"><span data-stu-id="96504-196">SQL Data Warehouse now supports the ability to rename a data warehouse.</span></span>

<span data-ttu-id="96504-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span><span class="sxs-lookup"><span data-stu-id="96504-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="96504-198">Rename "MyDW" by using the following ALTER DATABASE command.</span><span class="sxs-lookup"><span data-stu-id="96504-198">Rename "MyDW" by using the following ALTER DATABASE command.</span></span> <span data-ttu-id="96504-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in the master database to succeed.</span><span class="sxs-lookup"><span data-stu-id="96504-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in the master database to succeed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="96504-200">[Pause][Pause] "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="96504-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="96504-201">This takes an automatic backup.</span><span class="sxs-lookup"><span data-stu-id="96504-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="96504-202">[Restore][Restore] from your most recent snapshot a new database with the name it used to be (for example, "MyDW").</span><span class="sxs-lookup"><span data-stu-id="96504-202">[Restore][Restore] from your most recent snapshot a new database with the name it used to be (for example, "MyDW").</span></span>
4. <span data-ttu-id="96504-203">Delete "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="96504-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="96504-204">**If you fail to do this step, you will be charged for both data warehouses.**</span><span class="sxs-lookup"><span data-stu-id="96504-204">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="96504-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="96504-205">Next steps</span></span>
<span data-ttu-id="96504-206">With the change to premium storage, you also have an increased number of database blob files in the underlying architecture of your data warehouse.</span><span class="sxs-lookup"><span data-stu-id="96504-206">With the change to premium storage, you also have an increased number of database blob files in the underlying architecture of your data warehouse.</span></span> <span data-ttu-id="96504-207">To maximize the performance benefits of this change, rebuild your clustered columnstore indexes by using the following script.</span><span class="sxs-lookup"><span data-stu-id="96504-207">To maximize the performance benefits of this change, rebuild your clustered columnstore indexes by using the following script.</span></span> <span data-ttu-id="96504-208">The script works by forcing some of your existing data to the additional blobs.</span><span class="sxs-lookup"><span data-stu-id="96504-208">The script works by forcing some of your existing data to the additional blobs.</span></span> <span data-ttu-id="96504-209">If you take no action, the data will naturally redistribute over time as you load more data into your tables.</span><span class="sxs-lookup"><span data-stu-id="96504-209">If you take no action, the data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="96504-210">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="96504-210">**Prerequisites:**</span></span>

- <span data-ttu-id="96504-211">The data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="96504-211">The data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="96504-212">The user executing the script should be in the [mediumrc role][mediumrc role] or higher.</span><span class="sxs-lookup"><span data-stu-id="96504-212">The user executing the script should be in the [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="96504-213">To add a user to this role, execute the following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="96504-213">To add a user to this role, execute the following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table to control index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, the below can be re-run to restart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="96504-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration to premium storage” as the possible cause.</span><span class="sxs-lookup"><span data-stu-id="96504-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration to premium storage” as the possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps to rename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
