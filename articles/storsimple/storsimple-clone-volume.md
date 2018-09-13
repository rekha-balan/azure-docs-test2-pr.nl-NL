---
title: Clone your StorSimple volume | Microsoft Docs
description: Describes the different clone types and when to use them, and explains how you can use a backup set to clone an individual volume.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 6e4a097d77075885d979a261cb41ba4560591c0b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563348"
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume"></a><span data-ttu-id="a9a50-103">Use the StorSimple Manager service to clone a volume</span><span class="sxs-lookup"><span data-stu-id="a9a50-103">Use the StorSimple Manager service to clone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="a9a50-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a9a50-104">Overview</span></span>
<span data-ttu-id="a9a50-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span><span class="sxs-lookup"><span data-stu-id="a9a50-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="a9a50-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span><span class="sxs-lookup"><span data-stu-id="a9a50-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![Backup catalog page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="a9a50-108">This tutorial describes how you can use a backup set to clone an individual volume.</span><span class="sxs-lookup"><span data-stu-id="a9a50-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="a9a50-109">It also explains the difference between *transient* and *permanent* clones.</span><span class="sxs-lookup"><span data-stu-id="a9a50-109">It also explains the difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="a9a50-110">Create a clone of a volume</span><span class="sxs-lookup"><span data-stu-id="a9a50-110">Create a clone of a volume</span></span>
<span data-ttu-id="a9a50-111">You can create a clone on the same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span><span class="sxs-lookup"><span data-stu-id="a9a50-111">You can create a clone on the same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="a9a50-112">To clone a volume</span><span class="sxs-lookup"><span data-stu-id="a9a50-112">To clone a volume</span></span>
1. <span data-ttu-id="a9a50-113">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span><span class="sxs-lookup"><span data-stu-id="a9a50-113">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="a9a50-114">Expand the backup set to view the associated volumes.</span><span class="sxs-lookup"><span data-stu-id="a9a50-114">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="a9a50-115">Click and select a volume from the backup set.</span><span class="sxs-lookup"><span data-stu-id="a9a50-115">Click and select a volume from the backup set.</span></span>
   
     ![Clone a volume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="a9a50-117">Click **Clone** to begin cloning the selected volume.</span><span class="sxs-lookup"><span data-stu-id="a9a50-117">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="a9a50-118">In the Clone Volume wizard, under **Specify name and location**:</span><span class="sxs-lookup"><span data-stu-id="a9a50-118">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="a9a50-119">Identify a target device.</span><span class="sxs-lookup"><span data-stu-id="a9a50-119">Identify a target device.</span></span> <span data-ttu-id="a9a50-120">This is the location where the clone will be created.</span><span class="sxs-lookup"><span data-stu-id="a9a50-120">This is the location where the clone will be created.</span></span> <span data-ttu-id="a9a50-121">You can choose the same device or specify another device.</span><span class="sxs-lookup"><span data-stu-id="a9a50-121">You can choose the same device or specify another device.</span></span> <span data-ttu-id="a9a50-122">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span><span class="sxs-lookup"><span data-stu-id="a9a50-122">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="a9a50-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span><span class="sxs-lookup"><span data-stu-id="a9a50-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="a9a50-124">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span><span class="sxs-lookup"><span data-stu-id="a9a50-124">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="a9a50-125">Specify a unique volume name for your clone.</span><span class="sxs-lookup"><span data-stu-id="a9a50-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="a9a50-126">The name must contain between 3 and 127 characters.</span><span class="sxs-lookup"><span data-stu-id="a9a50-126">The name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="a9a50-127">Click the arrow icon</span><span class="sxs-lookup"><span data-stu-id="a9a50-127">Click the arrow icon</span></span> ![arrow-icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="a9a50-129">to proceed to the next page.</span><span class="sxs-lookup"><span data-stu-id="a9a50-129">to proceed to the next page.</span></span>
5. <span data-ttu-id="a9a50-130">Under **Specify hosts that can use this volume**:</span><span class="sxs-lookup"><span data-stu-id="a9a50-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="a9a50-131">Specify an access control record (ACR) for the clone.</span><span class="sxs-lookup"><span data-stu-id="a9a50-131">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="a9a50-132">You can add a new ACR or choose from the existing list.</span><span class="sxs-lookup"><span data-stu-id="a9a50-132">You can add a new ACR or choose from the existing list.</span></span>
   2. <span data-ttu-id="a9a50-133">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="a9a50-133">Click the check icon</span></span> ![check-icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="a9a50-135">to complete the operation.</span><span class="sxs-lookup"><span data-stu-id="a9a50-135">to complete the operation.</span></span>
6. <span data-ttu-id="a9a50-136">A clone job will be initiated and you will be notified when the clone is successfully created.</span><span class="sxs-lookup"><span data-stu-id="a9a50-136">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="a9a50-137">Click **View Job** to monitor the clone job on the **Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="a9a50-137">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span>
7. <span data-ttu-id="a9a50-138">After the clone job is completed:</span><span class="sxs-lookup"><span data-stu-id="a9a50-138">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="a9a50-139">Go to the **Devices** page, and select the **Volume Containers** tab.</span><span class="sxs-lookup"><span data-stu-id="a9a50-139">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="a9a50-140">Select the volume container that is associated with the source volume that you cloned.</span><span class="sxs-lookup"><span data-stu-id="a9a50-140">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="a9a50-141">In the list of volumes, you should see the clone that was just created.</span><span class="sxs-lookup"><span data-stu-id="a9a50-141">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="a9a50-142">Monitoring and default backup are automatically disabled on a cloned volume.</span><span class="sxs-lookup"><span data-stu-id="a9a50-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="a9a50-143">A clone that is created this way is a transient clone.</span><span class="sxs-lookup"><span data-stu-id="a9a50-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="a9a50-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs.-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="a9a50-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs.-permanent-clones).</span></span>

<span data-ttu-id="a9a50-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span><span class="sxs-lookup"><span data-stu-id="a9a50-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="a9a50-146">You will need to configure this volume for any backups.</span><span class="sxs-lookup"><span data-stu-id="a9a50-146">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="a9a50-147">Transient vs. permanent clones</span><span class="sxs-lookup"><span data-stu-id="a9a50-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="a9a50-148">Transient and permanent clones are created only when you are cloning on to a different device.</span><span class="sxs-lookup"><span data-stu-id="a9a50-148">Transient and permanent clones are created only when you are cloning on to a different device.</span></span> <span data-ttu-id="a9a50-149">You can clone a specific volume from a backup set to a different device.</span><span class="sxs-lookup"><span data-stu-id="a9a50-149">You can clone a specific volume from a backup set to a different device.</span></span> <span data-ttu-id="a9a50-150">A clone created in this way is a *transient* clone.</span><span class="sxs-lookup"><span data-stu-id="a9a50-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="a9a50-151">The transient clone will have references to the original volume and will use that volume to read while writing locally.</span><span class="sxs-lookup"><span data-stu-id="a9a50-151">The transient clone will have references to the original volume and will use that volume to read while writing locally.</span></span> 

<span data-ttu-id="a9a50-152">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span><span class="sxs-lookup"><span data-stu-id="a9a50-152">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="a9a50-153">The permanent clone is independent and doesn’t have any references to the original volume that it was cloned from.</span><span class="sxs-lookup"><span data-stu-id="a9a50-153">The permanent clone is independent and doesn’t have any references to the original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="a9a50-154">Scenarios for transient and permanent clones</span><span class="sxs-lookup"><span data-stu-id="a9a50-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="a9a50-155">The following sections describe example situations in which transient and permanent clones can be used.</span><span class="sxs-lookup"><span data-stu-id="a9a50-155">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="a9a50-156">Item-level recovery with a transient clone</span><span class="sxs-lookup"><span data-stu-id="a9a50-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="a9a50-157">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span><span class="sxs-lookup"><span data-stu-id="a9a50-157">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="a9a50-158">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span><span class="sxs-lookup"><span data-stu-id="a9a50-158">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="a9a50-159">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span><span class="sxs-lookup"><span data-stu-id="a9a50-159">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="a9a50-160">In this scenario, a transient clone is used.</span><span class="sxs-lookup"><span data-stu-id="a9a50-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="a9a50-161">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume/Video_icon.png) **Video available**</span><span class="sxs-lookup"><span data-stu-id="a9a50-161">![Video available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="a9a50-162">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="a9a50-162">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="a9a50-163">Testing in the production environment with a permanent clone</span><span class="sxs-lookup"><span data-stu-id="a9a50-163">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="a9a50-164">You need to verify a testing bug in the production environment.</span><span class="sxs-lookup"><span data-stu-id="a9a50-164">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="a9a50-165">You create a clone of the volume in the production environment by taking a cloud snapshot of this clone.</span><span class="sxs-lookup"><span data-stu-id="a9a50-165">You create a clone of the volume in the production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="a9a50-166">The cloned volume is now independent.</span><span class="sxs-lookup"><span data-stu-id="a9a50-166">The cloned volume is now independent.</span></span> <span data-ttu-id="a9a50-167">In this scenario, a permanent clone is used.</span><span class="sxs-lookup"><span data-stu-id="a9a50-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9a50-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9a50-168">Next steps</span></span>
* <span data-ttu-id="a9a50-169">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="a9a50-169">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="a9a50-170">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a9a50-170">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>






