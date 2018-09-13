---
title: Clone StorSimple 8000 series volume | Microsoft Docs
description: Describes the different clone types and when to use them, and explains how you can use a backup set to clone an individual volume.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/27/2016
ms.author: alkohli
ms.openlocfilehash: ea4e0390688306b1f690657ed2f814fd79779bc9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555541"
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume-update-2"></a><span data-ttu-id="f64a0-103">Use the StorSimple Manager service to clone a volume (Update 2)</span><span class="sxs-lookup"><span data-stu-id="f64a0-103">Use the StorSimple Manager service to clone a volume (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="f64a0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f64a0-104">Overview</span></span>
<span data-ttu-id="f64a0-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span><span class="sxs-lookup"><span data-stu-id="f64a0-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="f64a0-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span><span class="sxs-lookup"><span data-stu-id="f64a0-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![Backup catalog page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/backupCatalog.png)  

<span data-ttu-id="f64a0-108">This tutorial describes how you can use a backup set to clone an individual volume.</span><span class="sxs-lookup"><span data-stu-id="f64a0-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="f64a0-109">It also explains the difference between *transient* and *permanent* clones.</span><span class="sxs-lookup"><span data-stu-id="f64a0-109">It also explains the difference between *transient* and *permanent* clones.</span></span>

> [!NOTE]
> <span data-ttu-id="f64a0-110">A locally pinned volume will be cloned as a tiered volume.</span><span class="sxs-lookup"><span data-stu-id="f64a0-110">A locally pinned volume will be cloned as a tiered volume.</span></span> <span data-ttu-id="f64a0-111">If you need the cloned volume to be locally pinned, you can convert the clone to a locally pinned volume after the clone operation is successfully completed.</span><span class="sxs-lookup"><span data-stu-id="f64a0-111">If you need the cloned volume to be locally pinned, you can convert the clone to a locally pinned volume after the clone operation is successfully completed.</span></span> <span data-ttu-id="f64a0-112">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span><span class="sxs-lookup"><span data-stu-id="f64a0-112">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
> 
> <span data-ttu-id="f64a0-113">If you try to convert a cloned volume from tiered to locally pinned immediately after cloning (when it is still a transient clone), the conversion will fail with the following error message:</span><span class="sxs-lookup"><span data-stu-id="f64a0-113">If you try to convert a cloned volume from tiered to locally pinned immediately after cloning (when it is still a transient clone), the conversion will fail with the following error message:</span></span>
> 
> `Unable to modify the usage type for volume {0}. This can happen if the volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry the modify operation.` 
> 
> <span data-ttu-id="f64a0-114">This error is received only if you are cloning on to a different device.</span><span class="sxs-lookup"><span data-stu-id="f64a0-114">This error is received only if you are cloning on to a different device.</span></span> <span data-ttu-id="f64a0-115">You can successfully convert the volume to locally pinned if you first convert the transient clone to a permanent clone.</span><span class="sxs-lookup"><span data-stu-id="f64a0-115">You can successfully convert the volume to locally pinned if you first convert the transient clone to a permanent clone.</span></span> <span data-ttu-id="f64a0-116">To convert the transient clone to a permanent clone, take a cloud snapshot of it.</span><span class="sxs-lookup"><span data-stu-id="f64a0-116">To convert the transient clone to a permanent clone, take a cloud snapshot of it.</span></span>
> 
> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="f64a0-117">Create a clone of a volume</span><span class="sxs-lookup"><span data-stu-id="f64a0-117">Create a clone of a volume</span></span>
<span data-ttu-id="f64a0-118">You can create a clone on the same device, another device, or even a virtual machine by using a local or cloud snapshot.</span><span class="sxs-lookup"><span data-stu-id="f64a0-118">You can create a clone on the same device, another device, or even a virtual machine by using a local or cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="f64a0-119">To clone a volume</span><span class="sxs-lookup"><span data-stu-id="f64a0-119">To clone a volume</span></span>
1. <span data-ttu-id="f64a0-120">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span><span class="sxs-lookup"><span data-stu-id="f64a0-120">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="f64a0-121">Expand the backup set to view the associated volumes.</span><span class="sxs-lookup"><span data-stu-id="f64a0-121">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="f64a0-122">Click and select a volume from the backup set.</span><span class="sxs-lookup"><span data-stu-id="f64a0-122">Click and select a volume from the backup set.</span></span>
   
     ![Clone a volume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/CloneVol.png) 
