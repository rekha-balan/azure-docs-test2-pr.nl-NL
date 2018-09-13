---
title: Manage StorSimple Virtual Array shares | Microsoft Docs
description: Describes the StorSimple Device Manager and explains how to use it to manage shares on your StorSimple Virtual Array.
services: storsimple
documentationcenter: ''
author: manuaery
manager: syadav
editor: ''
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 5be57972c3da9c161f0f0904d9507a7ef0a7068b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563076"
---
# <a name="use-the-storsimple-device-manager-service-to-manage-shares-on-the-storsimple-virtual-array"></a><span data-ttu-id="2cf3c-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="2cf3c-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="2cf3c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2cf3c-104">Overview</span></span>

<span data-ttu-id="2cf3c-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="2cf3c-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="2cf3c-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="2cf3c-108">Share Types</span><span class="sxs-lookup"><span data-stu-id="2cf3c-108">Share Types</span></span>

<span data-ttu-id="2cf3c-109">StorSimple shares can be:</span><span class="sxs-lookup"><span data-stu-id="2cf3c-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="2cf3c-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="2cf3c-111">**Tiered**: Data in these shares can spill to the cloud.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-111">**Tiered**: Data in these shares can spill to the cloud.</span></span> <span data-ttu-id="2cf3c-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="2cf3c-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="2cf3c-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span><span class="sxs-lookup"><span data-stu-id="2cf3c-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="2cf3c-115">Provisioned capacity</span><span class="sxs-lookup"><span data-stu-id="2cf3c-115">Provisioned capacity</span></span>

<span data-ttu-id="2cf3c-116">Refer to the following table for maximum provisioned capacity for each share type.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-116">Refer to the following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="2cf3c-117">**Limit identifier**</span><span class="sxs-lookup"><span data-stu-id="2cf3c-117">**Limit identifier**</span></span> | <span data-ttu-id="2cf3c-118">**Limit**</span><span class="sxs-lookup"><span data-stu-id="2cf3c-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="2cf3c-119">Minimum size of a tiered share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="2cf3c-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="2cf3c-120">500 GB</span></span> |
| <span data-ttu-id="2cf3c-121">Maximum size of a tiered share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="2cf3c-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="2cf3c-122">20 TB</span></span> |
| <span data-ttu-id="2cf3c-123">Minimum size of a locally pinned share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="2cf3c-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="2cf3c-124">50 GB</span></span> |
| <span data-ttu-id="2cf3c-125">Maximum size of a locally pinned share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="2cf3c-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="2cf3c-126">2 TB</span></span> |

## <a name="the-shares-blade"></a><span data-ttu-id="2cf3c-127">The Shares blade</span><span class="sxs-lookup"><span data-stu-id="2cf3c-127">The Shares blade</span></span>

<span data-ttu-id="2cf3c-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span></span>

