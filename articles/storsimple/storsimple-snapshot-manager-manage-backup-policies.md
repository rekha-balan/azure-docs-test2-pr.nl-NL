---
title: StorSimple Snapshot Manager backup policies | Microsoft Docs
description: Describes how to use the StorSimple Snapshot Manager MMC snap-in to create and manage the backup policies that control scheduled backups.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: ''
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821293"
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a><span data-ttu-id="cc527-103">Use StorSimple Snapshot Manager to create and manage backup policies</span><span class="sxs-lookup"><span data-stu-id="cc527-103">Use StorSimple Snapshot Manager to create and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="cc527-104">Overview</span><span class="sxs-lookup"><span data-stu-id="cc527-104">Overview</span></span>
<span data-ttu-id="cc527-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="cc527-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span></span> <span data-ttu-id="cc527-106">When you create a backup policy, you can also specify a retention policy.</span><span class="sxs-lookup"><span data-stu-id="cc527-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="cc527-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc527-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="cc527-108">This tutorial explains how to:</span><span class="sxs-lookup"><span data-stu-id="cc527-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="cc527-109">Create a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-109">Create a backup policy</span></span>
* <span data-ttu-id="cc527-110">Edit a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-110">Edit a backup policy</span></span>
* <span data-ttu-id="cc527-111">Delete a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="cc527-112">Create a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-112">Create a backup policy</span></span>
<span data-ttu-id="cc527-113">Use the following procedure to create a new backup policy.</span><span class="sxs-lookup"><span data-stu-id="cc527-113">Use the following procedure to create a new backup policy.</span></span>