3. <span data-ttu-id="f64a0-124">Click **Clone** to begin cloning the selected volume.</span><span class="sxs-lookup"><span data-stu-id="f64a0-124">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="f64a0-125">In the Clone Volume wizard, under **Specify name and location**:</span><span class="sxs-lookup"><span data-stu-id="f64a0-125">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="f64a0-126">Identify a target device.</span><span class="sxs-lookup"><span data-stu-id="f64a0-126">Identify a target device.</span></span> <span data-ttu-id="f64a0-127">This is the location where the clone will be created.</span><span class="sxs-lookup"><span data-stu-id="f64a0-127">This is the location where the clone will be created.</span></span> <span data-ttu-id="f64a0-128">You can choose the same device or specify another device.</span><span class="sxs-lookup"><span data-stu-id="f64a0-128">You can choose the same device or specify another device.</span></span> <span data-ttu-id="f64a0-129">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span><span class="sxs-lookup"><span data-stu-id="f64a0-129">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="f64a0-130">You cannot clone a volume associated with other cloud service providers on a virtual device.</span><span class="sxs-lookup"><span data-stu-id="f64a0-130">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f64a0-131">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span><span class="sxs-lookup"><span data-stu-id="f64a0-131">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="f64a0-132">Specify a unique volume name for your clone.</span><span class="sxs-lookup"><span data-stu-id="f64a0-132">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="f64a0-133">The name must contain between 3 and 127 characters.</span><span class="sxs-lookup"><span data-stu-id="f64a0-133">The name must contain between 3 and 127 characters.</span></span> 
      
      > [!NOTE]
      > <span data-ttu-id="f64a0-134">The **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span><span class="sxs-lookup"><span data-stu-id="f64a0-134">The **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="f64a0-135">You cannot change this setting; however, if you need the cloned volume to be locally pinned as well, you can convert the clone to a locally pinned volume after you successfully create the clone.</span><span class="sxs-lookup"><span data-stu-id="f64a0-135">You cannot change this setting; however, if you need the cloned volume to be locally pinned as well, you can convert the clone to a locally pinned volume after you successfully create the clone.</span></span> <span data-ttu-id="f64a0-136">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span><span class="sxs-lookup"><span data-stu-id="f64a0-136">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
      > 
      > 
      
        ![Clone wizard 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/clone1.png) 
   3. <span data-ttu-id="f64a0-138">Click the arrow icon</span><span class="sxs-lookup"><span data-stu-id="f64a0-138">Click the arrow icon</span></span> ![arrow-icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) <span data-ttu-id="f64a0-140">to proceed to the next page.</span><span class="sxs-lookup"><span data-stu-id="f64a0-140">to proceed to the next page.</span></span>
5. <span data-ttu-id="f64a0-141">Under **Specify hosts that can use this volume**:</span><span class="sxs-lookup"><span data-stu-id="f64a0-141">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="f64a0-142">Specify an access control record (ACR) for the clone.</span><span class="sxs-lookup"><span data-stu-id="f64a0-142">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="f64a0-143">You can add a new ACR or choose from the existing list.</span><span class="sxs-lookup"><span data-stu-id="f64a0-143">You can add a new ACR or choose from the existing list.</span></span>
      
        ![Clone wizard 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/clone2.png) 
   2. <span data-ttu-id="f64a0-145">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="f64a0-145">Click the check icon</span></span> ![check-icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/HCS_CheckIcon.png)<span data-ttu-id="f64a0-147">to complete the operation.</span><span class="sxs-lookup"><span data-stu-id="f64a0-147">to complete the operation.</span></span>
6. <span data-ttu-id="f64a0-148">A clone job will be initiated and you will be notified when the clone is successfully created.</span><span class="sxs-lookup"><span data-stu-id="f64a0-148">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="f64a0-149">Click **View Job** to monitor the clone job on the **Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="f64a0-149">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span> <span data-ttu-id="f64a0-150">You will see the following message when the clone job is finished:</span><span class="sxs-lookup"><span data-stu-id="f64a0-150">You will see the following message when the clone job is finished:</span></span>
   
    ![Clone message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/CloneMsg.png) 
