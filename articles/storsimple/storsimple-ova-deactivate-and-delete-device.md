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
# <a name="deactivate-and-delete-a-storsimple-virtual-array-via-storsimple-manager"></a><span data-ttu-id="97455-103">Deactivate and delete a StorSimple Virtual Array via StorSimple Manager</span><span class="sxs-lookup"><span data-stu-id="97455-103">Deactivate and delete a StorSimple Virtual Array via StorSimple Manager</span></span>
## <a name="overview"></a><span data-ttu-id="97455-104">Overview</span><span class="sxs-lookup"><span data-stu-id="97455-104">Overview</span></span>
<span data-ttu-id="97455-105">When you deactivate a StorSimple Virtual Array, you sever the connection between the device and the corresponding StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="97455-105">When you deactivate a StorSimple Virtual Array, you sever the connection between the device and the corresponding StorSimple Manager service.</span></span> <span data-ttu-id="97455-106">Deactivation is a PERMANENT operation and cannot be undone.</span><span class="sxs-lookup"><span data-stu-id="97455-106">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="97455-107">A deactivated device cannot be registered with the StorSimple Manager service again.</span><span class="sxs-lookup"><span data-stu-id="97455-107">A deactivated device cannot be registered with the StorSimple Manager service again.</span></span>

<span data-ttu-id="97455-108">You may need to deactivate and delete a StorSimple virtual device in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="97455-108">You may need to deactivate and delete a StorSimple virtual device in the following scenarios:</span></span>

* <span data-ttu-id="97455-109">Your device is online and you plan to fail over this device.</span><span class="sxs-lookup"><span data-stu-id="97455-109">Your device is online and you plan to fail over this device.</span></span> <span data-ttu-id="97455-110">You may need to do this if you are planning  to upgrade to a larger device.</span><span class="sxs-lookup"><span data-stu-id="97455-110">You may need to do this if you are planning  to upgrade to a larger device.</span></span> <span data-ttu-id="97455-111">After the device data is transferred and the failover is complete, you can then delete the device.</span><span class="sxs-lookup"><span data-stu-id="97455-111">After the device data is transferred and the failover is complete, you can then delete the device.</span></span>
* <span data-ttu-id="97455-112">Your device is offline and you plan to fail over this device.</span><span class="sxs-lookup"><span data-stu-id="97455-112">Your device is offline and you plan to fail over this device.</span></span> <span data-ttu-id="97455-113">This may happen in the event of a disaster where due to an outage in the datacenter, your primary device is down.</span><span class="sxs-lookup"><span data-stu-id="97455-113">This may happen in the event of a disaster where due to an outage in the datacenter, your primary device is down.</span></span> <span data-ttu-id="97455-114">You plan to fail over the device to a secondary device.</span><span class="sxs-lookup"><span data-stu-id="97455-114">You plan to fail over the device to a secondary device.</span></span> <span data-ttu-id="97455-115">After the device data is transferred and the failover is complete, you can delete the device.</span><span class="sxs-lookup"><span data-stu-id="97455-115">After the device data is transferred and the failover is complete, you can delete the device.</span></span>
* <span data-ttu-id="97455-116">You want to decommission the device and then delete it.</span><span class="sxs-lookup"><span data-stu-id="97455-116">You want to decommission the device and then delete it.</span></span> 

<span data-ttu-id="97455-117">When you deactivate a device, any data that was stored locally will no longer be accessible.</span><span class="sxs-lookup"><span data-stu-id="97455-117">When you deactivate a device, any data that was stored locally will no longer be accessible.</span></span> <span data-ttu-id="97455-118">Only the data stored in the cloud can be recovered.</span><span class="sxs-lookup"><span data-stu-id="97455-118">Only the data stored in the cloud can be recovered.</span></span> <span data-ttu-id="97455-119">If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span><span class="sxs-lookup"><span data-stu-id="97455-119">If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="97455-120">This will allow you to recover all the data at a later stage.</span><span class="sxs-lookup"><span data-stu-id="97455-120">This will allow you to recover all the data at a later stage.</span></span>

<span data-ttu-id="97455-121">This tutorial explains how to:</span><span class="sxs-lookup"><span data-stu-id="97455-121">This tutorial explains how to:</span></span>

* <span data-ttu-id="97455-122">Deactivate a device</span><span class="sxs-lookup"><span data-stu-id="97455-122">Deactivate a device</span></span> 
* <span data-ttu-id="97455-123">Delete a deactivated device</span><span class="sxs-lookup"><span data-stu-id="97455-123">Delete a deactivated device</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="97455-124">Deactivate a device</span><span class="sxs-lookup"><span data-stu-id="97455-124">Deactivate a device</span></span>
<span data-ttu-id="97455-125">Perform the following steps to deactivate your device.</span><span class="sxs-lookup"><span data-stu-id="97455-125">Perform the following steps to deactivate your device.</span></span>

