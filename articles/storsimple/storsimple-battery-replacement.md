---
title: Replace battery on Microsoft Azure StorSimple device | Microsoft Docs
description: Describes how to remove, replace, and maintain the backup battery module on your StorSimple device.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: da89bf576a85d6bde880d31602de16888c3fa45b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555755"
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="61aeb-103">Replace the backup battery module on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="61aeb-103">Replace the backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="61aeb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="61aeb-104">Overview</span></span>
<span data-ttu-id="61aeb-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span><span class="sxs-lookup"><span data-stu-id="61aeb-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="61aeb-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span><span class="sxs-lookup"><span data-stu-id="61aeb-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="61aeb-107">This battery pack is referred to as the *backup battery module*.</span><span class="sxs-lookup"><span data-stu-id="61aeb-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="61aeb-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span><span class="sxs-lookup"><span data-stu-id="61aeb-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="61aeb-109">This tutorial explains how to:</span><span class="sxs-lookup"><span data-stu-id="61aeb-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="61aeb-110">Remove the backup battery module</span><span class="sxs-lookup"><span data-stu-id="61aeb-110">Remove the backup battery module</span></span> 
* <span data-ttu-id="61aeb-111">Install a new backup battery module</span><span class="sxs-lookup"><span data-stu-id="61aeb-111">Install a new backup battery module</span></span>
* <span data-ttu-id="61aeb-112">Maintain the backup battery module</span><span class="sxs-lookup"><span data-stu-id="61aeb-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61aeb-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="61aeb-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="61aeb-114">Remove the backup battery module</span><span class="sxs-lookup"><span data-stu-id="61aeb-114">Remove the backup battery module</span></span>
<span data-ttu-id="61aeb-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span><span class="sxs-lookup"><span data-stu-id="61aeb-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="61aeb-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span><span class="sxs-lookup"><span data-stu-id="61aeb-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="61aeb-117">Perform the following steps to remove the backup battery.</span><span class="sxs-lookup"><span data-stu-id="61aeb-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="61aeb-118">To remove the backup battery module</span><span class="sxs-lookup"><span data-stu-id="61aeb-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="61aeb-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span><span class="sxs-lookup"><span data-stu-id="61aeb-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="61aeb-120">Under **Shared Components**, look at the status of the battery.</span><span class="sxs-lookup"><span data-stu-id="61aeb-120">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="61aeb-121">Identify the PCM in which the battery has failed.</span><span class="sxs-lookup"><span data-stu-id="61aeb-121">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="61aeb-122">Figure 1 shows the back of the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="61aeb-122">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Backplane Of Device Primary Enclosure Modules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="61aeb-124">**Figure 1** Back of primary device showing PCM and controller modules</span><span class="sxs-lookup"><span data-stu-id="61aeb-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="61aeb-125">Label</span><span class="sxs-lookup"><span data-stu-id="61aeb-125">Label</span></span> | <span data-ttu-id="61aeb-126">Description</span><span class="sxs-lookup"><span data-stu-id="61aeb-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="61aeb-127">1</span><span class="sxs-lookup"><span data-stu-id="61aeb-127">1</span></span> |<span data-ttu-id="61aeb-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="61aeb-128">PCM 0</span></span> |
   | <span data-ttu-id="61aeb-129">2</span><span class="sxs-lookup"><span data-stu-id="61aeb-129">2</span></span> |<span data-ttu-id="61aeb-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="61aeb-130">PCM 1</span></span> |
   | <span data-ttu-id="61aeb-131">3</span><span class="sxs-lookup"><span data-stu-id="61aeb-131">3</span></span> |<span data-ttu-id="61aeb-132">Controller 0</span><span class="sxs-lookup"><span data-stu-id="61aeb-132">Controller 0</span></span> |
   | <span data-ttu-id="61aeb-133">4</span><span class="sxs-lookup"><span data-stu-id="61aeb-133">4</span></span> |<span data-ttu-id="61aeb-134">Controller 1</span><span class="sxs-lookup"><span data-stu-id="61aeb-134">Controller 1</span></span> |
   
    <span data-ttu-id="61aeb-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span><span class="sxs-lookup"><span data-stu-id="61aeb-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Backplane Of Device PCM Monitoring Indicator LEDs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="61aeb-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span><span class="sxs-lookup"><span data-stu-id="61aeb-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="61aeb-138">Label</span><span class="sxs-lookup"><span data-stu-id="61aeb-138">Label</span></span> | <span data-ttu-id="61aeb-139">Description</span><span class="sxs-lookup"><span data-stu-id="61aeb-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="61aeb-140">1</span><span class="sxs-lookup"><span data-stu-id="61aeb-140">1</span></span> |<span data-ttu-id="61aeb-141">AC power failure</span><span class="sxs-lookup"><span data-stu-id="61aeb-141">AC power failure</span></span> |
   | <span data-ttu-id="61aeb-142">2</span><span class="sxs-lookup"><span data-stu-id="61aeb-142">2</span></span> |<span data-ttu-id="61aeb-143">Fan failure</span><span class="sxs-lookup"><span data-stu-id="61aeb-143">Fan failure</span></span> |
   | <span data-ttu-id="61aeb-144">3</span><span class="sxs-lookup"><span data-stu-id="61aeb-144">3</span></span> |<span data-ttu-id="61aeb-145">Battery fault</span><span class="sxs-lookup"><span data-stu-id="61aeb-145">Battery fault</span></span> |
   | <span data-ttu-id="61aeb-146">4</span><span class="sxs-lookup"><span data-stu-id="61aeb-146">4</span></span> |<span data-ttu-id="61aeb-147">PCM OK</span><span class="sxs-lookup"><span data-stu-id="61aeb-147">PCM OK</span></span> |
   | <span data-ttu-id="61aeb-148">5</span><span class="sxs-lookup"><span data-stu-id="61aeb-148">5</span></span> |<span data-ttu-id="61aeb-149">DC power failure</span><span class="sxs-lookup"><span data-stu-id="61aeb-149">DC power failure</span></span> |
   | <span data-ttu-id="61aeb-150">6</span><span class="sxs-lookup"><span data-stu-id="61aeb-150">6</span></span> |<span data-ttu-id="61aeb-151">Battery healthy</span><span class="sxs-lookup"><span data-stu-id="61aeb-151">Battery healthy</span></span> |
