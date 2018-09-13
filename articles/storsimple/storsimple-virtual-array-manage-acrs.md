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
ms.openlocfilehash: c70000cc3ac2c5a2e95104b47ce0982505adb6d1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564401"
---
# <a name="use-storsimple-device-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="bc79f-103">Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="bc79f-103">Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="bc79f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bc79f-104">Overview</span></span>

<span data-ttu-id="bc79f-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span><span class="sxs-lookup"><span data-stu-id="bc79f-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span></span> <span data-ttu-id="bc79f-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span><span class="sxs-lookup"><span data-stu-id="bc79f-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="bc79f-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span><span class="sxs-lookup"><span data-stu-id="bc79f-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span></span> <span data-ttu-id="bc79f-108">The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.</span><span class="sxs-lookup"><span data-stu-id="bc79f-108">The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.</span></span>

![Manage access control records](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="bc79f-110">This tutorial explains the following common ACR-related tasks:</span><span class="sxs-lookup"><span data-stu-id="bc79f-110">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="bc79f-111">Get the IQN</span><span class="sxs-lookup"><span data-stu-id="bc79f-111">Get the IQN</span></span>
* <span data-ttu-id="bc79f-112">Add an access control record</span><span class="sxs-lookup"><span data-stu-id="bc79f-112">Add an access control record</span></span>
* <span data-ttu-id="bc79f-113">Edit an access control record</span><span class="sxs-lookup"><span data-stu-id="bc79f-113">Edit an access control record</span></span>
* <span data-ttu-id="bc79f-114">Delete an access control record</span><span class="sxs-lookup"><span data-stu-id="bc79f-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="bc79f-115">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span><span class="sxs-lookup"><span data-stu-id="bc79f-115">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="bc79f-116">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span><span class="sxs-lookup"><span data-stu-id="bc79f-116">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


## <a name="get-the-iqn"></a><span data-ttu-id="bc79f-117">Get the IQN</span><span class="sxs-lookup"><span data-stu-id="bc79f-117">Get the IQN</span></span>

<span data-ttu-id="bc79f-118">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="bc79f-118">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="bc79f-119">Add an ACR</span><span class="sxs-lookup"><span data-stu-id="bc79f-119">Add an ACR</span></span>

<span data-ttu-id="bc79f-120">You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs.</span><span class="sxs-lookup"><span data-stu-id="bc79f-120">You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs.</span></span> <span data-ttu-id="bc79f-121">Typically, you associate one ACR with one volume.</span><span class="sxs-lookup"><span data-stu-id="bc79f-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="bc79f-122">For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="bc79f-122">For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc79f-123">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span><span class="sxs-lookup"><span data-stu-id="bc79f-123">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>


<span data-ttu-id="bc79f-124">Perform the following steps to add an ACR.</span><span class="sxs-lookup"><span data-stu-id="bc79f-124">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="bc79f-125">To add an ACR</span><span class="sxs-lookup"><span data-stu-id="bc79f-125">To add an ACR</span></span>

1. <span data-ttu-id="bc79f-126">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="bc79f-126">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="bc79f-127">In the **Access control records** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="bc79f-127">In the **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="bc79f-128">In the **Add ACR** blade, do the following:</span><span class="sxs-lookup"><span data-stu-id="bc79f-128">In the **Add ACR** blade, do the following:</span></span>
   
    1. <span data-ttu-id="bc79f-129">Supply a **Name** for your ACR.</span><span class="sxs-lookup"><span data-stu-id="bc79f-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="bc79f-130">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span><span class="sxs-lookup"><span data-stu-id="bc79f-130">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span></span> <span data-ttu-id="bc79f-131">To get the IQN of your Windows Server host, do the following:</span><span class="sxs-lookup"><span data-stu-id="bc79f-131">To get the IQN of your Windows Server host, do the following:</span></span>
   
    3. <span data-ttu-id="bc79f-132">Start the Microsoft iSCSI initiator on your Windows host.</span><span class="sxs-lookup"><span data-stu-id="bc79f-132">Start the Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="bc79f-133">In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span><span class="sxs-lookup"><span data-stu-id="bc79f-133">In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
    <span data-ttu-id="bc79f-134">Paste this string in the **IQN** field in the **Add ACR** blade.</span><span class="sxs-lookup"><span data-stu-id="bc79f-134">Paste this string in the **IQN** field in the **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="bc79f-135">Click **Add** to add the ACR.</span><span class="sxs-lookup"><span data-stu-id="bc79f-135">Click **Add** to add the ACR.</span></span>  
   
        ![Add access control records](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="bc79f-137">The tabular listing is updated to reflect this addition.</span><span class="sxs-lookup"><span data-stu-id="bc79f-137">The tabular listing is updated to reflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="bc79f-138">Edit an ACR</span><span class="sxs-lookup"><span data-stu-id="bc79f-138">Edit an ACR</span></span>

<span data-ttu-id="bc79f-139">You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.</span><span class="sxs-lookup"><span data-stu-id="bc79f-139">You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="bc79f-140">You should not modify an ACR that is currently in use.</span><span class="sxs-lookup"><span data-stu-id="bc79f-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="bc79f-141">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span><span class="sxs-lookup"><span data-stu-id="bc79f-141">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>


<span data-ttu-id="bc79f-142">Perform the following steps to edit an ACR.</span><span class="sxs-lookup"><span data-stu-id="bc79f-142">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-acr"></a><span data-ttu-id="bc79f-143">To edit an ACR</span><span class="sxs-lookup"><span data-stu-id="bc79f-143">To edit an ACR</span></span>

1. <span data-ttu-id="bc79f-144">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="bc79f-144">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="bc79f-145">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.</span><span class="sxs-lookup"><span data-stu-id="bc79f-145">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="bc79f-146">In the **Edit access control records** blade, do the following:</span><span class="sxs-lookup"><span data-stu-id="bc79f-146">In the **Edit access control records** blade, do the following:</span></span>
   
    1. <span data-ttu-id="bc79f-147">Supply the IQN for the ACR.</span><span class="sxs-lookup"><span data-stu-id="bc79f-147">Supply the IQN for the ACR.</span></span>
   
    2. <span data-ttu-id="bc79f-148">Click **Save** at the top of the blade to save the modified ACR.</span><span class="sxs-lookup"><span data-stu-id="bc79f-148">Click **Save** at the top of the blade to save the modified ACR.</span></span> <span data-ttu-id="bc79f-149">You see the following confirmation message:</span><span class="sxs-lookup"><span data-stu-id="bc79f-149">You see the following confirmation message:</span></span>
   
        ![Edit access control records](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="bc79f-151">Delete an access control record</span><span class="sxs-lookup"><span data-stu-id="bc79f-151">Delete an access control record</span></span>

<span data-ttu-id="bc79f-152">You use the **Configuration** page in the Azure portal to delete ACRs.</span><span class="sxs-lookup"><span data-stu-id="bc79f-152">You use the **Configuration** page in the Azure portal to delete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="bc79f-153">You should not delete an ACR that is currently in use.</span><span class="sxs-lookup"><span data-stu-id="bc79f-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="bc79f-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span><span class="sxs-lookup"><span data-stu-id="bc79f-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> * <span data-ttu-id="bc79f-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span><span class="sxs-lookup"><span data-stu-id="bc79f-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="bc79f-156">Perform the following steps to delete an access control record.</span><span class="sxs-lookup"><span data-stu-id="bc79f-156">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="bc79f-157">To delete an access control record</span><span class="sxs-lookup"><span data-stu-id="bc79f-157">To delete an access control record</span></span>

1. <span data-ttu-id="bc79f-158">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="bc79f-158">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="bc79f-159">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="bc79f-159">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.</span></span>

3. <span data-ttu-id="bc79f-160">In the Edit access control records blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="bc79f-160">In the Edit access control records blade, click **Delete**.</span></span>
   
    ![Delete ACRS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="bc79f-162">When prompted for confirmation, click **Delete** to continue with the deletion.</span><span class="sxs-lookup"><span data-stu-id="bc79f-162">When prompted for confirmation, click **Delete** to continue with the deletion.</span></span> <span data-ttu-id="bc79f-163">The tabular listing is updated to reflect the deletion.</span><span class="sxs-lookup"><span data-stu-id="bc79f-163">The tabular listing is updated to reflect the deletion.</span></span>
   
   ![Warning message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="bc79f-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc79f-165">Next steps</span></span>

* <span data-ttu-id="bc79f-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="bc79f-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>






