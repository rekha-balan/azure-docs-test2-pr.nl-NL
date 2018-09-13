---
title: StorSimple Snapshot Manager volume groups | Microsoft Docs
description: Describes how to use the StorSimple Snapshot Manager MMC snap-in to create and manage volume groups.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: ''
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: ae2f19c70bd2042ac83e57d23f86dcc0edf322c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556007"
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-volume-groups"></a><span data-ttu-id="1e152-103">Use StorSimple Snapshot Manager to create and manage volume groups</span><span class="sxs-lookup"><span data-stu-id="1e152-103">Use StorSimple Snapshot Manager to create and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="1e152-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1e152-104">Overview</span></span>
<span data-ttu-id="1e152-105">You can use the **Volume Groups** node on the **Scope** pane to assign volumes to volume groups, view information about a volume group, schedule backups, and edit volume groups.</span><span class="sxs-lookup"><span data-stu-id="1e152-105">You can use the **Volume Groups** node on the **Scope** pane to assign volumes to volume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span> 

<span data-ttu-id="1e152-106">Volume groups are pools of related volumes used to ensure that backups are application-consistent.</span><span class="sxs-lookup"><span data-stu-id="1e152-106">Volume groups are pools of related volumes used to ensure that backups are application-consistent.</span></span> <span data-ttu-id="1e152-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="1e152-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="1e152-108">All volumes in a volume group must come from a single cloud service provider.</span><span class="sxs-lookup"><span data-stu-id="1e152-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="1e152-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="1e152-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in the same snapshot.</span><span class="sxs-lookup"><span data-stu-id="1e152-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in the same snapshot.</span></span>
> 
> 

