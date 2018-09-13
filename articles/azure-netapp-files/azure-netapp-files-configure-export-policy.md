---
title: Configure export policy for an Azure NetApp Files volume | Microsoft Docs
description: Describes how to configure export policy to control access to an Azure NetApp Files volume
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
ms.openlocfilehash: 08de7e2ca8cd993a0931f5b16cb9d6c9a04e53dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865574"
---
# <a name="configure-export-policy-for-a-volume-optional"></a><span data-ttu-id="82fc0-103">Configure export policy for a volume (optional)</span><span class="sxs-lookup"><span data-stu-id="82fc0-103">Configure export policy for a volume (optional)</span></span>

<span data-ttu-id="82fc0-104">You can optionally configure export policy to control access to an Azure NetApp Files volume.</span><span class="sxs-lookup"><span data-stu-id="82fc0-104">You can optionally configure export policy to control access to an Azure NetApp Files volume.</span></span> 

## <a name="steps"></a><span data-ttu-id="82fc0-105">Steps</span><span class="sxs-lookup"><span data-stu-id="82fc0-105">Steps</span></span> 

1.  <span data-ttu-id="82fc0-106">Click the **Create Export Policy** blade from the Manage Volume blade.</span><span class="sxs-lookup"><span data-stu-id="82fc0-106">Click the **Create Export Policy** blade from the Manage Volume blade.</span></span> 

2.  <span data-ttu-id="82fc0-107">Specify information for the following fields to create an export policy rule:</span><span class="sxs-lookup"><span data-stu-id="82fc0-107">Specify information for the following fields to create an export policy rule:</span></span>   
    *  <span data-ttu-id="82fc0-108">**Index** </span><span class="sxs-lookup"><span data-stu-id="82fc0-108">**Index** </span></span>  
        <span data-ttu-id="82fc0-109">Specify the index number for the rule.</span><span class="sxs-lookup"><span data-stu-id="82fc0-109">Specify the index number for the rule.</span></span>  
        <span data-ttu-id="82fc0-110">An export policy can consist of up to five rules.</span><span class="sxs-lookup"><span data-stu-id="82fc0-110">An export policy can consist of up to five rules.</span></span> <span data-ttu-id="82fc0-111">Rules are evaluated according to their order in the list of index numbers.</span><span class="sxs-lookup"><span data-stu-id="82fc0-111">Rules are evaluated according to their order in the list of index numbers.</span></span> <span data-ttu-id="82fc0-112">Rules with lower index numbers are evaluated first.</span><span class="sxs-lookup"><span data-stu-id="82fc0-112">Rules with lower index numbers are evaluated first.</span></span> <span data-ttu-id="82fc0-113">For example, the rule with index number 1 is evaluated before the rule with index number 2.</span><span class="sxs-lookup"><span data-stu-id="82fc0-113">For example, the rule with index number 1 is evaluated before the rule with index number 2.</span></span> 

    * <span data-ttu-id="82fc0-114">**Allowed Clients** </span><span class="sxs-lookup"><span data-stu-id="82fc0-114">**Allowed Clients** </span></span>  
        <span data-ttu-id="82fc0-115">Specify the value in one of the following formats:</span><span class="sxs-lookup"><span data-stu-id="82fc0-115">Specify the value in one of the following formats:</span></span>  
        * <span data-ttu-id="82fc0-116">IPv4 address, for example, `10.1.12.24`</span><span class="sxs-lookup"><span data-stu-id="82fc0-116">IPv4 address, for example, `10.1.12.24`</span></span> 
        * <span data-ttu-id="82fc0-117">IPv4 address with a subnet mask expressed as a number of bits, for example, `10.1.12.10/4`</span><span class="sxs-lookup"><span data-stu-id="82fc0-117">IPv4 address with a subnet mask expressed as a number of bits, for example, `10.1.12.10/4`</span></span>

    * <span data-ttu-id="82fc0-118">**Access**</span><span class="sxs-lookup"><span data-stu-id="82fc0-118">**Access**</span></span>  
        <span data-ttu-id="82fc0-119">Select one of the following access types:</span><span class="sxs-lookup"><span data-stu-id="82fc0-119">Select one of the following access types:</span></span>  
        * <span data-ttu-id="82fc0-120">No Access</span><span class="sxs-lookup"><span data-stu-id="82fc0-120">No Access</span></span> 
        * <span data-ttu-id="82fc0-121">Read & Write</span><span class="sxs-lookup"><span data-stu-id="82fc0-121">Read & Write</span></span>
        * <span data-ttu-id="82fc0-122">Read Only</span><span class="sxs-lookup"><span data-stu-id="82fc0-122">Read Only</span></span>

    * <span data-ttu-id="82fc0-123">**Protocols** </span><span class="sxs-lookup"><span data-stu-id="82fc0-123">**Protocols** </span></span>  
        <span data-ttu-id="82fc0-124">Specify the protocol to use for the export policy.</span><span class="sxs-lookup"><span data-stu-id="82fc0-124">Specify the protocol to use for the export policy.</span></span>   
        <span data-ttu-id="82fc0-125">Currently, Azure NetApp Files supports only NFSv3.</span><span class="sxs-lookup"><span data-stu-id="82fc0-125">Currently, Azure NetApp Files supports only NFSv3.</span></span>

    ![Export policy](../media/azure-netapp-files/azure-netapp-files-export-policy.png) 


## <a name="next-steps"></a><span data-ttu-id="82fc0-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="82fc0-127">Next steps</span></span> 
* [<span data-ttu-id="82fc0-128">Manage volumes</span><span class="sxs-lookup"><span data-stu-id="82fc0-128">Manage volumes</span></span>](azure-netapp-files-manage-volumes.md)
* [<span data-ttu-id="82fc0-129">Mount or unmount a volume for virtual machines</span><span class="sxs-lookup"><span data-stu-id="82fc0-129">Mount or unmount a volume for virtual machines</span></span>](azure-netapp-files-mount-unmount-volumes-for-virtual-machines.md)
* [<span data-ttu-id="82fc0-130">Manage snapshots</span><span class="sxs-lookup"><span data-stu-id="82fc0-130">Manage snapshots</span></span>](azure-netapp-files-manage-snapshots.md)