![Shares blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="2cf3c-130">A share consists of a series of attributes:</span><span class="sxs-lookup"><span data-stu-id="2cf3c-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="2cf3c-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span></span>
* <span data-ttu-id="2cf3c-132">**Status** – Can be online or offline.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="2cf3c-133">If a share is offline, users of the share will not be able to access it.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-133">If a share is offline, users of the share will not be able to access it.</span></span>
* <span data-ttu-id="2cf3c-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="2cf3c-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span></span>
* <span data-ttu-id="2cf3c-136">**Description** – An optional setting that helps describe the share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-136">**Description** – An optional setting that helps describe the share.</span></span>
* <span data-ttu-id="2cf3c-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="2cf3c-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Shares details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="2cf3c-140">Use the instructions in this tutorial to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="2cf3c-140">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="2cf3c-141">Add a share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-141">Add a share</span></span>
* <span data-ttu-id="2cf3c-142">Modify a share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-142">Modify a share</span></span>
* <span data-ttu-id="2cf3c-143">Take a share offline</span><span class="sxs-lookup"><span data-stu-id="2cf3c-143">Take a share offline</span></span>
* <span data-ttu-id="2cf3c-144">Delete a share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="2cf3c-145">Add a share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-145">Add a share</span></span>

1. <span data-ttu-id="2cf3c-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span></span> <span data-ttu-id="2cf3c-147">This opens up the **Add share** blade.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-147">This opens up the **Add share** blade.</span></span>

    ![Add share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="2cf3c-149">In the **Add share** blade, do the following:</span><span class="sxs-lookup"><span data-stu-id="2cf3c-149">In the **Add share** blade, do the following:</span></span>
   
    1. <span data-ttu-id="2cf3c-150">In the **Share name** field, enter a unique name for your share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-150">In the **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="2cf3c-151">The name must be a string that contains 3 to 127 characters.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-151">The name must be a string that contains 3 to 127 characters.</span></span>

    2. <span data-ttu-id="2cf3c-152">An optional **Description** for the share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-152">An optional **Description** for the share.</span></span> <span data-ttu-id="2cf3c-153">The description will help identify the share owners.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-153">The description will help identify the share owners.</span></span>

    3. <span data-ttu-id="2cf3c-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="2cf3c-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="2cf3c-156">For all other data, select **Tiered** share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="2cf3c-157">In the **Capacity** field, specify the size of the share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-157">In the **Capacity** field, specify the size of the share.</span></span> <span data-ttu-id="2cf3c-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="2cf3c-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="2cf3c-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="2cf3c-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="2cf3c-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
3. <span data-ttu-id="2cf3c-163">When you've finished configuring your share, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="2cf3c-164">A share will be created with the specified settings and you will see a notification.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-164">A share will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="2cf3c-165">By default, backup will be enabled for the share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-165">By default, backup will be enabled for the share.</span></span>
4. <span data-ttu-id="2cf3c-166">To confirm that the share was successfully created, go to the **Shares** blade.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-166">To confirm that the share was successfully created, go to the **Shares** blade.</span></span> <span data-ttu-id="2cf3c-167">You should see the share listed.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-167">You should see the share listed.</span></span>
   
    ![Share create success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="2cf3c-169">Modify a share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-169">Modify a share</span></span>

<span data-ttu-id="2cf3c-170">Modify a share when you need to change the description of the share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-170">Modify a share when you need to change the description of the share.</span></span> <span data-ttu-id="2cf3c-171">No other share properties can be modified once the share is created.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-171">No other share properties can be modified once the share is created.</span></span>

#### <a name="to-modify-a-share"></a><span data-ttu-id="2cf3c-172">To modify a share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-172">To modify a share</span></span>

1. <span data-ttu-id="2cf3c-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span></span>
2. <span data-ttu-id="2cf3c-174">**Select** the share to view the current description and modify it.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-174">**Select** the share to view the current description and modify it.</span></span>
3. <span data-ttu-id="2cf3c-175">Save your changes by clicking the **Save** command bar.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-175">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="2cf3c-176">Your specified settings will be applied and you will see a notification.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="2cf3c-177">Edit share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-177">Edit share</span></span>](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="2cf3c-178">Take a share offline</span><span class="sxs-lookup"><span data-stu-id="2cf3c-178">Take a share offline</span></span>

<span data-ttu-id="2cf3c-179">You may need to take a share offline when you are planning to modify it or delete it.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-179">You may need to take a share offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="2cf3c-180">When a share is offline, it is not available for read-write access.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="2cf3c-181">You will need to take the share offline on the host as well as on the device.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-181">You will need to take the share offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-share-offline"></a><span data-ttu-id="2cf3c-182">To take a share offline</span><span class="sxs-lookup"><span data-stu-id="2cf3c-182">To take a share offline</span></span>

1. <span data-ttu-id="2cf3c-183">Make sure that the share in question is not in use before taking it offline.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-183">Make sure that the share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="2cf3c-184">Take the share on the array offline by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="2cf3c-184">Take the share on the array offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="2cf3c-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span></span>

    2. <span data-ttu-id="2cf3c-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Offline share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="2cf3c-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="2cf3c-189">Click **Take offline** to take the share offline.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-189">Click **Take offline** to take the share offline.</span></span> <span data-ttu-id="2cf3c-190">You will see a notification of the operation in progress.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-190">You will see a notification of the operation in progress.</span></span>

    4. <span data-ttu-id="2cf3c-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span></span> <span data-ttu-id="2cf3c-192">You should see the status of the share as offline.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-192">You should see the status of the share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="2cf3c-193">Delete a share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cf3c-194">You can delete a share only if it is offline.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="2cf3c-195">Complete the following steps to delete a share.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-195">Complete the following steps to delete a share.</span></span>

#### <a name="to-delete-a-share"></a><span data-ttu-id="2cf3c-196">To delete a share</span><span class="sxs-lookup"><span data-stu-id="2cf3c-196">To delete a share</span></span>

1. <span data-ttu-id="2cf3c-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span></span>
2. <span data-ttu-id="2cf3c-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Delete share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="2cf3c-200">Check the status of the share you want to delete.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-200">Check the status of the share you want to delete.</span></span> <span data-ttu-id="2cf3c-201">If the share you want to delete is not offline, take it offline first.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-201">If the share you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="2cf3c-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="2cf3c-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="2cf3c-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="2cf3c-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cf3c-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="2cf3c-205">Next steps</span></span>
<span data-ttu-id="2cf3c-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="2cf3c-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>








