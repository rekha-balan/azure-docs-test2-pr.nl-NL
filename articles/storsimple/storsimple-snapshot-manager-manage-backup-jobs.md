---
title: StorSimple Snapshot Manager backup jobs | Microsoft Docs
description: Describes how to use the StorSimple Snapshot Manager MMC snap-in to view and manage scheduled, currently running, and completed backup jobs.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: ''
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/26/2016
ms.author: v-sharos
ms.openlocfilehash: ab27da17ad46ce72a111e2e0f7ce2bdb2cc3ba95
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564023"
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="3bccd-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span><span class="sxs-lookup"><span data-stu-id="3bccd-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>
## <a name="overview"></a><span data-ttu-id="3bccd-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3bccd-104">Overview</span></span>
<span data-ttu-id="3bccd-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span><span class="sxs-lookup"><span data-stu-id="3bccd-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="3bccd-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span><span class="sxs-lookup"><span data-stu-id="3bccd-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="3bccd-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span><span class="sxs-lookup"><span data-stu-id="3bccd-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="3bccd-108">View scheduled jobs</span><span class="sxs-lookup"><span data-stu-id="3bccd-108">View scheduled jobs</span></span>
<span data-ttu-id="3bccd-109">Use the following procedure to view scheduled backup jobs.</span><span class="sxs-lookup"><span data-stu-id="3bccd-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="3bccd-110">To view scheduled jobs</span><span class="sxs-lookup"><span data-stu-id="3bccd-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="3bccd-111">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="3bccd-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="3bccd-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span><span class="sxs-lookup"><span data-stu-id="3bccd-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="3bccd-113">The following information appears in the **Results** pane:</span><span class="sxs-lookup"><span data-stu-id="3bccd-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="3bccd-114">**Name** – the name of the scheduled snapshot</span><span class="sxs-lookup"><span data-stu-id="3bccd-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="3bccd-115">**Next Run** – the date and time of the next scheduled snapshot</span><span class="sxs-lookup"><span data-stu-id="3bccd-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="3bccd-116">**Last Run** – the date and time of the most recent scheduled snapshot</span><span class="sxs-lookup"><span data-stu-id="3bccd-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="3bccd-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span><span class="sxs-lookup"><span data-stu-id="3bccd-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span> 
     > 
     > 
     
     ![Scheduled backup jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="3bccd-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span><span class="sxs-lookup"><span data-stu-id="3bccd-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="3bccd-120">View recent jobs</span><span class="sxs-lookup"><span data-stu-id="3bccd-120">View recent jobs</span></span>
<span data-ttu-id="3bccd-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="3bccd-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="3bccd-122">To view recent jobs</span><span class="sxs-lookup"><span data-stu-id="3bccd-122">To view recent jobs</span></span>
1. <span data-ttu-id="3bccd-123">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="3bccd-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3bccd-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span><span class="sxs-lookup"><span data-stu-id="3bccd-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="3bccd-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span><span class="sxs-lookup"><span data-stu-id="3bccd-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="3bccd-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span><span class="sxs-lookup"><span data-stu-id="3bccd-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="3bccd-127">**Name** – the name of the scheduled snapshot.</span><span class="sxs-lookup"><span data-stu-id="3bccd-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="3bccd-128">**Started** – the date and time when the snapshot began.</span><span class="sxs-lookup"><span data-stu-id="3bccd-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="3bccd-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span><span class="sxs-lookup"><span data-stu-id="3bccd-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="3bccd-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span><span class="sxs-lookup"><span data-stu-id="3bccd-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="3bccd-131">**Status** – the state of the recently completed job.</span><span class="sxs-lookup"><span data-stu-id="3bccd-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="3bccd-132">**Success** indicates that the backup was created successfully.</span><span class="sxs-lookup"><span data-stu-id="3bccd-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="3bccd-133">**Failed** indicates that the job did not run successfully.</span><span class="sxs-lookup"><span data-stu-id="3bccd-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="3bccd-134">**Information** – the reason for the failure.</span><span class="sxs-lookup"><span data-stu-id="3bccd-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="3bccd-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span><span class="sxs-lookup"><span data-stu-id="3bccd-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![Jobs that ran in the last 24 hours](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="3bccd-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span><span class="sxs-lookup"><span data-stu-id="3bccd-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![Delete a job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png) 

## <a name="view-currently-running-jobs"></a><span data-ttu-id="3bccd-139">View currently running jobs</span><span class="sxs-lookup"><span data-stu-id="3bccd-139">View currently running jobs</span></span>
<span data-ttu-id="3bccd-140">Use the following procedure to view jobs that are currently running.</span><span class="sxs-lookup"><span data-stu-id="3bccd-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="3bccd-141">To view currently running jobs</span><span class="sxs-lookup"><span data-stu-id="3bccd-141">To view currently running jobs</span></span>
1. <span data-ttu-id="3bccd-142">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="3bccd-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3bccd-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span><span class="sxs-lookup"><span data-stu-id="3bccd-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="3bccd-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span><span class="sxs-lookup"><span data-stu-id="3bccd-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span> 
   
   * <span data-ttu-id="3bccd-145">**Name** – the name of the scheduled snapshot.</span><span class="sxs-lookup"><span data-stu-id="3bccd-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="3bccd-146">**Started** – the date and time when the snapshot began.</span><span class="sxs-lookup"><span data-stu-id="3bccd-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="3bccd-147">**Checkpoint** – the current action of the backup.</span><span class="sxs-lookup"><span data-stu-id="3bccd-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="3bccd-148">**Status** – the percentage of completion.</span><span class="sxs-lookup"><span data-stu-id="3bccd-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="3bccd-149">**Elapsed** – the amount of time that has passed since the backup began.</span><span class="sxs-lookup"><span data-stu-id="3bccd-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="3bccd-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span><span class="sxs-lookup"><span data-stu-id="3bccd-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="3bccd-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span><span class="sxs-lookup"><span data-stu-id="3bccd-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="3bccd-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span><span class="sxs-lookup"><span data-stu-id="3bccd-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="3bccd-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span><span class="sxs-lookup"><span data-stu-id="3bccd-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![Jobs currently running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="3bccd-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span><span class="sxs-lookup"><span data-stu-id="3bccd-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bccd-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="3bccd-156">Next steps</span></span>
* <span data-ttu-id="3bccd-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="3bccd-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="3bccd-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="3bccd-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>





