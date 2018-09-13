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
# <a name="use-storsimple-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="d8540-103">Use StorSimple Manager to manage access control records for StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="d8540-103">Use StorSimple Manager to manage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="d8540-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d8540-104">Overview</span></span>
<span data-ttu-id="d8540-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span><span class="sxs-lookup"><span data-stu-id="d8540-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span></span> <span data-ttu-id="d8540-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span><span class="sxs-lookup"><span data-stu-id="d8540-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="d8540-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span><span class="sxs-lookup"><span data-stu-id="d8540-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span></span> <span data-ttu-id="d8540-108">The **access control records** section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span><span class="sxs-lookup"><span data-stu-id="d8540-108">The **access control records** section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="d8540-109">This tutorial explains the following common ACR-related tasks:</span><span class="sxs-lookup"><span data-stu-id="d8540-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="d8540-110">Get the IQN</span><span class="sxs-lookup"><span data-stu-id="d8540-110">Get the IQN</span></span>
* <span data-ttu-id="d8540-111">Add an access control record</span><span class="sxs-lookup"><span data-stu-id="d8540-111">Add an access control record</span></span> 
* <span data-ttu-id="d8540-112">Edit an access control record</span><span class="sxs-lookup"><span data-stu-id="d8540-112">Edit an access control record</span></span> 
* <span data-ttu-id="d8540-113">Delete an access control record</span><span class="sxs-lookup"><span data-stu-id="d8540-113">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="d8540-114">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span><span class="sxs-lookup"><span data-stu-id="d8540-114">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="d8540-115">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span><span class="sxs-lookup"><span data-stu-id="d8540-115">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="get-the-iqn"></a><span data-ttu-id="d8540-116">Get the IQN</span><span class="sxs-lookup"><span data-stu-id="d8540-116">Get the IQN</span></span>
<span data-ttu-id="d8540-117">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="d8540-117">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="d8540-118">Add an ACR</span><span class="sxs-lookup"><span data-stu-id="d8540-118">Add an ACR</span></span>
<span data-ttu-id="d8540-119">You use the StorSimple Manager service **Configuration** page to add ACRs.</span><span class="sxs-lookup"><span data-stu-id="d8540-119">You use the StorSimple Manager service **Configuration** page to add ACRs.</span></span> <span data-ttu-id="d8540-120">Typically, you will associate one ACR with one volume.</span><span class="sxs-lookup"><span data-stu-id="d8540-120">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="d8540-121">For information about associating an ACR with a volume, go to [add a volume](storsimple-ova-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="d8540-121">For information about associating an ACR with a volume, go to [add a volume](storsimple-ova-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8540-122">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span><span class="sxs-lookup"><span data-stu-id="d8540-122">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> 
> 

<span data-ttu-id="d8540-123">Perform the following steps to add an ACR.</span><span class="sxs-lookup"><span data-stu-id="d8540-123">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="d8540-124">To add an ACR</span><span class="sxs-lookup"><span data-stu-id="d8540-124">To add an ACR</span></span>
1. <span data-ttu-id="d8540-125">On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.</span><span class="sxs-lookup"><span data-stu-id="d8540-125">On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.</span></span>
   
    ![configuration tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/acr1.png)
2. <span data-ttu-id="d8540-127">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span><span class="sxs-lookup"><span data-stu-id="d8540-127">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="d8540-128">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span><span class="sxs-lookup"><span data-stu-id="d8540-128">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span></span> 
4. <span data-ttu-id="d8540-129">Click **Save** at the bottom of the page to save the newly created ACR.</span><span class="sxs-lookup"><span data-stu-id="d8540-129">Click **Save** at the bottom of the page to save the newly created ACR.</span></span> <span data-ttu-id="d8540-130">You will see the following confirmation message.</span><span class="sxs-lookup"><span data-stu-id="d8540-130">You will see the following confirmation message.</span></span>
   
    ![confirmation message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/acr2.png)
5. <span data-ttu-id="d8540-132">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="d8540-132">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/check-icon.png)<span data-ttu-id="d8540-134">.</span><span class="sxs-lookup"><span data-stu-id="d8540-134">.</span></span> <span data-ttu-id="d8540-135">The tabular listing will be updated to reflect this addition.</span><span class="sxs-lookup"><span data-stu-id="d8540-135">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="d8540-136">Edit an ACR</span><span class="sxs-lookup"><span data-stu-id="d8540-136">Edit an ACR</span></span>
<span data-ttu-id="d8540-137">You use the **Configuration** page in the Azure classic portal to edit ACRs.</span><span class="sxs-lookup"><span data-stu-id="d8540-137">You use the **Configuration** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="d8540-138">You should modify only those ACRs that are currently not in use.</span><span class="sxs-lookup"><span data-stu-id="d8540-138">You should modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="d8540-139">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span><span class="sxs-lookup"><span data-stu-id="d8540-139">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="d8540-140">Perform the following steps to edit an ACR.</span><span class="sxs-lookup"><span data-stu-id="d8540-140">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-acr"></a><span data-ttu-id="d8540-141">To edit an ACR</span><span class="sxs-lookup"><span data-stu-id="d8540-141">To edit an ACR</span></span>
1. <span data-ttu-id="d8540-142">On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.</span><span class="sxs-lookup"><span data-stu-id="d8540-142">On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.</span></span>
2. <span data-ttu-id="d8540-143">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span><span class="sxs-lookup"><span data-stu-id="d8540-143">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="d8540-144">Supply a new name and/or IQN for the ACR.</span><span class="sxs-lookup"><span data-stu-id="d8540-144">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="d8540-145">Click **Save** at the bottom of the page to save the modified ACR.</span><span class="sxs-lookup"><span data-stu-id="d8540-145">Click **Save** at the bottom of the page to save the modified ACR.</span></span> <span data-ttu-id="d8540-146">You will see a confirmation message.</span><span class="sxs-lookup"><span data-stu-id="d8540-146">You will see a confirmation message.</span></span> 
5. <span data-ttu-id="d8540-147">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="d8540-147">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/check-icon.png)<span data-ttu-id="d8540-149">.</span><span class="sxs-lookup"><span data-stu-id="d8540-149">.</span></span> <span data-ttu-id="d8540-150">The tabular listing will be updated to reflect this change.</span><span class="sxs-lookup"><span data-stu-id="d8540-150">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="d8540-151">Delete an access control record</span><span class="sxs-lookup"><span data-stu-id="d8540-151">Delete an access control record</span></span>
<span data-ttu-id="d8540-152">You use the **Configuration** page in the Azure classic portal to delete ACRs.</span><span class="sxs-lookup"><span data-stu-id="d8540-152">You use the **Configuration** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> * <span data-ttu-id="d8540-153">You should delete only those ACRs that are currently not in use.</span><span class="sxs-lookup"><span data-stu-id="d8540-153">You should delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="d8540-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span><span class="sxs-lookup"><span data-stu-id="d8540-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> * <span data-ttu-id="d8540-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span><span class="sxs-lookup"><span data-stu-id="d8540-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