#### <a name="to-deactivate-the-device"></a><span data-ttu-id="97455-126">To deactivate the device</span><span class="sxs-lookup"><span data-stu-id="97455-126">To deactivate the device</span></span>
1. <span data-ttu-id="97455-127">Go to **Devices** page.</span><span class="sxs-lookup"><span data-stu-id="97455-127">Go to **Devices** page.</span></span> <span data-ttu-id="97455-128">Select the device that you wish to deactivate.</span><span class="sxs-lookup"><span data-stu-id="97455-128">Select the device that you wish to deactivate.</span></span>
   
    ![Select device to deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate1m.png)
2. <span data-ttu-id="97455-130">At the bottom of the page, click **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="97455-130">At the bottom of the page, click **Deactivate**.</span></span>
   
    ![Click deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate2m.png)
3. <span data-ttu-id="97455-132">A confirmation message will appear.</span><span class="sxs-lookup"><span data-stu-id="97455-132">A confirmation message will appear.</span></span> <span data-ttu-id="97455-133">Click **Yes** to continue.</span><span class="sxs-lookup"><span data-stu-id="97455-133">Click **Yes** to continue.</span></span> 
   
    ![Confirm deactivate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate3m.png)
   
    <span data-ttu-id="97455-135">The deactivate process will start and take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="97455-135">The deactivate process will start and take a few minutes to complete.</span></span>
   
    ![Deactivate in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate4m.png)
4. <span data-ttu-id="97455-137">After deactivation, the list of the devices will be refreshed.</span><span class="sxs-lookup"><span data-stu-id="97455-137">After deactivation, the list of the devices will be refreshed.</span></span> 
   
    ![Deactivate complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate5m.png)
   
    <span data-ttu-id="97455-139">You can now delete this device.</span><span class="sxs-lookup"><span data-stu-id="97455-139">You can now delete this device.</span></span> 

## <a name="delete-the-device"></a><span data-ttu-id="97455-140">Delete the device</span><span class="sxs-lookup"><span data-stu-id="97455-140">Delete the device</span></span>
<span data-ttu-id="97455-141">A device has to be first deactivated in order to delete it.</span><span class="sxs-lookup"><span data-stu-id="97455-141">A device has to be first deactivated in order to delete it.</span></span> <span data-ttu-id="97455-142">Deleting a device removes it from the list of devices connected to the service.</span><span class="sxs-lookup"><span data-stu-id="97455-142">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="97455-143">The service can then no longer manage the deleted device.</span><span class="sxs-lookup"><span data-stu-id="97455-143">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="97455-144">The data associated with the device will however remain in the cloud.</span><span class="sxs-lookup"><span data-stu-id="97455-144">The data associated with the device will however remain in the cloud.</span></span> <span data-ttu-id="97455-145">Be aware that this data will then accrue charges.</span><span class="sxs-lookup"><span data-stu-id="97455-145">Be aware that this data will then accrue charges.</span></span> 

<span data-ttu-id="97455-146">Complete the following steps to delete the device:</span><span class="sxs-lookup"><span data-stu-id="97455-146">Complete the following steps to delete the device:</span></span>

#### <a name="to-delete-the-device"></a><span data-ttu-id="97455-147">To delete the device</span><span class="sxs-lookup"><span data-stu-id="97455-147">To delete the device</span></span>
1. <span data-ttu-id="97455-148">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="97455-148">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   
   ![Select device to delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate5m.png)
2. <span data-ttu-id="97455-150">On the bottom on the page, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="97455-150">On the bottom on the page, click **Delete**.</span></span>
   
   ![Click delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate6m.png)
3. <span data-ttu-id="97455-152">You will be prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="97455-152">You will be prompted for confirmation.</span></span> <span data-ttu-id="97455-153">Type the device name to confirm device deletion.</span><span class="sxs-lookup"><span data-stu-id="97455-153">Type the device name to confirm device deletion.</span></span> <span data-ttu-id="97455-154">Note that deleting the device will not delete the cloud data associated with the device.</span><span class="sxs-lookup"><span data-stu-id="97455-154">Note that deleting the device will not delete the cloud data associated with the device.</span></span> <span data-ttu-id="97455-155">Click the check icon to continue.</span><span class="sxs-lookup"><span data-stu-id="97455-155">Click the check icon to continue.</span></span>
   
   ![Confirm delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate7m.png) 
4. <span data-ttu-id="97455-157">It may take a few minutes for the device to be deleted.</span><span class="sxs-lookup"><span data-stu-id="97455-157">It may take a few minutes for the device to be deleted.</span></span> 
   
   ![Delete in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate8m.png)
   
    <span data-ttu-id="97455-159">After the device is deleted, the list of devices will be refreshed.</span><span class="sxs-lookup"><span data-stu-id="97455-159">After the device is deleted, the list of devices will be refreshed.</span></span>
   
   ![Delete complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deactivate-and-delete-device/deactivate9m.png)

## <a name="next-steps"></a><span data-ttu-id="97455-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="97455-161">Next steps</span></span>
* <span data-ttu-id="97455-162">To learn more about how to use the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple Virtual Array](storsimple-ova-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="97455-162">To learn more about how to use the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple Virtual Array](storsimple-ova-manager-service-administration.md).</span></span> 











