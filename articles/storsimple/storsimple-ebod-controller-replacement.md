---
title: Replace a StorSimple EBOD controller | Microsoft Docs
description: Explains how to remove and replace one or both EBOD controllers on a StorSimple 8600 device.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 92f17010ac0a3fb2eebfb8256736bed4c5353646
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552727"
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="36c0c-103">Replace an EBOD controller on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="36c0c-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="36c0c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="36c0c-104">Overview</span></span>
<span data-ttu-id="36c0c-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="36c0c-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="36c0c-106">To replace an EBOD controller module, you need to:</span><span class="sxs-lookup"><span data-stu-id="36c0c-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="36c0c-107">Remove the faulty EBOD controller</span><span class="sxs-lookup"><span data-stu-id="36c0c-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="36c0c-108">Install a new EBOD controller</span><span class="sxs-lookup"><span data-stu-id="36c0c-108">Install a new EBOD controller</span></span>

<span data-ttu-id="36c0c-109">Consider the following information before you begin:</span><span class="sxs-lookup"><span data-stu-id="36c0c-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="36c0c-110">Blank EBOD modules must be inserted into all unused slots.</span><span class="sxs-lookup"><span data-stu-id="36c0c-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="36c0c-111">The enclosure will not cool properly if a slot is left open.</span><span class="sxs-lookup"><span data-stu-id="36c0c-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="36c0c-112">The EBOD controller is hot-swappable and can be removed or replaced.</span><span class="sxs-lookup"><span data-stu-id="36c0c-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="36c0c-113">Do not remove a failed module until you have a replacement.</span><span class="sxs-lookup"><span data-stu-id="36c0c-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="36c0c-114">When you initiate the replacement process, you must finish it within 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="36c0c-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36c0c-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="36c0c-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="36c0c-116">Remove an EBOD controller</span><span class="sxs-lookup"><span data-stu-id="36c0c-116">Remove an EBOD controller</span></span>
<span data-ttu-id="36c0c-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span><span class="sxs-lookup"><span data-stu-id="36c0c-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="36c0c-118">The following procedure and table explain how to remove the EBOD controller module.</span><span class="sxs-lookup"><span data-stu-id="36c0c-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="36c0c-119">To remove an EBOD module</span><span class="sxs-lookup"><span data-stu-id="36c0c-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="36c0c-120">Open the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="36c0c-120">Open the Azure classic portal.</span></span>
2. <span data-ttu-id="36c0c-121">Navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span><span class="sxs-lookup"><span data-stu-id="36c0c-121">Navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="36c0c-122">Locate the failed EBOD controller module at the back of the device.</span><span class="sxs-lookup"><span data-stu-id="36c0c-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="36c0c-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span><span class="sxs-lookup"><span data-stu-id="36c0c-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="36c0c-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span><span class="sxs-lookup"><span data-stu-id="36c0c-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="36c0c-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span><span class="sxs-lookup"><span data-stu-id="36c0c-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="36c0c-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="36c0c-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   > 
   > 
   
    ![Backplane of EBOD controller](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="36c0c-128">**Figure 1** Back of EBOD module</span><span class="sxs-lookup"><span data-stu-id="36c0c-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="36c0c-129">Label</span><span class="sxs-lookup"><span data-stu-id="36c0c-129">Label</span></span> | <span data-ttu-id="36c0c-130">Description</span><span class="sxs-lookup"><span data-stu-id="36c0c-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="36c0c-131">1</span><span class="sxs-lookup"><span data-stu-id="36c0c-131">1</span></span> |<span data-ttu-id="36c0c-132">Fault LED</span><span class="sxs-lookup"><span data-stu-id="36c0c-132">Fault LED</span></span> |
   | <span data-ttu-id="36c0c-133">2</span><span class="sxs-lookup"><span data-stu-id="36c0c-133">2</span></span> |<span data-ttu-id="36c0c-134">Power LED</span><span class="sxs-lookup"><span data-stu-id="36c0c-134">Power LED</span></span> |
   | <span data-ttu-id="36c0c-135">3</span><span class="sxs-lookup"><span data-stu-id="36c0c-135">3</span></span> |<span data-ttu-id="36c0c-136">SAS connectors</span><span class="sxs-lookup"><span data-stu-id="36c0c-136">SAS connectors</span></span> |
   | <span data-ttu-id="36c0c-137">4</span><span class="sxs-lookup"><span data-stu-id="36c0c-137">4</span></span> |<span data-ttu-id="36c0c-138">SAS LEDs</span><span class="sxs-lookup"><span data-stu-id="36c0c-138">SAS LEDs</span></span> |
   | <span data-ttu-id="36c0c-139">5</span><span class="sxs-lookup"><span data-stu-id="36c0c-139">5</span></span> |<span data-ttu-id="36c0c-140">Serial ports for factory use only</span><span class="sxs-lookup"><span data-stu-id="36c0c-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="36c0c-141">6</span><span class="sxs-lookup"><span data-stu-id="36c0c-141">6</span></span> |<span data-ttu-id="36c0c-142">Port A (Host in)</span><span class="sxs-lookup"><span data-stu-id="36c0c-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="36c0c-143">7</span><span class="sxs-lookup"><span data-stu-id="36c0c-143">7</span></span> |<span data-ttu-id="36c0c-144">Port B (Host out)</span><span class="sxs-lookup"><span data-stu-id="36c0c-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="36c0c-145">8</span><span class="sxs-lookup"><span data-stu-id="36c0c-145">8</span></span> |<span data-ttu-id="36c0c-146">Port C (Factory use only)</span><span class="sxs-lookup"><span data-stu-id="36c0c-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="36c0c-147">Install a new EBOD controller</span><span class="sxs-lookup"><span data-stu-id="36c0c-147">Install a new EBOD controller</span></span>
<span data-ttu-id="36c0c-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="36c0c-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="36c0c-149">To install an EBOD controller</span><span class="sxs-lookup"><span data-stu-id="36c0c-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="36c0c-150">Check the EBOD device for damage, especially to the interface connector.</span><span class="sxs-lookup"><span data-stu-id="36c0c-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="36c0c-151">Do not install the new EBOD controller if any pins are bent.</span><span class="sxs-lookup"><span data-stu-id="36c0c-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="36c0c-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span><span class="sxs-lookup"><span data-stu-id="36c0c-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![Installing EBOD controller](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="36c0c-154">**Figure 2**  Installing the EBOD controller module</span><span class="sxs-lookup"><span data-stu-id="36c0c-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="36c0c-155">Close the latch.</span><span class="sxs-lookup"><span data-stu-id="36c0c-155">Close the latch.</span></span> <span data-ttu-id="36c0c-156">You should hear a click as the latch engages.</span><span class="sxs-lookup"><span data-stu-id="36c0c-156">You should hear a click as the latch engages.</span></span>
   
    ![Releasing EBOD latch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="36c0c-158">**Figure 3**  Closing the EBOD module latch</span><span class="sxs-lookup"><span data-stu-id="36c0c-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="36c0c-159">Reconnect the cables.</span><span class="sxs-lookup"><span data-stu-id="36c0c-159">Reconnect the cables.</span></span> <span data-ttu-id="36c0c-160">Use the exact configuration that was present before the replacement.</span><span class="sxs-lookup"><span data-stu-id="36c0c-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="36c0c-161">See the following diagram and table for details about how to connect the cables.</span><span class="sxs-lookup"><span data-stu-id="36c0c-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![Cable your 4U device for power](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="36c0c-163">**Figure 4**.</span><span class="sxs-lookup"><span data-stu-id="36c0c-163">**Figure 4**.</span></span> <span data-ttu-id="36c0c-164">Reconnecting cables</span><span class="sxs-lookup"><span data-stu-id="36c0c-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="36c0c-165">Label</span><span class="sxs-lookup"><span data-stu-id="36c0c-165">Label</span></span> | <span data-ttu-id="36c0c-166">Description</span><span class="sxs-lookup"><span data-stu-id="36c0c-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="36c0c-167">1</span><span class="sxs-lookup"><span data-stu-id="36c0c-167">1</span></span> |<span data-ttu-id="36c0c-168">Primary enclosure</span><span class="sxs-lookup"><span data-stu-id="36c0c-168">Primary enclosure</span></span> |
   | <span data-ttu-id="36c0c-169">2</span><span class="sxs-lookup"><span data-stu-id="36c0c-169">2</span></span> |<span data-ttu-id="36c0c-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="36c0c-170">PCM 0</span></span> |
   | <span data-ttu-id="36c0c-171">3</span><span class="sxs-lookup"><span data-stu-id="36c0c-171">3</span></span> |<span data-ttu-id="36c0c-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="36c0c-172">PCM 1</span></span> |
   | <span data-ttu-id="36c0c-173">4</span><span class="sxs-lookup"><span data-stu-id="36c0c-173">4</span></span> |<span data-ttu-id="36c0c-174">Controller 0</span><span class="sxs-lookup"><span data-stu-id="36c0c-174">Controller 0</span></span> |
   | <span data-ttu-id="36c0c-175">5</span><span class="sxs-lookup"><span data-stu-id="36c0c-175">5</span></span> |<span data-ttu-id="36c0c-176">Controller 1</span><span class="sxs-lookup"><span data-stu-id="36c0c-176">Controller 1</span></span> |
   | <span data-ttu-id="36c0c-177">6</span><span class="sxs-lookup"><span data-stu-id="36c0c-177">6</span></span> |<span data-ttu-id="36c0c-178">EBOD controller 0</span><span class="sxs-lookup"><span data-stu-id="36c0c-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="36c0c-179">7</span><span class="sxs-lookup"><span data-stu-id="36c0c-179">7</span></span> |<span data-ttu-id="36c0c-180">EBOD controller 1</span><span class="sxs-lookup"><span data-stu-id="36c0c-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="36c0c-181">8</span><span class="sxs-lookup"><span data-stu-id="36c0c-181">8</span></span> |<span data-ttu-id="36c0c-182">EBOD enclosure</span><span class="sxs-lookup"><span data-stu-id="36c0c-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="36c0c-183">9</span><span class="sxs-lookup"><span data-stu-id="36c0c-183">9</span></span> |<span data-ttu-id="36c0c-184">Power Distribution Units</span><span class="sxs-lookup"><span data-stu-id="36c0c-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36c0c-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="36c0c-185">Next steps</span></span>
<span data-ttu-id="36c0c-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="36c0c-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>





