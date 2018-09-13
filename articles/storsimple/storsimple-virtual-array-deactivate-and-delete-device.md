---
title: Deactivate and delete a Microsoft Azure StorSimple Virtual Array | Microsoft Docs
description: Describes how to remove StorSimple device from service by  first deactivating it and then deleting it.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 2e5a150be74d22b575c35f8fe89b9a30e658df07
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553591"
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="35352-103">Deactivate and delete a StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="35352-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="35352-104">Overview</span><span class="sxs-lookup"><span data-stu-id="35352-104">Overview</span></span>

<span data-ttu-id="35352-105">When you deactivate a StorSimple Virtual Array, you break the connection between the device and the corresponding StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="35352-105">When you deactivate a StorSimple Virtual Array, you break the connection between the device and the corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="35352-106">This tutorial explains how to:</span><span class="sxs-lookup"><span data-stu-id="35352-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="35352-107">Deactivate a device</span><span class="sxs-lookup"><span data-stu-id="35352-107">Deactivate a device</span></span> 
* <span data-ttu-id="35352-108">Delete a deactivated device</span><span class="sxs-lookup"><span data-stu-id="35352-108">Delete a deactivated device</span></span>

<span data-ttu-id="35352-109">The information in this article applies to StorSimple Virtual Arrays only.</span><span class="sxs-lookup"><span data-stu-id="35352-109">The information in this article applies to StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="35352-110">For information on 8000 series, go to how to [deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="35352-110">For information on 8000 series, go to how to [deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-to-deactivate"></a><span data-ttu-id="35352-111">When to deactivate?</span><span class="sxs-lookup"><span data-stu-id="35352-111">When to deactivate?</span></span>

<span data-ttu-id="35352-112">Deactivation is a PERMANENT operation and cannot be undone.</span><span class="sxs-lookup"><span data-stu-id="35352-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="35352-113">You cannot register a deactivated device with the StorSimple Device Manager service again.</span><span class="sxs-lookup"><span data-stu-id="35352-113">You cannot register a deactivated device with the StorSimple Device Manager service again.</span></span> <span data-ttu-id="35352-114">You may need to deactivate and delete a StorSimple Virtual Array in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="35352-114">You may need to deactivate and delete a StorSimple Virtual Array in the following scenarios:</span></span>

* <span data-ttu-id="35352-115">**Planned failover** : Your device is online and you plan to fail over your device.</span><span class="sxs-lookup"><span data-stu-id="35352-115">**Planned failover** : Your device is online and you plan to fail over your device.</span></span> <span data-ttu-id="35352-116">If you are planning to upgrade to a larger device, you may need to fail over your device.</span><span class="sxs-lookup"><span data-stu-id="35352-116">If you are planning to upgrade to a larger device, you may need to fail over your device.</span></span> <span data-ttu-id="35352-117">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="35352-117">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="35352-118">**Unplanned failover** : Your device is offline and you need to fail over the device.</span><span class="sxs-lookup"><span data-stu-id="35352-118">**Unplanned failover** : Your device is offline and you need to fail over the device.</span></span> <span data-ttu-id="35352-119">This scenario may occur during a disaster when there is an outage in the datacenter and your primary device is down.</span><span class="sxs-lookup"><span data-stu-id="35352-119">This scenario may occur during a disaster when there is an outage in the datacenter and your primary device is down.</span></span> <span data-ttu-id="35352-120">You plan to fail over the device to a secondary device.</span><span class="sxs-lookup"><span data-stu-id="35352-120">You plan to fail over the device to a secondary device.</span></span> <span data-ttu-id="35352-121">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="35352-121">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="35352-122">**Decommission** : You want to decommission the device.</span><span class="sxs-lookup"><span data-stu-id="35352-122">**Decommission** : You want to decommission the device.</span></span> <span data-ttu-id="35352-123">This requires you to first deactivate the device and then delete it.</span><span class="sxs-lookup"><span data-stu-id="35352-123">This requires you to first deactivate the device and then delete it.</span></span> <span data-ttu-id="35352-124">When you deactivate a device, you can no longer access any data that is stored locally.</span><span class="sxs-lookup"><span data-stu-id="35352-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="35352-125">You can only access and recover the data stored in the cloud.</span><span class="sxs-lookup"><span data-stu-id="35352-125">You can only access and recover the data stored in the cloud.</span></span> <span data-ttu-id="35352-126">If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span><span class="sxs-lookup"><span data-stu-id="35352-126">If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="35352-127">This cloud snapshot allows you to recover all the data at a later stage.</span><span class="sxs-lookup"><span data-stu-id="35352-127">This cloud snapshot allows you to recover all the data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="35352-128">Deactivate a device</span><span class="sxs-lookup"><span data-stu-id="35352-128">Deactivate a device</span></span>

<span data-ttu-id="35352-129">To deactivate your device, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="35352-129">To deactivate your device, perform the following steps.</span></span>

#### <a name="to-deactivate-the-device"></a><span data-ttu-id="35352-130">To deactivate the device</span><span class="sxs-lookup"><span data-stu-id="35352-130">To deactivate the device</span></span>

1. <span data-ttu-id="35352-131">In your service, go to **Management > Devices**.</span><span class="sxs-lookup"><span data-stu-id="35352-131">In your service, go to **Management > Devices**.</span></span> <span data-ttu-id="35352-132">In the **Devices** blade, click and select the device that you wish to deactivate.</span><span class="sxs-lookup"><span data-stu-id="35352-132">In the **Devices** blade, click and select the device that you wish to deactivate.</span></span>
   
    ![Select device to deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="35352-134">In your **Device dashboard** blade, click **… More** and from the list, select **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="35352-134">In your **Device dashboard** blade, click **… More** and from the list, select **Deactivate**.</span></span>
   
    ![Click deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="35352-136">In the **Deactivate** blade, type the device name and then click **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="35352-136">In the **Deactivate** blade, type the device name and then click **Deactivate**.</span></span> 
   
    ![Confirm deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="35352-138">The deactivate process starts and takes a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="35352-138">The deactivate process starts and takes a few minutes to complete.</span></span>
   
    ![Deactivate in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="35352-140">After deactivation, the list of devices refreshes.</span><span class="sxs-lookup"><span data-stu-id="35352-140">After deactivation, the list of devices refreshes.</span></span>
   
    ![Deactivate complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="35352-142">You can now delete this device.</span><span class="sxs-lookup"><span data-stu-id="35352-142">You can now delete this device.</span></span>

## <a name="delete-the-device"></a><span data-ttu-id="35352-143">Delete the device</span><span class="sxs-lookup"><span data-stu-id="35352-143">Delete the device</span></span>

<span data-ttu-id="35352-144">A device has to be first deactivated to delete it.</span><span class="sxs-lookup"><span data-stu-id="35352-144">A device has to be first deactivated to delete it.</span></span> <span data-ttu-id="35352-145">Deleting a device removes it from the list of devices connected to the service.</span><span class="sxs-lookup"><span data-stu-id="35352-145">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="35352-146">The service can then no longer manage the deleted device.</span><span class="sxs-lookup"><span data-stu-id="35352-146">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="35352-147">The data associated with the device however remains in the cloud.</span><span class="sxs-lookup"><span data-stu-id="35352-147">The data associated with the device however remains in the cloud.</span></span> <span data-ttu-id="35352-148">This data then accrues charges.</span><span class="sxs-lookup"><span data-stu-id="35352-148">This data then accrues charges.</span></span>

<span data-ttu-id="35352-149">To delete the device, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="35352-149">To delete the device, perform the following steps.</span></span>

#### <a name="to-delete-the-device"></a><span data-ttu-id="35352-150">To delete the device</span><span class="sxs-lookup"><span data-stu-id="35352-150">To delete the device</span></span>

1. <span data-ttu-id="35352-151">In your StorSimple Device Manager, go to **Management > Devices**.</span><span class="sxs-lookup"><span data-stu-id="35352-151">In your StorSimple Device Manager, go to **Management > Devices**.</span></span> <span data-ttu-id="35352-152">In the **Devices** blade, select a deactivated device that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="35352-152">In the **Devices** blade, select a deactivated device that you wish to delete.</span></span>
2. <span data-ttu-id="35352-153">In the **Device dashboard** blade, click **… More** and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="35352-153">In the **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Select device to delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="35352-155">In the **Delete** blade, type the name of your device to confirm the deletion and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="35352-155">In the **Delete** blade, type the name of your device to confirm the deletion and then click **Delete**.</span></span> <span data-ttu-id="35352-156">Deleting the device does not delete the cloud data associated with the device.</span><span class="sxs-lookup"><span data-stu-id="35352-156">Deleting the device does not delete the cloud data associated with the device.</span></span> 
   
   ![Confirm delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="35352-158">The deletion starts and takes a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="35352-158">The deletion starts and takes a few minutes to complete.</span></span>
   
   ![Delete in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="35352-160">After the device is deleted, you can view the updated list of devices.</span><span class="sxs-lookup"><span data-stu-id="35352-160">After the device is deleted, you can view the updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35352-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="35352-161">Next steps</span></span>

* <span data-ttu-id="35352-162">For information on how to fail over, go to [Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="35352-162">For information on how to fail over, go to [Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="35352-163">To learn more about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="35352-163">To learn more about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 









