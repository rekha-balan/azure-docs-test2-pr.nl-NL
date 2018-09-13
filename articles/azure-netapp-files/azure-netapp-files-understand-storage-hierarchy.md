---
title: Understand the storage hierarchy of Azure NetApp Files | Microsoft Docs
description: Describes the storage hierarchy, including Azure NetApp Files accounts, capacity pools, and volumes.
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
ms.openlocfilehash: 6f5ed4e7ede9a098d69b7a40f44dd60f9b400472
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869027"
---
# <a name="understand-the-storage-hierarchy-of-azure-netapp-files"></a><span data-ttu-id="01991-103">Understand the storage hierarchy of Azure NetApp Files</span><span class="sxs-lookup"><span data-stu-id="01991-103">Understand the storage hierarchy of Azure NetApp Files</span></span>

<span data-ttu-id="01991-104">Before creating a volume in Azure NetApp Files, you must purchase and set up a pool for provisioned capacity.</span><span class="sxs-lookup"><span data-stu-id="01991-104">Before creating a volume in Azure NetApp Files, you must purchase and set up a pool for provisioned capacity.</span></span>  <span data-ttu-id="01991-105">To set up a capacity pool, you must have a NetApp account.</span><span class="sxs-lookup"><span data-stu-id="01991-105">To set up a capacity pool, you must have a NetApp account.</span></span> <span data-ttu-id="01991-106">Understanding the storage hierarchy helps you set up and manage your Azure NetApp Files resources.</span><span class="sxs-lookup"><span data-stu-id="01991-106">Understanding the storage hierarchy helps you set up and manage your Azure NetApp Files resources.</span></span>

## <a name="azure_netapp_files_account"></a><span data-ttu-id="01991-107">NetApp accounts</span><span class="sxs-lookup"><span data-stu-id="01991-107">NetApp accounts</span></span>

- <span data-ttu-id="01991-108">A NetApp account serves as an administrative grouping of the constituent capacity pools.</span><span class="sxs-lookup"><span data-stu-id="01991-108">A NetApp account serves as an administrative grouping of the constituent capacity pools.</span></span>  
- <span data-ttu-id="01991-109">A NetApp account is not the same as your general Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="01991-109">A NetApp account is not the same as your general Azure storage account.</span></span> 
- <span data-ttu-id="01991-110">A NetApp account is regional in scope.</span><span class="sxs-lookup"><span data-stu-id="01991-110">A NetApp account is regional in scope.</span></span>   
- <span data-ttu-id="01991-111">You can have multiple NetApp accounts in a region, but each NetApp account is tied to only a single region.</span><span class="sxs-lookup"><span data-stu-id="01991-111">You can have multiple NetApp accounts in a region, but each NetApp account is tied to only a single region.</span></span>

## <a name="capacity_pools"></a><span data-ttu-id="01991-112">Capacity pools</span><span class="sxs-lookup"><span data-stu-id="01991-112">Capacity pools</span></span>

- <span data-ttu-id="01991-113">A capacity pool is measured by its provisioned capacity.</span><span class="sxs-lookup"><span data-stu-id="01991-113">A capacity pool is measured by its provisioned capacity.</span></span>  
- <span data-ttu-id="01991-114">The capacity is provisioned by the fixed SKUs that you purchased (for example, a 4-TB capacity).</span><span class="sxs-lookup"><span data-stu-id="01991-114">The capacity is provisioned by the fixed SKUs that you purchased (for example, a 4-TB capacity).</span></span>
- <span data-ttu-id="01991-115">A capacity pool can have only one service level.</span><span class="sxs-lookup"><span data-stu-id="01991-115">A capacity pool can have only one service level.</span></span>  
  <span data-ttu-id="01991-116">Currently, only the Premium service level is available.</span><span class="sxs-lookup"><span data-stu-id="01991-116">Currently, only the Premium service level is available.</span></span>
