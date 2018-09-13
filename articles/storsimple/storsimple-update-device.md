---
title: Update your StorSimple device | Microsoft Docs
description: Explains how to use the StorSimple update feature to install regular and maintenance mode updates and hotfixes.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: ''
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 8490110942741b049b6d44ac93697303cef40e8a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564033"
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="f0e60-103">Update your StorSimple 8000 Series device</span><span class="sxs-lookup"><span data-stu-id="f0e60-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="f0e60-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f0e60-104">Overview</span></span>
<span data-ttu-id="f0e60-105">The StorSimple updates features allow you to easily keep your StorSimple device up-to-date.</span><span class="sxs-lookup"><span data-stu-id="f0e60-105">The StorSimple updates features allow you to easily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="f0e60-106">Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface.</span><span class="sxs-lookup"><span data-stu-id="f0e60-106">Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface.</span></span> <span data-ttu-id="f0e60-107">This tutorial describes the update types and how to install each of them.</span><span class="sxs-lookup"><span data-stu-id="f0e60-107">This tutorial describes the update types and how to install each of them.</span></span>

<span data-ttu-id="f0e60-108">You can apply two types of device updates:</span><span class="sxs-lookup"><span data-stu-id="f0e60-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="f0e60-109">Regular (or Normal mode) updates</span><span class="sxs-lookup"><span data-stu-id="f0e60-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="f0e60-110">Maintenance mode updates</span><span class="sxs-lookup"><span data-stu-id="f0e60-110">Maintenance mode updates</span></span>

<span data-ttu-id="f0e60-111">You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates.</span><span class="sxs-lookup"><span data-stu-id="f0e60-111">You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates.</span></span> 

