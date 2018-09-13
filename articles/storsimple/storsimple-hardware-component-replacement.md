---
title: StorSimple hardware component replacement | Microsoft Docs
description: Describes how to safely replace the PCMs, battery, controller modules, EBOD controllers, disk drives, and chassis of a StorSimple device.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: e8087ba7-0b66-4f59-8988-e53aad52ee21
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d36a063edce12c9195112bb01e15beb200b74817
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563639"
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a><span data-ttu-id="d6126-103">Replace a hardware component on your StorSimple 8000 series device</span><span class="sxs-lookup"><span data-stu-id="d6126-103">Replace a hardware component on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="d6126-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d6126-104">Overview</span></span>
<span data-ttu-id="d6126-105">The hardware component replacement tutorials describe the hardware components of your Microsoft Azure StorSimple 8000 series device and the steps necessary to remove and replace them.</span><span class="sxs-lookup"><span data-stu-id="d6126-105">The hardware component replacement tutorials describe the hardware components of your Microsoft Azure StorSimple 8000 series device and the steps necessary to remove and replace them.</span></span> <span data-ttu-id="d6126-106">This article describes the safety icons, provides pointers to the detailed tutorials, and lists the components that are replaceable.</span><span class="sxs-lookup"><span data-stu-id="d6126-106">This article describes the safety icons, provides pointers to the detailed tutorials, and lists the components that are replaceable.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6126-107">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="d6126-107">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

### <a name="safety-icon-conventions"></a><span data-ttu-id="d6126-108">Safety icon conventions</span><span class="sxs-lookup"><span data-stu-id="d6126-108">Safety icon conventions</span></span>
<span data-ttu-id="d6126-109">The following table describes the safety icons used in these tutorials.</span><span class="sxs-lookup"><span data-stu-id="d6126-109">The following table describes the safety icons used in these tutorials.</span></span> <span data-ttu-id="d6126-110">Pay close attention to these safety icons as you go through the steps to remove and replace device components.</span><span class="sxs-lookup"><span data-stu-id="d6126-110">Pay close attention to these safety icons as you go through the steps to remove and replace device components.</span></span>

