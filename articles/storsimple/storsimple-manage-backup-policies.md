---
title: Manage your StorSimple backup policies | Microsoft Docs
description: Explains how you can use the StorSimple Manager service to create and manage manual backups, backup schedules, and backup retention.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: ''
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 58e352b4ef54dea89fc2a1a19b4b61676540a361
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661986"
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies"></a><span data-ttu-id="2701d-103">Use the StorSimple Manager service to manage backup policies</span><span class="sxs-lookup"><span data-stu-id="2701d-103">Use the StorSimple Manager service to manage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="2701d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2701d-104">Overview</span></span>
<span data-ttu-id="2701d-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="2701d-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="2701d-106">It also describes how to complete a manual backup.</span><span class="sxs-lookup"><span data-stu-id="2701d-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="2701d-107">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span><span class="sxs-lookup"><span data-stu-id="2701d-107">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="2701d-108">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span><span class="sxs-lookup"><span data-stu-id="2701d-108">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="2701d-109">This means that the backups created by a backup policy will be crash-consistent copies.</span><span class="sxs-lookup"><span data-stu-id="2701d-109">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="2701d-110">This page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span><span class="sxs-lookup"><span data-stu-id="2701d-110">This page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="2701d-111">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span><span class="sxs-lookup"><span data-stu-id="2701d-111">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="2701d-112">**Policy name** – The name associated with the policy.</span><span class="sxs-lookup"><span data-stu-id="2701d-112">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="2701d-113">The different types of policies include:</span><span class="sxs-lookup"><span data-stu-id="2701d-113">The different types of policies include:</span></span>
  
  * <span data-ttu-id="2701d-114">Scheduled policies, which are explicitly created by the user.</span><span class="sxs-lookup"><span data-stu-id="2701d-114">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="2701d-115">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span><span class="sxs-lookup"><span data-stu-id="2701d-115">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="2701d-116">These policies are named as VolumeName_Default where Volume name refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="2701d-116">These policies are named as VolumeName_Default where Volume name refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="2701d-117">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span><span class="sxs-lookup"><span data-stu-id="2701d-117">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="2701d-118">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2701d-118">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="2701d-119">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span><span class="sxs-lookup"><span data-stu-id="2701d-119">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="2701d-120">**Volumes** – The volumes associated with the policy.</span><span class="sxs-lookup"><span data-stu-id="2701d-120">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="2701d-121">All the volumes associated with a backup policy are grouped together when backups are created.</span><span class="sxs-lookup"><span data-stu-id="2701d-121">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="2701d-122">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span><span class="sxs-lookup"><span data-stu-id="2701d-122">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="2701d-123">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span><span class="sxs-lookup"><span data-stu-id="2701d-123">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="2701d-124">**Schedules** – The number of schedules associated with the backup policy.</span><span class="sxs-lookup"><span data-stu-id="2701d-124">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="2701d-125">The frequently used operations that you can perform from this page are:</span><span class="sxs-lookup"><span data-stu-id="2701d-125">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="2701d-126">Add a backup policy</span><span class="sxs-lookup"><span data-stu-id="2701d-126">Add a backup policy</span></span> 
* <span data-ttu-id="2701d-127">Add or modify a schedule</span><span class="sxs-lookup"><span data-stu-id="2701d-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="2701d-128">Delete a backup policy</span><span class="sxs-lookup"><span data-stu-id="2701d-128">Delete a backup policy</span></span> 
* <span data-ttu-id="2701d-129">Take a manual backup</span><span class="sxs-lookup"><span data-stu-id="2701d-129">Take a manual backup</span></span> 
* <span data-ttu-id="2701d-130">Create a custom backup policy with multiple volumes and schedules</span><span class="sxs-lookup"><span data-stu-id="2701d-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="2701d-131">Add a backup policy</span><span class="sxs-lookup"><span data-stu-id="2701d-131">Add a backup policy</span></span>
<span data-ttu-id="2701d-132">Add a backup policy to automatically schedule your backups.</span><span class="sxs-lookup"><span data-stu-id="2701d-132">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="2701d-133">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2701d-133">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="2701d-134">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="2701d-134">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="2701d-135">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span><span class="sxs-lookup"><span data-stu-id="2701d-135">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="2701d-136">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="2701d-136">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="2701d-137">Add or modify a schedule</span><span class="sxs-lookup"><span data-stu-id="2701d-137">Add or modify a schedule</span></span>
<span data-ttu-id="2701d-138">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2701d-138">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="2701d-139">Perform the following steps in the Azure classic portal to add or modify a schedule.</span><span class="sxs-lookup"><span data-stu-id="2701d-139">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="2701d-140">Delete a backup policy</span><span class="sxs-lookup"><span data-stu-id="2701d-140">Delete a backup policy</span></span>
<span data-ttu-id="2701d-141">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2701d-141">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="2701d-142">Take a manual backup</span><span class="sxs-lookup"><span data-stu-id="2701d-142">Take a manual backup</span></span>
<span data-ttu-id="2701d-143">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span><span class="sxs-lookup"><span data-stu-id="2701d-143">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="2701d-144">Create a custom backup policy with multiple volumes and schedules</span><span class="sxs-lookup"><span data-stu-id="2701d-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="2701d-145">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span><span class="sxs-lookup"><span data-stu-id="2701d-145">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="2701d-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="2701d-146">Next steps</span></span>
<span data-ttu-id="2701d-147">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="2701d-147">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


