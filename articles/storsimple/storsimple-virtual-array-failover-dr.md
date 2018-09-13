---
title: StorSimple Virtual Array disaster recovery and device failover | Microsoft Docs
description: Learn more about how to failover your StorSimple Virtual Array.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: ''
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12079f8dbc409afe5acc274fa08bda878c90b76e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809314"
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a><span data-ttu-id="2b7e5-103">Disaster recovery and device failover for your StorSimple Virtual Array via Azure portal</span><span class="sxs-lookup"><span data-stu-id="2b7e5-103">Disaster recovery and device failover for your StorSimple Virtual Array via Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="2b7e5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2b7e5-104">Overview</span></span>
<span data-ttu-id="2b7e5-105">This article describes the disaster recovery for your Microsoft Azure StorSimple Virtual Array including the detailed steps to fail over to another virtual array.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-105">This article describes the disaster recovery for your Microsoft Azure StorSimple Virtual Array including the detailed steps to fail over to another virtual array.</span></span> <span data-ttu-id="2b7e5-106">A failover allows you to move your data from a *source* device in the datacenter to a *target* device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-106">A failover allows you to move your data from a *source* device in the datacenter to a *target* device.</span></span> <span data-ttu-id="2b7e5-107">The target device may be located in the same or a different geographical location.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-107">The target device may be located in the same or a different geographical location.</span></span> <span data-ttu-id="2b7e5-108">The device failover is for the entire device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-108">The device failover is for the entire device.</span></span> <span data-ttu-id="2b7e5-109">During failover, the cloud data for the source device changes ownership to that of the target device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-109">During failover, the cloud data for the source device changes ownership to that of the target device.</span></span>

