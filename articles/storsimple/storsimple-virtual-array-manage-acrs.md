---
title: Manage access control records for StorSimple Virtual Array | Microsoft Docs
description: Describes how to manage access control records (ACRs) to determine which hosts can connect to a volume on the StorSimple Virtual Array.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2ce65aa4efba735305208f7a6d761bc2814d1b8f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44780512"
---
# <a name="use-storsimple-device-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a>Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array

## <a name="overview"></a>Overview

Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device). ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts. When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established. The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.

![Manage access control records](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

This tutorial explains the following common ACR-related tasks:

* Get the IQN
* Add an access control record
* Edit an access control record
* Delete an access control record

> [!IMPORTANT]
> 
> * When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.
> * When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.


## <a name="get-the-iqn"></a>Get the IQN

Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Add an ACR

You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs. Typically, you associate one ACR with one volume.

For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.


Perform the following steps to add an ACR.

#### <a name="to-add-an-acr"></a>To add an ACR

1. On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.
2. In the **Access control records** blade, click **Add**.
3. In the **Add ACR** blade, do the following:
   
    1. Supply a **Name** for your ACR.
    
    2. Under **iSCSI Initiator Name**, provide the IQN name of your Windows host. To get the IQN of your Windows Server host, do the following:
   
    3. Start the Microsoft iSCSI initiator on your Windows host. In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.
    Paste this string in the **IQN** field in the **Add ACR** blade.
   
    6. Click **Add** to add the ACR.  
   
        ![Add access control records](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. The tabular listing is updated to reflect this addition.

## <a name="edit-an-acr"></a>Edit an ACR

You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.

> [!NOTE]
> You should not modify an ACR that is currently in use. To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.


Perform the following steps to edit an ACR.

#### <a name="to-edit-an-acr"></a>To edit an ACR

1. On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.
2. In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.
3. In the **Edit access control records** blade, do the following:
   
    1. Supply the IQN for the ACR.
   
    2. Click **Save** at the top of the blade to save the modified ACR. You see the following confirmation message:
   
        ![Edit access control records](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>Delete an access control record

You use the **Configuration** page in the Azure portal to delete ACRs.

> [!NOTE]
> 
> * You should not delete an ACR that is currently in use. To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.
> * When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.


Perform the following steps to delete an access control record.

#### <a name="to-delete-an-access-control-record"></a>To delete an access control record

1. On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.

2. In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.

3. In the Edit access control records blade, click **Delete**.
   
    ![Delete ACRS](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. When prompted for confirmation, click **Delete** to continue with the deletion. The tabular listing is updated to reflect the deletion.
   
   ![Warning message](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>Next steps

* Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