| <span data-ttu-id="d6126-111">Icon</span><span class="sxs-lookup"><span data-stu-id="d6126-111">Icon</span></span> | <span data-ttu-id="d6126-112">Text</span><span class="sxs-lookup"><span data-stu-id="d6126-112">Text</span></span> | <span data-ttu-id="d6126-113">Additional information</span><span class="sxs-lookup"><span data-stu-id="d6126-113">Additional information</span></span> |
|:--- |:--- |:--- |
| ![Warning icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="d6126-115">**DANGER!**</span><span class="sxs-lookup"><span data-stu-id="d6126-115">**DANGER!**</span></span> |<span data-ttu-id="d6126-116">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span><span class="sxs-lookup"><span data-stu-id="d6126-116">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span></span> <span data-ttu-id="d6126-117">This signal word is limited to the most extreme situations.</span><span class="sxs-lookup"><span data-stu-id="d6126-117">This signal word is limited to the most extreme situations.</span></span> |
| ![Warning icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="d6126-119">**WARNING!**</span><span class="sxs-lookup"><span data-stu-id="d6126-119">**WARNING!**</span></span> |<span data-ttu-id="d6126-120">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span><span class="sxs-lookup"><span data-stu-id="d6126-120">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span></span> |
| ![Caution icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Caution.png) |<span data-ttu-id="d6126-122">**CAUTION!**</span><span class="sxs-lookup"><span data-stu-id="d6126-122">**CAUTION!**</span></span> |<span data-ttu-id="d6126-123">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span><span class="sxs-lookup"><span data-stu-id="d6126-123">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span></span> |
| ![Notice icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/NoticeIcon.png) |<span data-ttu-id="d6126-125">**NOTICE:**</span><span class="sxs-lookup"><span data-stu-id="d6126-125">**NOTICE:**</span></span> |<span data-ttu-id="d6126-126">Indicates information considered important, but not hazard-related.</span><span class="sxs-lookup"><span data-stu-id="d6126-126">Indicates information considered important, but not hazard-related.</span></span> |
| ![Electrical shock icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Electric.png) |<span data-ttu-id="d6126-128">**Electrical Shock Hazard**</span><span class="sxs-lookup"><span data-stu-id="d6126-128">**Electrical Shock Hazard**</span></span> |<span data-ttu-id="d6126-129">Indicates high voltage.</span><span class="sxs-lookup"><span data-stu-id="d6126-129">Indicates high voltage.</span></span> |
| ![Heavy weight icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Weight.png) |<span data-ttu-id="d6126-131">**Heavy Weight**</span><span class="sxs-lookup"><span data-stu-id="d6126-131">**Heavy Weight**</span></span> | |
| ![No user serviceable parts icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |<span data-ttu-id="d6126-133">**No User Serviceable Parts**</span><span class="sxs-lookup"><span data-stu-id="d6126-133">**No User Serviceable Parts**</span></span> |<span data-ttu-id="d6126-134">Do not access unless properly trained.</span><span class="sxs-lookup"><span data-stu-id="d6126-134">Do not access unless properly trained.</span></span> |
| ![Read instructions icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/ReadInstructions.png) |<span data-ttu-id="d6126-136">**Read All Instructions First**</span><span class="sxs-lookup"><span data-stu-id="d6126-136">**Read All Instructions First**</span></span> | |
| ![Tip hazard icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/TipHazard.png) |<span data-ttu-id="d6126-138">**Tip Hazard**</span><span class="sxs-lookup"><span data-stu-id="d6126-138">**Tip Hazard**</span></span> | |

### <a name="before-you-begin"></a><span data-ttu-id="d6126-139">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d6126-139">Before you begin</span></span>
<span data-ttu-id="d6126-140">Familiarize yourself with the safety information about your device and safety icons used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6126-140">Familiarize yourself with the safety information about your device and safety icons used in this tutorial.</span></span> <span data-ttu-id="d6126-141">Go to [Safely install and operate your StorSimple device](storsimple-safety.md) for complete information.</span><span class="sxs-lookup"><span data-stu-id="d6126-141">Go to [Safely install and operate your StorSimple device](storsimple-safety.md) for complete information.</span></span> <span data-ttu-id="d6126-142">Be sure to review the [Safety precautions](storsimple-safety.md#handling-precautions) before you handle your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d6126-142">Be sure to review the [Safety precautions](storsimple-safety.md#handling-precautions) before you handle your StorSimple device.</span></span> 

<span data-ttu-id="d6126-143">Before you attempt to replace a component, consider the following information.</span><span class="sxs-lookup"><span data-stu-id="d6126-143">Before you attempt to replace a component, consider the following information.</span></span>

<span data-ttu-id="d6126-144">![Warning Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Electric.png) **WARNING!**</span><span class="sxs-lookup"><span data-stu-id="d6126-144">![Warning Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Electric.png) **WARNING!**</span></span> 

* <span data-ttu-id="d6126-145">Ground yourself properly by using an electrostatic discharge or antistatic mat when handling modules and components of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="d6126-145">Ground yourself properly by using an electrostatic discharge or antistatic mat when handling modules and components of your StorSimple device.</span></span>
* <span data-ttu-id="d6126-146">Do not touch any circuitry.</span><span class="sxs-lookup"><span data-stu-id="d6126-146">Do not touch any circuitry.</span></span> <span data-ttu-id="d6126-147">Use the supplied handles and guides while handling components that may have exposed circuitry.</span><span class="sxs-lookup"><span data-stu-id="d6126-147">Use the supplied handles and guides while handling components that may have exposed circuitry.</span></span>

<span data-ttu-id="d6126-148">![Warning Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/NoticeIcon.png) **NOTICE:**</span><span class="sxs-lookup"><span data-stu-id="d6126-148">![Warning Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/NoticeIcon.png) **NOTICE:**</span></span>

<span data-ttu-id="d6126-149">When you replace a module, **NEVER leave an empty bay in the rear of the enclosure**.</span><span class="sxs-lookup"><span data-stu-id="d6126-149">When you replace a module, **NEVER leave an empty bay in the rear of the enclosure**.</span></span> <span data-ttu-id="d6126-150">Obtain a replacement or blank module before removing the problem part.</span><span class="sxs-lookup"><span data-stu-id="d6126-150">Obtain a replacement or blank module before removing the problem part.</span></span>

## <a name="hardware-component-replacement-procedures"></a><span data-ttu-id="d6126-151">Hardware component replacement procedures</span><span class="sxs-lookup"><span data-stu-id="d6126-151">Hardware component replacement procedures</span></span>
<span data-ttu-id="d6126-152">Your StorSimple 8000 series device consists of several plug-in modules in the primary and/or EBOD enclosures.</span><span class="sxs-lookup"><span data-stu-id="d6126-152">Your StorSimple 8000 series device consists of several plug-in modules in the primary and/or EBOD enclosures.</span></span> <span data-ttu-id="d6126-153">The 8100 has a single primary enclosure, whereas the 8600 is a dual enclosure device with a primary enclosure and an EBOD enclosure.</span><span class="sxs-lookup"><span data-stu-id="d6126-153">The 8100 has a single primary enclosure, whereas the 8600 is a dual enclosure device with a primary enclosure and an EBOD enclosure.</span></span>

<span data-ttu-id="d6126-154">The main hardware components in your device are summarized in the following tables.</span><span class="sxs-lookup"><span data-stu-id="d6126-154">The main hardware components in your device are summarized in the following tables.</span></span> <span data-ttu-id="d6126-155">Click the link in the **Replacement procedure** column to go to the associated tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6126-155">Click the link in the **Replacement procedure** column to go to the associated tutorial.</span></span>

| <span data-ttu-id="d6126-156">Components</span><span class="sxs-lookup"><span data-stu-id="d6126-156">Components</span></span> | <span data-ttu-id="d6126-157"># Present</span><span class="sxs-lookup"><span data-stu-id="d6126-157"># Present</span></span> | <span data-ttu-id="d6126-158">Plug-in module?</span><span class="sxs-lookup"><span data-stu-id="d6126-158">Plug-in module?</span></span> | <span data-ttu-id="d6126-159">Replacement procedure</span><span class="sxs-lookup"><span data-stu-id="d6126-159">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d6126-160">Chassis</span><span class="sxs-lookup"><span data-stu-id="d6126-160">Chassis</span></span> |<span data-ttu-id="d6126-161">1</span><span class="sxs-lookup"><span data-stu-id="d6126-161">1</span></span> |<span data-ttu-id="d6126-162">No</span><span class="sxs-lookup"><span data-stu-id="d6126-162">No</span></span> |[<span data-ttu-id="d6126-163">Replace the chassis on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-163">Replace the chassis on your StorSimple device</span></span>](storsimple-chassis-replacement.md) |
| <span data-ttu-id="d6126-164">Primary controllers</span><span class="sxs-lookup"><span data-stu-id="d6126-164">Primary controllers</span></span> |<span data-ttu-id="d6126-165">2</span><span class="sxs-lookup"><span data-stu-id="d6126-165">2</span></span> |<span data-ttu-id="d6126-166">Yes</span><span class="sxs-lookup"><span data-stu-id="d6126-166">Yes</span></span> |[<span data-ttu-id="d6126-167">Replace a controller module on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-167">Replace a controller module on your StorSimple device</span></span>](storsimple-controller-replacement.md) |
| <span data-ttu-id="d6126-168">764W Power and Cooling Modules (PCMs)</span><span class="sxs-lookup"><span data-stu-id="d6126-168">764W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="d6126-169">2</span><span class="sxs-lookup"><span data-stu-id="d6126-169">2</span></span> |<span data-ttu-id="d6126-170">Yes</span><span class="sxs-lookup"><span data-stu-id="d6126-170">Yes</span></span> |[<span data-ttu-id="d6126-171">Replace a Power and Cooling Module on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-171">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-power-cooling-module-replacement.md) |
| <span data-ttu-id="d6126-172">Backup battery</span><span class="sxs-lookup"><span data-stu-id="d6126-172">Backup battery</span></span> |<span data-ttu-id="d6126-173">2</span><span class="sxs-lookup"><span data-stu-id="d6126-173">2</span></span> |<span data-ttu-id="d6126-174">Yes</span><span class="sxs-lookup"><span data-stu-id="d6126-174">Yes</span></span> |[<span data-ttu-id="d6126-175">Replace the backup battery module on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-175">Replace the backup battery module on your StorSimple device</span></span>](storsimple-battery-replacement.md) |
| <span data-ttu-id="d6126-176">Disk drives</span><span class="sxs-lookup"><span data-stu-id="d6126-176">Disk drives</span></span> |<span data-ttu-id="d6126-177">12</span><span class="sxs-lookup"><span data-stu-id="d6126-177">12</span></span> |<span data-ttu-id="d6126-178">Yes</span><span class="sxs-lookup"><span data-stu-id="d6126-178">Yes</span></span> |[<span data-ttu-id="d6126-179">Replace a disk drive on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-179">Replace a disk drive on your StorSimple device</span></span>](storsimple-disk-drive-replacement.md) |

<span data-ttu-id="d6126-180">**Table 1** Hardware components in the primary enclosure</span><span class="sxs-lookup"><span data-stu-id="d6126-180">**Table 1** Hardware components in the primary enclosure</span></span>

<span data-ttu-id="d6126-181">The primary enclosure and the EBOD enclosure differ in their I/O modules.</span><span class="sxs-lookup"><span data-stu-id="d6126-181">The primary enclosure and the EBOD enclosure differ in their I/O modules.</span></span> <span data-ttu-id="d6126-182">Additionally, the PCMs have different wattage.</span><span class="sxs-lookup"><span data-stu-id="d6126-182">Additionally, the PCMs have different wattage.</span></span> <span data-ttu-id="d6126-183">The PCMs in the primary enclosure are 764 W, whereas those in the EBOD enclosure are 580 W. The PCMs in the primary enclosure also contain a backup battery module.</span><span class="sxs-lookup"><span data-stu-id="d6126-183">The PCMs in the primary enclosure are 764 W, whereas those in the EBOD enclosure are 580 W. The PCMs in the primary enclosure also contain a backup battery module.</span></span>

| <span data-ttu-id="d6126-184">Components</span><span class="sxs-lookup"><span data-stu-id="d6126-184">Components</span></span> | <span data-ttu-id="d6126-185"># Present</span><span class="sxs-lookup"><span data-stu-id="d6126-185"># Present</span></span> | <span data-ttu-id="d6126-186">Plug-in module?</span><span class="sxs-lookup"><span data-stu-id="d6126-186">Plug-in module?</span></span> | <span data-ttu-id="d6126-187">Replacement procedure</span><span class="sxs-lookup"><span data-stu-id="d6126-187">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d6126-188">Chassis</span><span class="sxs-lookup"><span data-stu-id="d6126-188">Chassis</span></span> |<span data-ttu-id="d6126-189">1</span><span class="sxs-lookup"><span data-stu-id="d6126-189">1</span></span> |<span data-ttu-id="d6126-190">No</span><span class="sxs-lookup"><span data-stu-id="d6126-190">No</span></span> |[<span data-ttu-id="d6126-191">Replace the chassis on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-191">Replace the chassis on your StorSimple device</span></span>](storsimple-chassis-replacement.md) |
| <span data-ttu-id="d6126-192">EBOD controllers</span><span class="sxs-lookup"><span data-stu-id="d6126-192">EBOD controllers</span></span> |<span data-ttu-id="d6126-193">2</span><span class="sxs-lookup"><span data-stu-id="d6126-193">2</span></span> |<span data-ttu-id="d6126-194">Yes</span><span class="sxs-lookup"><span data-stu-id="d6126-194">Yes</span></span> |[<span data-ttu-id="d6126-195">Replace an EBOD controller on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-195">Replace an EBOD controller on your StorSimple device</span></span>](storsimple-ebod-controller-replacement.md) |
| <span data-ttu-id="d6126-196">580W Power and Cooling Modules (PCMs)</span><span class="sxs-lookup"><span data-stu-id="d6126-196">580W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="d6126-197">2</span><span class="sxs-lookup"><span data-stu-id="d6126-197">2</span></span> |<span data-ttu-id="d6126-198">Yes</span><span class="sxs-lookup"><span data-stu-id="d6126-198">Yes</span></span> |[<span data-ttu-id="d6126-199">Replace a Power and Cooling Module on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-199">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-power-cooling-module-replacement.md) |
| <span data-ttu-id="d6126-200">Disk drives</span><span class="sxs-lookup"><span data-stu-id="d6126-200">Disk drives</span></span> |<span data-ttu-id="d6126-201">12</span><span class="sxs-lookup"><span data-stu-id="d6126-201">12</span></span> |<span data-ttu-id="d6126-202">Yes</span><span class="sxs-lookup"><span data-stu-id="d6126-202">Yes</span></span> |[<span data-ttu-id="d6126-203">Replace a disk drive on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="d6126-203">Replace a disk drive on your StorSimple device</span></span>](storsimple-disk-drive-replacement.md) |

<span data-ttu-id="d6126-204">**Table 2** Hardware components in the EBOD enclosure</span><span class="sxs-lookup"><span data-stu-id="d6126-204">**Table 2** Hardware components in the EBOD enclosure</span></span>

<span data-ttu-id="d6126-205">The plug-in modules on the device are highlighted in the following front and rear diagrams.</span><span class="sxs-lookup"><span data-stu-id="d6126-205">The plug-in modules on the device are highlighted in the following front and rear diagrams.</span></span> <span data-ttu-id="d6126-206">You can use these diagrams to determine the location of the various plug-in modules if a replacement is required.</span><span class="sxs-lookup"><span data-stu-id="d6126-206">You can use these diagrams to determine the location of the various plug-in modules if a replacement is required.</span></span> <span data-ttu-id="d6126-207">The front diagram shows the disk drives, and the rear diagrams of the EBOD enclosure and the primary enclosure show the plug-in modules.</span><span class="sxs-lookup"><span data-stu-id="d6126-207">The front diagram shows the disk drives, and the rear diagrams of the EBOD enclosure and the primary enclosure show the plug-in modules.</span></span>

![Frontplane of device with disk drives](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/IC741028.png)

<span data-ttu-id="d6126-209">**Figure 1** Front of the device</span><span class="sxs-lookup"><span data-stu-id="d6126-209">**Figure 1** Front of the device</span></span>

| <span data-ttu-id="d6126-210">Label</span><span class="sxs-lookup"><span data-stu-id="d6126-210">Label</span></span> | <span data-ttu-id="d6126-211">Description</span><span class="sxs-lookup"><span data-stu-id="d6126-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d6126-212">0 - 11</span><span class="sxs-lookup"><span data-stu-id="d6126-212">0 - 11</span></span> |<span data-ttu-id="d6126-213">Disk drives (total of 12)</span><span class="sxs-lookup"><span data-stu-id="d6126-213">Disk drives (total of 12)</span></span> |

<span data-ttu-id="d6126-214">Both the primary enclosure and the EBOD enclosure have drive carrier modules.</span><span class="sxs-lookup"><span data-stu-id="d6126-214">Both the primary enclosure and the EBOD enclosure have drive carrier modules.</span></span> <span data-ttu-id="d6126-215">The chassis houses twelve 3.5" disk drives arranged in a 3 by 4 format.</span><span class="sxs-lookup"><span data-stu-id="d6126-215">The chassis houses twelve 3.5" disk drives arranged in a 3 by 4 format.</span></span>

![Backplane of device primary enclosure modules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/IC740994.png)

<span data-ttu-id="d6126-217">**Figure 2** Back of the primary enclosure</span><span class="sxs-lookup"><span data-stu-id="d6126-217">**Figure 2** Back of the primary enclosure</span></span>

| <span data-ttu-id="d6126-218">Label</span><span class="sxs-lookup"><span data-stu-id="d6126-218">Label</span></span> | <span data-ttu-id="d6126-219">Description</span><span class="sxs-lookup"><span data-stu-id="d6126-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d6126-220">1</span><span class="sxs-lookup"><span data-stu-id="d6126-220">1</span></span> |<span data-ttu-id="d6126-221">PCM 0</span><span class="sxs-lookup"><span data-stu-id="d6126-221">PCM 0</span></span> |
| <span data-ttu-id="d6126-222">2</span><span class="sxs-lookup"><span data-stu-id="d6126-222">2</span></span> |<span data-ttu-id="d6126-223">PCM 1</span><span class="sxs-lookup"><span data-stu-id="d6126-223">PCM 1</span></span> |
| <span data-ttu-id="d6126-224">3</span><span class="sxs-lookup"><span data-stu-id="d6126-224">3</span></span> |<span data-ttu-id="d6126-225">Controller 0</span><span class="sxs-lookup"><span data-stu-id="d6126-225">Controller 0</span></span> |
| <span data-ttu-id="d6126-226">4</span><span class="sxs-lookup"><span data-stu-id="d6126-226">4</span></span> |<span data-ttu-id="d6126-227">Controller 1</span><span class="sxs-lookup"><span data-stu-id="d6126-227">Controller 1</span></span> |

![Backplane of device EBOD enclosure plug-in modules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-hardware-component-replacement/IC769599.png)

<span data-ttu-id="d6126-229">**Figure 3** Back of the EBOD enclosure</span><span class="sxs-lookup"><span data-stu-id="d6126-229">**Figure 3** Back of the EBOD enclosure</span></span>

| <span data-ttu-id="d6126-230">Label</span><span class="sxs-lookup"><span data-stu-id="d6126-230">Label</span></span> | <span data-ttu-id="d6126-231">Description</span><span class="sxs-lookup"><span data-stu-id="d6126-231">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d6126-232">1</span><span class="sxs-lookup"><span data-stu-id="d6126-232">1</span></span> |<span data-ttu-id="d6126-233">PCM 0</span><span class="sxs-lookup"><span data-stu-id="d6126-233">PCM 0</span></span> |
| <span data-ttu-id="d6126-234">2</span><span class="sxs-lookup"><span data-stu-id="d6126-234">2</span></span> |<span data-ttu-id="d6126-235">PCM 1</span><span class="sxs-lookup"><span data-stu-id="d6126-235">PCM 1</span></span> |
| <span data-ttu-id="d6126-236">3</span><span class="sxs-lookup"><span data-stu-id="d6126-236">3</span></span> |<span data-ttu-id="d6126-237">EBOD Controller 0</span><span class="sxs-lookup"><span data-stu-id="d6126-237">EBOD Controller 0</span></span> |
| <span data-ttu-id="d6126-238">4</span><span class="sxs-lookup"><span data-stu-id="d6126-238">4</span></span> |<span data-ttu-id="d6126-239">EBOD Controller 1</span><span class="sxs-lookup"><span data-stu-id="d6126-239">EBOD Controller 1</span></span> |

## <a name="field-replaceable-units"></a><span data-ttu-id="d6126-240">Field replaceable units</span><span class="sxs-lookup"><span data-stu-id="d6126-240">Field replaceable units</span></span>
<span data-ttu-id="d6126-241">The following field replaceable units (FRUs) are available for your StorSimple device:</span><span class="sxs-lookup"><span data-stu-id="d6126-241">The following field replaceable units (FRUs) are available for your StorSimple device:</span></span>

* <span data-ttu-id="d6126-242">Chassis (including the integrated operations panel)</span><span class="sxs-lookup"><span data-stu-id="d6126-242">Chassis (including the integrated operations panel)</span></span>
* <span data-ttu-id="d6126-243">764 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="d6126-243">764 W AC PCM</span></span>
* <span data-ttu-id="d6126-244">580 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="d6126-244">580 W AC PCM</span></span>
* <span data-ttu-id="d6126-245">Hard disk drive with drive carrier module</span><span class="sxs-lookup"><span data-stu-id="d6126-245">Hard disk drive with drive carrier module</span></span>
* <span data-ttu-id="d6126-246">Controller module</span><span class="sxs-lookup"><span data-stu-id="d6126-246">Controller module</span></span>
* <span data-ttu-id="d6126-247">EBOD controller module</span><span class="sxs-lookup"><span data-stu-id="d6126-247">EBOD controller module</span></span>
* <span data-ttu-id="d6126-248">Backup battery module</span><span class="sxs-lookup"><span data-stu-id="d6126-248">Backup battery module</span></span>
* <span data-ttu-id="d6126-249">Rack mounting rail kit</span><span class="sxs-lookup"><span data-stu-id="d6126-249">Rack mounting rail kit</span></span>

<span data-ttu-id="d6126-250">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) to order any of these replacement units.</span><span class="sxs-lookup"><span data-stu-id="d6126-250">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) to order any of these replacement units.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6126-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6126-251">Next steps</span></span>
<span data-ttu-id="d6126-252">Review all [safety information](storsimple-safety.md) before you attempt to replace a StorSimple hardware component.</span><span class="sxs-lookup"><span data-stu-id="d6126-252">Review all [safety information](storsimple-safety.md) before you attempt to replace a StorSimple hardware component.</span></span>

















