---
title: Deactivate and delete a StorSimple device | Microsoft Docs
description: Describes how to remove StorSimple device from service by  first deactivating it and then deleting it.
services: storsimple
documentationcenter: ''
author: SharS
manager: timlt
editor: ''
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 833dee54ef9de46c50e9e760594359baf4f89b5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555769"
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a><span data-ttu-id="40587-103">Deactivate and delete a StorSimple 8000 series device via StorSimple Manager service</span><span class="sxs-lookup"><span data-stu-id="40587-103">Deactivate and delete a StorSimple 8000 series device via StorSimple Manager service</span></span>
## <a name="overview"></a><span data-ttu-id="40587-104">Overview</span><span class="sxs-lookup"><span data-stu-id="40587-104">Overview</span></span>
<span data-ttu-id="40587-105">You may wish to take a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span><span class="sxs-lookup"><span data-stu-id="40587-105">You may wish to take a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="40587-106">If this is the case, you will need to deactivate the device before you can delete it.</span><span class="sxs-lookup"><span data-stu-id="40587-106">If this is the case, you will need to deactivate the device before you can delete it.</span></span> <span data-ttu-id="40587-107">Deactivating severs the connection between the device and the corresponding StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="40587-107">Deactivating severs the connection between the device and the corresponding StorSimple Manager service.</span></span> <span data-ttu-id="40587-108">This tutorial explains how to remove a StorSimple device from service by first deactivating it and then deleting it.</span><span class="sxs-lookup"><span data-stu-id="40587-108">This tutorial explains how to remove a StorSimple device from service by first deactivating it and then deleting it.</span></span> 

<span data-ttu-id="40587-109">When you deactivate a device, any data that was stored locally on the device will no longer be accessible.</span><span class="sxs-lookup"><span data-stu-id="40587-109">When you deactivate a device, any data that was stored locally on the device will no longer be accessible.</span></span> <span data-ttu-id="40587-110">Only the data associated with the device that was stored in the cloud can be recovered.</span><span class="sxs-lookup"><span data-stu-id="40587-110">Only the data associated with the device that was stored in the cloud can be recovered.</span></span>  

> [!WARNING]
> <span data-ttu-id="40587-111">Deactivation is a PERMANENT operation and cannot be undone.</span><span class="sxs-lookup"><span data-stu-id="40587-111">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="40587-112">A deactivated device cannot be registered with the StorSimple Manager service unless it is first reset by the factory.</span><span class="sxs-lookup"><span data-stu-id="40587-112">A deactivated device cannot be registered with the StorSimple Manager service unless it is first reset by the factory.</span></span> 
> 
> <span data-ttu-id="40587-113">The factory reset process deletes all the data that was stored locally on your device.</span><span class="sxs-lookup"><span data-stu-id="40587-113">The factory reset process deletes all the data that was stored locally on your device.</span></span> <span data-ttu-id="40587-114">Therefore, it is essential that you take a cloud snapshot of all your data before you deactivate a device.</span><span class="sxs-lookup"><span data-stu-id="40587-114">Therefore, it is essential that you take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="40587-115">This will allow you to recover all the data at a later stage.</span><span class="sxs-lookup"><span data-stu-id="40587-115">This will allow you to recover all the data at a later stage.</span></span>
> 
> 

<span data-ttu-id="40587-116">This tutorial explains how to:</span><span class="sxs-lookup"><span data-stu-id="40587-116">This tutorial explains how to:</span></span>

* <span data-ttu-id="40587-117">Deactivate a device and delete the data</span><span class="sxs-lookup"><span data-stu-id="40587-117">Deactivate a device and delete the data</span></span>
* <span data-ttu-id="40587-118">Deactivate a device and retain the data</span><span class="sxs-lookup"><span data-stu-id="40587-118">Deactivate a device and retain the data</span></span>

<span data-ttu-id="40587-119">It also explains how deactivation and deletion works on a StorSimple virtual device.</span><span class="sxs-lookup"><span data-stu-id="40587-119">It also explains how deactivation and deletion works on a StorSimple virtual device.</span></span>

> [!NOTE]
> <span data-ttu-id="40587-120">Before you deactivate a StorSimple physical or virtual device, make sure to stop or delete clients and hosts that depend on that device.</span><span class="sxs-lookup"><span data-stu-id="40587-120">Before you deactivate a StorSimple physical or virtual device, make sure to stop or delete clients and hosts that depend on that device.</span></span>
> 
> 