<span data-ttu-id="2b7e5-110">This article is applicable to StorSimple Virtual Arrays only.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-110">This article is applicable to StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="2b7e5-111">To fail over an 8000 series device, go to [Device failover and disaster recovery of your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-111">To fail over an 8000 series device, go to [Device failover and disaster recovery of your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>

## <a name="what-is-disaster-recovery-and-device-failover"></a><span data-ttu-id="2b7e5-112">What is disaster recovery and device failover?</span><span class="sxs-lookup"><span data-stu-id="2b7e5-112">What is disaster recovery and device failover?</span></span>

<span data-ttu-id="2b7e5-113">In a disaster recovery (DR) scenario, the primary device stops functioning.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-113">In a disaster recovery (DR) scenario, the primary device stops functioning.</span></span> <span data-ttu-id="2b7e5-114">In this scenario, you can move the cloud data associated with the failed device to another device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-114">In this scenario, you can move the cloud data associated with the failed device to another device.</span></span> <span data-ttu-id="2b7e5-115">You can use the primary device as the *source* and specify another device as the *target*.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-115">You can use the primary device as the *source* and specify another device as the *target*.</span></span> <span data-ttu-id="2b7e5-116">This process is referred to as the *failover*.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-116">This process is referred to as the *failover*.</span></span> <span data-ttu-id="2b7e5-117">During failover, all the volumes or the shares from the source device change ownership and are transferred to the target device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-117">During failover, all the volumes or the shares from the source device change ownership and are transferred to the target device.</span></span> <span data-ttu-id="2b7e5-118">No filtering of the data is allowed.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-118">No filtering of the data is allowed.</span></span>

<span data-ttu-id="2b7e5-119">DR is modeled as a full device restore using the heat map–based tiering and tracking.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-119">DR is modeled as a full device restore using the heat map–based tiering and tracking.</span></span> <span data-ttu-id="2b7e5-120">A heat map is defined by assigning a heat value to the data based on read and write patterns.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-120">A heat map is defined by assigning a heat value to the data based on read and write patterns.</span></span> <span data-ttu-id="2b7e5-121">This heat map then tiers the lowest heat data chunks to the cloud first while keeping the high heat (most used) data chunks in the local tier.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-121">This heat map then tiers the lowest heat data chunks to the cloud first while keeping the high heat (most used) data chunks in the local tier.</span></span> <span data-ttu-id="2b7e5-122">During a DR, StorSimple uses the heat map to restore and rehydrate the data from the cloud.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-122">During a DR, StorSimple uses the heat map to restore and rehydrate the data from the cloud.</span></span> <span data-ttu-id="2b7e5-123">The device fetches all the volumes/shares in the last recent backup (as determined internally) and performs a restore from that backup.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-123">The device fetches all the volumes/shares in the last recent backup (as determined internally) and performs a restore from that backup.</span></span> <span data-ttu-id="2b7e5-124">The virtual array orchestrates the entire DR process.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-124">The virtual array orchestrates the entire DR process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b7e5-125">The source device is deleted at the end of device failover and hence a failback is not supported.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-125">The source device is deleted at the end of device failover and hence a failback is not supported.</span></span>
> 
> 

<span data-ttu-id="2b7e5-126">Disaster recovery is orchestrated via the device failover feature and is initiated from the **Devices** blade.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-126">Disaster recovery is orchestrated via the device failover feature and is initiated from the **Devices** blade.</span></span> <span data-ttu-id="2b7e5-127">This blade tabulates all the StorSimple devices connected to your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-127">This blade tabulates all the StorSimple devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="2b7e5-128">For each device, you can see the friendly name, status, provisioned and maximum capacity, type, and model.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-128">For each device, you can see the friendly name, status, provisioned and maximum capacity, type, and model.</span></span>

## <a name="prerequisites-for-device-failover"></a><span data-ttu-id="2b7e5-129">Prerequisites for device failover</span><span class="sxs-lookup"><span data-stu-id="2b7e5-129">Prerequisites for device failover</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2b7e5-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b7e5-130">Prerequisites</span></span>

<span data-ttu-id="2b7e5-131">For a device failover, ensure that the following prerequisites are satisfied:</span><span class="sxs-lookup"><span data-stu-id="2b7e5-131">For a device failover, ensure that the following prerequisites are satisfied:</span></span>

* <span data-ttu-id="2b7e5-132">The source device needs to be in a **Deactivated** state.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-132">The source device needs to be in a **Deactivated** state.</span></span>
* <span data-ttu-id="2b7e5-133">The target device needs to show up as **Ready to set up** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-133">The target device needs to show up as **Ready to set up** in the Azure portal.</span></span> <span data-ttu-id="2b7e5-134">Provision a target virtual array of the same or higher capacity.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-134">Provision a target virtual array of the same or higher capacity.</span></span> <span data-ttu-id="2b7e5-135">Use the local web UI to configure and successfully register the target virtual array.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-135">Use the local web UI to configure and successfully register the target virtual array.</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="2b7e5-136">Do not attempt to configure the registered virtual device through the service.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-136">Do not attempt to configure the registered virtual device through the service.</span></span> <span data-ttu-id="2b7e5-137">No device configuration should be performed through the service.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-137">No device configuration should be performed through the service.</span></span>
  > 
  > 
* <span data-ttu-id="2b7e5-138">The target device cannot have the same name as the source device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-138">The target device cannot have the same name as the source device.</span></span>
* <span data-ttu-id="2b7e5-139">The source and target device have to be the same type.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-139">The source and target device have to be the same type.</span></span> <span data-ttu-id="2b7e5-140">You can only fail over a virtual array configured as a file server to another file server.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-140">You can only fail over a virtual array configured as a file server to another file server.</span></span> <span data-ttu-id="2b7e5-141">The same is true for an iSCSI server.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-141">The same is true for an iSCSI server.</span></span>
* <span data-ttu-id="2b7e5-142">For a file server DR, we recommend that you join the target device to the same domain as the source.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-142">For a file server DR, we recommend that you join the target device to the same domain as the source.</span></span> <span data-ttu-id="2b7e5-143">This configuration ensures that the share permissions are automatically resolved.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-143">This configuration ensures that the share permissions are automatically resolved.</span></span> <span data-ttu-id="2b7e5-144">Only the failover to a target device in the same domain.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-144">Only the failover to a target device in the same domain.</span></span>
* <span data-ttu-id="2b7e5-145">The available target devices for DR are devices that have the same or larger capacity compared to the source device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-145">The available target devices for DR are devices that have the same or larger capacity compared to the source device.</span></span> <span data-ttu-id="2b7e5-146">The devices that are connected to your service but do not meet the criteria of sufficient space are not available as target devices.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-146">The devices that are connected to your service but do not meet the criteria of sufficient space are not available as target devices.</span></span>

### <a name="other-considerations"></a><span data-ttu-id="2b7e5-147">Other considerations</span><span class="sxs-lookup"><span data-stu-id="2b7e5-147">Other considerations</span></span>

* <span data-ttu-id="2b7e5-148">For a planned failover</span><span class="sxs-lookup"><span data-stu-id="2b7e5-148">For a planned failover</span></span> 
  
  * <span data-ttu-id="2b7e5-149">We recommend that you take all the volumes or shares on the source device offline.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-149">We recommend that you take all the volumes or shares on the source device offline.</span></span>
  * <span data-ttu-id="2b7e5-150">We recommend that you take a backup of the device and then proceed with the failover to minimize data loss.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-150">We recommend that you take a backup of the device and then proceed with the failover to minimize data loss.</span></span> 
* <span data-ttu-id="2b7e5-151">For an unplanned failover, the device uses the most recent backup to restore the data.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-151">For an unplanned failover, the device uses the most recent backup to restore the data.</span></span>

### <a name="device-failover-prechecks"></a><span data-ttu-id="2b7e5-152">Device failover prechecks</span><span class="sxs-lookup"><span data-stu-id="2b7e5-152">Device failover prechecks</span></span>

<span data-ttu-id="2b7e5-153">Before the DR begins, the device performs prechecks.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-153">Before the DR begins, the device performs prechecks.</span></span> <span data-ttu-id="2b7e5-154">These checks help ensure that no errors occur when DR commences.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-154">These checks help ensure that no errors occur when DR commences.</span></span> <span data-ttu-id="2b7e5-155">The prechecks include:</span><span class="sxs-lookup"><span data-stu-id="2b7e5-155">The prechecks include:</span></span>

* <span data-ttu-id="2b7e5-156">Validating the storage account.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-156">Validating the storage account.</span></span>
* <span data-ttu-id="2b7e5-157">Checking the cloud connectivity to Azure.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-157">Checking the cloud connectivity to Azure.</span></span>
* <span data-ttu-id="2b7e5-158">Checking available space on the target device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-158">Checking available space on the target device.</span></span>
* <span data-ttu-id="2b7e5-159">Checking if an iSCSI server source device volume has</span><span class="sxs-lookup"><span data-stu-id="2b7e5-159">Checking if an iSCSI server source device volume has</span></span>
  
  * <span data-ttu-id="2b7e5-160">valid ACR names.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-160">valid ACR names.</span></span>
  * <span data-ttu-id="2b7e5-161">valid IQN (not exceeding 220 characters).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-161">valid IQN (not exceeding 220 characters).</span></span>
  * <span data-ttu-id="2b7e5-162">valid CHAP passwords (12-16 characters long).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-162">valid CHAP passwords (12-16 characters long).</span></span>

<span data-ttu-id="2b7e5-163">If any of the preceding prechecks fail, you cannot proceed with the DR.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-163">If any of the preceding prechecks fail, you cannot proceed with the DR.</span></span> <span data-ttu-id="2b7e5-164">Resolve those issues and then retry DR.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-164">Resolve those issues and then retry DR.</span></span>

<span data-ttu-id="2b7e5-165">After the DR is successfully completed, the ownership of the cloud data on the source device is transferred to the target device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-165">After the DR is successfully completed, the ownership of the cloud data on the source device is transferred to the target device.</span></span> <span data-ttu-id="2b7e5-166">The source device is then no longer available in the portal.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-166">The source device is then no longer available in the portal.</span></span> <span data-ttu-id="2b7e5-167">Access to all the volumes/shares on the source device is blocked and the target device becomes active.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-167">Access to all the volumes/shares on the source device is blocked and the target device becomes active.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b7e5-168">Though the device is no longer available, the virtual machine that you provisioned on the host system is still consuming resources.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-168">Though the device is no longer available, the virtual machine that you provisioned on the host system is still consuming resources.</span></span> <span data-ttu-id="2b7e5-169">Once the DR is successfully complete, you can delete this virtual machine from your host system.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-169">Once the DR is successfully complete, you can delete this virtual machine from your host system.</span></span>
> 
> 

## <a name="fail-over-to-a-virtual-array"></a><span data-ttu-id="2b7e5-170">Fail over to a virtual array</span><span class="sxs-lookup"><span data-stu-id="2b7e5-170">Fail over to a virtual array</span></span>

<span data-ttu-id="2b7e5-171">We recommend that you provision, configure, and register another StorSimple Virtual Array with your StorSimple Device Manager service before you run this procedure.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-171">We recommend that you provision, configure, and register another StorSimple Virtual Array with your StorSimple Device Manager service before you run this procedure.</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="2b7e5-172">You cannot fail over from a StorSimple 8000 series device to a 1200 virtual device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-172">You cannot fail over from a StorSimple 8000 series device to a 1200 virtual device.</span></span>
> * <span data-ttu-id="2b7e5-173">You can fail over from a Federal Information Processing Standard (FIPS) enabled virtual device to another FIPS enabled device or to a non-FIPS device deployed in the Government portal.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-173">You can fail over from a Federal Information Processing Standard (FIPS) enabled virtual device to another FIPS enabled device or to a non-FIPS device deployed in the Government portal.</span></span>


<span data-ttu-id="2b7e5-174">Perform the following steps to restore the device to a target StorSimple virtual device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-174">Perform the following steps to restore the device to a target StorSimple virtual device.</span></span>

1. <span data-ttu-id="2b7e5-175">Provision and configure a target device that meets the [prerequisites for device failover](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-175">Provision and configure a target device that meets the [prerequisites for device failover](#prerequisites).</span></span> <span data-ttu-id="2b7e5-176">Complete the device configuration via the local web UI and register it to your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-176">Complete the device configuration via the local web UI and register it to your StorSimple Device Manager service.</span></span> <span data-ttu-id="2b7e5-177">If creating a file server, go to step 1 of [set up as file server](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-177">If creating a file server, go to step 1 of [set up as file server](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span> <span data-ttu-id="2b7e5-178">If creating an iSCSI server, go to step 1 of [set up as iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-178">If creating an iSCSI server, go to step 1 of [set up as iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span>

2. <span data-ttu-id="2b7e5-179">Take volumes/shares offline on the host.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-179">Take volumes/shares offline on the host.</span></span> <span data-ttu-id="2b7e5-180">To take the volumes/shares offline, refer to the operating system–specific instructions for the host.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-180">To take the volumes/shares offline, refer to the operating system–specific instructions for the host.</span></span> <span data-ttu-id="2b7e5-181">If not already offline, you need to take all the volumes/shares offline on the device by doing the following.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-181">If not already offline, you need to take all the volumes/shares offline on the device by doing the following.</span></span>
   
    1. <span data-ttu-id="2b7e5-182">Go to **Devices** blade and select your device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-182">Go to **Devices** blade and select your device.</span></span>
   
    2. <span data-ttu-id="2b7e5-183">Go to **Settings > Manage > Shares** (or **Settings > Manage > Volumes**).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-183">Go to **Settings > Manage > Shares** (or **Settings > Manage > Volumes**).</span></span> 
   
    3. <span data-ttu-id="2b7e5-184">Select a share/volume, right click and select **Take offline**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-184">Select a share/volume, right click and select **Take offline**.</span></span> 
   
    4. <span data-ttu-id="2b7e5-185">When prompted for confirmation, check **I understand the impact of taking this share offline.**</span><span class="sxs-lookup"><span data-stu-id="2b7e5-185">When prompted for confirmation, check **I understand the impact of taking this share offline.**</span></span> 
   
    5. <span data-ttu-id="2b7e5-186">Click **Take offline**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-186">Click **Take offline**.</span></span>

3. <span data-ttu-id="2b7e5-187">In your StorSimple Device Manager service, go to **Management > Devices**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-187">In your StorSimple Device Manager service, go to **Management > Devices**.</span></span> <span data-ttu-id="2b7e5-188">In the **Devices** blade, select and click your source device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-188">In the **Devices** blade, select and click your source device.</span></span>

4. <span data-ttu-id="2b7e5-189">In your **Device dashboard** blade, click **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-189">In your **Device dashboard** blade, click **Deactivate**.</span></span>

5. <span data-ttu-id="2b7e5-190">In the **Deactivate** blade, you are prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-190">In the **Deactivate** blade, you are prompted for confirmation.</span></span> <span data-ttu-id="2b7e5-191">Device deactivation is a *permanent* process that cannot be undone.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-191">Device deactivation is a *permanent* process that cannot be undone.</span></span> <span data-ttu-id="2b7e5-192">You are also reminded to take your shares/volumes offline on the host.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-192">You are also reminded to take your shares/volumes offline on the host.</span></span> <span data-ttu-id="2b7e5-193">Type the device name to confirm and click **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-193">Type the device name to confirm and click **Deactivate**.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. <span data-ttu-id="2b7e5-194">The deactivation starts.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-194">The deactivation starts.</span></span> <span data-ttu-id="2b7e5-195">You will receive a notification after the deactivation is successfully completed.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-195">You will receive a notification after the deactivation is successfully completed.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. <span data-ttu-id="2b7e5-196">On the Devices page, the device state will now change to **Deactivated**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-196">On the Devices page, the device state will now change to **Deactivated**.</span></span>
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. <span data-ttu-id="2b7e5-197">In the **Devices** blade, select and click the deactivated source device for failover.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-197">In the **Devices** blade, select and click the deactivated source device for failover.</span></span> 
9. <span data-ttu-id="2b7e5-198">In the **Device dashboard** blade, click **Fail over**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-198">In the **Device dashboard** blade, click **Fail over**.</span></span> 
10. <span data-ttu-id="2b7e5-199">In the **Fail over device** blade, do the following:</span><span class="sxs-lookup"><span data-stu-id="2b7e5-199">In the **Fail over device** blade, do the following:</span></span>
    
    1. <span data-ttu-id="2b7e5-200">The source device field is automatically populated.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-200">The source device field is automatically populated.</span></span> <span data-ttu-id="2b7e5-201">Note the total data size for the source device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-201">Note the total data size for the source device.</span></span> <span data-ttu-id="2b7e5-202">The data size should be lesser than the available capacity on the target device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-202">The data size should be lesser than the available capacity on the target device.</span></span> <span data-ttu-id="2b7e5-203">Review the details associated with the source device such as device name, total capacity, and the names of the shares that are failed over.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-203">Review the details associated with the source device such as device name, total capacity, and the names of the shares that are failed over.</span></span>

    2. <span data-ttu-id="2b7e5-204">From the dropdown list of available devices, choose a **Target device**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-204">From the dropdown list of available devices, choose a **Target device**.</span></span> <span data-ttu-id="2b7e5-205">Only the devices that have sufficient capacity are displayed in the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-205">Only the devices that have sufficient capacity are displayed in the dropdown list.</span></span>

    3. <span data-ttu-id="2b7e5-206">Check that **I understand that this operation will fail over data to the target device**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-206">Check that **I understand that this operation will fail over data to the target device**.</span></span> 

    4. <span data-ttu-id="2b7e5-207">Click **Fail over**.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-207">Click **Fail over**.</span></span>
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. <span data-ttu-id="2b7e5-208">A failover job initiates and you receive a notification.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-208">A failover job initiates and you receive a notification.</span></span> <span data-ttu-id="2b7e5-209">Go to **Devices > Jobs** to monitor the failover.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-209">Go to **Devices > Jobs** to monitor the failover.</span></span>
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. <span data-ttu-id="2b7e5-210">In the **Jobs** blade, you see a failover job created for the source device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-210">In the **Jobs** blade, you see a failover job created for the source device.</span></span> <span data-ttu-id="2b7e5-211">This job performs the DR prechecks.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-211">This job performs the DR prechecks.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     <span data-ttu-id="2b7e5-212">After the DR prechecks are successful, the failover job will spawn restore jobs for each share/volume that exists on your source device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-212">After the DR prechecks are successful, the failover job will spawn restore jobs for each share/volume that exists on your source device.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. <span data-ttu-id="2b7e5-213">After the failover is complete, go to the **Devices** blade.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-213">After the failover is complete, go to the **Devices** blade.</span></span>
    
    1. <span data-ttu-id="2b7e5-214">Select and click the StorSimple device that was used as the target device for the failover process.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-214">Select and click the StorSimple device that was used as the target device for the failover process.</span></span>
    2. <span data-ttu-id="2b7e5-215">Go to **Settings > Management > Shares** (or **Volumes** if iSCSI server).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-215">Go to **Settings > Management > Shares** (or **Volumes** if iSCSI server).</span></span> <span data-ttu-id="2b7e5-216">In the **Shares** blade, you can view all the shares (volumes) from the old device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-216">In the **Shares** blade, you can view all the shares (volumes) from the old device.</span></span>
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. <span data-ttu-id="2b7e5-217">You will need to [create a DNS alias](https://support.microsoft.com/kb/168322) so that all the applications that are trying to connect can get redirected to the new device.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-217">You will need to [create a DNS alias](https://support.microsoft.com/kb/168322) so that all the applications that are trying to connect can get redirected to the new device.</span></span>

## <a name="errors-during-dr"></a><span data-ttu-id="2b7e5-218">Errors during DR</span><span class="sxs-lookup"><span data-stu-id="2b7e5-218">Errors during DR</span></span>

<span data-ttu-id="2b7e5-219">**Cloud connectivity outage during DR**</span><span class="sxs-lookup"><span data-stu-id="2b7e5-219">**Cloud connectivity outage during DR**</span></span>

<span data-ttu-id="2b7e5-220">If the cloud connectivity is disrupted after DR has started and before the device restore is complete, the DR will fail.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-220">If the cloud connectivity is disrupted after DR has started and before the device restore is complete, the DR will fail.</span></span> <span data-ttu-id="2b7e5-221">You receive a failore notification.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-221">You receive a failore notification.</span></span> <span data-ttu-id="2b7e5-222">The target device for DR is marked as *unusable.*</span><span class="sxs-lookup"><span data-stu-id="2b7e5-222">The target device for DR is marked as *unusable.*</span></span> <span data-ttu-id="2b7e5-223">You cannot use the same target device for future DRs.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-223">You cannot use the same target device for future DRs.</span></span>

<span data-ttu-id="2b7e5-224">**No compatible target devices**</span><span class="sxs-lookup"><span data-stu-id="2b7e5-224">**No compatible target devices**</span></span>

<span data-ttu-id="2b7e5-225">If the available target devices do not have sufficient space, you see an error to the effect that there are no compatible target devices.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-225">If the available target devices do not have sufficient space, you see an error to the effect that there are no compatible target devices.</span></span>

<span data-ttu-id="2b7e5-226">**Precheck failures**</span><span class="sxs-lookup"><span data-stu-id="2b7e5-226">**Precheck failures**</span></span>

<span data-ttu-id="2b7e5-227">If one of the prechecks is not satisfied, then you see precheck failures.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-227">If one of the prechecks is not satisfied, then you see precheck failures.</span></span>

## <a name="business-continuity-disaster-recovery-bcdr"></a><span data-ttu-id="2b7e5-228">Business continuity disaster recovery (BCDR)</span><span class="sxs-lookup"><span data-stu-id="2b7e5-228">Business continuity disaster recovery (BCDR)</span></span>

<span data-ttu-id="2b7e5-229">A business continuity disaster recovery (BCDR) scenario occurs when the entire Azure datacenter stops functioning.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-229">A business continuity disaster recovery (BCDR) scenario occurs when the entire Azure datacenter stops functioning.</span></span> <span data-ttu-id="2b7e5-230">This can affect your StorSimple Device Manager service and the associated StorSimple devices.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-230">This can affect your StorSimple Device Manager service and the associated StorSimple devices.</span></span>

<span data-ttu-id="2b7e5-231">If there are StorSimple devices that were registered just before a disaster occurred, then these StorSimple devices may need to be deleted.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-231">If there are StorSimple devices that were registered just before a disaster occurred, then these StorSimple devices may need to be deleted.</span></span> <span data-ttu-id="2b7e5-232">After the disaster, you can recreate and configure those devices.</span><span class="sxs-lookup"><span data-stu-id="2b7e5-232">After the disaster, you can recreate and configure those devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b7e5-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b7e5-233">Next steps</span></span>

<span data-ttu-id="2b7e5-234">Learn more about how to [administer your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="2b7e5-234">Learn more about how to [administer your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span></span>