- <span data-ttu-id="01991-117">Each capacity pool belongs to only one NetApp account.</span><span class="sxs-lookup"><span data-stu-id="01991-117">Each capacity pool belongs to only one NetApp account.</span></span>  
- <span data-ttu-id="01991-118">A capacity pool cannot be moved across NetApp accounts.</span><span class="sxs-lookup"><span data-stu-id="01991-118">A capacity pool cannot be moved across NetApp accounts.</span></span>   
  <span data-ttu-id="01991-119">For example, in the [Conceptual diagram of storage hierarchy](#conceptual_diagram_of_storage_hierarchy) below, Capacity Pool 1 cannot be moved from US East NetApp account to US West 2 NetApp account.</span><span class="sxs-lookup"><span data-stu-id="01991-119">For example, in the [Conceptual diagram of storage hierarchy](#conceptual_diagram_of_storage_hierarchy) below, Capacity Pool 1 cannot be moved from US East NetApp account to US West 2 NetApp account.</span></span>  

## <a name="volumes"></a><span data-ttu-id="01991-120">Volumes</span><span class="sxs-lookup"><span data-stu-id="01991-120">Volumes</span></span>

- <span data-ttu-id="01991-121">A volume is measured by logical capacity consumption and is scalable up to 100 TB per volume.</span><span class="sxs-lookup"><span data-stu-id="01991-121">A volume is measured by logical capacity consumption and is scalable up to 100 TB per volume.</span></span>
- <span data-ttu-id="01991-122">A volume's capacity consumption counts against its pool's provisioned capacity.</span><span class="sxs-lookup"><span data-stu-id="01991-122">A volume's capacity consumption counts against its pool's provisioned capacity.</span></span>
- <span data-ttu-id="01991-123">Each volume belongs to only one pool, but a pool can contain multiple volumes.</span><span class="sxs-lookup"><span data-stu-id="01991-123">Each volume belongs to only one pool, but a pool can contain multiple volumes.</span></span> 
- <span data-ttu-id="01991-124">Within the same NetApp account, you can move a volume across pools.</span><span class="sxs-lookup"><span data-stu-id="01991-124">Within the same NetApp account, you can move a volume across pools.</span></span>    
  <span data-ttu-id="01991-125">For example, in the [Conceptual diagram of storage hierarchy](#conceptual_diagram_of_storage_hierarchy) below, you can move the volumes from Capacity Pool 1 to Capacity Pool 2.</span><span class="sxs-lookup"><span data-stu-id="01991-125">For example, in the [Conceptual diagram of storage hierarchy](#conceptual_diagram_of_storage_hierarchy) below, you can move the volumes from Capacity Pool 1 to Capacity Pool 2.</span></span>

## <a name="conceptual_diagram_of_storage_hierarchy"></a><span data-ttu-id="01991-126">Conceptual diagram of storage hierarchy</span><span class="sxs-lookup"><span data-stu-id="01991-126">Conceptual diagram of storage hierarchy</span></span> 
<span data-ttu-id="01991-127">The following example shows the relationships of the Azure subscription, NetApp accounts, capacity pools,  and volumes.</span><span class="sxs-lookup"><span data-stu-id="01991-127">The following example shows the relationships of the Azure subscription, NetApp accounts, capacity pools,  and volumes.</span></span>   

![Conceptual diagram of storage hierarchy](../media/azure-netapp-files/azure-netapp-files-storage-hierarchy.png)

## <a name="next-steps"></a><span data-ttu-id="01991-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="01991-129">Next steps</span></span>

1. [<span data-ttu-id="01991-130">Create a NetApp account</span><span class="sxs-lookup"><span data-stu-id="01991-130">Create a NetApp account</span></span>](azure-netapp-files-create-netapp-account.md)
2. [<span data-ttu-id="01991-131">Set up a capacity pool</span><span class="sxs-lookup"><span data-stu-id="01991-131">Set up a capacity pool</span></span>](azure-netapp-files-set-up-capacity-pool.md)
3. [<span data-ttu-id="01991-132">Create a volume for Azure NetApp Files</span><span class="sxs-lookup"><span data-stu-id="01991-132">Create a volume for Azure NetApp Files</span></span>](azure-netapp-files-create-volumes.md)
4. [<span data-ttu-id="01991-133">Configure export policy for a volume (optional)</span><span class="sxs-lookup"><span data-stu-id="01991-133">Configure export policy for a volume (optional)</span></span>](azure-netapp-files-configure-export-policy.md)