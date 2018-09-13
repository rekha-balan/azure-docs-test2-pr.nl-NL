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
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a>Use StorSimple Snapshot Manager to view and manage backup jobs
## <a name="overview"></a>Overview
The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy. 

This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs. (The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.

## <a name="view-scheduled-jobs"></a>View scheduled jobs
Use the following procedure to view scheduled backup jobs.

#### <a name="to-view-scheduled-jobs"></a>To view scheduled jobs
1. Click the desktop icon to start StorSimple Snapshot Manager. 
2. In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**. The following information appears in the **Results** pane:
   
   * **Name** – the name of the scheduled snapshot
   * **Next Run** – the date and time of the next scheduled snapshot
   * **Last Run** – the date and time of the most recent scheduled snapshot
     
     > [!NOTE]
     > For one-time only snapshots, the **Next Run** and **Last Run** will be the same. 
     > 
     > 
     
     ![Scheduled backup jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.

## <a name="view-recent-jobs"></a>View recent jobs
Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.

#### <a name="to-view-recent-jobs"></a>To view recent jobs
1. Click the desktop icon to start StorSimple Snapshot Manager.
2. In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**. The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs). The following information appears in the **Results** pane, depending on the **View** options you specify:
   
   * **Name** – the name of the scheduled snapshot.
   * **Started** – the date and time when the snapshot began.
   * **Stopped** – the date and time when the snapshot finished or was terminated.
   * **Elapsed** – the amount of time between the **Started** and **Stopped** times.
   * **Status** – the state of the recently completed job. **Success** indicates that the backup was created successfully. **Failed** indicates that the job did not run successfully.
   * **Information** – the reason for the failure.
   * **Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs). 
     
     ![Jobs that ran in the last 24 hours](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.
   
    ![Delete a job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png) 

## <a name="view-currently-running-jobs"></a>View currently running jobs
Use the following procedure to view jobs that are currently running.

#### <a name="to-view-currently-running-jobs"></a>To view currently running jobs
1. Click the desktop icon to start StorSimple Snapshot Manager.
2. In the **Scope** pane, expand the **Jobs** node, and click **Running**. Depending on the **View** options you specify, the following information appears in the **Results** pane: 
   
   * **Name** – the name of the scheduled snapshot.
   * **Started** – the date and time when the snapshot began.
   * **Checkpoint** – the current action of the backup.
   * **Status** – the percentage of completion.
   * **Elapsed** – the amount of time that has passed since the backup began. 
   * **Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).
   * **Bytes processed (MB)** – total bytes of data processed (in MBs).
   * **Bytes written (MB)** – total bytes of data written (in MBs). It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.
     
     ![Jobs currently running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.

## <a name="next-steps"></a>Next steps
* Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).
* Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).





