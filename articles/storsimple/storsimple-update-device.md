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
# <a name="update-your-storsimple-8000-series-device"></a>Update your StorSimple 8000 Series device
## <a name="overview"></a>Overview
The StorSimple updates features allow you to easily keep your StorSimple device up-to-date. Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface. This tutorial describes the update types and how to install each of them.

You can apply two types of device updates: 

* Regular (or Normal mode) updates
* Maintenance mode updates

You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates. 

Each update type is described separately, below.

### <a name="regular-updates"></a>Regular updates
Regular updates are non-disruptive updates that can be installed when the device is in Normal mode. These updates are applied through the Microsoft Update website to each device controller. 

> [!IMPORTANT]
> A controller failover may occur during the update process. However, this will not affect system availability or operation.
> 
> 

* For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).
* You can also install regular updates via Windows PowerShell for StorSimple. For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Maintenance mode updates
Maintenance Mode updates are disruptive updates such as disk firmware upgrades. These updates require the device to be put into Maintenance mode. For details, see [Step 2: Enter Maintenance mode](#step2). You cannot use the Azure classic portal to install Maintenance mode updates. Instead, you must use Windows PowerShell for StorSimple. 

For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Maintenance mode updates must be applied separately to each controller. 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a>Install regular updates via the Azure classic portal
You can use the Azure classic portal to apply updates to your StorSimple device.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Install regular updates via Windows PowerShell for StorSimple
Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.

> [!IMPORTANT]
> Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal. Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal. These pre-checks will preempt failures and ensure a smoother experience. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Install Maintenance mode updates via Windows PowerShell for StorSimple
You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device. All I/O requests are paused in this mode. Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped. Both controllers are rebooted when you enter or exit this mode. When you exit this mode, all the services will resume and should be healthy. (This may take a few minutes.)

If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed. This alert will include instructions for using Windows PowerShell for StorSimple to install the updates. After you update your device, use the same procedure to change the device to Regular mode. For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).

> [!IMPORTANT]
> * Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal. If the controller is not healthy, contact Microsoft Support for the next steps. For more information, go to Contact Microsoft Support. 
> * When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a>Step 1: Connect to the serial console <a name="step1">
First, use an application such as PuTTY to access the serial console. The following procedure explains how to use PuTTY to connect to the serial console.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Step 2: Enter Maintenance mode <a name="step2">
After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Step 3: Install your updates <a name="step3">
Next, install your updates.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Step 4: Exit Maintenance mode <a name="step4">
Finally, exit Maintenance mode.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Install hotfixes via Windows PowerShell for StorSimple
Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder. As with updates, there are two types of hotfixes: 

* Regular hotfixes 
* Maintenance mode hotfixes  

The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a>What happens to updates if you perform a factory reset of the device?
If a device is reset to factory settings, then all the updates are lost. After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple. For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Next steps
* Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).
* Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).