## <a name="deactivate-and-delete-data"></a><span data-ttu-id="40587-121">Deactivate and delete data</span><span class="sxs-lookup"><span data-stu-id="40587-121">Deactivate and delete data</span></span>
<span data-ttu-id="40587-122">If you are interested in deleting the device completely and do not want to retain the data on the device, then complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="40587-122">If you are interested in deleting the device completely and do not want to retain the data on the device, then complete the following steps.</span></span>

#### <a name="to-deactivate-the-device-and-delete-the-data"></a><span data-ttu-id="40587-123">To deactivate the device and delete the data</span><span class="sxs-lookup"><span data-stu-id="40587-123">To deactivate the device and delete the data</span></span>
1. <span data-ttu-id="40587-124">Prior to deactivating a device, you must delete all the volume containers (and the volumes) associated with the device.</span><span class="sxs-lookup"><span data-stu-id="40587-124">Prior to deactivating a device, you must delete all the volume containers (and the volumes) associated with the device.</span></span> <span data-ttu-id="40587-125">You can delete volume containers only after you have deleted the associated backups.</span><span class="sxs-lookup"><span data-stu-id="40587-125">You can delete volume containers only after you have deleted the associated backups.</span></span>
2. <span data-ttu-id="40587-126">Deactivate the device as follows:</span><span class="sxs-lookup"><span data-stu-id="40587-126">Deactivate the device as follows:</span></span>
   
   1. <span data-ttu-id="40587-127">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="40587-127">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="40587-128">A confirmation message will appear.</span><span class="sxs-lookup"><span data-stu-id="40587-128">A confirmation message will appear.</span></span> <span data-ttu-id="40587-129">Click **Yes** to continue.</span><span class="sxs-lookup"><span data-stu-id="40587-129">Click **Yes** to continue.</span></span> <span data-ttu-id="40587-130">The deactivate process will start and take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="40587-130">The deactivate process will start and take a few minutes to complete.</span></span>
3. <span data-ttu-id="40587-131">After deactivation, you can delete the device completely.</span><span class="sxs-lookup"><span data-stu-id="40587-131">After deactivation, you can delete the device completely.</span></span> <span data-ttu-id="40587-132">Deleting a device removes it from the list of devices connected to the service.</span><span class="sxs-lookup"><span data-stu-id="40587-132">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="40587-133">The service can then no longer manage the deleted device.</span><span class="sxs-lookup"><span data-stu-id="40587-133">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="40587-134">Use the following steps to delete the device:</span><span class="sxs-lookup"><span data-stu-id="40587-134">Use the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="40587-135">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="40587-135">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   2. <span data-ttu-id="40587-136">On the bottom on the page, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="40587-136">On the bottom on the page, click **Delete**.</span></span>
   3. <span data-ttu-id="40587-137">You will be prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="40587-137">You will be prompted for confirmation.</span></span> <span data-ttu-id="40587-138">Click **Yes** to continue.</span><span class="sxs-lookup"><span data-stu-id="40587-138">Click **Yes** to continue.</span></span>
      
      <span data-ttu-id="40587-139">It may take a few minutes for the device to be deleted.</span><span class="sxs-lookup"><span data-stu-id="40587-139">It may take a few minutes for the device to be deleted.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="40587-140">Deactivate and retain data</span><span class="sxs-lookup"><span data-stu-id="40587-140">Deactivate and retain data</span></span>
<span data-ttu-id="40587-141">If you are interested in deleting the device but want to retain the data, then complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="40587-141">If you are interested in deleting the device but want to retain the data, then complete the following steps.</span></span>

#### <a name="to-deactivate-a-device-and-retain-the-data"></a><span data-ttu-id="40587-142">To deactivate a device and retain the data</span><span class="sxs-lookup"><span data-stu-id="40587-142">To deactivate a device and retain the data</span></span>
1. <span data-ttu-id="40587-143">Deactivate the device.</span><span class="sxs-lookup"><span data-stu-id="40587-143">Deactivate the device.</span></span> <span data-ttu-id="40587-144">All the volume containers and the snapshots of the device will remain.</span><span class="sxs-lookup"><span data-stu-id="40587-144">All the volume containers and the snapshots of the device will remain.</span></span>
   
   1. <span data-ttu-id="40587-145">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="40587-145">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="40587-146">A confirmation message will appear.</span><span class="sxs-lookup"><span data-stu-id="40587-146">A confirmation message will appear.</span></span> <span data-ttu-id="40587-147">Click **Yes** to continue.</span><span class="sxs-lookup"><span data-stu-id="40587-147">Click **Yes** to continue.</span></span> <span data-ttu-id="40587-148">The deactivate process will start and take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="40587-148">The deactivate process will start and take a few minutes to complete.</span></span>
