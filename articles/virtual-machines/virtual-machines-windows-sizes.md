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
ms.openlocfilehash: 193cb2570e4c71c5205cc029543a3a7602a6574e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563283"
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="181e4-103">Sizes for Windows virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="181e4-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="181e4-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Windows apps and workloads.</span><span class="sxs-lookup"><span data-stu-id="181e4-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Windows apps and workloads.</span></span> <span data-ttu-id="181e4-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span><span class="sxs-lookup"><span data-stu-id="181e4-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span>  <span data-ttu-id="181e4-106">This article is also available for [Linux virtual machines](linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="181e4-106">This article is also available for [Linux virtual machines](linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!IMPORTANT]
>* <span data-ttu-id="181e4-107">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="181e4-107">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
>* <span data-ttu-id="181e4-108">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="181e4-108">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
>* <span data-ttu-id="181e4-109">Storage costs are calculated separately based on used pages in the storage account.</span><span class="sxs-lookup"><span data-stu-id="181e4-109">Storage costs are calculated separately based on used pages in the storage account.</span></span> <span data-ttu-id="181e4-110">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="181e4-110">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
> * <span data-ttu-id="181e4-111">Learn more about how [Azure compute units (ACU)](windows/acu.md) can help you compare compute performance across Azure SKUs.</span><span class="sxs-lookup"><span data-stu-id="181e4-111">Learn more about how [Azure compute units (ACU)](windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>
>
>
<br>    




| <span data-ttu-id="181e4-112">Type</span><span class="sxs-lookup"><span data-stu-id="181e4-112">Type</span></span>                     | <span data-ttu-id="181e4-113">Sizes</span><span class="sxs-lookup"><span data-stu-id="181e4-113">Sizes</span></span>           |    <span data-ttu-id="181e4-114">Description</span><span class="sxs-lookup"><span data-stu-id="181e4-114">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="181e4-115">General purpose</span><span class="sxs-lookup"><span data-stu-id="181e4-115">General purpose</span></span>](virtual-machines-windows-sizes-general.md)          | <span data-ttu-id="181e4-116">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="181e4-116">DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="181e4-117">Balanced CPU-to-memory ratio.</span><span class="sxs-lookup"><span data-stu-id="181e4-117">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="181e4-118">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span><span class="sxs-lookup"><span data-stu-id="181e4-118">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="181e4-119">Compute optimized</span><span class="sxs-lookup"><span data-stu-id="181e4-119">Compute optimized</span></span>](virtual-machines-windows-sizes-compute.md)        | <span data-ttu-id="181e4-120">Fs, F</span><span class="sxs-lookup"><span data-stu-id="181e4-120">Fs, F</span></span>             | <span data-ttu-id="181e4-121">High CPU-to-memory ratio.</span><span class="sxs-lookup"><span data-stu-id="181e4-121">High CPU-to-memory ratio.</span></span> <span data-ttu-id="181e4-122">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span><span class="sxs-lookup"><span data-stu-id="181e4-122">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="181e4-123">Memory optimized</span><span class="sxs-lookup"><span data-stu-id="181e4-123">Memory optimized</span></span>](virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="181e4-124">GS, G, DSv2, DS</span><span class="sxs-lookup"><span data-stu-id="181e4-124">GS, G, DSv2, DS</span></span>   | <span data-ttu-id="181e4-125">High memory-to-core ratio.</span><span class="sxs-lookup"><span data-stu-id="181e4-125">High memory-to-core ratio.</span></span> <span data-ttu-id="181e4-126">Great for relational database servers, medium to large caches, and in-memory analytics.</span><span class="sxs-lookup"><span data-stu-id="181e4-126">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="181e4-127">Storage optimized</span><span class="sxs-lookup"><span data-stu-id="181e4-127">Storage optimized</span></span>](virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="181e4-128">Ls</span><span class="sxs-lookup"><span data-stu-id="181e4-128">Ls</span></span>                | <span data-ttu-id="181e4-129">High disk throughput and IO.</span><span class="sxs-lookup"><span data-stu-id="181e4-129">High disk throughput and IO.</span></span> <span data-ttu-id="181e4-130">Ideal for Big Data, SQL, and NoSQL databases.</span><span class="sxs-lookup"><span data-stu-id="181e4-130">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="181e4-131">GPU</span><span class="sxs-lookup"><span data-stu-id="181e4-131">GPU</span></span>](virtual-machines-windows-sizes-gpu.md)            | <span data-ttu-id="181e4-132">NV, NC</span><span class="sxs-lookup"><span data-stu-id="181e4-132">NV, NC</span></span>            | <span data-ttu-id="181e4-133">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span><span class="sxs-lookup"><span data-stu-id="181e4-133">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="181e4-134">Available with single or multiple GPUs.</span><span class="sxs-lookup"><span data-stu-id="181e4-134">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="181e4-135">High performance compute</span><span class="sxs-lookup"><span data-stu-id="181e4-135">High performance compute</span></span>](virtual-machines-windows-sizes-hpc.md) | <span data-ttu-id="181e4-136">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="181e4-136">H, A8-11</span></span>          | <span data-ttu-id="181e4-137">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span><span class="sxs-lookup"><span data-stu-id="181e4-137">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

<span data-ttu-id="181e4-138">Learn more about how [Azure compute units (ACU)](windows/acu.md) can help you compare compute performance across Azure SKUs.</span><span class="sxs-lookup"><span data-stu-id="181e4-138">Learn more about how [Azure compute units (ACU)](windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>

<span data-ttu-id="181e4-139">Learn more about the different VM sizes that are available:</span><span class="sxs-lookup"><span data-stu-id="181e4-139">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="181e4-140">General purpose</span><span class="sxs-lookup"><span data-stu-id="181e4-140">General purpose</span></span>](virtual-machines-windows-sizes-general.md)
- [<span data-ttu-id="181e4-141">Compute optimized</span><span class="sxs-lookup"><span data-stu-id="181e4-141">Compute optimized</span></span>](virtual-machines-windows-sizes-compute.md)
- [<span data-ttu-id="181e4-142">Memory optimized</span><span class="sxs-lookup"><span data-stu-id="181e4-142">Memory optimized</span></span>](virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="181e4-143">Storage optimized</span><span class="sxs-lookup"><span data-stu-id="181e4-143">Storage optimized</span></span>](virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="181e4-144">GPU optimized</span><span class="sxs-lookup"><span data-stu-id="181e4-144">GPU optimized</span></span>](virtual-machines-windows-sizes-gpu.md)
- [<span data-ttu-id="181e4-145">High performance compute</span><span class="sxs-lookup"><span data-stu-id="181e4-145">High performance compute</span></span>](virtual-machines-windows-sizes-hpc.md)



