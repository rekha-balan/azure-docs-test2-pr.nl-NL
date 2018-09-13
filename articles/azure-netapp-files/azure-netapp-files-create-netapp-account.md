---
title: Create a NetApp account for Access Azure NetApp Files | Microsoft Docs
description: Describes how to access Azure NetApp Files and create a NetApp account so that you can set up a capacity pool and create a volume.
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
ms.openlocfilehash: ad8cc550ce69e4dc4c19a569718fa873a65b3620
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868293"
---
# <a name="create-a-netapp-account"></a><span data-ttu-id="dba06-103">Create a NetApp account</span><span class="sxs-lookup"><span data-stu-id="dba06-103">Create a NetApp account</span></span>
<span data-ttu-id="dba06-104">Creating a NetApp account enables you to set up a capacity pool and subsequently create a volume.</span><span class="sxs-lookup"><span data-stu-id="dba06-104">Creating a NetApp account enables you to set up a capacity pool and subsequently create a volume.</span></span> <span data-ttu-id="dba06-105">You use the Azure NetApp Files blade to create a new NetApp account.</span><span class="sxs-lookup"><span data-stu-id="dba06-105">You use the Azure NetApp Files blade to create a new NetApp account.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dba06-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="dba06-106">Before you begin</span></span>
<span data-ttu-id="dba06-107">You must have been whitelisted for accessing the Microsoft.NetApp Azure Resource Provider and configured for using the Azure NetApp Files service.</span><span class="sxs-lookup"><span data-stu-id="dba06-107">You must have been whitelisted for accessing the Microsoft.NetApp Azure Resource Provider and configured for using the Azure NetApp Files service.</span></span>  

<span data-ttu-id="dba06-108">[Azure NetApp Files Public Preview signup page](https://aka.ms/nfspublicpreview).</span><span class="sxs-lookup"><span data-stu-id="dba06-108">[Azure NetApp Files Public Preview signup page](https://aka.ms/nfspublicpreview).</span></span> 

## <a name="steps"></a><span data-ttu-id="dba06-109">Steps</span><span class="sxs-lookup"><span data-stu-id="dba06-109">Steps</span></span> 

1. <span data-ttu-id="dba06-110">Locate the preview Azure portal URL from your preview invitation, and log in to the portal.</span><span class="sxs-lookup"><span data-stu-id="dba06-110">Locate the preview Azure portal URL from your preview invitation, and log in to the portal.</span></span> 
2.  <span data-ttu-id="dba06-111">Access the Azure NetApp Files blade by using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="dba06-111">Access the Azure NetApp Files blade by using one of the following methods:</span></span>  
  * <span data-ttu-id="dba06-112">Search for **Azure NetApp Files** in the Azure portal search box.</span><span class="sxs-lookup"><span data-stu-id="dba06-112">Search for **Azure NetApp Files** in the Azure portal search box.</span></span>  
  * <span data-ttu-id="dba06-113">Click **All services** in the navigation, and then filter to Azure NetApp Files.</span><span class="sxs-lookup"><span data-stu-id="dba06-113">Click **All services** in the navigation, and then filter to Azure NetApp Files.</span></span>  

  <span data-ttu-id="dba06-114">You can "favorite" the Azure NetApp Files blade by clicking the star icon next to it.</span><span class="sxs-lookup"><span data-stu-id="dba06-114">You can "favorite" the Azure NetApp Files blade by clicking the star icon next to it.</span></span> 

3. <span data-ttu-id="dba06-115">Click **+ Add** to create a new NetApp account.</span><span class="sxs-lookup"><span data-stu-id="dba06-115">Click **+ Add** to create a new NetApp account.</span></span>  
  <span data-ttu-id="dba06-116">The New NetApp account window appears.</span><span class="sxs-lookup"><span data-stu-id="dba06-116">The New NetApp account window appears.</span></span>  

4. <span data-ttu-id="dba06-117">Provide the following information for your NetApp account:</span><span class="sxs-lookup"><span data-stu-id="dba06-117">Provide the following information for your NetApp account:</span></span> 
  * <span data-ttu-id="dba06-118">**Account name**</span><span class="sxs-lookup"><span data-stu-id="dba06-118">**Account name**</span></span>  
    <span data-ttu-id="dba06-119">Specify a unique name for the subscription.</span><span class="sxs-lookup"><span data-stu-id="dba06-119">Specify a unique name for the subscription.</span></span>
  *  <span data-ttu-id="dba06-120">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="dba06-120">**Subscription**</span></span>  
    <span data-ttu-id="dba06-121">Select a subscription from your existing subscriptions.</span><span class="sxs-lookup"><span data-stu-id="dba06-121">Select a subscription from your existing subscriptions.</span></span>
  * <span data-ttu-id="dba06-122">**Resource group** </span><span class="sxs-lookup"><span data-stu-id="dba06-122">**Resource group** </span></span>  
    <span data-ttu-id="dba06-123">Use an existing Resource Group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="dba06-123">Use an existing Resource Group or create a new one.</span></span>
  * <span data-ttu-id="dba06-124">**Location**</span><span class="sxs-lookup"><span data-stu-id="dba06-124">**Location**</span></span>  
    <span data-ttu-id="dba06-125">Select the region where you want the account and its child resources to be located.</span><span class="sxs-lookup"><span data-stu-id="dba06-125">Select the region where you want the account and its child resources to be located.</span></span>  
    <span data-ttu-id="dba06-126">Currently, the Azure NetApp Files service is supported only in the US East region.</span><span class="sxs-lookup"><span data-stu-id="dba06-126">Currently, the Azure NetApp Files service is supported only in the US East region.</span></span>  

    ![New NetApp account](../media/azure-netapp-files/azure-netapp-files-new-netapp-account.png)


5. <span data-ttu-id="dba06-128">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dba06-128">Click **Create**.</span></span>     
  <span data-ttu-id="dba06-129">The NetApp account you created now appears in the Azure NetApp Files blade.</span><span class="sxs-lookup"><span data-stu-id="dba06-129">The NetApp account you created now appears in the Azure NetApp Files blade.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dba06-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="dba06-130">Next steps</span></span>  

1. [<span data-ttu-id="dba06-131">Set up a capacity pool</span><span class="sxs-lookup"><span data-stu-id="dba06-131">Set up a capacity pool</span></span>](azure-netapp-files-set-up-capacity-pool.md)
2. [<span data-ttu-id="dba06-132">Create a volume for Azure NetApp Files</span><span class="sxs-lookup"><span data-stu-id="dba06-132">Create a volume for Azure NetApp Files</span></span>](azure-netapp-files-create-volumes.md)
3. [<span data-ttu-id="dba06-133">Configure export policy for a volume (optional)</span><span class="sxs-lookup"><span data-stu-id="dba06-133">Configure export policy for a volume (optional)</span></span>](azure-netapp-files-configure-export-policy.md)
