---
title: Microsoft Azure StorSimple Virtual Array backup tutorial | Microsoft Docs
description: Describes how to back up StorSimple Virtual Array shares and volumes.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: ''
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 069e05bbe9829e4d6685ca0e8680371e72e2b5ce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554453"
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="0e4bb-103">Back up shares or volumes on your StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="0e4bb-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="0e4bb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="0e4bb-104">Overview</span></span>

<span data-ttu-id="0e4bb-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="0e4bb-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span></span> <span data-ttu-id="0e4bb-107">When configured as a file server, it also allows item-level recovery.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="0e4bb-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span></span>

<span data-ttu-id="0e4bb-109">This tutorial applies to the StorSimple Virtual Arrays only.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-109">This tutorial applies to the StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="0e4bb-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="0e4bb-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="0e4bb-111">Back up shares and volumes</span><span class="sxs-lookup"><span data-stu-id="0e4bb-111">Back up shares and volumes</span></span>

<span data-ttu-id="0e4bb-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="0e4bb-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="0e4bb-114">Each of the methods is discussed in the following sections.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-114">Each of the methods is discussed in the following sections.</span></span>

## <a name="change-the-backup-start-time"></a><span data-ttu-id="0e4bb-115">Change the backup start time</span><span class="sxs-lookup"><span data-stu-id="0e4bb-115">Change the backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="0e4bb-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="0e4bb-117">It is not possible to create custom policies for scheduled backups at this time.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-117">It is not possible to create custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="0e4bb-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="0e4bb-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="0e4bb-120">During these backups, the entire virtual device is backed up.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-120">During these backups, the entire virtual device is backed up.</span></span> <span data-ttu-id="0e4bb-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span></span> <span data-ttu-id="0e4bb-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="0e4bb-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0e4bb-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="0e4bb-124">To change the start time for the default backup policy</span><span class="sxs-lookup"><span data-stu-id="0e4bb-124">To change the start time for the default backup policy</span></span>

1. <span data-ttu-id="0e4bb-125">Go to **Devices**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-125">Go to **Devices**.</span></span> <span data-ttu-id="0e4bb-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![navigate to devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="0e4bb-128">Select and click your device.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-128">Select and click your device.</span></span> <span data-ttu-id="0e4bb-129">The **Settings** blade will be displayed.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-129">The **Settings** blade will be displayed.</span></span> <span data-ttu-id="0e4bb-130">Go to **Manage > Backup policies**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-130">Go to **Manage > Backup policies**.</span></span>
   
    ![select your device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="0e4bb-132">In the **Backup policies** blade, the default start time is 22:30.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-132">In the **Backup policies** blade, the default start time is 22:30.</span></span> <span data-ttu-id="0e4bb-133">You can specify the new start time for the daily schedule in device time zone.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-133">You can specify the new start time for the daily schedule in device time zone.</span></span>
   
    ![navigate to backup policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="0e4bb-135">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="0e4bb-136">Take a manual backup</span><span class="sxs-lookup"><span data-stu-id="0e4bb-136">Take a manual backup</span></span>

<span data-ttu-id="0e4bb-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="0e4bb-138">To create a manual backup</span><span class="sxs-lookup"><span data-stu-id="0e4bb-138">To create a manual backup</span></span>

1. <span data-ttu-id="0e4bb-139">Go to **Devices**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-139">Go to **Devices**.</span></span> <span data-ttu-id="0e4bb-140">Select your device and right-click **...** at the far right in the selected row.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-140">Select your device and right-click **...** at the far right in the selected row.</span></span> <span data-ttu-id="0e4bb-141">From the context menu, select **Take backup**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-141">From the context menu, select **Take backup**.</span></span>
   
    ![navigate to take backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="0e4bb-143">In the **Take backup** blade, click **Take backup**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-143">In the **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="0e4bb-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span></span> 
   
    ![backup starting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="0e4bb-146">An on-demand backup starts and you see that a backup job has started.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![backup starting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="0e4bb-148">Once the job has successfully completed, you are notified again.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-148">Once the job has successfully completed, you are notified again.</span></span> <span data-ttu-id="0e4bb-149">The backup process then starts.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-149">The backup process then starts.</span></span>
   
    ![backup job created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="0e4bb-151">To track the progress of the backups and look at the job details, click the notification.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-151">To track the progress of the backups and look at the job details, click the notification.</span></span> <span data-ttu-id="0e4bb-152">This takes you to  **Job details**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-152">This takes you to  **Job details**.</span></span>
   
     ![backup job details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="0e4bb-154">After the backup is complete, go to **Management > Backup catalog**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-154">After the backup is complete, go to **Management > Backup catalog**.</span></span> <span data-ttu-id="0e4bb-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span></span>
   
    ![Completed backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="0e4bb-157">View existing backups</span><span class="sxs-lookup"><span data-stu-id="0e4bb-157">View existing backups</span></span>
<span data-ttu-id="0e4bb-158">To view the existing backups, perform the following steps in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-158">To view the existing backups, perform the following steps in the Azure portal.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="0e4bb-159">To view existing backups</span><span class="sxs-lookup"><span data-stu-id="0e4bb-159">To view existing backups</span></span>

1. <span data-ttu-id="0e4bb-160">Go to **Devices** blade.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-160">Go to **Devices** blade.</span></span> <span data-ttu-id="0e4bb-161">Select and click your device.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-161">Select and click your device.</span></span> <span data-ttu-id="0e4bb-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span></span>
   
    ![Navigate to backup catalog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="0e4bb-164">Specify the following criteria to be used for filtering:</span><span class="sxs-lookup"><span data-stu-id="0e4bb-164">Specify the following criteria to be used for filtering:</span></span>
   
    - <span data-ttu-id="0e4bb-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="0e4bb-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="0e4bb-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span><span class="sxs-lookup"><span data-stu-id="0e4bb-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filter backups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="0e4bb-169">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-169">Click **Apply**.</span></span> <span data-ttu-id="0e4bb-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span></span> <span data-ttu-id="0e4bb-171">Note only 100 backup elements can be displayed at a given time.</span><span class="sxs-lookup"><span data-stu-id="0e4bb-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Updated backup catalog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="0e4bb-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="0e4bb-173">Next steps</span></span>

<span data-ttu-id="0e4bb-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="0e4bb-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>













