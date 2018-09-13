---
title: View and manage StorSimple Virtual Array jobs | Microsoft Docs
description: Describes the StorSimple Device Manager service Jobs page and how to use it to track recent and current jobs for the StorSimple Virtual Array.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: fc13aa40574192b5f6244d1a6836cd774b162eaa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662879"
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a>Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array
## <a name="overview"></a>Overview
The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service. You can view running, completed, and failed jobs for multiple virtual devices. Results are presented in a tabular format.

![Jobs blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

You can quickly find the jobs you are interested in by filtering on fields such as:

* **Time range** – Jobs can be filtered based on the date and time range.
* **Devices** – Jobs are initiated on a specific device connected to your service. The filtered jobs are then tabulated based on the following attributes:
  
  * **Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.
  * **Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.
  * **Entity** – The jobs can be associated with a volume, share, or device.
  * **Device** – The name of the device on which the job was started.
  * **Started on** – The time when the job was started.
  * **Duration** – The duration for on which the job was run.
* **Status** – You can search for all, running, completed, or failed jobs.
* **Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.

The list of jobs is refreshed every 30 seconds.

## <a name="view-job-details"></a>View job details
Perform the following steps to view the details of any job.

#### <a name="to-view-job-details"></a>To view job details
1. On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters. You can search for completed or running jobs.
2. Select a job from the tabular list of jobs.
   
    ![Job blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. At the bottom of the page, click **Details**.
4. In the **Details** dialog box, you can view status, details, and time statistics. The following illustration shows an example of the **Backup Job Details** dialog box.
   
    ![Job details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a>Job failures when the virtual machine is paused in the hypervisor
When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails. This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time. 

You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes. Ensure that the hypervisor and the device times are synchronized with an NTP servier. Verify that there are no connectivity issues. To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."

These failures apply to backup, restore, update, and failover jobs. If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor. Once that happens, you can restart your job.

## <a name="next-steps"></a>Next steps
[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).




