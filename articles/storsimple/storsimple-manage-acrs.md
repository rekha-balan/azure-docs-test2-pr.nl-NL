---
title: Manage access control records in StorSimple | Microsoft Docs
description: Describes how to use access control records (ACRs) to determine which hosts can connect to a volume on the StorSimple device.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553200"
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="f33b6-103">Use the StorSimple Manager service to manage access control records</span><span class="sxs-lookup"><span data-stu-id="f33b6-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="f33b6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f33b6-104">Overview</span></span>
<span data-ttu-id="f33b6-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="f33b6-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="f33b6-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span><span class="sxs-lookup"><span data-stu-id="f33b6-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="f33b6-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span><span class="sxs-lookup"><span data-stu-id="f33b6-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="f33b6-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span><span class="sxs-lookup"><span data-stu-id="f33b6-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="f33b6-109">This tutorial explains the following common ACR-related tasks:</span><span class="sxs-lookup"><span data-stu-id="f33b6-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="f33b6-110">Add an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-110">Add an access control record</span></span> 
* <span data-ttu-id="f33b6-111">Edit an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-111">Edit an access control record</span></span> 
* <span data-ttu-id="f33b6-112">Delete an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="f33b6-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span><span class="sxs-lookup"><span data-stu-id="f33b6-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="f33b6-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span><span class="sxs-lookup"><span data-stu-id="f33b6-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="f33b6-115">Add an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-115">Add an access control record</span></span>
<span data-ttu-id="f33b6-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span><span class="sxs-lookup"><span data-stu-id="f33b6-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="f33b6-117">Typically, you will associate one ACR with one volume.</span><span class="sxs-lookup"><span data-stu-id="f33b6-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="f33b6-118">Perform the following steps to add an ACR.</span><span class="sxs-lookup"><span data-stu-id="f33b6-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="f33b6-119">To add an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-119">To add an access control record</span></span>
1. <span data-ttu-id="f33b6-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="f33b6-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="f33b6-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span><span class="sxs-lookup"><span data-stu-id="f33b6-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="f33b6-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span><span class="sxs-lookup"><span data-stu-id="f33b6-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="f33b6-123">To get the IQN of your Windows Server host, do the following:</span><span class="sxs-lookup"><span data-stu-id="f33b6-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="f33b6-124">Start the Microsoft iSCSI initiator on your Windows host.</span><span class="sxs-lookup"><span data-stu-id="f33b6-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="f33b6-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span><span class="sxs-lookup"><span data-stu-id="f33b6-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="f33b6-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="f33b6-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="f33b6-127">Click **Save** to save the newly created ACR.</span><span class="sxs-lookup"><span data-stu-id="f33b6-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="f33b6-128">The tabular listing will be updated to reflect this addition.</span><span class="sxs-lookup"><span data-stu-id="f33b6-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="f33b6-129">Edit an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-129">Edit an access control record</span></span>
<span data-ttu-id="f33b6-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span><span class="sxs-lookup"><span data-stu-id="f33b6-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="f33b6-131">You can modify only those ACRs that are currently not in use.</span><span class="sxs-lookup"><span data-stu-id="f33b6-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="f33b6-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span><span class="sxs-lookup"><span data-stu-id="f33b6-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="f33b6-133">Perform the following steps to edit an ACR.</span><span class="sxs-lookup"><span data-stu-id="f33b6-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="f33b6-134">To edit an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-134">To edit an access control record</span></span>
1. <span data-ttu-id="f33b6-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="f33b6-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="f33b6-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span><span class="sxs-lookup"><span data-stu-id="f33b6-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="f33b6-137">Supply a new name and/or IQN for the ACR.</span><span class="sxs-lookup"><span data-stu-id="f33b6-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="f33b6-138">Click **Save** to save the modified ACR.</span><span class="sxs-lookup"><span data-stu-id="f33b6-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="f33b6-139">The tabular listing will be updated to reflect this change.</span><span class="sxs-lookup"><span data-stu-id="f33b6-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="f33b6-140">Delete an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-140">Delete an access control record</span></span>
<span data-ttu-id="f33b6-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span><span class="sxs-lookup"><span data-stu-id="f33b6-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="f33b6-142">You can delete only those ACRs that are currently not in use.</span><span class="sxs-lookup"><span data-stu-id="f33b6-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="f33b6-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span><span class="sxs-lookup"><span data-stu-id="f33b6-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="f33b6-144">Perform the following steps to delete an access control record.</span><span class="sxs-lookup"><span data-stu-id="f33b6-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="f33b6-145">To delete an access control record</span><span class="sxs-lookup"><span data-stu-id="f33b6-145">To delete an access control record</span></span>
1. <span data-ttu-id="f33b6-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="f33b6-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="f33b6-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="f33b6-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="f33b6-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span><span class="sxs-lookup"><span data-stu-id="f33b6-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="f33b6-149">Click the **x** icon to delete the ACR.</span><span class="sxs-lookup"><span data-stu-id="f33b6-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="f33b6-150">When prompted for confirmation, click **YES** to continue with the deletion.</span><span class="sxs-lookup"><span data-stu-id="f33b6-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="f33b6-151">The tabular listing will be updated to reflect the deletion.</span><span class="sxs-lookup"><span data-stu-id="f33b6-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f33b6-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="f33b6-152">Next steps</span></span>
* <span data-ttu-id="f33b6-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="f33b6-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="f33b6-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f33b6-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

