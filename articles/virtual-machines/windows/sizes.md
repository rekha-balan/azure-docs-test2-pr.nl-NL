---
title: Windows VM sizes in Azure | Microsoft Docs
description: Lists the different sizes available for Windows virtual machines in Azure.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: b6044ef2e73823d4a30838d0462e77fbc046ae9b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551898"
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="bb626-103">Sizes for Windows virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="bb626-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="bb626-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Windows apps and workloads.</span><span class="sxs-lookup"><span data-stu-id="bb626-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Windows apps and workloads.</span></span> <span data-ttu-id="bb626-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span><span class="sxs-lookup"><span data-stu-id="bb626-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span>  <span data-ttu-id="bb626-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb626-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!IMPORTANT]
>* <span data-ttu-id="bb626-107">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="bb626-107">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
>* <span data-ttu-id="bb626-108">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="bb626-108">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
>* <span data-ttu-id="bb626-109">Storage costs are calculated separately based on used pages in the storage account.</span><span class="sxs-lookup"><span data-stu-id="bb626-109">Storage costs are calculated separately based on used pages in the storage account.</span></span> <span data-ttu-id="bb626-110">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="bb626-110">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
> * <span data-ttu-id="bb626-111">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span><span class="sxs-lookup"><span data-stu-id="bb626-111">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>
>
>
<br>    




| <span data-ttu-id="bb626-112">Type</span><span class="sxs-lookup"><span data-stu-id="bb626-112">Type</span></span>                     | <span data-ttu-id="bb626-113">Sizes</span><span class="sxs-lookup"><span data-stu-id="bb626-113">Sizes</span></span>           |    <span data-ttu-id="bb626-114">Description</span><span class="sxs-lookup"><span data-stu-id="bb626-114">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="bb626-115">General purpose</span><span class="sxs-lookup"><span data-stu-id="bb626-115">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="bb626-116">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="bb626-116">DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="bb626-117">Balanced CPU-to-memory ratio.</span><span class="sxs-lookup"><span data-stu-id="bb626-117">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="bb626-118">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span><span class="sxs-lookup"><span data-stu-id="bb626-118">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="bb626-119">Compute optimized</span><span class="sxs-lookup"><span data-stu-id="bb626-119">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="bb626-120">Fs, F</span><span class="sxs-lookup"><span data-stu-id="bb626-120">Fs, F</span></span>             | <span data-ttu-id="bb626-121">High CPU-to-memory ratio.</span><span class="sxs-lookup"><span data-stu-id="bb626-121">High CPU-to-memory ratio.</span></span> <span data-ttu-id="bb626-122">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span><span class="sxs-lookup"><span data-stu-id="bb626-122">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="bb626-123">Memory optimized</span><span class="sxs-lookup"><span data-stu-id="bb626-123">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="bb626-124">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="bb626-124">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="bb626-125">High memory-to-core ratio.</span><span class="sxs-lookup"><span data-stu-id="bb626-125">High memory-to-core ratio.</span></span> <span data-ttu-id="bb626-126">Great for relational database servers, medium to large caches, and in-memory analytics.</span><span class="sxs-lookup"><span data-stu-id="bb626-126">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="bb626-127">Storage optimized</span><span class="sxs-lookup"><span data-stu-id="bb626-127">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="bb626-128">Ls</span><span class="sxs-lookup"><span data-stu-id="bb626-128">Ls</span></span>                | <span data-ttu-id="bb626-129">High disk throughput and IO.</span><span class="sxs-lookup"><span data-stu-id="bb626-129">High disk throughput and IO.</span></span> <span data-ttu-id="bb626-130">Ideal for Big Data, SQL, and NoSQL databases.</span><span class="sxs-lookup"><span data-stu-id="bb626-130">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="bb626-131">GPU</span><span class="sxs-lookup"><span data-stu-id="bb626-131">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="bb626-132">NV, NC</span><span class="sxs-lookup"><span data-stu-id="bb626-132">NV, NC</span></span>            | <span data-ttu-id="bb626-133">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span><span class="sxs-lookup"><span data-stu-id="bb626-133">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="bb626-134">Available with single or multiple GPUs.</span><span class="sxs-lookup"><span data-stu-id="bb626-134">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="bb626-135">High performance compute</span><span class="sxs-lookup"><span data-stu-id="bb626-135">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="bb626-136">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="bb626-136">H, A8-11</span></span>          | <span data-ttu-id="bb626-137">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span><span class="sxs-lookup"><span data-stu-id="bb626-137">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

<span data-ttu-id="bb626-138">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span><span class="sxs-lookup"><span data-stu-id="bb626-138">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

<span data-ttu-id="bb626-139">Learn more about the different VM sizes that are available:</span><span class="sxs-lookup"><span data-stu-id="bb626-139">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="bb626-140">General purpose</span><span class="sxs-lookup"><span data-stu-id="bb626-140">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="bb626-141">Compute optimized</span><span class="sxs-lookup"><span data-stu-id="bb626-141">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="bb626-142">Memory optimized</span><span class="sxs-lookup"><span data-stu-id="bb626-142">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="bb626-143">Storage optimized</span><span class="sxs-lookup"><span data-stu-id="bb626-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="bb626-144">GPU optimized</span><span class="sxs-lookup"><span data-stu-id="bb626-144">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="bb626-145">High performance compute</span><span class="sxs-lookup"><span data-stu-id="bb626-145">High performance compute</span></span>](sizes-hpc.md)