3. <span data-ttu-id="61aeb-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="61aeb-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="61aeb-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span><span class="sxs-lookup"><span data-stu-id="61aeb-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Removing Battery From PCM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="61aeb-155">**Figure 3** Removing the battery from the PCM</span><span class="sxs-lookup"><span data-stu-id="61aeb-155">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="61aeb-156">Place the module in the field-replaceable unit packaging.</span><span class="sxs-lookup"><span data-stu-id="61aeb-156">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="61aeb-157">Return the defective unit to Microsoft for proper servicing and handling.</span><span class="sxs-lookup"><span data-stu-id="61aeb-157">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="61aeb-158">Install a new backup battery module</span><span class="sxs-lookup"><span data-stu-id="61aeb-158">Install a new backup battery module</span></span>
<span data-ttu-id="61aeb-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="61aeb-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="61aeb-160">To install the battery module</span><span class="sxs-lookup"><span data-stu-id="61aeb-160">To install the battery module</span></span>
1. <span data-ttu-id="61aeb-161">Place the backup battery module in the proper orientation in the PCM.</span><span class="sxs-lookup"><span data-stu-id="61aeb-161">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="61aeb-162">Press down the battery module handle all the way to seat the connector.</span><span class="sxs-lookup"><span data-stu-id="61aeb-162">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="61aeb-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="61aeb-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="61aeb-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="61aeb-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span></span> <span data-ttu-id="61aeb-165">Verify the status of the battery to make sure that the installation was successful.</span><span class="sxs-lookup"><span data-stu-id="61aeb-165">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="61aeb-166">A green status indicates that the battery is healthy.</span><span class="sxs-lookup"><span data-stu-id="61aeb-166">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="61aeb-167">Maintain the backup battery module</span><span class="sxs-lookup"><span data-stu-id="61aeb-167">Maintain the backup battery module</span></span>
<span data-ttu-id="61aeb-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span><span class="sxs-lookup"><span data-stu-id="61aeb-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="61aeb-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span><span class="sxs-lookup"><span data-stu-id="61aeb-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="61aeb-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span><span class="sxs-lookup"><span data-stu-id="61aeb-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="61aeb-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span><span class="sxs-lookup"><span data-stu-id="61aeb-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="61aeb-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span><span class="sxs-lookup"><span data-stu-id="61aeb-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="61aeb-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span><span class="sxs-lookup"><span data-stu-id="61aeb-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="61aeb-174">The battery can report **FAILED** when it simply needs to be charged.</span><span class="sxs-lookup"><span data-stu-id="61aeb-174">The battery can report **FAILED** when it simply needs to be charged.</span></span>
> 
> 

<span data-ttu-id="61aeb-175">If the **DEGRADED** state appears, we recommend the following course of action:</span><span class="sxs-lookup"><span data-stu-id="61aeb-175">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="61aeb-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span><span class="sxs-lookup"><span data-stu-id="61aeb-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="61aeb-177">Observe the system for 12 hours before proceeding.</span><span class="sxs-lookup"><span data-stu-id="61aeb-177">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="61aeb-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span><span class="sxs-lookup"><span data-stu-id="61aeb-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="61aeb-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span><span class="sxs-lookup"><span data-stu-id="61aeb-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="61aeb-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span><span class="sxs-lookup"><span data-stu-id="61aeb-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="61aeb-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span><span class="sxs-lookup"><span data-stu-id="61aeb-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="61aeb-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span><span class="sxs-lookup"><span data-stu-id="61aeb-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61aeb-183">Dispose of the failed battery according to national and regional regulations.</span><span class="sxs-lookup"><span data-stu-id="61aeb-183">Dispose of the failed battery according to national and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="61aeb-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="61aeb-184">Next steps</span></span>
<span data-ttu-id="61aeb-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="61aeb-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>




