---
title: Restore a StorSimple volume from backup | Microsoft Docs
description: Explains how to use the StorSimple Manager service Backup Catalog page to restore a StorSimple volume from a backup set.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: c9e297932dc84ca7019bf6b843a773c9b9be4fe6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553695"
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="7238e-103">Restore a StorSimple volume from a backup set</span><span class="sxs-lookup"><span data-stu-id="7238e-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="7238e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7238e-104">Overview</span></span>
<span data-ttu-id="7238e-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span><span class="sxs-lookup"><span data-stu-id="7238e-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="7238e-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span><span class="sxs-lookup"><span data-stu-id="7238e-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

 ![Backup Catalog page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="7238e-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span><span class="sxs-lookup"><span data-stu-id="7238e-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="7238e-109">How to use the backup catalog</span><span class="sxs-lookup"><span data-stu-id="7238e-109">How to use the backup catalog</span></span>
<span data-ttu-id="7238e-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span><span class="sxs-lookup"><span data-stu-id="7238e-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="7238e-111">You can filter the backup sets that are retrieved based on the following parameters:</span><span class="sxs-lookup"><span data-stu-id="7238e-111">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="7238e-112">**Device** – The device on which the backup set was created.</span><span class="sxs-lookup"><span data-stu-id="7238e-112">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="7238e-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span><span class="sxs-lookup"><span data-stu-id="7238e-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="7238e-114">**From** and **To** – The date and time range when the backup set was created.</span><span class="sxs-lookup"><span data-stu-id="7238e-114">**From** and **To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="7238e-115">The filtered backup sets are then tabulated based on the following attributes:</span><span class="sxs-lookup"><span data-stu-id="7238e-115">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="7238e-116">**Name** – The name of the backup policy or volume associated with the backup set.</span><span class="sxs-lookup"><span data-stu-id="7238e-116">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="7238e-117">**Size** – The actual size of the backup set.</span><span class="sxs-lookup"><span data-stu-id="7238e-117">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="7238e-118">**Created on** – The date and time when the backups were created.</span><span class="sxs-lookup"><span data-stu-id="7238e-118">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="7238e-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span><span class="sxs-lookup"><span data-stu-id="7238e-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="7238e-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span><span class="sxs-lookup"><span data-stu-id="7238e-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="7238e-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span><span class="sxs-lookup"><span data-stu-id="7238e-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="7238e-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span><span class="sxs-lookup"><span data-stu-id="7238e-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="7238e-123">(You can use a backup policy to schedule backups.</span><span class="sxs-lookup"><span data-stu-id="7238e-123">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="7238e-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span><span class="sxs-lookup"><span data-stu-id="7238e-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="7238e-125">How to restore your StorSimple volume from a backup</span><span class="sxs-lookup"><span data-stu-id="7238e-125">How to restore your StorSimple volume from a backup</span></span>
<span data-ttu-id="7238e-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span><span class="sxs-lookup"><span data-stu-id="7238e-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="7238e-127">Restoring from a backup will replace the existing volumes from the backup.</span><span class="sxs-lookup"><span data-stu-id="7238e-127">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="7238e-128">This may cause the loss of any data that was written after the backup was taken.</span><span class="sxs-lookup"><span data-stu-id="7238e-128">This may cause the loss of any data that was written after the backup was taken.</span></span>
> 
> 

<span data-ttu-id="7238e-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span><span class="sxs-lookup"><span data-stu-id="7238e-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span></span> <span data-ttu-id="7238e-130">You will need to take the volume offline on the host first and then the device.</span><span class="sxs-lookup"><span data-stu-id="7238e-130">You will need to take the volume offline on the host first and then the device.</span></span> <span data-ttu-id="7238e-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="7238e-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="7238e-132">Perform the following steps to restore a volume from a backup set.</span><span class="sxs-lookup"><span data-stu-id="7238e-132">Perform the following steps to restore a volume from a backup set.</span></span>

### <a name="to-restore-from-a-backup-set"></a><span data-ttu-id="7238e-133">To restore from a backup set</span><span class="sxs-lookup"><span data-stu-id="7238e-133">To restore from a backup set</span></span>
1. <span data-ttu-id="7238e-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span><span class="sxs-lookup"><span data-stu-id="7238e-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
   
    ![Backup catalog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="7238e-136">Select a backup set as follows:</span><span class="sxs-lookup"><span data-stu-id="7238e-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="7238e-137">Select the appropriate device.</span><span class="sxs-lookup"><span data-stu-id="7238e-137">Select the appropriate device.</span></span>
   2. <span data-ttu-id="7238e-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span><span class="sxs-lookup"><span data-stu-id="7238e-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="7238e-139">Specify the time range.</span><span class="sxs-lookup"><span data-stu-id="7238e-139">Specify the time range.</span></span>
   4. <span data-ttu-id="7238e-140">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="7238e-140">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="7238e-142">to execute this query.</span><span class="sxs-lookup"><span data-stu-id="7238e-142">to execute this query.</span></span>
      
      <span data-ttu-id="7238e-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span><span class="sxs-lookup"><span data-stu-id="7238e-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="7238e-144">Expand the backup set to view the associated volumes.</span><span class="sxs-lookup"><span data-stu-id="7238e-144">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="7238e-145">These volumes must be taken offline on the host and device before you can restore them.</span><span class="sxs-lookup"><span data-stu-id="7238e-145">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="7238e-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="7238e-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7238e-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span><span class="sxs-lookup"><span data-stu-id="7238e-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="7238e-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span><span class="sxs-lookup"><span data-stu-id="7238e-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="7238e-149">Select a backup set.</span><span class="sxs-lookup"><span data-stu-id="7238e-149">Select a backup set.</span></span> <span data-ttu-id="7238e-150">Click **Restore** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7238e-150">Click **Restore** at the bottom of the page.</span></span>
5. <span data-ttu-id="7238e-151">You will be prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="7238e-151">You will be prompted for confirmation.</span></span> 
   
    ![Confirmation page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="7238e-153">Review the restore information and click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="7238e-153">Review the restore information and click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="7238e-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="7238e-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span></span> 
7. <span data-ttu-id="7238e-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span><span class="sxs-lookup"><span data-stu-id="7238e-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span></span>

<span data-ttu-id="7238e-156">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span><span class="sxs-lookup"><span data-stu-id="7238e-156">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="7238e-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="7238e-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7238e-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="7238e-158">Next steps</span></span>
* <span data-ttu-id="7238e-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="7238e-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="7238e-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7238e-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>







