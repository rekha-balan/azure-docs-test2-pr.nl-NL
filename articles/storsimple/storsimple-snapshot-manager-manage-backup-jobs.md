---
title: StorSimple Snapshot Manager backup jobs | Microsoft Docs
description: Describes how to use the StorSimple Snapshot Manager MMC snap-in to view and manage scheduled, currently running, and completed backup jobs.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: ''
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819031"
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="1aa71-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span><span class="sxs-lookup"><span data-stu-id="1aa71-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="1aa71-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1aa71-104">Overview</span></span>
<span data-ttu-id="1aa71-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span><span class="sxs-lookup"><span data-stu-id="1aa71-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="1aa71-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span><span class="sxs-lookup"><span data-stu-id="1aa71-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="1aa71-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span><span class="sxs-lookup"><span data-stu-id="1aa71-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="1aa71-108">View scheduled jobs</span><span class="sxs-lookup"><span data-stu-id="1aa71-108">View scheduled jobs</span></span>
<span data-ttu-id="1aa71-109">Use the following procedure to view scheduled backup jobs.</span><span class="sxs-lookup"><span data-stu-id="1aa71-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="1aa71-110">To view scheduled jobs</span><span class="sxs-lookup"><span data-stu-id="1aa71-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="1aa71-111">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1aa71-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="1aa71-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span><span class="sxs-lookup"><span data-stu-id="1aa71-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="1aa71-113">The following information appears in the **Results** pane:</span><span class="sxs-lookup"><span data-stu-id="1aa71-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="1aa71-114">**Name** – the name of the scheduled snapshot</span><span class="sxs-lookup"><span data-stu-id="1aa71-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="1aa71-115">**Next Run** – the date and time of the next scheduled snapshot</span><span class="sxs-lookup"><span data-stu-id="1aa71-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="1aa71-116">**Last Run** – the date and time of the most recent scheduled snapshot</span><span class="sxs-lookup"><span data-stu-id="1aa71-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="1aa71-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span><span class="sxs-lookup"><span data-stu-id="1aa71-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span>
     
     ![Scheduled backup jobs](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="1aa71-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span><span class="sxs-lookup"><span data-stu-id="1aa71-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="1aa71-120">View recent jobs</span><span class="sxs-lookup"><span data-stu-id="1aa71-120">View recent jobs</span></span>
<span data-ttu-id="1aa71-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="1aa71-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="1aa71-122">To view recent jobs</span><span class="sxs-lookup"><span data-stu-id="1aa71-122">To view recent jobs</span></span>
1. <span data-ttu-id="1aa71-123">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1aa71-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1aa71-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span><span class="sxs-lookup"><span data-stu-id="1aa71-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="1aa71-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span><span class="sxs-lookup"><span data-stu-id="1aa71-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="1aa71-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span><span class="sxs-lookup"><span data-stu-id="1aa71-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="1aa71-127">**Name** – the name of the scheduled snapshot.</span><span class="sxs-lookup"><span data-stu-id="1aa71-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="1aa71-128">**Started** – the date and time when the snapshot began.</span><span class="sxs-lookup"><span data-stu-id="1aa71-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="1aa71-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span><span class="sxs-lookup"><span data-stu-id="1aa71-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="1aa71-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span><span class="sxs-lookup"><span data-stu-id="1aa71-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="1aa71-131">**Status** – the state of the recently completed job.</span><span class="sxs-lookup"><span data-stu-id="1aa71-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="1aa71-132">**Success** indicates that the backup was created successfully.</span><span class="sxs-lookup"><span data-stu-id="1aa71-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="1aa71-133">**Failed** indicates that the job did not run successfully.</span><span class="sxs-lookup"><span data-stu-id="1aa71-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="1aa71-134">**Information** – the reason for the failure.</span><span class="sxs-lookup"><span data-stu-id="1aa71-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="1aa71-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span><span class="sxs-lookup"><span data-stu-id="1aa71-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![Jobs that ran in the last 24 hours](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="1aa71-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span><span class="sxs-lookup"><span data-stu-id="1aa71-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![Delete a job](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="1aa71-139">View currently running jobs</span><span class="sxs-lookup"><span data-stu-id="1aa71-139">View currently running jobs</span></span>
<span data-ttu-id="1aa71-140">Use the following procedure to view jobs that are currently running.</span><span class="sxs-lookup"><span data-stu-id="1aa71-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="1aa71-141">To view currently running jobs</span><span class="sxs-lookup"><span data-stu-id="1aa71-141">To view currently running jobs</span></span>
1. <span data-ttu-id="1aa71-142">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1aa71-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1aa71-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span><span class="sxs-lookup"><span data-stu-id="1aa71-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="1aa71-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span><span class="sxs-lookup"><span data-stu-id="1aa71-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="1aa71-145">**Name** – the name of the scheduled snapshot.</span><span class="sxs-lookup"><span data-stu-id="1aa71-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="1aa71-146">**Started** – the date and time when the snapshot began.</span><span class="sxs-lookup"><span data-stu-id="1aa71-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="1aa71-147">**Checkpoint** – the current action of the backup.</span><span class="sxs-lookup"><span data-stu-id="1aa71-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="1aa71-148">**Status** – the percentage of completion.</span><span class="sxs-lookup"><span data-stu-id="1aa71-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="1aa71-149">**Elapsed** – the amount of time that has passed since the backup began.</span><span class="sxs-lookup"><span data-stu-id="1aa71-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="1aa71-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span><span class="sxs-lookup"><span data-stu-id="1aa71-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="1aa71-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span><span class="sxs-lookup"><span data-stu-id="1aa71-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="1aa71-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span><span class="sxs-lookup"><span data-stu-id="1aa71-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="1aa71-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span><span class="sxs-lookup"><span data-stu-id="1aa71-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![Jobs currently running](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="1aa71-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span><span class="sxs-lookup"><span data-stu-id="1aa71-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aa71-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="1aa71-156">Next steps</span></span>
* <span data-ttu-id="1aa71-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1aa71-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="1aa71-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="1aa71-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

