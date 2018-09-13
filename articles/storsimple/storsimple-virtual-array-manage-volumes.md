---
title: Manage volumes on StorSimple Virtual Array | Microsoft Docs
description: Describes the StorSimple Device Manager and explains how to use it to manage volumes on your StorSimple Virtual Array.
services: storsimple
documentationcenter: ''
author: manuaery
manager: syadav
editor: ''
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 323a4e9f27e92827a1f786e036f9f41c58763249
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554154"
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="9abcb-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9abcb-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="9abcb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="9abcb-104">Overview</span></span>

<span data-ttu-id="9abcb-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="9abcb-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="9abcb-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span><span class="sxs-lookup"><span data-stu-id="9abcb-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="9abcb-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span><span class="sxs-lookup"><span data-stu-id="9abcb-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="9abcb-108">Volume Types</span><span class="sxs-lookup"><span data-stu-id="9abcb-108">Volume Types</span></span>

<span data-ttu-id="9abcb-109">StorSimple volumes can be:</span><span class="sxs-lookup"><span data-stu-id="9abcb-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="9abcb-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span><span class="sxs-lookup"><span data-stu-id="9abcb-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="9abcb-111">**Tiered**: Data in these volumes can spill to the cloud.</span><span class="sxs-lookup"><span data-stu-id="9abcb-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="9abcb-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span><span class="sxs-lookup"><span data-stu-id="9abcb-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="9abcb-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span><span class="sxs-lookup"><span data-stu-id="9abcb-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="9abcb-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span><span class="sxs-lookup"><span data-stu-id="9abcb-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="9abcb-115">Provisioned capacity</span><span class="sxs-lookup"><span data-stu-id="9abcb-115">Provisioned capacity</span></span>
<span data-ttu-id="9abcb-116">Refer to the following table for maximum provisioned capacity for each volume type.</span><span class="sxs-lookup"><span data-stu-id="9abcb-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="9abcb-117">**Limit identifier**</span><span class="sxs-lookup"><span data-stu-id="9abcb-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="9abcb-118">**Limit**</span><span class="sxs-lookup"><span data-stu-id="9abcb-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="9abcb-119">Minimum size of a tiered volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="9abcb-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="9abcb-120">500 GB</span></span>        |
| <span data-ttu-id="9abcb-121">Maximum size of a tiered volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="9abcb-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="9abcb-122">5 TB</span></span>          |
| <span data-ttu-id="9abcb-123">Minimum size of a locally pinned volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="9abcb-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="9abcb-124">50 GB</span></span>         |
| <span data-ttu-id="9abcb-125">Maximum size of a locally pinned volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="9abcb-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="9abcb-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="9abcb-127">The Volumes blade</span><span class="sxs-lookup"><span data-stu-id="9abcb-127">The Volumes blade</span></span>
<span data-ttu-id="9abcb-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span><span class="sxs-lookup"><span data-stu-id="9abcb-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![Volumes blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="9abcb-130">A volume consists of a series of attributes:</span><span class="sxs-lookup"><span data-stu-id="9abcb-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="9abcb-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="9abcb-132">**Status** – Can be online or offline.</span><span class="sxs-lookup"><span data-stu-id="9abcb-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="9abcb-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="9abcb-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span><span class="sxs-lookup"><span data-stu-id="9abcb-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="9abcb-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span><span class="sxs-lookup"><span data-stu-id="9abcb-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="9abcb-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span><span class="sxs-lookup"><span data-stu-id="9abcb-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="9abcb-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![Volumes details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="9abcb-139">Use the instructions in this tutorial to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="9abcb-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="9abcb-140">Add a volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-140">Add a volume</span></span>
* <span data-ttu-id="9abcb-141">Modify a volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-141">Modify a volume</span></span>
* <span data-ttu-id="9abcb-142">Take a volume offline</span><span class="sxs-lookup"><span data-stu-id="9abcb-142">Take a volume offline</span></span>
* <span data-ttu-id="9abcb-143">Delete a volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="9abcb-144">Add a volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-144">Add a volume</span></span>

1. <span data-ttu-id="9abcb-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span><span class="sxs-lookup"><span data-stu-id="9abcb-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="9abcb-146">This opens up the **Add volume** blade.</span><span class="sxs-lookup"><span data-stu-id="9abcb-146">This opens up the **Add volume** blade.</span></span>
   
    ![Add volume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="9abcb-148">In the **Add volume** blade, do the following:</span><span class="sxs-lookup"><span data-stu-id="9abcb-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="9abcb-149">In the **Volume name** field, enter a unique name for your volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="9abcb-150">The name must be a string that contains 3 to 127 characters.</span><span class="sxs-lookup"><span data-stu-id="9abcb-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="9abcb-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="9abcb-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span><span class="sxs-lookup"><span data-stu-id="9abcb-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="9abcb-153">For all other data, select **Tiered** volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="9abcb-154">In the **Capacity** field, specify the size of the volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="9abcb-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span><span class="sxs-lookup"><span data-stu-id="9abcb-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="9abcb-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="9abcb-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="9abcb-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="9abcb-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Add volume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="9abcb-159">When you've finished configuring your volume, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9abcb-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="9abcb-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span><span class="sxs-lookup"><span data-stu-id="9abcb-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="9abcb-161">By default backup will be enabled for the volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="9abcb-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span><span class="sxs-lookup"><span data-stu-id="9abcb-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="9abcb-163">You should see the volume listed.</span><span class="sxs-lookup"><span data-stu-id="9abcb-163">You should see the volume listed.</span></span>
   
    ![Volume create success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="9abcb-165">Modify a volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-165">Modify a volume</span></span>

<span data-ttu-id="9abcb-166">Modify a volume when you need to change the hosts that access the volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="9abcb-167">The other attributes of a volume cannot be modified once the volume has been created.</span><span class="sxs-lookup"><span data-stu-id="9abcb-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="9abcb-168">To modify a volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-168">To modify a volume</span></span>

1. <span data-ttu-id="9abcb-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span><span class="sxs-lookup"><span data-stu-id="9abcb-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="9abcb-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span><span class="sxs-lookup"><span data-stu-id="9abcb-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![Edit volume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="9abcb-172">Save your changes by clicking the **Save** command bar.</span><span class="sxs-lookup"><span data-stu-id="9abcb-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="9abcb-173">Your specified settings will be applied and you will see a notification.</span><span class="sxs-lookup"><span data-stu-id="9abcb-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="9abcb-174">Take a volume offline</span><span class="sxs-lookup"><span data-stu-id="9abcb-174">Take a volume offline</span></span>

<span data-ttu-id="9abcb-175">You may need to take a volume offline when you are planning to modify it or delete it.</span><span class="sxs-lookup"><span data-stu-id="9abcb-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="9abcb-176">When a volume is offline, it is not available for read-write access.</span><span class="sxs-lookup"><span data-stu-id="9abcb-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="9abcb-177">You will need to take the volume offline on the host as well as on the device.</span><span class="sxs-lookup"><span data-stu-id="9abcb-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="9abcb-178">To take a volume offline</span><span class="sxs-lookup"><span data-stu-id="9abcb-178">To take a volume offline</span></span>

1. <span data-ttu-id="9abcb-179">Make sure that the volume in question is not in use before taking it offline.</span><span class="sxs-lookup"><span data-stu-id="9abcb-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="9abcb-180">Take the volume offline on the host first.</span><span class="sxs-lookup"><span data-stu-id="9abcb-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="9abcb-181">This eliminates any potential risk of data corruption on the volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="9abcb-182">For specific steps, refer to the instructions for your host operating system.</span><span class="sxs-lookup"><span data-stu-id="9abcb-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="9abcb-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="9abcb-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="9abcb-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span><span class="sxs-lookup"><span data-stu-id="9abcb-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="9abcb-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span><span class="sxs-lookup"><span data-stu-id="9abcb-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Offline volume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="9abcb-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span><span class="sxs-lookup"><span data-stu-id="9abcb-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="9abcb-188">Click **Take offline** to take the volume offline.</span><span class="sxs-lookup"><span data-stu-id="9abcb-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="9abcb-189">You will see a notification of the operation in progress.</span><span class="sxs-lookup"><span data-stu-id="9abcb-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="9abcb-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span><span class="sxs-lookup"><span data-stu-id="9abcb-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="9abcb-191">You should see the status of the volume as offline.</span><span class="sxs-lookup"><span data-stu-id="9abcb-191">You should see the status of the volume as offline.</span></span>
     
       ![Offline volume confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="9abcb-193">Delete a volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9abcb-194">You can delete a volume only if it is offline.</span><span class="sxs-lookup"><span data-stu-id="9abcb-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="9abcb-195">Complete the following steps to delete a volume.</span><span class="sxs-lookup"><span data-stu-id="9abcb-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="9abcb-196">To delete a volume</span><span class="sxs-lookup"><span data-stu-id="9abcb-196">To delete a volume</span></span>

1. <span data-ttu-id="9abcb-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span><span class="sxs-lookup"><span data-stu-id="9abcb-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="9abcb-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="9abcb-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Delete volume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="9abcb-200">Check the status of the volume you want to delete.</span><span class="sxs-lookup"><span data-stu-id="9abcb-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="9abcb-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="9abcb-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="9abcb-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="9abcb-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="9abcb-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span><span class="sxs-lookup"><span data-stu-id="9abcb-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9abcb-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="9abcb-204">Next steps</span></span>

<span data-ttu-id="9abcb-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="9abcb-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>