![Volume groups node](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="1e152-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span><span class="sxs-lookup"><span data-stu-id="1e152-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="1e152-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span><span class="sxs-lookup"><span data-stu-id="1e152-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="1e152-114">View information about your volume groups</span><span class="sxs-lookup"><span data-stu-id="1e152-114">View information about your volume groups</span></span> 
* <span data-ttu-id="1e152-115">Create a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-115">Create a volume group</span></span>
* <span data-ttu-id="1e152-116">Back up a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-116">Back up a volume group</span></span>
* <span data-ttu-id="1e152-117">Edit a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-117">Edit a volume group</span></span>
* <span data-ttu-id="1e152-118">Delete a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-118">Delete a volume group</span></span>

<span data-ttu-id="1e152-119">All of these actions are also available on the **Actions** pane.</span><span class="sxs-lookup"><span data-stu-id="1e152-119">All of these actions are also available on the **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="1e152-120">View volume groups</span><span class="sxs-lookup"><span data-stu-id="1e152-120">View volume groups</span></span>
<span data-ttu-id="1e152-121">If you click the **Volume Groups** node, the **Results** pane shows the following information about each volume group, depending on the column selections you make.</span><span class="sxs-lookup"><span data-stu-id="1e152-121">If you click the **Volume Groups** node, the **Results** pane shows the following information about each volume group, depending on the column selections you make.</span></span> <span data-ttu-id="1e152-122">(The columns in the **Results** pane are configurable.</span><span class="sxs-lookup"><span data-stu-id="1e152-122">(The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="1e152-123">Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span><span class="sxs-lookup"><span data-stu-id="1e152-123">Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="1e152-124">Results column</span><span class="sxs-lookup"><span data-stu-id="1e152-124">Results column</span></span> | <span data-ttu-id="1e152-125">Description</span><span class="sxs-lookup"><span data-stu-id="1e152-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1e152-126">Name</span><span class="sxs-lookup"><span data-stu-id="1e152-126">Name</span></span> |<span data-ttu-id="1e152-127">The **Name** column contains the name of the volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-127">The **Name** column contains the name of the volume group.</span></span> |
| <span data-ttu-id="1e152-128">Application</span><span class="sxs-lookup"><span data-stu-id="1e152-128">Application</span></span> |<span data-ttu-id="1e152-129">The **Applications** column shows the number of VSS writers currently installed and running on the Windows host.</span><span class="sxs-lookup"><span data-stu-id="1e152-129">The **Applications** column shows the number of VSS writers currently installed and running on the Windows host.</span></span> |
| <span data-ttu-id="1e152-130">Selected</span><span class="sxs-lookup"><span data-stu-id="1e152-130">Selected</span></span> |<span data-ttu-id="1e152-131">The **Selected** column shows the number of volumes that are contained in the volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-131">The **Selected** column shows the number of volumes that are contained in the volume group.</span></span> <span data-ttu-id="1e152-132">A zero (0) indicates that no application is associated with the volumes in the volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-132">A zero (0) indicates that no application is associated with the volumes in the volume group.</span></span> |
| <span data-ttu-id="1e152-133">Imported</span><span class="sxs-lookup"><span data-stu-id="1e152-133">Imported</span></span> |<span data-ttu-id="1e152-134">The **Imported** column shows the number of imported volumes.</span><span class="sxs-lookup"><span data-stu-id="1e152-134">The **Imported** column shows the number of imported volumes.</span></span> <span data-ttu-id="1e152-135">When set to **True**, this column indicates that a volume group was imported from the Azure classic portal and was not created in StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1e152-135">When set to **True**, this column indicates that a volume group was imported from the Azure classic portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="1e152-136">StorSimple Snapshot Manager volume groups are also displayed on the **Backup Policies** tab in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="1e152-136">StorSimple Snapshot Manager volume groups are also displayed on the **Backup Policies** tab in the Azure classic portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="1e152-137">Create a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-137">Create a volume group</span></span>
<span data-ttu-id="1e152-138">Use the following procedure to create a volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-138">Use the following procedure to create a volume group.</span></span>

#### <a name="to-create-a-volume-group"></a><span data-ttu-id="1e152-139">To create a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-139">To create a volume group</span></span>
1. <span data-ttu-id="1e152-140">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1e152-140">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="1e152-141">In the **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span><span class="sxs-lookup"><span data-stu-id="1e152-141">In the **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span> 
   
    ![Create volume group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="1e152-143">The **Create a volume group** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="1e152-143">The **Create a volume group** dialog box appears.</span></span> 
   
    ![Create a volume group dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png) 
3. <span data-ttu-id="1e152-145">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="1e152-145">Enter the following information:</span></span> 
   
   1. <span data-ttu-id="1e152-146">In the **Name** box, type a unique name for the new volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-146">In the **Name** box, type a unique name for the new volume group.</span></span> 
   2. <span data-ttu-id="1e152-147">In the **Applications** box, select applications associated with the volumes that you will be adding to the volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-147">In the **Applications** box, select applications associated with the volumes that you will be adding to the volume group.</span></span> 
      
       <span data-ttu-id="1e152-148">The **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span><span class="sxs-lookup"><span data-stu-id="1e152-148">The **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="1e152-149">A VSS writer is enabled only if all the volumes that the writer is aware of are StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="1e152-149">A VSS writer is enabled only if all the volumes that the writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="1e152-150">If the Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span><span class="sxs-lookup"><span data-stu-id="1e152-150">If the Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="1e152-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="1e152-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="1e152-152">If you select an application, all volumes associated with it are automatically selected.</span><span class="sxs-lookup"><span data-stu-id="1e152-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="1e152-153">Conversely, if you select volumes associated with a specific application, the application is automatically selected in the **Applications** box.</span><span class="sxs-lookup"><span data-stu-id="1e152-153">Conversely, if you select volumes associated with a specific application, the application is automatically selected in the **Applications** box.</span></span> 
   3. <span data-ttu-id="1e152-154">In the **Volumes** box, select StorSimple volumes to add to the volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-154">In the **Volumes** box, select StorSimple volumes to add to the volume group.</span></span> 
      
      * <span data-ttu-id="1e152-155">You can include volumes with single or multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="1e152-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="1e152-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span><span class="sxs-lookup"><span data-stu-id="1e152-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="1e152-157">Consequently, if you add only one of the partitions to a volume group, all the other partitions are automatically added to that volume group at the same time.</span><span class="sxs-lookup"><span data-stu-id="1e152-157">Consequently, if you add only one of the partitions to a volume group, all the other partitions are automatically added to that volume group at the same time.</span></span> <span data-ttu-id="1e152-158">After you add a multiple partition volume to a volume group, the multiple partition volume continues to be treated as a single unit.</span><span class="sxs-lookup"><span data-stu-id="1e152-158">After you add a multiple partition volume to a volume group, the multiple partition volume continues to be treated as a single unit.</span></span>
      * <span data-ttu-id="1e152-159">You can create empty volume groups by not assigning any volumes to them.</span><span class="sxs-lookup"><span data-stu-id="1e152-159">You can create empty volume groups by not assigning any volumes to them.</span></span> 
      * <span data-ttu-id="1e152-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="1e152-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in the same snapshot.</span><span class="sxs-lookup"><span data-stu-id="1e152-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in the same snapshot.</span></span> 
4. <span data-ttu-id="1e152-162">Click **OK** to save the volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-162">Click **OK** to save the volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="1e152-163">Back up a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-163">Back up a volume group</span></span>
<span data-ttu-id="1e152-164">Use the following procedure to back up a volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-164">Use the following procedure to back up a volume group.</span></span>

#### <a name="to-back-up-a-volume-group"></a><span data-ttu-id="1e152-165">To back up a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-165">To back up a volume group</span></span>
1. <span data-ttu-id="1e152-166">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1e152-166">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1e152-167">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span><span class="sxs-lookup"><span data-stu-id="1e152-167">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span> 
   
    ![Back up volume group immediately](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="1e152-169">In the **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1e152-169">In the **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span> 
   
    ![Take backup dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png) 
4. <span data-ttu-id="1e152-171">To confirm that the backup is running, expand the **Jobs** node, and then click **Running**.</span><span class="sxs-lookup"><span data-stu-id="1e152-171">To confirm that the backup is running, expand the **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="1e152-172">The backup should be listed.</span><span class="sxs-lookup"><span data-stu-id="1e152-172">The backup should be listed.</span></span>
5. <span data-ttu-id="1e152-173">To view the completed snapshot, expand the **Backup Catalog** node, expand the volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span><span class="sxs-lookup"><span data-stu-id="1e152-173">To view the completed snapshot, expand the **Backup Catalog** node, expand the volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="1e152-174">The backup will be listed if it finished successfully.</span><span class="sxs-lookup"><span data-stu-id="1e152-174">The backup will be listed if it finished successfully.</span></span> 

## <a name="edit-a-volume-group"></a><span data-ttu-id="1e152-175">Edit a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-175">Edit a volume group</span></span>
<span data-ttu-id="1e152-176">Use the following procedure to edit a volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-176">Use the following procedure to edit a volume group.</span></span>

#### <a name="to-edit-a-volume-group"></a><span data-ttu-id="1e152-177">To edit a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-177">To edit a volume group</span></span>
1. <span data-ttu-id="1e152-178">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1e152-178">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1e152-179">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="1e152-179">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span> 
3. <span data-ttu-id="1e152-180">The \*\*Create a volume group \*\*dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="1e152-180">The \*\*Create a volume group \*\*dialog box appears.</span></span> <span data-ttu-id="1e152-181">You can change the **Name**, **Applications**, and **Volumes** entries.</span><span class="sxs-lookup"><span data-stu-id="1e152-181">You can change the **Name**, **Applications**, and **Volumes** entries.</span></span> 
4. <span data-ttu-id="1e152-182">Click **OK** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="1e152-182">Click **OK** to save your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="1e152-183">Delete a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-183">Delete a volume group</span></span>
<span data-ttu-id="1e152-184">Use the following procedure to delete a volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-184">Use the following procedure to delete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="1e152-185">This also deletes all the backups associated with the volume group.</span><span class="sxs-lookup"><span data-stu-id="1e152-185">This also deletes all the backups associated with the volume group.</span></span>
> 
> 

#### <a name="to-delete-a-volume-group"></a><span data-ttu-id="1e152-186">To delete a volume group</span><span class="sxs-lookup"><span data-stu-id="1e152-186">To delete a volume group</span></span>
1. <span data-ttu-id="1e152-187">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1e152-187">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="1e152-188">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="1e152-188">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span> 
3. <span data-ttu-id="1e152-189">The **Delete Volume Group** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="1e152-189">The **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="1e152-190">Type **Confirm** in the text box, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e152-190">Type **Confirm** in the text box, and then click **OK**.</span></span> 
   
    <span data-ttu-id="1e152-191">The deleted volume group vanishes from the list in the **Results** pane and all backups that are associated with that volume group are deleted from the backup catalog.</span><span class="sxs-lookup"><span data-stu-id="1e152-191">The deleted volume group vanishes from the list in the **Results** pane and all backups that are associated with that volume group are deleted from the backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e152-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e152-192">Next steps</span></span>
* <span data-ttu-id="1e152-193">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1e152-193">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="1e152-194">Learn how to [use StorSimple Snapshot Manager to create and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1e152-194">Learn how to [use StorSimple Snapshot Manager to create and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>






