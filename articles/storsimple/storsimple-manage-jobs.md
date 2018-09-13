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
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs"></a><span data-ttu-id="04fd8-103">Use the StorSimple Manager service to view and manage StorSimple jobs</span><span class="sxs-lookup"><span data-stu-id="04fd8-103">Use the StorSimple Manager service to view and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="04fd8-104">Overview</span><span class="sxs-lookup"><span data-stu-id="04fd8-104">Overview</span></span>
<span data-ttu-id="04fd8-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="04fd8-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="04fd8-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span><span class="sxs-lookup"><span data-stu-id="04fd8-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="04fd8-107">Results are presented in a tabular format.</span><span class="sxs-lookup"><span data-stu-id="04fd8-107">Results are presented in a tabular format.</span></span> 

![Jobs page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="04fd8-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span><span class="sxs-lookup"><span data-stu-id="04fd8-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="04fd8-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span><span class="sxs-lookup"><span data-stu-id="04fd8-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="04fd8-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span><span class="sxs-lookup"><span data-stu-id="04fd8-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="04fd8-112">**Devices** – Jobs are initiated on a certain device connected to your service.</span><span class="sxs-lookup"><span data-stu-id="04fd8-112">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
* <span data-ttu-id="04fd8-113">**From and To** – Jobs can be filtered based on the date and time range.</span><span class="sxs-lookup"><span data-stu-id="04fd8-113">**From and To** – Jobs can be filtered based on the date and time range.</span></span>

<span data-ttu-id="04fd8-114">The filtered jobs are then tabulated on the basis of the following attributes:</span><span class="sxs-lookup"><span data-stu-id="04fd8-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>

* <span data-ttu-id="04fd8-115">**Type** – Backup, clone, restore, failover, or update.</span><span class="sxs-lookup"><span data-stu-id="04fd8-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="04fd8-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span><span class="sxs-lookup"><span data-stu-id="04fd8-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="04fd8-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span><span class="sxs-lookup"><span data-stu-id="04fd8-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="04fd8-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span><span class="sxs-lookup"><span data-stu-id="04fd8-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="04fd8-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span><span class="sxs-lookup"><span data-stu-id="04fd8-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="04fd8-120">**Device** – The name of the device on which the job was started.</span><span class="sxs-lookup"><span data-stu-id="04fd8-120">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="04fd8-121">**Started On** – The time when the job was started.</span><span class="sxs-lookup"><span data-stu-id="04fd8-121">**Started On** – The time when the job was started.</span></span>
* <span data-ttu-id="04fd8-122">**Progress** – The percentage completion of a running job.</span><span class="sxs-lookup"><span data-stu-id="04fd8-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="04fd8-123">For a completed job, this should always be 100%.</span><span class="sxs-lookup"><span data-stu-id="04fd8-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="04fd8-124">The list of jobs is refreshed every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="04fd8-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="04fd8-125">You can perform the following job-related actions on this page:</span><span class="sxs-lookup"><span data-stu-id="04fd8-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="04fd8-126">View job details</span><span class="sxs-lookup"><span data-stu-id="04fd8-126">View job details</span></span>
* <span data-ttu-id="04fd8-127">Cancel a job</span><span class="sxs-lookup"><span data-stu-id="04fd8-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="04fd8-128">View job details</span><span class="sxs-lookup"><span data-stu-id="04fd8-128">View job details</span></span>
<span data-ttu-id="04fd8-129">Perform the following steps to view the details of any job.</span><span class="sxs-lookup"><span data-stu-id="04fd8-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="04fd8-130">To view job details</span><span class="sxs-lookup"><span data-stu-id="04fd8-130">To view job details</span></span>
1. <span data-ttu-id="04fd8-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span><span class="sxs-lookup"><span data-stu-id="04fd8-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="04fd8-132">You can search for completed, running, or canceled jobs.</span><span class="sxs-lookup"><span data-stu-id="04fd8-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="04fd8-133">Select a job.</span><span class="sxs-lookup"><span data-stu-id="04fd8-133">Select a job.</span></span>
3. <span data-ttu-id="04fd8-134">At the bottom of the page, click **Details**.</span><span class="sxs-lookup"><span data-stu-id="04fd8-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="04fd8-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span><span class="sxs-lookup"><span data-stu-id="04fd8-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="04fd8-136">Cancel a job</span><span class="sxs-lookup"><span data-stu-id="04fd8-136">Cancel a job</span></span>
<span data-ttu-id="04fd8-137">Perform the following steps to cancel a running job.</span><span class="sxs-lookup"><span data-stu-id="04fd8-137">Perform the following steps to cancel a running job.</span></span>

### <a name="to-cancel-a-job"></a><span data-ttu-id="04fd8-138">To cancel a job</span><span class="sxs-lookup"><span data-stu-id="04fd8-138">To cancel a job</span></span>
1. <span data-ttu-id="04fd8-139">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span><span class="sxs-lookup"><span data-stu-id="04fd8-139">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="04fd8-140">Select the job.</span><span class="sxs-lookup"><span data-stu-id="04fd8-140">Select the job.</span></span>
3. <span data-ttu-id="04fd8-141">At the bottom of the page, click **Cancel**.</span><span class="sxs-lookup"><span data-stu-id="04fd8-141">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="04fd8-142">When prompted for confirmation, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="04fd8-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="04fd8-143">This job is now canceled.</span><span class="sxs-lookup"><span data-stu-id="04fd8-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04fd8-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="04fd8-144">Next steps</span></span>
* <span data-ttu-id="04fd8-145">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="04fd8-145">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="04fd8-146">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="04fd8-146">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


