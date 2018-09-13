---
title: Deactivate and delete a StorSimple Virtual Array | Microsoft Docs
description: Describes how to remove StorSimple device from service by  first deactivating it and then deleting it.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: bf5ddb32-da4b-446f-ab91-215e9020e1c8
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7afc6ff986bfa0e28c2f00c5e4e2e5ee3ba92cd3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550984"
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array-via-storsimple-manager"></a>Deactivate and delete a StorSimple Virtual Array via StorSimple Manager
## <a name="overview"></a>Overview
When you deactivate a StorSimple Virtual Array, you sever the connection between the device and the corresponding StorSimple Manager service. Deactivation is a PERMANENT operation and cannot be undone. A deactivated device cannot be registered with the StorSimple Manager service again.

You may need to deactivate and delete a StorSimple virtual device in the following scenarios:

* Your device is online and you plan to fail over this device. You may need to do this if you are planning  to upgrade to a larger device. After the device data is transferred and the failover is complete, you can then delete the device.
* Your device is offline and you plan to fail over this device. This may happen in the event of a disaster where due to an outage in the datacenter, your primary device is down. You plan to fail over the device to a secondary device. After the device data is transferred and the failover is complete, you can delete the device.
* You want to decommission the device and then delete it. 

When you deactivate a device, any data that was stored locally will no longer be accessible. Only the data stored in the cloud can be recovered. If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device. This will allow you to recover all the data at a later stage.

This tutorial explains how to:

* Deactivate a device 
* Delete a deactivated device

## <a name="deactivate-a-device"></a>Deactivate a device
Perform the following steps to deactivate your device.

#### <a name="to-deactivate-the-device"></a>To deactivate the device
1. Go to **Devices** page. Select the device that you wish to deactivate.
   
    ![Select device to deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate1m.png)
2. At the bottom of the page, click **Deactivate**.
   
    ![Click deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate2m.png)
3. A confirmation message will appear. Click **Yes** to continue. 
   
    ![Confirm deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate3m.png)
   
    The deactivate process will start and take a few minutes to complete.
   
    ![Deactivate in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate4m.png)
4. After deactivation, the list of the devices will be refreshed. 
   
    ![Deactivate complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate5m.png)
   
    You can now delete this device. 

## <a name="delete-the-device"></a>Delete the device
A device has to be first deactivated in order to delete it. Deleting a device removes it from the list of devices connected to the service. The service can then no longer manage the deleted device. The data associated with the device will however remain in the cloud. Be aware that this data will then accrue charges. 

Complete the following steps to delete the device:

#### <a name="to-delete-the-device"></a>To delete the device
1. On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.
   
   ![Select device to delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate5m.png)
2. On the bottom on the page, click **Delete**.
   
   ![Click delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate6m.png)
3. You will be prompted for confirmation. Type the device name to confirm device deletion. Note that deleting the device will not delete the cloud data associated with the device. Click the check icon to continue.
   
   ![Confirm delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate7m.png) 
4. It may take a few minutes for the device to be deleted. 
   
   ![Delete in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate8m.png)
   
    After the device is deleted, the list of devices will be refreshed.
   
   ![Delete complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate9m.png)

## <a name="next-steps"></a>Next steps
* To learn more about how to use the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple Virtual Array](storsimple-ova-manager-service-administration.md). 











