---
title: Create a volume for Azure NetApp Files | Microsoft Docs
description: Describes how to create a volume for Azure NetApp Files.
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''
ms.assetid: ''
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/28/2018
ms.author: b-juche
ms.openlocfilehash: 42e475f4da2102bb8b010daec6e6451ba7f13848
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871109"
---
# <a name="create-a-volume-for-azure-netapp-files"></a><span data-ttu-id="1fe20-103">Create a volume for Azure NetApp Files</span><span class="sxs-lookup"><span data-stu-id="1fe20-103">Create a volume for Azure NetApp Files</span></span>

<span data-ttu-id="1fe20-104">A volume's capacity consumption counts against its pool's provisioned capacity.</span><span class="sxs-lookup"><span data-stu-id="1fe20-104">A volume's capacity consumption counts against its pool's provisioned capacity.</span></span>  <span data-ttu-id="1fe20-105">You can create multiple volumes in a capacity pool, but the volumes' total capacity consumption must not exceed the pool size.</span><span class="sxs-lookup"><span data-stu-id="1fe20-105">You can create multiple volumes in a capacity pool, but the volumes' total capacity consumption must not exceed the pool size.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="1fe20-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1fe20-106">Before you begin</span></span> 
<span data-ttu-id="1fe20-107">You must have already set up a capacity pool.</span><span class="sxs-lookup"><span data-stu-id="1fe20-107">You must have already set up a capacity pool.</span></span>  

[<span data-ttu-id="1fe20-108">Set up a capacity pool</span><span class="sxs-lookup"><span data-stu-id="1fe20-108">Set up a capacity pool</span></span>](azure-netapp-files-set-up-capacity-pool.md)

## <a name="steps"></a><span data-ttu-id="1fe20-109">Steps</span><span class="sxs-lookup"><span data-stu-id="1fe20-109">Steps</span></span> 
1.  <span data-ttu-id="1fe20-110">Click the **Volumes** blade from the Manage Capacity Pools blade.</span><span class="sxs-lookup"><span data-stu-id="1fe20-110">Click the **Volumes** blade from the Manage Capacity Pools blade.</span></span> 
2.  <span data-ttu-id="1fe20-111">Click **+ Add volume** to create a volume.</span><span class="sxs-lookup"><span data-stu-id="1fe20-111">Click **+ Add volume** to create a volume.</span></span>  
    <span data-ttu-id="1fe20-112">The New Volume window appears.</span><span class="sxs-lookup"><span data-stu-id="1fe20-112">The New Volume window appears.</span></span>