2. <span data-ttu-id="40587-149">You can now fail over the volume containers and the associated snapshots.</span><span class="sxs-lookup"><span data-stu-id="40587-149">You can now fail over the volume containers and the associated snapshots.</span></span> <span data-ttu-id="40587-150">For procedures, go to [Failover and disaster recovery for your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="40587-150">For procedures, go to [Failover and disaster recovery for your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="40587-151">After deactivation and failover, you can delete the device completely.</span><span class="sxs-lookup"><span data-stu-id="40587-151">After deactivation and failover, you can delete the device completely.</span></span> <span data-ttu-id="40587-152">Deleting a device removes it from the list of devices connected to the service.</span><span class="sxs-lookup"><span data-stu-id="40587-152">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="40587-153">The service can then no longer manage the deleted device.</span><span class="sxs-lookup"><span data-stu-id="40587-153">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="40587-154">Complete the following steps to delete the device:</span><span class="sxs-lookup"><span data-stu-id="40587-154">Complete the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="40587-155">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="40587-155">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   2. <span data-ttu-id="40587-156">On the bottom on the page, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="40587-156">On the bottom on the page, click **Delete**.</span></span>
   3. <span data-ttu-id="40587-157">You will be prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="40587-157">You will be prompted for confirmation.</span></span> <span data-ttu-id="40587-158">Click **Yes** to continue.</span><span class="sxs-lookup"><span data-stu-id="40587-158">Click **Yes** to continue.</span></span>
      
      <span data-ttu-id="40587-159">It may take a few minutes for the device to be deleted.</span><span class="sxs-lookup"><span data-stu-id="40587-159">It may take a few minutes for the device to be deleted.</span></span>

## <a name="deactivate-and-delete-a-virtual-device"></a><span data-ttu-id="40587-160">Deactivate and delete a virtual device</span><span class="sxs-lookup"><span data-stu-id="40587-160">Deactivate and delete a virtual device</span></span>
<span data-ttu-id="40587-161">For a StorSimple virtual device, deactivation deallocates the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="40587-161">For a StorSimple virtual device, deactivation deallocates the virtual machine.</span></span> <span data-ttu-id="40587-162">You can then delete the virtual machine and the resources created when it was provisioned.</span><span class="sxs-lookup"><span data-stu-id="40587-162">You can then delete the virtual machine and the resources created when it was provisioned.</span></span> <span data-ttu-id="40587-163">After the virtual device is deactivated, it cannot be restored to its previous state.</span><span class="sxs-lookup"><span data-stu-id="40587-163">After the virtual device is deactivated, it cannot be restored to its previous state.</span></span> 

<span data-ttu-id="40587-164">Deactivation results in the following actions:</span><span class="sxs-lookup"><span data-stu-id="40587-164">Deactivation results in the following actions:</span></span>

* <span data-ttu-id="40587-165">The StorSimple virtual device is removed.</span><span class="sxs-lookup"><span data-stu-id="40587-165">The StorSimple virtual device is removed.</span></span>
* <span data-ttu-id="40587-166">The OSDisk and Data Disks created for the StorSimple virtual device are removed.</span><span class="sxs-lookup"><span data-stu-id="40587-166">The OSDisk and Data Disks created for the StorSimple virtual device are removed.</span></span>
* <span data-ttu-id="40587-167">The Hosted Service and Virtual Network that were created during provisioning are retained.</span><span class="sxs-lookup"><span data-stu-id="40587-167">The Hosted Service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="40587-168">If you are not using these entities, you should delete them manually.</span><span class="sxs-lookup"><span data-stu-id="40587-168">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="40587-169">Cloud snapshots created by the StorSimple virtual device are retained.</span><span class="sxs-lookup"><span data-stu-id="40587-169">Cloud snapshots created by the StorSimple virtual device are retained.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40587-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="40587-170">Next steps</span></span>
* <span data-ttu-id="40587-171">To restore the deactivated device to factory defaults, go to [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="40587-171">To restore the deactivated device to factory defaults, go to [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="40587-172">For technical assistance, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="40587-172">For technical assistance, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="40587-173">To learn more about how to use the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="40587-173">To learn more about how to use the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span> 