#### <a name="to-create-a-backup-policy"></a><span data-ttu-id="cc527-114">To create a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-114">To create a backup policy</span></span>
1. <span data-ttu-id="cc527-115">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="cc527-115">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="cc527-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span><span class="sxs-lookup"><span data-stu-id="cc527-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Create a backup policy](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="cc527-118">The **Create a Policy** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="cc527-118">The **Create a Policy** dialog box appears.</span></span>

    ![Create a Policy - General tab](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="cc527-120">On the **General** tab, complete the following information:</span><span class="sxs-lookup"><span data-stu-id="cc527-120">On the **General** tab, complete the following information:</span></span>

   1. <span data-ttu-id="cc527-121">In the **Name** text box, type a name for the policy.</span><span class="sxs-lookup"><span data-stu-id="cc527-121">In the **Name** text box, type a name for the policy.</span></span>
   2. <span data-ttu-id="cc527-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span><span class="sxs-lookup"><span data-stu-id="cc527-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span></span>
   3. <span data-ttu-id="cc527-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span><span class="sxs-lookup"><span data-stu-id="cc527-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="cc527-124">Select the number of snapshots to retain.</span><span class="sxs-lookup"><span data-stu-id="cc527-124">Select the number of snapshots to retain.</span></span> <span data-ttu-id="cc527-125">If you select **All**, 64 snapshots will be retained (the maximum).</span><span class="sxs-lookup"><span data-stu-id="cc527-125">If you select **All**, 64 snapshots will be retained (the maximum).</span></span>
4. <span data-ttu-id="cc527-126">Click the **Schedule** tab.</span><span class="sxs-lookup"><span data-stu-id="cc527-126">Click the **Schedule** tab.</span></span>

    ![Create a Policy - Schedule tab](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="cc527-128">On the **Schedule** tab, complete the following information:</span><span class="sxs-lookup"><span data-stu-id="cc527-128">On the **Schedule** tab, complete the following information:</span></span>

   1. <span data-ttu-id="cc527-129">Click the **Enable** check box to schedule the next backup.</span><span class="sxs-lookup"><span data-stu-id="cc527-129">Click the **Enable** check box to schedule the next backup.</span></span>
   2. <span data-ttu-id="cc527-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span><span class="sxs-lookup"><span data-stu-id="cc527-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="cc527-131">In the **Start** text box, click the calendar icon and select a start date.</span><span class="sxs-lookup"><span data-stu-id="cc527-131">In the **Start** text box, click the calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="cc527-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span><span class="sxs-lookup"><span data-stu-id="cc527-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="cc527-133">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc527-133">Click **OK**.</span></span>

<span data-ttu-id="cc527-134">After you create a backup policy, the following information appears in the **Results** pane:</span><span class="sxs-lookup"><span data-stu-id="cc527-134">After you create a backup policy, the following information appears in the **Results** pane:</span></span>

* <span data-ttu-id="cc527-135">**Name** – the name of backup policy.</span><span class="sxs-lookup"><span data-stu-id="cc527-135">**Name** – the name of backup policy.</span></span>
* <span data-ttu-id="cc527-136">**Type** – local snapshot or cloud snapshot.</span><span class="sxs-lookup"><span data-stu-id="cc527-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="cc527-137">**Volume Group** – the volume group associated with the policy.</span><span class="sxs-lookup"><span data-stu-id="cc527-137">**Volume Group** – the volume group associated with the policy.</span></span>
* <span data-ttu-id="cc527-138">**Retention** – the number of snapshots retained; the maximum is 64.</span><span class="sxs-lookup"><span data-stu-id="cc527-138">**Retention** – the number of snapshots retained; the maximum is 64.</span></span>
* <span data-ttu-id="cc527-139">**Created** – the date that this policy was created.</span><span class="sxs-lookup"><span data-stu-id="cc527-139">**Created** – the date that this policy was created.</span></span>
* <span data-ttu-id="cc527-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span><span class="sxs-lookup"><span data-stu-id="cc527-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="cc527-141">Edit a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-141">Edit a backup policy</span></span>
<span data-ttu-id="cc527-142">Use the following procedure to edit an existing backup policy.</span><span class="sxs-lookup"><span data-stu-id="cc527-142">Use the following procedure to edit an existing backup policy.</span></span>

#### <a name="to-edit-a-backup-policy"></a><span data-ttu-id="cc527-143">To edit a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-143">To edit a backup policy</span></span>
1. <span data-ttu-id="cc527-144">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="cc527-144">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="cc527-145">In the **Scope** pane, click the **Backup Policies** node.</span><span class="sxs-lookup"><span data-stu-id="cc527-145">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="cc527-146">All the backup policies appear in the **Results** pane.</span><span class="sxs-lookup"><span data-stu-id="cc527-146">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="cc527-147">Right-click the policy that you want to edit, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="cc527-147">Right-click the policy that you want to edit, and then click **Edit**.</span></span>

    ![Edit a backup policy](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="cc527-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc527-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="cc527-150">Delete a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-150">Delete a backup policy</span></span>
<span data-ttu-id="cc527-151">Use the following procedure to delete a backup policy.</span><span class="sxs-lookup"><span data-stu-id="cc527-151">Use the following procedure to delete a backup policy.</span></span>

#### <a name="to-delete-a-backup-policy"></a><span data-ttu-id="cc527-152">To delete a backup policy</span><span class="sxs-lookup"><span data-stu-id="cc527-152">To delete a backup policy</span></span>
1. <span data-ttu-id="cc527-153">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="cc527-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="cc527-154">In the **Scope** pane, click the **Backup Policies** node.</span><span class="sxs-lookup"><span data-stu-id="cc527-154">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="cc527-155">All the backup policies appear in the **Results** pane.</span><span class="sxs-lookup"><span data-stu-id="cc527-155">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="cc527-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="cc527-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span></span>
4. <span data-ttu-id="cc527-157">When the confirmation message appears, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="cc527-157">When the confirmation message appears, click **Yes**.</span></span>

    ![Delete backup policy confirmation](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="cc527-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc527-159">Next steps</span></span>
* <span data-ttu-id="cc527-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="cc527-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="cc527-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="cc527-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