7. <span data-ttu-id="f64a0-152">After the clone job is completed:</span><span class="sxs-lookup"><span data-stu-id="f64a0-152">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="f64a0-153">Go to the **Devices** page, and select the **Volume Containers** tab.</span><span class="sxs-lookup"><span data-stu-id="f64a0-153">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="f64a0-154">Select the volume container that is associated with the source volume that you cloned.</span><span class="sxs-lookup"><span data-stu-id="f64a0-154">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="f64a0-155">In the list of volumes, you should see the clone that was just created.</span><span class="sxs-lookup"><span data-stu-id="f64a0-155">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="f64a0-156">Monitoring and default backup are automatically disabled on a cloned volume.</span><span class="sxs-lookup"><span data-stu-id="f64a0-156">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="f64a0-157">A clone that is created this way is a transient clone.</span><span class="sxs-lookup"><span data-stu-id="f64a0-157">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="f64a0-158">For more information about clone types, see [Transient vs. permanent clones](#transient-vs.-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="f64a0-158">For more information about clone types, see [Transient vs. permanent clones](#transient-vs.-permanent-clones).</span></span>

<span data-ttu-id="f64a0-159">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span><span class="sxs-lookup"><span data-stu-id="f64a0-159">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="f64a0-160">You will need to configure this volume for any backups.</span><span class="sxs-lookup"><span data-stu-id="f64a0-160">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="f64a0-161">Transient vs. permanent clones</span><span class="sxs-lookup"><span data-stu-id="f64a0-161">Transient vs. permanent clones</span></span>
<span data-ttu-id="f64a0-162">Transient clones are created only when you are cloning to a different device.</span><span class="sxs-lookup"><span data-stu-id="f64a0-162">Transient clones are created only when you are cloning to a different device.</span></span> <span data-ttu-id="f64a0-163">You can clone a specific volume from a backup set to a different device managed by the StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="f64a0-163">You can clone a specific volume from a backup set to a different device managed by the StorSimple Manager.</span></span> <span data-ttu-id="f64a0-164">The transient clone will have references to the data in the original volume and will use that data to read and write locally on the target device.</span><span class="sxs-lookup"><span data-stu-id="f64a0-164">The transient clone will have references to the data in the original volume and will use that data to read and write locally on the target device.</span></span> 

<span data-ttu-id="f64a0-165">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span><span class="sxs-lookup"><span data-stu-id="f64a0-165">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="f64a0-166">During this process, a copy of the data is created on the cloud and the time to copy this data is determined by the size of the data and the Azure latencies (this is an Azure-to-Azure copy).</span><span class="sxs-lookup"><span data-stu-id="f64a0-166">During this process, a copy of the data is created on the cloud and the time to copy this data is determined by the size of the data and the Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="f64a0-167">This process can take days to weeks.</span><span class="sxs-lookup"><span data-stu-id="f64a0-167">This process can take days to weeks.</span></span> <span data-ttu-id="f64a0-168">The transient clone becomes a permanent clone this way and doesn’t have any references to the original volume data that it was cloned from.</span><span class="sxs-lookup"><span data-stu-id="f64a0-168">The transient clone becomes a permanent clone this way and doesn’t have any references to the original volume data that it was cloned from.</span></span> 

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="f64a0-169">Scenarios for transient and permanent clones</span><span class="sxs-lookup"><span data-stu-id="f64a0-169">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="f64a0-170">The following sections describe example situations in which transient and permanent clones can be used.</span><span class="sxs-lookup"><span data-stu-id="f64a0-170">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="f64a0-171">Item-level recovery with a transient clone</span><span class="sxs-lookup"><span data-stu-id="f64a0-171">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="f64a0-172">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span><span class="sxs-lookup"><span data-stu-id="f64a0-172">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="f64a0-173">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span><span class="sxs-lookup"><span data-stu-id="f64a0-173">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="f64a0-174">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span><span class="sxs-lookup"><span data-stu-id="f64a0-174">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="f64a0-175">In this scenario, a transient clone is used.</span><span class="sxs-lookup"><span data-stu-id="f64a0-175">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="f64a0-176">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/Video_icon.png) **Video available**</span><span class="sxs-lookup"><span data-stu-id="f64a0-176">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="f64a0-177">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="f64a0-177">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="f64a0-178">Testing in the production environment with a permanent clone</span><span class="sxs-lookup"><span data-stu-id="f64a0-178">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="f64a0-179">You need to verify a testing bug in the production environment.</span><span class="sxs-lookup"><span data-stu-id="f64a0-179">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="f64a0-180">You create a clone of the volume in the production environment and then take a cloud snapshot of this clone to create an independent cloned volume.</span><span class="sxs-lookup"><span data-stu-id="f64a0-180">You create a clone of the volume in the production environment and then take a cloud snapshot of this clone to create an independent cloned volume.</span></span> <span data-ttu-id="f64a0-181">In this scenario, a permanent clone is used.</span><span class="sxs-lookup"><span data-stu-id="f64a0-181">In this scenario, a permanent clone is used.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f64a0-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="f64a0-182">Next steps</span></span>
* <span data-ttu-id="f64a0-183">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f64a0-183">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="f64a0-184">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f64a0-184">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>









