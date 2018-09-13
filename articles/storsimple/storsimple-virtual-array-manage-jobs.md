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
ms.openlocfilehash: 3fd1c262a8ce94d8e98f2b066a8028d974b15b1d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44815690"
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="d21c1-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="d21c1-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="d21c1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d21c1-104">Overview</span></span>
<span data-ttu-id="d21c1-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="d21c1-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="d21c1-106">You can view running, completed, and failed jobs for multiple virtual devices.</span><span class="sxs-lookup"><span data-stu-id="d21c1-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="d21c1-107">Results are presented in a tabular format.</span><span class="sxs-lookup"><span data-stu-id="d21c1-107">Results are presented in a tabular format.</span></span>

![Jobs blade](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="d21c1-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span><span class="sxs-lookup"><span data-stu-id="d21c1-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="d21c1-110">**Time range** – Jobs can be filtered based on the date and time range.</span><span class="sxs-lookup"><span data-stu-id="d21c1-110">**Time range** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="d21c1-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span><span class="sxs-lookup"><span data-stu-id="d21c1-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="d21c1-112">The filtered jobs are then tabulated based on the following attributes:</span><span class="sxs-lookup"><span data-stu-id="d21c1-112">The filtered jobs are then tabulated based on the following attributes:</span></span>
  
  * <span data-ttu-id="d21c1-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span><span class="sxs-lookup"><span data-stu-id="d21c1-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="d21c1-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span><span class="sxs-lookup"><span data-stu-id="d21c1-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="d21c1-115">**Entity** – The jobs can be associated with a volume, share, or device.</span><span class="sxs-lookup"><span data-stu-id="d21c1-115">**Entity** – The jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="d21c1-116">**Device** – The name of the device on which the job was started.</span><span class="sxs-lookup"><span data-stu-id="d21c1-116">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="d21c1-117">**Started on** – The time when the job was started.</span><span class="sxs-lookup"><span data-stu-id="d21c1-117">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="d21c1-118">**Duration** – The duration for on which the job was run.</span><span class="sxs-lookup"><span data-stu-id="d21c1-118">**Duration** – The duration for on which the job was run.</span></span>
* <span data-ttu-id="d21c1-119">**Status** – You can search for all, running, completed, or failed jobs.</span><span class="sxs-lookup"><span data-stu-id="d21c1-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="d21c1-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span><span class="sxs-lookup"><span data-stu-id="d21c1-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="d21c1-121">The list of jobs is refreshed every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="d21c1-121">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="d21c1-122">View job details</span><span class="sxs-lookup"><span data-stu-id="d21c1-122">View job details</span></span>
<span data-ttu-id="d21c1-123">Perform the following steps to view the details of any job.</span><span class="sxs-lookup"><span data-stu-id="d21c1-123">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="d21c1-124">To view job details</span><span class="sxs-lookup"><span data-stu-id="d21c1-124">To view job details</span></span>
1. <span data-ttu-id="d21c1-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span><span class="sxs-lookup"><span data-stu-id="d21c1-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="d21c1-126">You can search for completed or running jobs.</span><span class="sxs-lookup"><span data-stu-id="d21c1-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="d21c1-127">Select a job from the tabular list of jobs.</span><span class="sxs-lookup"><span data-stu-id="d21c1-127">Select a job from the tabular list of jobs.</span></span>
   
    ![Job blade](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="d21c1-129">At the bottom of the page, click **Details**.</span><span class="sxs-lookup"><span data-stu-id="d21c1-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="d21c1-130">In the **Details** dialog box, you can view status, details, and time statistics.</span><span class="sxs-lookup"><span data-stu-id="d21c1-130">In the **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="d21c1-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d21c1-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![Job details](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="d21c1-133">Job failures when the virtual machine is paused in the hypervisor</span><span class="sxs-lookup"><span data-stu-id="d21c1-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="d21c1-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span><span class="sxs-lookup"><span data-stu-id="d21c1-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span></span> <span data-ttu-id="d21c1-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span><span class="sxs-lookup"><span data-stu-id="d21c1-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> 

<span data-ttu-id="d21c1-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="d21c1-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="d21c1-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span><span class="sxs-lookup"><span data-stu-id="d21c1-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="d21c1-138">Verify that there are no connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="d21c1-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="d21c1-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span><span class="sxs-lookup"><span data-stu-id="d21c1-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span></span>

<span data-ttu-id="d21c1-140">These failures apply to backup, restore, update, and failover jobs.</span><span class="sxs-lookup"><span data-stu-id="d21c1-140">These failures apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="d21c1-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="d21c1-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="d21c1-142">Once that happens, you can restart your job.</span><span class="sxs-lookup"><span data-stu-id="d21c1-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d21c1-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="d21c1-143">Next steps</span></span>
<span data-ttu-id="d21c1-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="d21c1-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