<span data-ttu-id="d8540-156">Perform the following steps to delete an access control record.</span><span class="sxs-lookup"><span data-stu-id="d8540-156">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="d8540-157">To delete an access control record</span><span class="sxs-lookup"><span data-stu-id="d8540-157">To delete an access control record</span></span>
1. <span data-ttu-id="d8540-158">On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.</span><span class="sxs-lookup"><span data-stu-id="d8540-158">On the service landing page, select your service, double-click the service name, and then click the **Configuration** tab.</span></span>
2. <span data-ttu-id="d8540-159">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="d8540-159">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="d8540-160">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span><span class="sxs-lookup"><span data-stu-id="d8540-160">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="d8540-161">Click the **x** icon to delete the ACR.</span><span class="sxs-lookup"><span data-stu-id="d8540-161">Click the **x** icon to delete the ACR.</span></span> <span data-ttu-id="d8540-162">You will see the following confirmation message.</span><span class="sxs-lookup"><span data-stu-id="d8540-162">You will see the following confirmation message.</span></span>
   
    ![confirmation message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/acr3.png)
4. <span data-ttu-id="d8540-164">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="d8540-164">Click the check icon</span></span> ![check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-manage-acrs/check-icon.png)<span data-ttu-id="d8540-166">.</span><span class="sxs-lookup"><span data-stu-id="d8540-166">.</span></span> <span data-ttu-id="d8540-167">The tabular listing will be updated to reflect the deletion.</span><span class="sxs-lookup"><span data-stu-id="d8540-167">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8540-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8540-168">Next steps</span></span>
* <span data-ttu-id="d8540-169">Learn more about [adding volumes and configuring ACRs](storsimple-ova-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="d8540-169">Learn more about [adding volumes and configuring ACRs](storsimple-ova-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>







