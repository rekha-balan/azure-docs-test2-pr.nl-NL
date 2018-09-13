---
title: Change the StorSimple device mode | Microsoft Docs
description: Describes the StorSimple device modes and explains how to use Windows PowerShell for StorSimple to change the device mode.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 33c65bf2eecff3914f3227c76f7d638a4507e1f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548807"
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="b4412-103">Change the device mode on your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="b4412-103">Change the device mode on your StorSimple device</span></span>
<span data-ttu-id="b4412-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span><span class="sxs-lookup"><span data-stu-id="b4412-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="b4412-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span><span class="sxs-lookup"><span data-stu-id="b4412-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="b4412-106">After reading this article, you will know:</span><span class="sxs-lookup"><span data-stu-id="b4412-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="b4412-107">What the StorSimple device modes are</span><span class="sxs-lookup"><span data-stu-id="b4412-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="b4412-108">How to figure out which mode the StorSimple device is in</span><span class="sxs-lookup"><span data-stu-id="b4412-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="b4412-109">How to change from normal to maintenance mode and *vice versa*</span><span class="sxs-lookup"><span data-stu-id="b4412-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="b4412-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="b4412-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="b4412-111">About StorSimple device modes</span><span class="sxs-lookup"><span data-stu-id="b4412-111">About StorSimple device modes</span></span>
<span data-ttu-id="b4412-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="b4412-113">Each of these modes is briefly described below.</span><span class="sxs-lookup"><span data-stu-id="b4412-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="b4412-114">Normal mode</span><span class="sxs-lookup"><span data-stu-id="b4412-114">Normal mode</span></span>
<span data-ttu-id="b4412-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="b4412-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="b4412-116">By default, your device should be in normal mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="b4412-117">Maintenance mode</span><span class="sxs-lookup"><span data-stu-id="b4412-117">Maintenance mode</span></span>
<span data-ttu-id="b4412-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="b4412-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span><span class="sxs-lookup"><span data-stu-id="b4412-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="b4412-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b4412-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b4412-121">All I/O requests are paused in this mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="b4412-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span><span class="sxs-lookup"><span data-stu-id="b4412-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="b4412-123">Both the controllers are restarted when you enter or exit this mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="b4412-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span><span class="sxs-lookup"><span data-stu-id="b4412-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="b4412-125">This may take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="b4412-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="b4412-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**</span><span class="sxs-lookup"><span data-stu-id="b4412-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**</span></span>
> </br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="b4412-127">Recovery mode</span><span class="sxs-lookup"><span data-stu-id="b4412-127">Recovery mode</span></span>
<span data-ttu-id="b4412-128">Recovery mode can be described as "Windows Safe Mode with network support".</span><span class="sxs-lookup"><span data-stu-id="b4412-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="b4412-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span><span class="sxs-lookup"><span data-stu-id="b4412-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="b4412-130">The primary goal of recovery mode is to retrieve the system logs.</span><span class="sxs-lookup"><span data-stu-id="b4412-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="b4412-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span><span class="sxs-lookup"><span data-stu-id="b4412-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="b4412-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b4412-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b4412-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span><span class="sxs-lookup"><span data-stu-id="b4412-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="b4412-134">Determine StorSimple device mode</span><span class="sxs-lookup"><span data-stu-id="b4412-134">Determine StorSimple device mode</span></span>
#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="b4412-135">To determine the current device mode</span><span class="sxs-lookup"><span data-stu-id="b4412-135">To determine the current device mode</span></span>
1. <span data-ttu-id="b4412-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b4412-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="b4412-137">Look at the banner message in the serial console menu of the device.</span><span class="sxs-lookup"><span data-stu-id="b4412-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="b4412-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="b4412-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="b4412-140">Change the StorSimple device mode</span><span class="sxs-lookup"><span data-stu-id="b4412-140">Change the StorSimple device mode</span></span>
<span data-ttu-id="b4412-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span><span class="sxs-lookup"><span data-stu-id="b4412-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="b4412-142">Perform the following procedures to enter or exit maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4412-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="b4412-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="b4412-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span><span class="sxs-lookup"><span data-stu-id="b4412-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="b4412-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b4412-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="b4412-146">To enter maintenance mode</span><span class="sxs-lookup"><span data-stu-id="b4412-146">To enter maintenance mode</span></span>
1. <span data-ttu-id="b4412-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b4412-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="b4412-148">In the serial console menu, choose option 1, **Log in with full access**.</span><span class="sxs-lookup"><span data-stu-id="b4412-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="b4412-149">When prompted, provide the **device administrator password**.</span><span class="sxs-lookup"><span data-stu-id="b4412-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="b4412-150">The default password is: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="b4412-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="b4412-151">At the command prompt, type</span><span class="sxs-lookup"><span data-stu-id="b4412-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="b4412-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="b4412-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="b4412-153">Type **Y** to enter maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="b4412-154">Both controllers will restart.</span><span class="sxs-lookup"><span data-stu-id="b4412-154">Both controllers will restart.</span></span> <span data-ttu-id="b4412-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span></span>

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="b4412-156">To exit maintenance mode</span><span class="sxs-lookup"><span data-stu-id="b4412-156">To exit maintenance mode</span></span>
1. <span data-ttu-id="b4412-157">Log on to the device serial console.</span><span class="sxs-lookup"><span data-stu-id="b4412-157">Log on to the device serial console.</span></span> <span data-ttu-id="b4412-158">Verify from the banner message that your device is in maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-158">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="b4412-159">At the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="b4412-159">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="b4412-160">A warning message and a confirmation message will appear.</span><span class="sxs-lookup"><span data-stu-id="b4412-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="b4412-161">Type **Y** to exit maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-161">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="b4412-162">Both controllers will restart.</span><span class="sxs-lookup"><span data-stu-id="b4412-162">Both controllers will restart.</span></span> <span data-ttu-id="b4412-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span><span class="sxs-lookup"><span data-stu-id="b4412-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4412-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4412-164">Next steps</span></span>
<span data-ttu-id="b4412-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="b4412-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