3.  <span data-ttu-id="1fe20-113">In the New Volume window, click **Create** and provide information for the following fields:</span><span class="sxs-lookup"><span data-stu-id="1fe20-113">In the New Volume window, click **Create** and provide information for the following fields:</span></span>   
    * <span data-ttu-id="1fe20-114">**Name**    </span><span class="sxs-lookup"><span data-stu-id="1fe20-114">**Name**    </span></span>  
        <span data-ttu-id="1fe20-115">Specify the name for the volume that you are creating.</span><span class="sxs-lookup"><span data-stu-id="1fe20-115">Specify the name for the volume that you are creating.</span></span>   
        <span data-ttu-id="1fe20-116">The name must be unique within a resource group.</span><span class="sxs-lookup"><span data-stu-id="1fe20-116">The name must be unique within a resource group.</span></span> <span data-ttu-id="1fe20-117">It must be at least 3 characters long.</span><span class="sxs-lookup"><span data-stu-id="1fe20-117">It must be at least 3 characters long.</span></span>  <span data-ttu-id="1fe20-118">It can use any alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="1fe20-118">It can use any alphanumeric characters.</span></span>

    * <span data-ttu-id="1fe20-119">**File path**</span><span class="sxs-lookup"><span data-stu-id="1fe20-119">**File path**</span></span>  
        <span data-ttu-id="1fe20-120">Specify the file path that will be used to create the export path for the new volume.</span><span class="sxs-lookup"><span data-stu-id="1fe20-120">Specify the file path that will be used to create the export path for the new volume.</span></span> <span data-ttu-id="1fe20-121">The export path is used to mount and access the volume.</span><span class="sxs-lookup"><span data-stu-id="1fe20-121">The export path is used to mount and access the volume.</span></span>   
        <span data-ttu-id="1fe20-122">A mount target is the endpoint of the NFS service IP address.</span><span class="sxs-lookup"><span data-stu-id="1fe20-122">A mount target is the endpoint of the NFS service IP address.</span></span> <span data-ttu-id="1fe20-123">It is automatically generated.</span><span class="sxs-lookup"><span data-stu-id="1fe20-123">It is automatically generated.</span></span>    
        <span data-ttu-id="1fe20-124">The file path name can contain letters, numbers, and hyphens ("-") only.</span><span class="sxs-lookup"><span data-stu-id="1fe20-124">The file path name can contain letters, numbers, and hyphens ("-") only.</span></span> <span data-ttu-id="1fe20-125">It must be between 16 and 40 characters in length.</span><span class="sxs-lookup"><span data-stu-id="1fe20-125">It must be between 16 and 40 characters in length.</span></span>  

    * <span data-ttu-id="1fe20-126">**Quota**</span><span class="sxs-lookup"><span data-stu-id="1fe20-126">**Quota**</span></span>  
        <span data-ttu-id="1fe20-127">Specify the amount of logical storage that is allocated to the volume.</span><span class="sxs-lookup"><span data-stu-id="1fe20-127">Specify the amount of logical storage that is allocated to the volume.</span></span>  
        <span data-ttu-id="1fe20-128">The **Available quota** field shows the amount of unused space in the chosen capacity pool that you can use towards creating a new volume.</span><span class="sxs-lookup"><span data-stu-id="1fe20-128">The **Available quota** field shows the amount of unused space in the chosen capacity pool that you can use towards creating a new volume.</span></span> <span data-ttu-id="1fe20-129">The size of the new volume must not exceed the available quota.</span><span class="sxs-lookup"><span data-stu-id="1fe20-129">The size of the new volume must not exceed the available quota.</span></span>  

    * <span data-ttu-id="1fe20-130">**Virtual network**</span><span class="sxs-lookup"><span data-stu-id="1fe20-130">**Virtual network**</span></span>  
        <span data-ttu-id="1fe20-131">Specify the Azure virtual network (Vnet) from which you want to access the volume.</span><span class="sxs-lookup"><span data-stu-id="1fe20-131">Specify the Azure virtual network (Vnet) from which you want to access the volume.</span></span> <span data-ttu-id="1fe20-132">The Vnet you specify must have Azure NetApp Files configured.</span><span class="sxs-lookup"><span data-stu-id="1fe20-132">The Vnet you specify must have Azure NetApp Files configured.</span></span> <span data-ttu-id="1fe20-133">The Azure NetApp Files service can be accessed only from a Vnet that is in the same location as the volume.</span><span class="sxs-lookup"><span data-stu-id="1fe20-133">The Azure NetApp Files service can be accessed only from a Vnet that is in the same location as the volume.</span></span>   

    ![New volume](../media/azure-netapp-files/azure-netapp-files-new-volume.png)

4.  <span data-ttu-id="1fe20-135">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fe20-135">Click **OK**.</span></span> 
 
<span data-ttu-id="1fe20-136">A volume inherits subscription, resource group, location attributes from its capacity pool.</span><span class="sxs-lookup"><span data-stu-id="1fe20-136">A volume inherits subscription, resource group, location attributes from its capacity pool.</span></span> <span data-ttu-id="1fe20-137">To monitor the volume deployment status, you can use the Notifications tab.</span><span class="sxs-lookup"><span data-stu-id="1fe20-137">To monitor the volume deployment status, you can use the Notifications tab.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fe20-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="1fe20-138">Next steps</span></span>  
[<span data-ttu-id="1fe20-139">Configure export policy for a volume (optional)</span><span class="sxs-lookup"><span data-stu-id="1fe20-139">Configure export policy for a volume (optional)</span></span>](azure-netapp-files-configure-export-policy.md)

