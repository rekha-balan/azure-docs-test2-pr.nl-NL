---
title: StorSimple Virtual Array backup tutorial | Microsoft Docs
description: Describes how to back up StorSimple Virtual Array shares and volumes.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: a4f55053-a664-4f7c-ba9d-0cb1fb200ff4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/07/2016
ms.author: alkohli
ms.openlocfilehash: f7258d0bef8020f6486bdde0c9d008604a9c16bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554447"
---
# <a name="back-up-your-storsimple-virtual-array"></a><span data-ttu-id="74b6f-103">Back up your StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="74b6f-103">Back up your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="74b6f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="74b6f-104">Overview</span></span>
<span data-ttu-id="74b6f-105">This tutorial applies to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device or StorSimple virtual device) running March 2016 general availability (GA) release or later versions.</span><span class="sxs-lookup"><span data-stu-id="74b6f-105">This tutorial applies to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device or StorSimple virtual device) running March 2016 general availability (GA) release or later versions.</span></span>

<span data-ttu-id="74b6f-106">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span><span class="sxs-lookup"><span data-stu-id="74b6f-106">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="74b6f-107">It can create backups, restore from backups, and perform device failover if disaster recovery is needed.</span><span class="sxs-lookup"><span data-stu-id="74b6f-107">It can create backups, restore from backups, and perform device failover if disaster recovery is needed.</span></span> <span data-ttu-id="74b6f-108">When configured as a file server, it also allows item-level recovery.</span><span class="sxs-lookup"><span data-stu-id="74b6f-108">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="74b6f-109">This tutorial describes how to use the Azure classic portal or the StorSimple web UI to create scheduled and manual backups of your StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="74b6f-109">This tutorial describes how to use the Azure classic portal or the StorSimple web UI to create scheduled and manual backups of your StorSimple Virtual Array.</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="74b6f-110">Back up shares and volumes</span><span class="sxs-lookup"><span data-stu-id="74b6f-110">Back up shares and volumes</span></span>
<span data-ttu-id="74b6f-111">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span><span class="sxs-lookup"><span data-stu-id="74b6f-111">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="74b6f-112">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span><span class="sxs-lookup"><span data-stu-id="74b6f-112">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="74b6f-113">Each of the methods is discussed in the following sections.</span><span class="sxs-lookup"><span data-stu-id="74b6f-113">Each of the methods is discussed in the following sections.</span></span>

> [!NOTE]
> <span data-ttu-id="74b6f-114">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span><span class="sxs-lookup"><span data-stu-id="74b6f-114">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="74b6f-115">It is not possible to create custom policies for scheduled backups at this time.</span><span class="sxs-lookup"><span data-stu-id="74b6f-115">It is not possible to create custom policies for scheduled backups at this time.</span></span>
> 
> 

## <a name="change-the-backup-schedule"></a><span data-ttu-id="74b6f-116">Change the backup schedule</span><span class="sxs-lookup"><span data-stu-id="74b6f-116">Change the backup schedule</span></span>
<span data-ttu-id="74b6f-117">Your StorSimple virtual device has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span><span class="sxs-lookup"><span data-stu-id="74b6f-117">Your StorSimple virtual device has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="74b6f-118">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="74b6f-118">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="74b6f-119">During these backups, the entire virtual device is backed up; therefore, we recommend that you schedule these backups for off-peak hours.</span><span class="sxs-lookup"><span data-stu-id="74b6f-119">During these backups, the entire virtual device is backed up; therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

<span data-ttu-id="74b6f-120">Perform the following steps in the [Azure classic portal](https://manage.windowsazure.com/) to change the default backup start time.</span><span class="sxs-lookup"><span data-stu-id="74b6f-120">Perform the following steps in the [Azure classic portal](https://manage.windowsazure.com/) to change the default backup start time.</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="74b6f-121">To change the start time for the default backup policy</span><span class="sxs-lookup"><span data-stu-id="74b6f-121">To change the start time for the default backup policy</span></span>
1. <span data-ttu-id="74b6f-122">Navigate to the device **Configuration** tab.</span><span class="sxs-lookup"><span data-stu-id="74b6f-122">Navigate to the device **Configuration** tab.</span></span>
2. <span data-ttu-id="74b6f-123">Under the **Backup** section, specify the start time for the daily backup.</span><span class="sxs-lookup"><span data-stu-id="74b6f-123">Under the **Backup** section, specify the start time for the daily backup.</span></span>
3. <span data-ttu-id="74b6f-124">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="74b6f-124">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="74b6f-125">Take a manual backup</span><span class="sxs-lookup"><span data-stu-id="74b6f-125">Take a manual backup</span></span>
<span data-ttu-id="74b6f-126">In addition to scheduled backups, you can take a manual (on-demand) backup at any time.</span><span class="sxs-lookup"><span data-stu-id="74b6f-126">In addition to scheduled backups, you can take a manual (on-demand) backup at any time.</span></span>

#### <a name="to-create-a-manual-on-demand-backup"></a><span data-ttu-id="74b6f-127">To create a manual (on-demand) backup</span><span class="sxs-lookup"><span data-stu-id="74b6f-127">To create a manual (on-demand) backup</span></span>
1. <span data-ttu-id="74b6f-128">Navigate to the **Shares** tab or the **Volumes** tab.</span><span class="sxs-lookup"><span data-stu-id="74b6f-128">Navigate to the **Shares** tab or the **Volumes** tab.</span></span>
2. <span data-ttu-id="74b6f-129">At the bottom of the page, click **Backup all**.</span><span class="sxs-lookup"><span data-stu-id="74b6f-129">At the bottom of the page, click **Backup all**.</span></span> <span data-ttu-id="74b6f-130">You will be prompted to verify that you would like to take the backup now.</span><span class="sxs-lookup"><span data-stu-id="74b6f-130">You will be prompted to verify that you would like to take the backup now.</span></span> <span data-ttu-id="74b6f-131">Click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image3.png) to proceed with the backup.</span><span class="sxs-lookup"><span data-stu-id="74b6f-131">Click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image3.png) to proceed with the backup.</span></span>
   
    ![backup confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image4.png)
   
    <span data-ttu-id="74b6f-133">You will be notified that a backup job is starting.</span><span class="sxs-lookup"><span data-stu-id="74b6f-133">You will be notified that a backup job is starting.</span></span>
   
    ![backup starting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image5.png)
   
    <span data-ttu-id="74b6f-135">You will be notified that the job was created successfully.</span><span class="sxs-lookup"><span data-stu-id="74b6f-135">You will be notified that the job was created successfully.</span></span>
   
    ![backup job created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image7.png)
