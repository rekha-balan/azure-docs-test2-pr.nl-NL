---
title: Manage access control records for the StorSimple Virtual Array | Microsoft Docs
description: Describes how to manage access control records (ACRs) to determine which hosts can connect to a volume on the StorSimple Virtual Array.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: 11252938-5b97-4178-8c37-f58eaa3d00b1
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c660606acf028ea1cd4ac11425fc2c3c5579f1eb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553677"
---
# <a name="use-storsimple-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a>Use StorSimple Manager to manage access control records for StorSimple Virtual Array

## <a name="overview"></a>Overview
Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device). ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts. When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established. The **access control records** section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.

This tutorial explains the following common ACR-related tasks:

* Get the IQN
* Add an access control record 
* Edit an access control record 
* Delete an access control record 

> [!IMPORTANT]
> * When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume. 
> * When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.
> 
> 

## <a name="get-the-iqn"></a>Get the IQN
Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Add an ACR
You use the StorSimple Manager service **Configuration** page to add ACRs. Typically, you will associate one ACR with one volume.

For information about associating an ACR with a volume, go to [add a volume](storsimple-ova-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.
> 
> 

Perform the following steps to add an ACR.

#### <a name="to-add-an-acr"></a>To add an ACR
1. On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.
   
    ![configuration tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/acr1.png)
2. In the tabular listing under **Access control records**, supply a **Name** for your ACR.
3. Under **iSCSI Initiator Name**, provide the IQN name of your Windows host. 
4. Click **Save** at the bottom of the page to save the newly created ACR. You will see the following confirmation message.
   
    ![confirmation message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/acr2.png)
5. Click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/check-icon.png). The tabular listing will be updated to reflect this addition.

## <a name="edit-an-acr"></a>Edit an ACR
You use the **Configuration** page in the Azure classic portal to edit ACRs. 

> [!NOTE]
> You should modify only those ACRs that are currently not in use. To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.
> 
> 

Perform the following steps to edit an ACR.

#### <a name="to-edit-an-acr"></a>To edit an ACR
1. On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.
2. In the tabular listing of the access control records, hover over the ACR that you wish to modify.
3. Supply a new name and/or IQN for the ACR.
4. Click **Save** at the bottom of the page to save the modified ACR. You will see a confirmation message. 
5. Click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/check-icon.png). The tabular listing will be updated to reflect this change.

## <a name="delete-an-access-control-record"></a>Delete an access control record
You use the **Configuration** page in the Azure classic portal to delete ACRs. 

> [!NOTE]
> * You should delete only those ACRs that are currently not in use. To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.
> * When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.
> 
> 

Perform the following steps to delete an access control record.

#### <a name="to-delete-an-access-control-record"></a>To delete an access control record
1. On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.
2. In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.
3. A delete icon (**x**) will appear in the extreme right column for the ACR that you select. Click the **x** icon to delete the ACR. You will see the following confirmation message.
   
    ![confirmation message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/acr3.png)
4. Click the check icon ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/check-icon.png). The tabular listing will be updated to reflect the deletion.

## <a name="next-steps"></a>Next steps
* Learn more about [adding volumes and configuring ACRs](storsimple-ova-deploy3-iscsi-setup.md#step-3-add-a-volume).







