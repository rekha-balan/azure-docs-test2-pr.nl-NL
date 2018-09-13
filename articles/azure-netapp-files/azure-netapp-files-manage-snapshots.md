---
title: Manage snapshots by using Azure NetApp Files | Microsoft Docs
description: Describes how to create an on-demand snapshot for a volume or restore from a snapshot to a new volume by using Azure NetApp Files.
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
ms.topic: how-to-article
ms.date: 03/28/2018
ms.author: b-juche
ms.openlocfilehash: 48cb88b9815ba723d93c18caf63f33b50eea850c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865138"
---
# <a name="manage-snapshots-by-using-azure-netapp-files"></a><span data-ttu-id="799fa-103">Manage snapshots by using Azure NetApp Files</span><span class="sxs-lookup"><span data-stu-id="799fa-103">Manage snapshots by using Azure NetApp Files</span></span>
<span data-ttu-id="799fa-104">You can use Azure NetApp Files to create an on-demand snapshot for a volume or restore from a snapshot to a new volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-104">You can use Azure NetApp Files to create an on-demand snapshot for a volume or restore from a snapshot to a new volume.</span></span>

## <a name="create-an-on-demand-snapshot-for-a-volume"></a><span data-ttu-id="799fa-105">Create an on-demand snapshot for a volume</span><span class="sxs-lookup"><span data-stu-id="799fa-105">Create an on-demand snapshot for a volume</span></span>
<span data-ttu-id="799fa-106">You can create snapshots only on demand.</span><span class="sxs-lookup"><span data-stu-id="799fa-106">You can create snapshots only on demand.</span></span>  <span data-ttu-id="799fa-107">Snapshot policies are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="799fa-107">Snapshot policies are not currently supported.</span></span>  
1.  <span data-ttu-id="799fa-108">From the Manage Volume blade, click **Snapshots**, then click **+ Add snapshot** to create an on-demand snapshot for a volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-108">From the Manage Volume blade, click **Snapshots**, then click **+ Add snapshot** to create an on-demand snapshot for a volume.</span></span>

2.  <span data-ttu-id="799fa-109">In the New Snapshot window, provide a name for the new snapshot that you are creating.</span><span class="sxs-lookup"><span data-stu-id="799fa-109">In the New Snapshot window, provide a name for the new snapshot that you are creating.</span></span>   

3. <span data-ttu-id="799fa-110">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="799fa-110">Click **OK**.</span></span> 


## <a name="restore-a-snapshot-to-a-new-volume"></a><span data-ttu-id="799fa-111">Restore a snapshot to a new volume</span><span class="sxs-lookup"><span data-stu-id="799fa-111">Restore a snapshot to a new volume</span></span>
<span data-ttu-id="799fa-112">Currently, you can restore a snapshot only to a new volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-112">Currently, you can restore a snapshot only to a new volume.</span></span> 
1. <span data-ttu-id="799fa-113">Go to the **Manage Snapshots** blade from the Volume blade to display the snapshot list.</span><span class="sxs-lookup"><span data-stu-id="799fa-113">Go to the **Manage Snapshots** blade from the Volume blade to display the snapshot list.</span></span> 
2. <span data-ttu-id="799fa-114">Select a snapshot to restore.</span><span class="sxs-lookup"><span data-stu-id="799fa-114">Select a snapshot to restore.</span></span>  
3. <span data-ttu-id="799fa-115">Right-click the snapshot name and select **Restore to new volume** from the menu option.</span><span class="sxs-lookup"><span data-stu-id="799fa-115">Right-click the snapshot name and select **Restore to new volume** from the menu option.</span></span>  

    ![Restore snapshot to new volume](../media/azure-netapp-files/azure-netapp-files-snapshot-restore-to-new-volume.png)

