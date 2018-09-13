---
title: Set up a capacity pool for Azure NetApp Files | Microsoft Docs
description: Describes how to set up a capacity pool so that you can create volumes within it.
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
ms.openlocfilehash: 0e9203f5b4e2a9043e242b804c82017cf6fc3ee1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968129"
---
# <a name="set-up-a-capacity-pool"></a><span data-ttu-id="a601b-103">Set up a capacity pool</span><span class="sxs-lookup"><span data-stu-id="a601b-103">Set up a capacity pool</span></span>
<span data-ttu-id="a601b-104">Setting up a capacity pool enables you to create volumes within it.</span><span class="sxs-lookup"><span data-stu-id="a601b-104">Setting up a capacity pool enables you to create volumes within it.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="a601b-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a601b-105">Before you begin</span></span> 
<span data-ttu-id="a601b-106">You must have already created a NetApp account.</span><span class="sxs-lookup"><span data-stu-id="a601b-106">You must have already created a NetApp account.</span></span>   

[<span data-ttu-id="a601b-107">Create a NetApp account</span><span class="sxs-lookup"><span data-stu-id="a601b-107">Create a NetApp account</span></span>](azure-netapp-files-create-netapp-account.md)

## <a name="steps"></a><span data-ttu-id="a601b-108">Steps</span><span class="sxs-lookup"><span data-stu-id="a601b-108">Steps</span></span> 

1. <span data-ttu-id="a601b-109">Go to the management blade for your NetApp account, and then, from the navigation pane, select **Capacity pools**.</span><span class="sxs-lookup"><span data-stu-id="a601b-109">Go to the management blade for your NetApp account, and then, from the navigation pane, select **Capacity pools**.</span></span>

2. <span data-ttu-id="a601b-110">Click **+ Add pools** to create a new capacity pool.</span><span class="sxs-lookup"><span data-stu-id="a601b-110">Click **+ Add pools** to create a new capacity pool.</span></span>   
    <span data-ttu-id="a601b-111">The New Capacity Pool window appears.</span><span class="sxs-lookup"><span data-stu-id="a601b-111">The New Capacity Pool window appears.</span></span>

3. <span data-ttu-id="a601b-112">Provide the following information for the new capacity pool:</span><span class="sxs-lookup"><span data-stu-id="a601b-112">Provide the following information for the new capacity pool:</span></span>  
  * <span data-ttu-id="a601b-113">**Name**</span><span class="sxs-lookup"><span data-stu-id="a601b-113">**Name**</span></span>  
    <span data-ttu-id="a601b-114">Specify the name for the capacity pool.</span><span class="sxs-lookup"><span data-stu-id="a601b-114">Specify the name for the capacity pool.</span></span>  
    <span data-ttu-id="a601b-115">The capacity pool name must be unique for each NetApp account.</span><span class="sxs-lookup"><span data-stu-id="a601b-115">The capacity pool name must be unique for each NetApp account.</span></span>

  * <span data-ttu-id="a601b-116">**Service level** </span><span class="sxs-lookup"><span data-stu-id="a601b-116">**Service level** </span></span>  
    <span data-ttu-id="a601b-117">This field shows the target performance for the capacity pool.</span><span class="sxs-lookup"><span data-stu-id="a601b-117">This field shows the target performance for the capacity pool.</span></span>  
    <span data-ttu-id="a601b-118">Currently, only the Premium service level is available.</span><span class="sxs-lookup"><span data-stu-id="a601b-118">Currently, only the Premium service level is available.</span></span> 

  *  <span data-ttu-id="a601b-119">**Size**   </span><span class="sxs-lookup"><span data-stu-id="a601b-119">**Size**   </span></span>  
      <span data-ttu-id="a601b-120">Specify the size of the capacity pool that you are purchasing.</span><span class="sxs-lookup"><span data-stu-id="a601b-120">Specify the size of the capacity pool that you are purchasing.</span></span>        
      <span data-ttu-id="a601b-121">The minimum capacity pool size is 4 TiB.</span><span class="sxs-lookup"><span data-stu-id="a601b-121">The minimum capacity pool size is 4 TiB.</span></span> <span data-ttu-id="a601b-122">You can create a pool with a size that is multiples of 4 TiB.</span><span class="sxs-lookup"><span data-stu-id="a601b-122">You can create a pool with a size that is multiples of 4 TiB.</span></span>   
      
      ![New capacity pool](../media/azure-netapp-files/azure-netapp-files-new-capacity-pool.png)

4. <span data-ttu-id="a601b-124">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a601b-124">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a601b-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="a601b-125">Next steps</span></span> 

1. [<span data-ttu-id="a601b-126">Create a volume for Azure NetApp Files</span><span class="sxs-lookup"><span data-stu-id="a601b-126">Create a volume for Azure NetApp Files</span></span>](azure-netapp-files-create-volumes.md)
2. [<span data-ttu-id="a601b-127">Configure export policy for a volume (optional)</span><span class="sxs-lookup"><span data-stu-id="a601b-127">Configure export policy for a volume (optional)</span></span>](azure-netapp-files-configure-export-policy.md)