<span data-ttu-id="f0e60-112">Each update type is described separately, below.</span><span class="sxs-lookup"><span data-stu-id="f0e60-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="f0e60-113">Regular updates</span><span class="sxs-lookup"><span data-stu-id="f0e60-113">Regular updates</span></span>
<span data-ttu-id="f0e60-114">Regular updates are non-disruptive updates that can be installed when the device is in Normal mode.</span><span class="sxs-lookup"><span data-stu-id="f0e60-114">Regular updates are non-disruptive updates that can be installed when the device is in Normal mode.</span></span> <span data-ttu-id="f0e60-115">These updates are applied through the Microsoft Update website to each device controller.</span><span class="sxs-lookup"><span data-stu-id="f0e60-115">These updates are applied through the Microsoft Update website to each device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f0e60-116">A controller failover may occur during the update process.</span><span class="sxs-lookup"><span data-stu-id="f0e60-116">A controller failover may occur during the update process.</span></span> <span data-ttu-id="f0e60-117">However, this will not affect system availability or operation.</span><span class="sxs-lookup"><span data-stu-id="f0e60-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="f0e60-118">For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="f0e60-118">For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="f0e60-119">You can also install regular updates via Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f0e60-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="f0e60-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="f0e60-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="f0e60-121">Maintenance mode updates</span><span class="sxs-lookup"><span data-stu-id="f0e60-121">Maintenance mode updates</span></span>
<span data-ttu-id="f0e60-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span><span class="sxs-lookup"><span data-stu-id="f0e60-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="f0e60-123">These updates require the device to be put into Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="f0e60-123">These updates require the device to be put into Maintenance mode.</span></span> <span data-ttu-id="f0e60-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span><span class="sxs-lookup"><span data-stu-id="f0e60-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="f0e60-125">You cannot use the Azure classic portal to install Maintenance mode updates.</span><span class="sxs-lookup"><span data-stu-id="f0e60-125">You cannot use the Azure classic portal to install Maintenance mode updates.</span></span> <span data-ttu-id="f0e60-126">Instead, you must use Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f0e60-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="f0e60-127">For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="f0e60-127">For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0e60-128">Maintenance mode updates must be applied separately to each controller.</span><span class="sxs-lookup"><span data-stu-id="f0e60-128">Maintenance mode updates must be applied separately to each controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a><span data-ttu-id="f0e60-129">Install regular updates via the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="f0e60-129">Install regular updates via the Azure classic portal</span></span>
<span data-ttu-id="f0e60-130">You can use the Azure classic portal to apply updates to your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="f0e60-130">You can use the Azure classic portal to apply updates to your StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="f0e60-131">Install regular updates via Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="f0e60-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="f0e60-132">Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.</span><span class="sxs-lookup"><span data-stu-id="f0e60-132">Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0e60-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="f0e60-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal.</span></span> <span data-ttu-id="f0e60-134">Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal.</span><span class="sxs-lookup"><span data-stu-id="f0e60-134">Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal.</span></span> <span data-ttu-id="f0e60-135">These pre-checks will preempt failures and ensure a smoother experience.</span><span class="sxs-lookup"><span data-stu-id="f0e60-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="f0e60-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="f0e60-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="f0e60-137">You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="f0e60-137">You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device.</span></span> <span data-ttu-id="f0e60-138">All I/O requests are paused in this mode.</span><span class="sxs-lookup"><span data-stu-id="f0e60-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="f0e60-139">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span><span class="sxs-lookup"><span data-stu-id="f0e60-139">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="f0e60-140">Both controllers are rebooted when you enter or exit this mode.</span><span class="sxs-lookup"><span data-stu-id="f0e60-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="f0e60-141">When you exit this mode, all the services will resume and should be healthy.</span><span class="sxs-lookup"><span data-stu-id="f0e60-141">When you exit this mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="f0e60-142">(This may take a few minutes.)</span><span class="sxs-lookup"><span data-stu-id="f0e60-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="f0e60-143">If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed.</span><span class="sxs-lookup"><span data-stu-id="f0e60-143">If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="f0e60-144">This alert will include instructions for using Windows PowerShell for StorSimple to install the updates.</span><span class="sxs-lookup"><span data-stu-id="f0e60-144">This alert will include instructions for using Windows PowerShell for StorSimple to install the updates.</span></span> <span data-ttu-id="f0e60-145">After you update your device, use the same procedure to change the device to Regular mode.</span><span class="sxs-lookup"><span data-stu-id="f0e60-145">After you update your device, use the same procedure to change the device to Regular mode.</span></span> <span data-ttu-id="f0e60-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span><span class="sxs-lookup"><span data-stu-id="f0e60-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f0e60-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="f0e60-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="f0e60-148">If the controller is not healthy, contact Microsoft Support for the next steps.</span><span class="sxs-lookup"><span data-stu-id="f0e60-148">If the controller is not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="f0e60-149">For more information, go to Contact Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="f0e60-149">For more information, go to Contact Microsoft Support.</span></span> 
> * <span data-ttu-id="f0e60-150">When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.</span><span class="sxs-lookup"><span data-stu-id="f0e60-150">When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.</span></span>
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a><span data-ttu-id="f0e60-151">Step 1: Connect to the serial console <a name="step1"></span><span class="sxs-lookup"><span data-stu-id="f0e60-151">Step 1: Connect to the serial console <a name="step1"></span></span>
<span data-ttu-id="f0e60-152">First, use an application such as PuTTY to access the serial console.</span><span class="sxs-lookup"><span data-stu-id="f0e60-152">First, use an application such as PuTTY to access the serial console.</span></span> <span data-ttu-id="f0e60-153">The following procedure explains how to use PuTTY to connect to the serial console.</span><span class="sxs-lookup"><span data-stu-id="f0e60-153">The following procedure explains how to use PuTTY to connect to the serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="f0e60-154">Step 2: Enter Maintenance mode <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="f0e60-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="f0e60-155">After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.</span><span class="sxs-lookup"><span data-stu-id="f0e60-155">After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="f0e60-156">Step 3: Install your updates <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="f0e60-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="f0e60-157">Next, install your updates.</span><span class="sxs-lookup"><span data-stu-id="f0e60-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="f0e60-158">Step 4: Exit Maintenance mode <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="f0e60-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="f0e60-159">Finally, exit Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="f0e60-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="f0e60-160">Install hotfixes via Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="f0e60-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="f0e60-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span><span class="sxs-lookup"><span data-stu-id="f0e60-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="f0e60-162">As with updates, there are two types of hotfixes:</span><span class="sxs-lookup"><span data-stu-id="f0e60-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="f0e60-163">Regular hotfixes</span><span class="sxs-lookup"><span data-stu-id="f0e60-163">Regular hotfixes</span></span> 
* <span data-ttu-id="f0e60-164">Maintenance mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="f0e60-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="f0e60-165">The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.</span><span class="sxs-lookup"><span data-stu-id="f0e60-165">The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a><span data-ttu-id="f0e60-166">What happens to updates if you perform a factory reset of the device?</span><span class="sxs-lookup"><span data-stu-id="f0e60-166">What happens to updates if you perform a factory reset of the device?</span></span>
<span data-ttu-id="f0e60-167">If a device is reset to factory settings, then all the updates are lost.</span><span class="sxs-lookup"><span data-stu-id="f0e60-167">If a device is reset to factory settings, then all the updates are lost.</span></span> <span data-ttu-id="f0e60-168">After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f0e60-168">After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="f0e60-169">For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="f0e60-169">For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0e60-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="f0e60-170">Next steps</span></span>
* <span data-ttu-id="f0e60-171">Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f0e60-171">Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="f0e60-172">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f0e60-172">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

