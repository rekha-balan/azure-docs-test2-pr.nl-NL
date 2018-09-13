---
title: Manage your StorSimple backup policies | Microsoft Docs
description: Explains how you can use the StorSimple Manager service to create and manage manual backups, backup schedules, and backup retention.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: ''
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 220deff83da0f4ec6fa6979e0ef412f736659051
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550738"
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies-update-2"></a><span data-ttu-id="5c9d0-103">Use the StorSimple Manager service to manage backup policies (Update 2)</span><span class="sxs-lookup"><span data-stu-id="5c9d0-103">Use the StorSimple Manager service to manage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="5c9d0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5c9d0-104">Overview</span></span>
<span data-ttu-id="5c9d0-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="5c9d0-106">It also describes how to complete a manual backup.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="5c9d0-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="5c9d0-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="5c9d0-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="5c9d0-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="5c9d0-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span> 

## <a name="the-backup-policies-page"></a><span data-ttu-id="5c9d0-112">The Backup Policies page</span><span class="sxs-lookup"><span data-stu-id="5c9d0-112">The Backup Policies page</span></span>
<span data-ttu-id="5c9d0-113">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-113">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="5c9d0-114">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-114">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="5c9d0-115">This means that the backups created by a backup policy will be crash-consistent copies.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-115">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="5c9d0-116">The **Backup Policies** page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-116">The **Backup Policies** page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="5c9d0-117">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span><span class="sxs-lookup"><span data-stu-id="5c9d0-117">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="5c9d0-118">**Policy name** – The name associated with the policy.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="5c9d0-119">The different types of policies include:</span><span class="sxs-lookup"><span data-stu-id="5c9d0-119">The different types of policies include:</span></span>
  
  * <span data-ttu-id="5c9d0-120">Scheduled policies, which are explicitly created by the user.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="5c9d0-121">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-121">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="5c9d0-122">These policies are named as *VolumeName*_Default where *VolumeName* refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-122">These policies are named as *VolumeName*_Default where *VolumeName* refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="5c9d0-123">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-123">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="5c9d0-124">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-124">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="5c9d0-125">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-125">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="5c9d0-126">**Volumes** – The volumes associated with the policy.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="5c9d0-127">All the volumes associated with a backup policy are grouped together when backups are created.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="5c9d0-128">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-128">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="5c9d0-129">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-129">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="5c9d0-130">**Schedules** – The number of schedules associated with the backup policy.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-130">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="5c9d0-131">The frequently used operations that you can perform from this page are:</span><span class="sxs-lookup"><span data-stu-id="5c9d0-131">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="5c9d0-132">Add a backup policy</span><span class="sxs-lookup"><span data-stu-id="5c9d0-132">Add a backup policy</span></span> 
* <span data-ttu-id="5c9d0-133">Add or modify a schedule</span><span class="sxs-lookup"><span data-stu-id="5c9d0-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="5c9d0-134">Delete a backup policy</span><span class="sxs-lookup"><span data-stu-id="5c9d0-134">Delete a backup policy</span></span> 
* <span data-ttu-id="5c9d0-135">Take a manual backup</span><span class="sxs-lookup"><span data-stu-id="5c9d0-135">Take a manual backup</span></span> 
* <span data-ttu-id="5c9d0-136">Create a custom backup policy with multiple volumes and schedules</span><span class="sxs-lookup"><span data-stu-id="5c9d0-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="5c9d0-137">Add a backup policy</span><span class="sxs-lookup"><span data-stu-id="5c9d0-137">Add a backup policy</span></span>
<span data-ttu-id="5c9d0-138">Add a backup policy to automatically schedule your backups.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-138">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="5c9d0-139">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-139">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="5c9d0-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="5c9d0-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="5c9d0-141">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span><span class="sxs-lookup"><span data-stu-id="5c9d0-141">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="5c9d0-142">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="5c9d0-142">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="5c9d0-143">Add or modify a schedule</span><span class="sxs-lookup"><span data-stu-id="5c9d0-143">Add or modify a schedule</span></span>
<span data-ttu-id="5c9d0-144">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-144">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="5c9d0-145">Perform the following steps in the Azure classic portal to add or modify a schedule.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-145">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="5c9d0-146">Delete a backup policy</span><span class="sxs-lookup"><span data-stu-id="5c9d0-146">Delete a backup policy</span></span>
<span data-ttu-id="5c9d0-147">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-147">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="5c9d0-148">Take a manual backup</span><span class="sxs-lookup"><span data-stu-id="5c9d0-148">Take a manual backup</span></span>
<span data-ttu-id="5c9d0-149">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-149">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="5c9d0-150">Create a custom backup policy with multiple volumes and schedules</span><span class="sxs-lookup"><span data-stu-id="5c9d0-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="5c9d0-151">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span><span class="sxs-lookup"><span data-stu-id="5c9d0-151">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="5c9d0-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c9d0-152">Next steps</span></span>
<span data-ttu-id="5c9d0-153">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5c9d0-153">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


