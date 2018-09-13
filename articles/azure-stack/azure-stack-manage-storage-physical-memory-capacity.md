---
title: Manage physical memory capacity for Azure Stack | Microsoft Docs
description: Monitor and manage available storage space for Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 84518E90-75E1-4037-8D4E-497EAC72AAA1
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/08/2018
ms.author: mabrigg
ms.reviewer: Thomas.Roettinger
ms.openlocfilehash: dc572353c2e27ddfbae2398f1aece56586955e26
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870909"
---
<!---Loc Comment: Please, check the comment in coversation section---> 
# <a name="manage-physical-memory-capacity-for-azure-stack"></a><span data-ttu-id="431d0-103">Manage physical memory capacity for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="431d0-103">Manage physical memory capacity for Azure Stack</span></span>

<span data-ttu-id="431d0-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="431d0-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="431d0-105">To increase the total available memory capacity for Azure Stack, you can add additional memory.</span><span class="sxs-lookup"><span data-stu-id="431d0-105">To increase the total available memory capacity for Azure Stack, you can add additional memory.</span></span> <span data-ttu-id="431d0-106">In Azure Stack your physical server is also referred to as a *scale unit node*.</span><span class="sxs-lookup"><span data-stu-id="431d0-106">In Azure Stack your physical server is also referred to as a *scale unit node*.</span></span> <span data-ttu-id="431d0-107">All scale unit nodes that are members of a single scale unit must have the same amount of memory.</span><span class="sxs-lookup"><span data-stu-id="431d0-107">All scale unit nodes that are members of a single scale unit must have the same amount of memory.</span></span>

> [!note]  
> <span data-ttu-id="431d0-108">Before you continue, consult your hardware manufacturer's documentation to see if a your manufacturer supports a physical memory upgrade.</span><span class="sxs-lookup"><span data-stu-id="431d0-108">Before you continue, consult your hardware manufacturer's documentation to see if a your manufacturer supports a physical memory upgrade.</span></span> <span data-ttu-id="431d0-109">Your OEM hardware vendor support contract may require that the vendor perform the physical server rack placement and the device firmware update.</span><span class="sxs-lookup"><span data-stu-id="431d0-109">Your OEM hardware vendor support contract may require that the vendor perform the physical server rack placement and the device firmware update.</span></span>

<span data-ttu-id="431d0-110">The following flow diagram shows the general process to add memory to each scale unit node.</span><span class="sxs-lookup"><span data-stu-id="431d0-110">The following flow diagram shows the general process to add memory to each scale unit node.</span></span>

![Add memory into each scale unit node](media\azure-stack-manage-storage-physical-capacity\process-to-add-memory-to-scale-unit.png)

## <a name="add-memory-to-an-existing-node"></a><span data-ttu-id="431d0-112">Add memory to an existing node</span><span class="sxs-lookup"><span data-stu-id="431d0-112">Add memory to an existing node</span></span>
<span data-ttu-id="431d0-113">The following steps provide a high-level overview of the add memory process.</span><span class="sxs-lookup"><span data-stu-id="431d0-113">The following steps provide a high-level overview of the add memory process.</span></span> 

> [!Warning]  
<span data-ttu-id="431d0-114">Do not follow these steps without referring to your OEM-provided documentation.</span><span class="sxs-lookup"><span data-stu-id="431d0-114">Do not follow these steps without referring to your OEM-provided documentation.</span></span>

> [!Warning]  
<span data-ttu-id="431d0-115">The entire scale unit must be shut down as a rolling memory upgrade is not supported.</span><span class="sxs-lookup"><span data-stu-id="431d0-115">The entire scale unit must be shut down as a rolling memory upgrade is not supported.</span></span>

1. <span data-ttu-id="431d0-116">Stop Azure Stack using the steps documented in the [Start and stop Azure Stack](azure-stack-start-and-stop.md) article.</span><span class="sxs-lookup"><span data-stu-id="431d0-116">Stop Azure Stack using the steps documented in the [Start and stop Azure Stack](azure-stack-start-and-stop.md) article.</span></span>
2. <span data-ttu-id="431d0-117">Upgrade the memory on each physical computer using your hardware manufacturer’s documentation.</span><span class="sxs-lookup"><span data-stu-id="431d0-117">Upgrade the memory on each physical computer using your hardware manufacturer’s documentation.</span></span>
3. <span data-ttu-id="431d0-118">Start Azure Stack using the steps in the [Start and stop Azure Stack](azure-stack-start-and-stop.md) article.</span><span class="sxs-lookup"><span data-stu-id="431d0-118">Start Azure Stack using the steps in the [Start and stop Azure Stack](azure-stack-start-and-stop.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="431d0-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="431d0-119">Next steps</span></span>

 - <span data-ttu-id="431d0-120">To learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs, see [Manage storage accounts in Azure Stack](azure-stack-manage-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="431d0-120">To learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs, see [Manage storage accounts in Azure Stack](azure-stack-manage-storage-accounts.md).</span></span>
 - <span data-ttu-id="431d0-121">To learn the Azure Stack cloud operator monitors and manages the storage capacity of their Azure Stack deployment, see [Manage storage capacity for Azure Stack](azure-stack-manage-storage-shares.md).</span><span class="sxs-lookup"><span data-stu-id="431d0-121">To learn the Azure Stack cloud operator monitors and manages the storage capacity of their Azure Stack deployment, see [Manage storage capacity for Azure Stack](azure-stack-manage-storage-shares.md).</span></span> 
