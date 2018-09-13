---
title: View and manage StorSimple Virtual Array jobs | Microsoft Docs
description: Describes the StorSimple Manager service Jobs page and how to use it to track recent and current jobs for the StorSimple Virtual Array.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 789f7e04-7b3f-456d-be69-37ea48446e9b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/07/2016
ms.author: alkohli
ms.openlocfilehash: e9122d18e11e3698057f881ae8ebd025c1e9155d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562952"
---
# <a name="use-the-storsimple-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="a3d43-103">Use the StorSimple Manager service to view jobs for the StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="a3d43-103">Use the StorSimple Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="a3d43-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a3d43-104">Overview</span></span>
<span data-ttu-id="a3d43-105">The **Jobs** page provides a single central portal for viewing and managing jobs that are started on Virtual Arrays (also known as on-premises virtual devices) that are connected to your StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="a3d43-105">The **Jobs** page provides a single central portal for viewing and managing jobs that are started on Virtual Arrays (also known as on-premises virtual devices) that are connected to your StorSimple Manager service.</span></span> <span data-ttu-id="a3d43-106">You can view running, completed, and failed jobs for multiple virtual devices.</span><span class="sxs-lookup"><span data-stu-id="a3d43-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="a3d43-107">Results are presented in a tabular format.</span><span class="sxs-lookup"><span data-stu-id="a3d43-107">Results are presented in a tabular format.</span></span> 

![Jobs page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-jobs/ovajobs1.png)

<span data-ttu-id="a3d43-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span><span class="sxs-lookup"><span data-stu-id="a3d43-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="a3d43-110">**Status** – You can search for all, running, completed, or failed jobs.</span><span class="sxs-lookup"><span data-stu-id="a3d43-110">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="a3d43-111">**From and To** – Jobs can be filtered based on the date and time range.</span><span class="sxs-lookup"><span data-stu-id="a3d43-111">**From and To** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="a3d43-112">**Type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span><span class="sxs-lookup"><span data-stu-id="a3d43-112">**Type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>
* <span data-ttu-id="a3d43-113">**Devices** – Jobs are initiated on a specific device connected to your service.</span><span class="sxs-lookup"><span data-stu-id="a3d43-113">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="a3d43-114">The filtered jobs are then tabulated on the basis of the following attributes:</span><span class="sxs-lookup"><span data-stu-id="a3d43-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
  * <span data-ttu-id="a3d43-115">**Type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span><span class="sxs-lookup"><span data-stu-id="a3d43-115">**Type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>
  * <span data-ttu-id="a3d43-116">**Status** – Jobs can be all, running, completed, or failed.</span><span class="sxs-lookup"><span data-stu-id="a3d43-116">**Status** – Jobs can be all, running, completed, or failed.</span></span>
  * <span data-ttu-id="a3d43-117">**Entity** – The jobs can be associated with a volume, share, or device.</span><span class="sxs-lookup"><span data-stu-id="a3d43-117">**Entity** – The jobs can be associated with a volume, share, or device.</span></span> 
  * <span data-ttu-id="a3d43-118">**Device** – The name of the device on which the job was started.</span><span class="sxs-lookup"><span data-stu-id="a3d43-118">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="a3d43-119">**Started on** – The time when the job was started.</span><span class="sxs-lookup"><span data-stu-id="a3d43-119">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="a3d43-120">**Progress** – The percentage completion of a running job.</span><span class="sxs-lookup"><span data-stu-id="a3d43-120">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="a3d43-121">For a completed job, this should always be 100%.</span><span class="sxs-lookup"><span data-stu-id="a3d43-121">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="a3d43-122">The list of jobs is refreshed every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="a3d43-122">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="a3d43-123">View job details</span><span class="sxs-lookup"><span data-stu-id="a3d43-123">View job details</span></span>
<span data-ttu-id="a3d43-124">Perform the following steps to view the details of any job.</span><span class="sxs-lookup"><span data-stu-id="a3d43-124">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="a3d43-125">To view job details</span><span class="sxs-lookup"><span data-stu-id="a3d43-125">To view job details</span></span>
1. <span data-ttu-id="a3d43-126">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span><span class="sxs-lookup"><span data-stu-id="a3d43-126">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="a3d43-127">You can search for completed or running jobs.</span><span class="sxs-lookup"><span data-stu-id="a3d43-127">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="a3d43-128">Select a job from the tabular list of jobs.</span><span class="sxs-lookup"><span data-stu-id="a3d43-128">Select a job from the tabular list of jobs.</span></span>
3. <span data-ttu-id="a3d43-129">At the bottom of the page, click **Details**.</span><span class="sxs-lookup"><span data-stu-id="a3d43-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="a3d43-130">In the **Details** dialog box, you can view status, details,  and time statistics.</span><span class="sxs-lookup"><span data-stu-id="a3d43-130">In the **Details** dialog box, you can view status, details,  and time statistics.</span></span> <span data-ttu-id="a3d43-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a3d43-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![Job details page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-jobs/ovajobs2.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="a3d43-133">Job failures when the virtual machine is paused in the hypervisor</span><span class="sxs-lookup"><span data-stu-id="a3d43-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="a3d43-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job will fail.</span><span class="sxs-lookup"><span data-stu-id="a3d43-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job will fail.</span></span> <span data-ttu-id="a3d43-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span><span class="sxs-lookup"><span data-stu-id="a3d43-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> <span data-ttu-id="a3d43-136">An example for a restore job failure is shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="a3d43-136">An example for a restore job failure is shown in the following screenshot.</span></span>

![Restore job failure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-jobs/restorejobfailure.png)

<span data-ttu-id="a3d43-138">These failures will apply to backup, restore, update, and failover jobs.</span><span class="sxs-lookup"><span data-stu-id="a3d43-138">These failures will apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="a3d43-139">If your virtual machine is provisioned in Hyper-V, the machine will eventually synchronize time with your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="a3d43-139">If your virtual machine is provisioned in Hyper-V, the machine will eventually synchronize time with your hypervisor.</span></span> <span data-ttu-id="a3d43-140">Once that happens, you can restart your job.</span><span class="sxs-lookup"><span data-stu-id="a3d43-140">Once that happens, you can restart your job.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a3d43-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3d43-141">Next steps</span></span>
<span data-ttu-id="a3d43-142">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a3d43-142">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>




