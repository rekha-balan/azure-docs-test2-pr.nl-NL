---
title: View and manage StorSimple jobs | Microsoft Docs
description: Describes the StorSimple Manager service Jobs page and how to use it to track recent, current, and scheduled backup jobs.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b4ba577d0b7c5767d7f0d8ab292cf89bc58a3d96
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549521"
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs"></a>Use the StorSimple Manager service to view and manage StorSimple jobs
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Overview
The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service. You can view scheduled, running, completed, and failed jobs for multiple devices. Results are presented in a tabular format. 

![Jobs page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-jobs/HCS_JobsPage.png)

You can quickly find the jobs you are interested in by filtering on fields such as:

* **Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.
* **Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.
* **Devices** – Jobs are initiated on a certain device connected to your service.
* **From and To** – Jobs can be filtered based on the date and time range.

The filtered jobs are then tabulated on the basis of the following attributes:

* **Type** – Backup, clone, restore, failover, or update.
* **Status** – Running, scheduled, failed, completed, canceling, or canceled.
* **Entity** – The jobs can be associated with a volume, a backup policy, or a device. A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy. A device job is created as a result of a disaster recovery (DR) or a restore operation.
* **Device** – The name of the device on which the job was started.
* **Started On** – The time when the job was started.
* **Progress** – The percentage completion of a running job. For a completed job, this should always be 100%.

The list of jobs is refreshed every 30 seconds.

You can perform the following job-related actions on this page:

* View job details
* Cancel a job

## <a name="view-job-details"></a>View job details
Perform the following steps to view the details of any job.

#### <a name="to-view-job-details"></a>To view job details
1. On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters. You can search for completed, running, or canceled jobs.
2. Select a job.
3. At the bottom of the page, click **Details**.
4. In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.

## <a name="cancel-a-job"></a>Cancel a job
Perform the following steps to cancel a running job.

### <a name="to-cancel-a-job"></a>To cancel a job
1. On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.
2. Select the job.
3. At the bottom of the page, click **Cancel**.
4. When prompted for confirmation, click **Yes**.

This job is now canceled.

## <a name="next-steps"></a>Next steps
* Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).
* Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).