4. <span data-ttu-id="799fa-117">In the New Volume window, provide information for the new volume:</span><span class="sxs-lookup"><span data-stu-id="799fa-117">In the New Volume window, provide information for the new volume:</span></span>  
    * <span data-ttu-id="799fa-118">**Name** </span><span class="sxs-lookup"><span data-stu-id="799fa-118">**Name** </span></span>  
        <span data-ttu-id="799fa-119">Specify the name for the volume that you are creating.</span><span class="sxs-lookup"><span data-stu-id="799fa-119">Specify the name for the volume that you are creating.</span></span>  
        
        <span data-ttu-id="799fa-120">The name must be unique within a resource group.</span><span class="sxs-lookup"><span data-stu-id="799fa-120">The name must be unique within a resource group.</span></span> <span data-ttu-id="799fa-121">It must be at least 3 characters long.</span><span class="sxs-lookup"><span data-stu-id="799fa-121">It must be at least 3 characters long.</span></span>  <span data-ttu-id="799fa-122">It can use any alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="799fa-122">It can use any alphanumeric characters.</span></span>

    * <span data-ttu-id="799fa-123">**File path**   </span><span class="sxs-lookup"><span data-stu-id="799fa-123">**File path**   </span></span>  
        <span data-ttu-id="799fa-124">Specify the file path that will be used to create the export path for the new volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-124">Specify the file path that will be used to create the export path for the new volume.</span></span> <span data-ttu-id="799fa-125">The export path is used to mount and access the volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-125">The export path is used to mount and access the volume.</span></span>   
        
        <span data-ttu-id="799fa-126">A mount target is the endpoint of the NFS service IP address.</span><span class="sxs-lookup"><span data-stu-id="799fa-126">A mount target is the endpoint of the NFS service IP address.</span></span> <span data-ttu-id="799fa-127">It is automatically generated.</span><span class="sxs-lookup"><span data-stu-id="799fa-127">It is automatically generated.</span></span>   
        
        <span data-ttu-id="799fa-128">The file path name can contain letters, numbers, and hyphens ("-") only.</span><span class="sxs-lookup"><span data-stu-id="799fa-128">The file path name can contain letters, numbers, and hyphens ("-") only.</span></span> <span data-ttu-id="799fa-129">It must be between 16 and 40 characters in length.</span><span class="sxs-lookup"><span data-stu-id="799fa-129">It must be between 16 and 40 characters in length.</span></span> 

    * <span data-ttu-id="799fa-130">**Quota**</span><span class="sxs-lookup"><span data-stu-id="799fa-130">**Quota**</span></span>  
        <span data-ttu-id="799fa-131">Specify the amount of logical storage that is allocated to the volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-131">Specify the amount of logical storage that is allocated to the volume.</span></span>  

        <span data-ttu-id="799fa-132">The **Available quota** field shows the amount of unused space in the chosen capacity pool that you can use towards creating a new volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-132">The **Available quota** field shows the amount of unused space in the chosen capacity pool that you can use towards creating a new volume.</span></span> <span data-ttu-id="799fa-133">The size of the new volume must not exceed the available quota.</span><span class="sxs-lookup"><span data-stu-id="799fa-133">The size of the new volume must not exceed the available quota.</span></span>

    *   <span data-ttu-id="799fa-134">**Virtual network**</span><span class="sxs-lookup"><span data-stu-id="799fa-134">**Virtual network**</span></span>  
        <span data-ttu-id="799fa-135">Specify the Azure virtual network (Vnet) from which you want to access the volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-135">Specify the Azure virtual network (Vnet) from which you want to access the volume.</span></span> 
        
        <span data-ttu-id="799fa-136">The Vnet you specify must have Azure NetApp Files configured.</span><span class="sxs-lookup"><span data-stu-id="799fa-136">The Vnet you specify must have Azure NetApp Files configured.</span></span> <span data-ttu-id="799fa-137">The Azure NetApp Files service can be accessed only from a Vnet that is in the same location as the volume.</span><span class="sxs-lookup"><span data-stu-id="799fa-137">The Azure NetApp Files service can be accessed only from a Vnet that is in the same location as the volume.</span></span>  

    ![Restored new volume](../media/azure-netapp-files/azure-netapp-files-snapshot-new-volume.png) 
    
5. <span data-ttu-id="799fa-139">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="799fa-139">Click **OK**.</span></span>   
    <span data-ttu-id="799fa-140">The new volume to which the snapshot is restored appears in the Volumes blade.</span><span class="sxs-lookup"><span data-stu-id="799fa-140">The new volume to which the snapshot is restored appears in the Volumes blade.</span></span>

