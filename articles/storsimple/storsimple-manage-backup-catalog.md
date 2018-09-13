---
title: Manage your StorSimple backup catalog | Microsoft Docs
description: Explains how to use the StorSimple Manager service Backup Catalog page to list, select, and delete backup sets for a volume.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: ''
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 6a6052a5936be061adc28f5f60accb68feeb0f23
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551167"
---
# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="37bc5-103">Use the StorSimple Manager service to manage your backup catalog</span><span class="sxs-lookup"><span data-stu-id="37bc5-103">Use the StorSimple Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="37bc5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="37bc5-104">Overview</span></span>
<span data-ttu-id="37bc5-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span><span class="sxs-lookup"><span data-stu-id="37bc5-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="37bc5-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span><span class="sxs-lookup"><span data-stu-id="37bc5-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="37bc5-107">This tutorial explains how to list, select, and delete a backup set.</span><span class="sxs-lookup"><span data-stu-id="37bc5-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="37bc5-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="37bc5-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="37bc5-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span><span class="sxs-lookup"><span data-stu-id="37bc5-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![Backup catalog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="37bc5-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span><span class="sxs-lookup"><span data-stu-id="37bc5-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="37bc5-112">You can filter the backup sets that are retrieved, based on the following parameters:</span><span class="sxs-lookup"><span data-stu-id="37bc5-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="37bc5-113">**Device** – The device on which the backup set was created.</span><span class="sxs-lookup"><span data-stu-id="37bc5-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="37bc5-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span><span class="sxs-lookup"><span data-stu-id="37bc5-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="37bc5-115">**From and To** – The date and time range when the backup set was created.</span><span class="sxs-lookup"><span data-stu-id="37bc5-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="37bc5-116">The filtered backup sets are then tabulated based on the following attributes:</span><span class="sxs-lookup"><span data-stu-id="37bc5-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="37bc5-117">**Name** – The name of the backup policy or volume associated with the backup set.</span><span class="sxs-lookup"><span data-stu-id="37bc5-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="37bc5-118">**Size** – The actual size of the backup set.</span><span class="sxs-lookup"><span data-stu-id="37bc5-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="37bc5-119">**Created On** – The date and time when the backups were created.</span><span class="sxs-lookup"><span data-stu-id="37bc5-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="37bc5-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span><span class="sxs-lookup"><span data-stu-id="37bc5-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="37bc5-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span><span class="sxs-lookup"><span data-stu-id="37bc5-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="37bc5-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span><span class="sxs-lookup"><span data-stu-id="37bc5-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="37bc5-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span><span class="sxs-lookup"><span data-stu-id="37bc5-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="37bc5-124">You can use a backup policy to schedule backups.</span><span class="sxs-lookup"><span data-stu-id="37bc5-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="37bc5-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span><span class="sxs-lookup"><span data-stu-id="37bc5-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="37bc5-126">List backup sets for a volume</span><span class="sxs-lookup"><span data-stu-id="37bc5-126">List backup sets for a volume</span></span>
<span data-ttu-id="37bc5-127">Complete the following steps to list all the backups for a volume.</span><span class="sxs-lookup"><span data-stu-id="37bc5-127">Complete the following steps to list all the backups for a volume.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="37bc5-128">To list backup sets</span><span class="sxs-lookup"><span data-stu-id="37bc5-128">To list backup sets</span></span>
1. <span data-ttu-id="37bc5-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span><span class="sxs-lookup"><span data-stu-id="37bc5-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="37bc5-130">Filter the selections as follows:</span><span class="sxs-lookup"><span data-stu-id="37bc5-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="37bc5-131">Select the appropriate device.</span><span class="sxs-lookup"><span data-stu-id="37bc5-131">Select the appropriate device.</span></span>
   2. <span data-ttu-id="37bc5-132">In the drop-down list, choose a volume to view the corresponding the backups.</span><span class="sxs-lookup"><span data-stu-id="37bc5-132">In the drop-down list, choose a volume to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="37bc5-133">Specify the time range.</span><span class="sxs-lookup"><span data-stu-id="37bc5-133">Specify the time range.</span></span>
   4. <span data-ttu-id="37bc5-134">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="37bc5-134">Click the check icon</span></span> ![Check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="37bc5-136">to execute this query.</span><span class="sxs-lookup"><span data-stu-id="37bc5-136">to execute this query.</span></span>
      
      <span data-ttu-id="37bc5-137">The backups associated with the selected volume should appear in the list of backup sets.</span><span class="sxs-lookup"><span data-stu-id="37bc5-137">The backups associated with the selected volume should appear in the list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="37bc5-138">Select a backup set</span><span class="sxs-lookup"><span data-stu-id="37bc5-138">Select a backup set</span></span>
<span data-ttu-id="37bc5-139">Complete the following steps to select a backup set for a volume or backup policy.</span><span class="sxs-lookup"><span data-stu-id="37bc5-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="37bc5-140">To select a backup set</span><span class="sxs-lookup"><span data-stu-id="37bc5-140">To select a backup set</span></span>
1. <span data-ttu-id="37bc5-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span><span class="sxs-lookup"><span data-stu-id="37bc5-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="37bc5-142">Filter the selections as follows:</span><span class="sxs-lookup"><span data-stu-id="37bc5-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="37bc5-143">Select the appropriate device.</span><span class="sxs-lookup"><span data-stu-id="37bc5-143">Select the appropriate device.</span></span>
   2. <span data-ttu-id="37bc5-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span><span class="sxs-lookup"><span data-stu-id="37bc5-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="37bc5-145">Specify the time range.</span><span class="sxs-lookup"><span data-stu-id="37bc5-145">Specify the time range.</span></span>
   4. <span data-ttu-id="37bc5-146">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="37bc5-146">Click the check icon</span></span> ![Check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="37bc5-148">to execute this query.</span><span class="sxs-lookup"><span data-stu-id="37bc5-148">to execute this query.</span></span>
      
      <span data-ttu-id="37bc5-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span><span class="sxs-lookup"><span data-stu-id="37bc5-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="37bc5-150">Select and expand a backup set.</span><span class="sxs-lookup"><span data-stu-id="37bc5-150">Select and expand a backup set.</span></span> <span data-ttu-id="37bc5-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="37bc5-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="37bc5-152">You can perform either of these actions on the backup set that you selected.</span><span class="sxs-lookup"><span data-stu-id="37bc5-152">You can perform either of these actions on the backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="37bc5-153">Delete a backup set</span><span class="sxs-lookup"><span data-stu-id="37bc5-153">Delete a backup set</span></span>
<span data-ttu-id="37bc5-154">Delete a backup when you no longer wish to retain the data associated with it.</span><span class="sxs-lookup"><span data-stu-id="37bc5-154">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="37bc5-155">Perform the following steps to delete a backup set.</span><span class="sxs-lookup"><span data-stu-id="37bc5-155">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="37bc5-156">To delete a backup set</span><span class="sxs-lookup"><span data-stu-id="37bc5-156">To delete a backup set</span></span>
1. <span data-ttu-id="37bc5-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span><span class="sxs-lookup"><span data-stu-id="37bc5-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="37bc5-158">Filter the selections as follows:</span><span class="sxs-lookup"><span data-stu-id="37bc5-158">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="37bc5-159">Select the appropriate device.</span><span class="sxs-lookup"><span data-stu-id="37bc5-159">Select the appropriate device.</span></span>
   2. <span data-ttu-id="37bc5-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span><span class="sxs-lookup"><span data-stu-id="37bc5-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="37bc5-161">Specify the time range.</span><span class="sxs-lookup"><span data-stu-id="37bc5-161">Specify the time range.</span></span>
   4. <span data-ttu-id="37bc5-162">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="37bc5-162">Click the check icon</span></span> ![Check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="37bc5-164">to execute this query.</span><span class="sxs-lookup"><span data-stu-id="37bc5-164">to execute this query.</span></span>
      
      <span data-ttu-id="37bc5-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span><span class="sxs-lookup"><span data-stu-id="37bc5-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="37bc5-166">Select and expand a backup set.</span><span class="sxs-lookup"><span data-stu-id="37bc5-166">Select and expand a backup set.</span></span> <span data-ttu-id="37bc5-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="37bc5-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="37bc5-168">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="37bc5-168">Click **Delete**.</span></span>
4. <span data-ttu-id="37bc5-169">You will be notified when the deletion is in progress and when it has successfully finished.</span><span class="sxs-lookup"><span data-stu-id="37bc5-169">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="37bc5-170">After the deletion is done, refresh the query on this page.</span><span class="sxs-lookup"><span data-stu-id="37bc5-170">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="37bc5-171">The deleted backup set will no longer appear in the list of backup sets.</span><span class="sxs-lookup"><span data-stu-id="37bc5-171">The deleted backup set will no longer appear in the list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37bc5-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="37bc5-172">Next steps</span></span>
* <span data-ttu-id="37bc5-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="37bc5-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="37bc5-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="37bc5-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>





