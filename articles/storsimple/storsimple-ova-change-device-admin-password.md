---
title: Change the StorSimple virtual device admin password | Microsoft Docs
description: Describes how to use either the Azure classic portal or the StorSimple Virtual Array web UI to change the device administrator password.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 52acde45-ae29-4edb-9377-46918ab7eef8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 6a6233332786f9dc03bf8482f459a96fb1b1f0e4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670479"
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password"></a>Change the StorSimple Virtual Array device administrator password
## <a name="overview"></a>Overview
When you use the Windows PowerShell interface to access the StorSimple virtual device, you are required to enter a device administrator password. When the StorSimple device is first provisioned and started, the default password is *Password1*. For the security of your data, the default password expires the first time that you sign in and you are required to change this password.

You can also use either the local web UI or the Azure classic portal to change the device administrator password at any time after the device is deployed in  your production environment. Each of these procedures is described in this article.

## <a name="use-the-azure-classic-portal-to-change-the-password"></a>Use the Azure classic portal to change the password
Perform the following steps to change the device administrator password through the Azure classic portal.

#### <a name="to-change-the-device-administrator-password-via-the-azure-classic-portal"></a>To change the device administrator password via the Azure classic portal
1. In the portal, click **Devices** > **Configuration** for your device.
2. Scroll down to the **Device Administrator Password** section. Provide an administrator password that contains from 8 to 15 characters. The password must be a combination of uppercase, lowercase, numeric, and special characters.
3. Confirm the password.
4. Click **Save** at the bottom of the page.

The device administrator password should now be updated. You can use this modified password to access the device locally.

## <a name="use-the-storsimple-virtual-array-web-ui-to-change-the-password"></a>Use the StorSimple Virtual Array web UI to change the password
Perform the following steps to change the device administrator password through the local web UI.

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a>To change the device administrator password via the local web UI
1. In the local web UI, click **Maintenance** > **Password change** for your device.
   
    ![change password1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-change-device-admin-password/image40.png)
2. Enter the **Current password**.
3. Provide a **New Password**. The password must be at least 8 characters long. It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.
   
    Note that your password cannot be the same as the last 24 passwords.
4. Reenter the password to confirm it.
   
    ![change password2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-change-device-admin-password/image41.png)
5. At the bottom of the page, click **Apply**. The new password will then be applied. If the password change is not successful, you will see the following error.
   
    ![password error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-change-device-admin-password/image42.png)
   
    After the password is successfully updated, you will be notified. You can then use this modified password to access the device locally.

## <a name="next-steps"></a>Next steps
Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).




