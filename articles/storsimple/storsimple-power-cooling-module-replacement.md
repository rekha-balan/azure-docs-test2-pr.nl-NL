---
title: Replace a PCM on your StorSimple device | Microsoft Docs
description: Explains how to remove and replace the Power and Cooling Module (PCM) on your StorSimple device
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: b65aeda336cc0bb268ddfb181334db321238168f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553593"
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="b5fb2-103">Replace a Power and Cooling Module on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="b5fb2-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="b5fb2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b5fb2-104">Overview</span></span>
<span data-ttu-id="b5fb2-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="b5fb2-106">There is only one model of PCM that is certified for each enclosure.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="b5fb2-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="b5fb2-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="b5fb2-109">This tutorial explains how to:</span><span class="sxs-lookup"><span data-stu-id="b5fb2-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="b5fb2-110">Remove a PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-110">Remove a PCM</span></span>
* <span data-ttu-id="b5fb2-111">Install a replacement PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5fb2-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b5fb2-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="b5fb2-113">Before you replace a PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-113">Before you replace a PCM</span></span>
<span data-ttu-id="b5fb2-114">Be aware of the following important issues before you replace your PCM:</span><span class="sxs-lookup"><span data-stu-id="b5fb2-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="b5fb2-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="b5fb2-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="b5fb2-117">If the fan fails, the PCM needs to be replaced immediately.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="b5fb2-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="b5fb2-119">This provides a warning to your system that a power shutdown is imminent.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="b5fb2-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="b5fb2-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="b5fb2-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="b5fb2-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="b5fb2-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="b5fb2-125">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b5fb2-125">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="b5fb2-126">Remove a PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-126">Remove a PCM</span></span>
<span data-ttu-id="b5fb2-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="b5fb2-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span><span class="sxs-lookup"><span data-stu-id="b5fb2-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>
> 
> 

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="b5fb2-129">To remove a PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-129">To remove a PCM</span></span>
1. <span data-ttu-id="b5fb2-130">In the Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-130">In the Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="b5fb2-131">Check the status of the PCM components under **Shared Components** to identify which PCM has failed:</span><span class="sxs-lookup"><span data-stu-id="b5fb2-131">Check the status of the PCM components under **Shared Components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="b5fb2-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="b5fb2-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="b5fb2-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="b5fb2-135">Locate the failed PCM on the back of the primary enclosure.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="b5fb2-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="b5fb2-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="b5fb2-138">The following diagram and table explain the front panel of the LED display.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![System ID on front OPS panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="b5fb2-140">**Figure 1** Front panel of the device</span><span class="sxs-lookup"><span data-stu-id="b5fb2-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="b5fb2-141">Label</span><span class="sxs-lookup"><span data-stu-id="b5fb2-141">Label</span></span> | <span data-ttu-id="b5fb2-142">Description</span><span class="sxs-lookup"><span data-stu-id="b5fb2-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b5fb2-143">1</span><span class="sxs-lookup"><span data-stu-id="b5fb2-143">1</span></span> |<span data-ttu-id="b5fb2-144">Mute button</span><span class="sxs-lookup"><span data-stu-id="b5fb2-144">Mute button</span></span> |
   | <span data-ttu-id="b5fb2-145">2</span><span class="sxs-lookup"><span data-stu-id="b5fb2-145">2</span></span> |<span data-ttu-id="b5fb2-146">System power</span><span class="sxs-lookup"><span data-stu-id="b5fb2-146">System power</span></span> |
   | <span data-ttu-id="b5fb2-147">3</span><span class="sxs-lookup"><span data-stu-id="b5fb2-147">3</span></span> |<span data-ttu-id="b5fb2-148">Module fault</span><span class="sxs-lookup"><span data-stu-id="b5fb2-148">Module fault</span></span> |
   | <span data-ttu-id="b5fb2-149">4</span><span class="sxs-lookup"><span data-stu-id="b5fb2-149">4</span></span> |<span data-ttu-id="b5fb2-150">Logical fault</span><span class="sxs-lookup"><span data-stu-id="b5fb2-150">Logical fault</span></span> |
   | <span data-ttu-id="b5fb2-151">5</span><span class="sxs-lookup"><span data-stu-id="b5fb2-151">5</span></span> |<span data-ttu-id="b5fb2-152">Unit ID display</span><span class="sxs-lookup"><span data-stu-id="b5fb2-152">Unit ID display</span></span> |
3. <span data-ttu-id="b5fb2-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="b5fb2-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="b5fb2-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="b5fb2-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![Backplane of device PCM monitoring indicator LEDs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="b5fb2-158">**Figure 2** Back of PCM with indicator LEDs</span><span class="sxs-lookup"><span data-stu-id="b5fb2-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="b5fb2-159">Label</span><span class="sxs-lookup"><span data-stu-id="b5fb2-159">Label</span></span> | <span data-ttu-id="b5fb2-160">Description</span><span class="sxs-lookup"><span data-stu-id="b5fb2-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b5fb2-161">1</span><span class="sxs-lookup"><span data-stu-id="b5fb2-161">1</span></span> |<span data-ttu-id="b5fb2-162">AC power failure</span><span class="sxs-lookup"><span data-stu-id="b5fb2-162">AC power failure</span></span> |
   | <span data-ttu-id="b5fb2-163">2</span><span class="sxs-lookup"><span data-stu-id="b5fb2-163">2</span></span> |<span data-ttu-id="b5fb2-164">Fan failure</span><span class="sxs-lookup"><span data-stu-id="b5fb2-164">Fan failure</span></span> |
   | <span data-ttu-id="b5fb2-165">3</span><span class="sxs-lookup"><span data-stu-id="b5fb2-165">3</span></span> |<span data-ttu-id="b5fb2-166">Battery fault</span><span class="sxs-lookup"><span data-stu-id="b5fb2-166">Battery fault</span></span> |
   | <span data-ttu-id="b5fb2-167">4</span><span class="sxs-lookup"><span data-stu-id="b5fb2-167">4</span></span> |<span data-ttu-id="b5fb2-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="b5fb2-168">PCM OK</span></span> |
   | <span data-ttu-id="b5fb2-169">5</span><span class="sxs-lookup"><span data-stu-id="b5fb2-169">5</span></span> |<span data-ttu-id="b5fb2-170">DC power failure</span><span class="sxs-lookup"><span data-stu-id="b5fb2-170">DC power failure</span></span> |
   | <span data-ttu-id="b5fb2-171">6</span><span class="sxs-lookup"><span data-stu-id="b5fb2-171">6</span></span> |<span data-ttu-id="b5fb2-172">Battery healthy</span><span class="sxs-lookup"><span data-stu-id="b5fb2-172">Battery healthy</span></span> |
4. <span data-ttu-id="b5fb2-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="b5fb2-174">PCM 0 is on the left and PCM 1 is on the right.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="b5fb2-175">The table that follows explains the modules.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-175">The table that follows explains the modules.</span></span>
   
     ![Backplane of device primary enclosure modules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="b5fb2-177">**Figure 3** Back of device with plug-in modules</span><span class="sxs-lookup"><span data-stu-id="b5fb2-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="b5fb2-178">Label</span><span class="sxs-lookup"><span data-stu-id="b5fb2-178">Label</span></span> | <span data-ttu-id="b5fb2-179">Description</span><span class="sxs-lookup"><span data-stu-id="b5fb2-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b5fb2-180">1</span><span class="sxs-lookup"><span data-stu-id="b5fb2-180">1</span></span> |<span data-ttu-id="b5fb2-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="b5fb2-181">PCM 0</span></span> |
   | <span data-ttu-id="b5fb2-182">2</span><span class="sxs-lookup"><span data-stu-id="b5fb2-182">2</span></span> |<span data-ttu-id="b5fb2-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="b5fb2-183">PCM 1</span></span> |
   | <span data-ttu-id="b5fb2-184">3</span><span class="sxs-lookup"><span data-stu-id="b5fb2-184">3</span></span> |<span data-ttu-id="b5fb2-185">Controller 0</span><span class="sxs-lookup"><span data-stu-id="b5fb2-185">Controller 0</span></span> |
   | <span data-ttu-id="b5fb2-186">4</span><span class="sxs-lookup"><span data-stu-id="b5fb2-186">4</span></span> |<span data-ttu-id="b5fb2-187">Controller 1</span><span class="sxs-lookup"><span data-stu-id="b5fb2-187">Controller 1</span></span> |
5. <span data-ttu-id="b5fb2-188">Turn off the faulty PCM and disconnect the power supply cord.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="b5fb2-189">You can now remove the PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="b5fb2-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![Opening PCM Handle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="b5fb2-192">**Figure 4** Opening the PCM handle</span><span class="sxs-lookup"><span data-stu-id="b5fb2-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="b5fb2-193">Grip the handle and remove the PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-193">Grip the handle and remove the PCM.</span></span>
   
    ![Removing Device PCM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="b5fb2-195">**Figure 5** Removing the PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="b5fb2-196">Install a replacement PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-196">Install a replacement PCM</span></span>
<span data-ttu-id="b5fb2-197">Follow these instructions to install a PCM in your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="b5fb2-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span><span class="sxs-lookup"><span data-stu-id="b5fb2-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="b5fb2-199">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b5fb2-199">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="b5fb2-200">To install a PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-200">To install a PCM</span></span>
1. <span data-ttu-id="b5fb2-201">Verify that you have the correct replacement PCM for this enclosure.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="b5fb2-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="b5fb2-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="b5fb2-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![Device PCM Label](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="b5fb2-206">**Figure 6** PCM label</span><span class="sxs-lookup"><span data-stu-id="b5fb2-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="b5fb2-207">Check for damage to the enclosure, paying particular attention to the connectors.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b5fb2-208">**Do not install the module if any connector pins are bent.**</span><span class="sxs-lookup"><span data-stu-id="b5fb2-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="b5fb2-209">With the PCM handle in the open position, slide the module into the enclosure.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![Installing Device PCM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="b5fb2-211">**Figure 7** Installing the PCM</span><span class="sxs-lookup"><span data-stu-id="b5fb2-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="b5fb2-212">Manually close the PCM handle.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-212">Manually close the PCM handle.</span></span> <span data-ttu-id="b5fb2-213">You should hear a click as the handle latch engages.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-213">You should hear a click as the handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b5fb2-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="b5fb2-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="b5fb2-216">Connect the power cables to the power source and to the PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="b5fb2-217">Secure the strain relief bales.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-217">Secure the strain relief bales.</span></span> 
7. <span data-ttu-id="b5fb2-218">Turn on the PCM.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="b5fb2-219">Verify that the replacement was successful: in the Azure classic portal of your StorSimple Manager service, navigate to **Devices** > **Maintenance** > **Hardware Status**.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-219">Verify that the replacement was successful: in the Azure classic portal of your StorSimple Manager service, navigate to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="b5fb2-220">Under **Shared Components**, the status of the PCM should be green.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-220">Under **Shared Components**, the status of the PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b5fb2-221">It may take a few minutes for the replacement PCM to completely initialize.</span><span class="sxs-lookup"><span data-stu-id="b5fb2-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="b5fb2-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5fb2-222">Next steps</span></span>
<span data-ttu-id="b5fb2-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b5fb2-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>








