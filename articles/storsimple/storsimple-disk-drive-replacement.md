---
title: Replace a disk drive on a StorSimple device | Microsoft Docs
description: Explains how to replace a disk drive on a StorSimple primary enclosure or an EBOD enclosure.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 9c4fec8d60b5b5d8505fca201dd0b1fb34314722
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562963"
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="84306-103">Replace a disk drive on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="84306-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="84306-104">Overview</span><span class="sxs-lookup"><span data-stu-id="84306-104">Overview</span></span>
<span data-ttu-id="84306-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="84306-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="84306-106">To replace a disk drive, you need to:</span><span class="sxs-lookup"><span data-stu-id="84306-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="84306-107">Disengage the antitamper lock</span><span class="sxs-lookup"><span data-stu-id="84306-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="84306-108">Remove the disk drive</span><span class="sxs-lookup"><span data-stu-id="84306-108">Remove the disk drive</span></span>
* <span data-ttu-id="84306-109">Install the replacement disk drive</span><span class="sxs-lookup"><span data-stu-id="84306-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84306-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="84306-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="84306-111">Disengage the antitamper lock</span><span class="sxs-lookup"><span data-stu-id="84306-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="84306-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span><span class="sxs-lookup"><span data-stu-id="84306-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="84306-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span><span class="sxs-lookup"><span data-stu-id="84306-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="84306-114">Drives are supplied with the locks set to the locked position.</span><span class="sxs-lookup"><span data-stu-id="84306-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="84306-115">To unlock the antitamper lock</span><span class="sxs-lookup"><span data-stu-id="84306-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="84306-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span><span class="sxs-lookup"><span data-stu-id="84306-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="84306-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span><span class="sxs-lookup"><span data-stu-id="84306-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
   > 
   > 
   
    ![Locked disk drive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="84306-119">**Figure 1** Anti-tamper lock engaged</span><span class="sxs-lookup"><span data-stu-id="84306-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="84306-120">Label</span><span class="sxs-lookup"><span data-stu-id="84306-120">Label</span></span> | <span data-ttu-id="84306-121">Description</span><span class="sxs-lookup"><span data-stu-id="84306-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="84306-122">1</span><span class="sxs-lookup"><span data-stu-id="84306-122">1</span></span> |<span data-ttu-id="84306-123">Indicator aperture</span><span class="sxs-lookup"><span data-stu-id="84306-123">Indicator aperture</span></span> |
   | <span data-ttu-id="84306-124">2</span><span class="sxs-lookup"><span data-stu-id="84306-124">2</span></span> |<span data-ttu-id="84306-125">Antitamper lock</span><span class="sxs-lookup"><span data-stu-id="84306-125">Antitamper lock</span></span> |
2. <span data-ttu-id="84306-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span><span class="sxs-lookup"><span data-stu-id="84306-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="84306-127">Remove the key.</span><span class="sxs-lookup"><span data-stu-id="84306-127">Remove the key.</span></span>
   
    ![Unlocked disk drive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="84306-129">**Figure 2** Unlocked disk drive</span><span class="sxs-lookup"><span data-stu-id="84306-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="84306-130">The disk drive can now be removed.</span><span class="sxs-lookup"><span data-stu-id="84306-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="84306-131">Follow the steps in reverse to engage the lock.</span><span class="sxs-lookup"><span data-stu-id="84306-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="84306-132">Remove the disk drive</span><span class="sxs-lookup"><span data-stu-id="84306-132">Remove the disk drive</span></span>
<span data-ttu-id="84306-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span><span class="sxs-lookup"><span data-stu-id="84306-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="84306-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span><span class="sxs-lookup"><span data-stu-id="84306-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="84306-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span><span class="sxs-lookup"><span data-stu-id="84306-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="84306-136">Doing so could result in loss of data.</span><span class="sxs-lookup"><span data-stu-id="84306-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="84306-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span><span class="sxs-lookup"><span data-stu-id="84306-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="84306-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span><span class="sxs-lookup"><span data-stu-id="84306-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="84306-139">In the Azure classic portal, slots are numbered from 0 – 11.</span><span class="sxs-lookup"><span data-stu-id="84306-139">In the Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="84306-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span><span class="sxs-lookup"><span data-stu-id="84306-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="84306-141">Drives can be removed and replaced while the system is operating.</span><span class="sxs-lookup"><span data-stu-id="84306-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="84306-142">To remove a drive</span><span class="sxs-lookup"><span data-stu-id="84306-142">To remove a drive</span></span>
1. <span data-ttu-id="84306-143">To identify the failed disk, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span><span class="sxs-lookup"><span data-stu-id="84306-143">To identify the failed disk, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="84306-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span><span class="sxs-lookup"><span data-stu-id="84306-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="84306-145">A failed disk in either enclosure will be shown with a red status.</span><span class="sxs-lookup"><span data-stu-id="84306-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="84306-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span><span class="sxs-lookup"><span data-stu-id="84306-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="84306-147">If the disk is unlocked, proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="84306-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="84306-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="84306-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="84306-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span><span class="sxs-lookup"><span data-stu-id="84306-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span> 
   
    ![Releasing disk drive handle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="84306-151">**Figure 3** Releasing the drive handle</span><span class="sxs-lookup"><span data-stu-id="84306-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="84306-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span><span class="sxs-lookup"><span data-stu-id="84306-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Sliding disk out of disk drive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="84306-154">**Figure 4** Sliding the disk drive out of the carrier</span><span class="sxs-lookup"><span data-stu-id="84306-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="84306-155">Install the replacement disk drive</span><span class="sxs-lookup"><span data-stu-id="84306-155">Install the replacement disk drive</span></span>
<span data-ttu-id="84306-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span><span class="sxs-lookup"><span data-stu-id="84306-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="84306-157">To insert a drive</span><span class="sxs-lookup"><span data-stu-id="84306-157">To insert a drive</span></span>
1. <span data-ttu-id="84306-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="84306-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![Disk drive with handle extended](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="84306-160">**Figure 5** Drive with handle extended</span><span class="sxs-lookup"><span data-stu-id="84306-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="84306-161">Slide the drive carrier all the way into the chassis.</span><span class="sxs-lookup"><span data-stu-id="84306-161">Slide the drive carrier all the way into the chassis.</span></span> 
   
    ![Sliding disk into disk drive carrier](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="84306-163">**Figure 6**  Sliding the drive carrier into the chassis</span><span class="sxs-lookup"><span data-stu-id="84306-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="84306-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span><span class="sxs-lookup"><span data-stu-id="84306-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="84306-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span><span class="sxs-lookup"><span data-stu-id="84306-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="84306-166">Verify that the replacement was successful and the drive is operational by accessing the Azure classic portal and navigating to **Maintenance** > **Hardware Status**.</span><span class="sxs-lookup"><span data-stu-id="84306-166">Verify that the replacement was successful and the drive is operational by accessing the Azure classic portal and navigating to **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="84306-167">Under **Shared Components** or **EBOD enclosure Shared Components**, the drive status should be green, indicating that it is healthy.</span><span class="sxs-lookup"><span data-stu-id="84306-167">Under **Shared Components** or **EBOD enclosure Shared Components**, the drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="84306-168">It may take several hours for the disk status to turn green after the replacement.</span><span class="sxs-lookup"><span data-stu-id="84306-168">It may take several hours for the disk status to turn green after the replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="84306-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="84306-169">Next steps</span></span>
<span data-ttu-id="84306-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="84306-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>