3. <span data-ttu-id="74b6f-137">To track the progress of the job, click **View Job**.</span><span class="sxs-lookup"><span data-stu-id="74b6f-137">To track the progress of the job, click **View Job**.</span></span>
4. <span data-ttu-id="74b6f-138">After the backup job is finished, go to the **Backup catalog** tab. You should see your completed backup.</span><span class="sxs-lookup"><span data-stu-id="74b6f-138">After the backup job is finished, go to the **Backup catalog** tab. You should see your completed backup.</span></span>
   
    ![Completed backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image8.png)
5. <span data-ttu-id="74b6f-140">Set the filter selections to the appropriate device, backup policy, and time range, and then click the check icon</span><span class="sxs-lookup"><span data-stu-id="74b6f-140">Set the filter selections to the appropriate device, backup policy, and time range, and then click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image3.png)<span data-ttu-id="74b6f-142">.</span><span class="sxs-lookup"><span data-stu-id="74b6f-142">.</span></span>
   
    <span data-ttu-id="74b6f-143">The backup should appear in the list of backup sets that is displayed in the catalog.</span><span class="sxs-lookup"><span data-stu-id="74b6f-143">The backup should appear in the list of backup sets that is displayed in the catalog.</span></span>

## <a name="view-existing-backups"></a><span data-ttu-id="74b6f-144">View existing backups</span><span class="sxs-lookup"><span data-stu-id="74b6f-144">View existing backups</span></span>
<span data-ttu-id="74b6f-145">Perform the following steps in the Azure classic portal to view the existing backups.</span><span class="sxs-lookup"><span data-stu-id="74b6f-145">Perform the following steps in the Azure classic portal to view the existing backups.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="74b6f-146">To view existing backups</span><span class="sxs-lookup"><span data-stu-id="74b6f-146">To view existing backups</span></span>
1. <span data-ttu-id="74b6f-147">On the StorSimple Manager service page, click the **Backup catalog** tab.</span><span class="sxs-lookup"><span data-stu-id="74b6f-147">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="74b6f-148">Select a backup set as follows:</span><span class="sxs-lookup"><span data-stu-id="74b6f-148">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="74b6f-149">Select the device.</span><span class="sxs-lookup"><span data-stu-id="74b6f-149">Select the device.</span></span>
   2. <span data-ttu-id="74b6f-150">In the drop-down list, choose the share or volume for the backup that you wish to select.</span><span class="sxs-lookup"><span data-stu-id="74b6f-150">In the drop-down list, choose the share or volume for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="74b6f-151">Specify the time range.</span><span class="sxs-lookup"><span data-stu-id="74b6f-151">Specify the time range.</span></span>
   4. <span data-ttu-id="74b6f-152">Click the check icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image3.png) to execute this query.</span><span class="sxs-lookup"><span data-stu-id="74b6f-152">Click the check icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/image3.png) to execute this query.</span></span>
      
      <span data-ttu-id="74b6f-153">The backups associated with the selected share or volume should appear in the list of backup sets.</span><span class="sxs-lookup"><span data-stu-id="74b6f-153">The backups associated with the selected share or volume should appear in the list of backup sets.</span></span>

<span data-ttu-id="74b6f-154">![video_icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/video_icon.png) **Video available**</span><span class="sxs-lookup"><span data-stu-id="74b6f-154">![video_icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-backup/video_icon.png) **Video available**</span></span>

<span data-ttu-id="74b6f-155">Watch the video to see how you can create shares, back up shares, and restore data on a StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="74b6f-155">Watch the video to see how you can create shares, back up shares, and restore data on a StorSimple Virtual Array.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-the-StorSimple-Virtual-Array/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="74b6f-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="74b6f-156">Next steps</span></span>
<span data-ttu-id="74b6f-157">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="74b6f-157">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>









