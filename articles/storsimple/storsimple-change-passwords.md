---
title: Change passwords via StorSimple Device Manager | Microsoft Docs
description: Describes how to use the StorSimple Manager service to change your StorSimple Snapshot Manager and device administrator passwords.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d890b59595628ca3eeff1df258847c2bb54d29ff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549230"
---
# <a name="use-the-storsimple-manager-service-to-change-your-storsimple-passwords"></a>Use the StorSimple Manager service to change your StorSimple passwords
## <a name="overview"></a>Overview
The Azure classic portal **Configure** page contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Manager service. This tutorial explains how you can use the **Configure** page to change your device administrator or StorSimple Snapshot Manager password.

## <a name="change-the-device-administrator-password"></a>Change the device administrator password
When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password. When the first StorSimple device is registered with a service, the default password for this interface is *Password1*. For the security of your data, you are required to change this password at the end of the registration process. You cannot exit from the registration process without changing this password. For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

The password that was first set through the Windows PowerShell interface during registration can then be changed via the Azure classic portal. Perform the following steps to change the device administrator password.

#### <a name="to-change-the-device-administrator-password"></a>To change the device administrator password
1. In the classic portal, click **Devices** > **Configure** for your device.
2. Scroll down to the **Device Administrator Password** section. Provide an administrator password that contains from 8 to 15 characters. The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.
3. Confirm the password.
4. Click **Save** at the bottom of the page.

The device administrator password should now be updated. You can use this modified password to access the Windows PowerShell interface.

## <a name="change-the-storsimple-snapshot-manager-password"></a>Change the StorSimple Snapshot Manager password
StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.

When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device. This password is first configured through the Windows PowerShell interface. For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

The password that was first set through the Windows PowerShell interface during registration can then be changed via the classic portal. Perform the following steps to change the StorSimple Snapshot Manager password.

#### <a name="to-change-the-storsimple-snapshot-manager-password"></a>To change the StorSimple Snapshot Manager password
1. In the classic portal, click **Devices** > **Configure** for your device.
2. Scroll down to the **StorSimple Snapshot Manager** section. Enter a password that is 14 or 15 characters. Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.
3. Confirm the password.
4. Click **Save** at the bottom of the page.

The StorSimple Snapshot Manager password should now be updated.

## <a name="next-steps"></a>Next steps
* Learn more about [StorSimple security](storsimple-security.md).
* Learn more about [modifying your device configuration](storsimple-modify-device-config.md).
* Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).

