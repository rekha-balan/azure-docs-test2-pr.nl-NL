---
title: Linux VM sizes in Azure | Microsoft Docs
description: Lists the different sizes available for Linux virtual machines in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 1e20697985cb10d5867f804c3ce8dad1028be05e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44668889"
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="cda07-103">Sizes for Linux virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="cda07-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="cda07-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span><span class="sxs-lookup"><span data-stu-id="cda07-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span></span> <span data-ttu-id="cda07-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span><span class="sxs-lookup"><span data-stu-id="cda07-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span> <span data-ttu-id="cda07-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cda07-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="cda07-107">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="cda07-107">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
> * <span data-ttu-id="cda07-108">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="cda07-108">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
> * <span data-ttu-id="cda07-109">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="cda07-109">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
> * <span data-ttu-id="cda07-110">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span><span class="sxs-lookup"><span data-stu-id="cda07-110">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>
> 
> 

<br>   


| <span data-ttu-id="cda07-111">Type</span><span class="sxs-lookup"><span data-stu-id="cda07-111">Type</span></span>                     | <span data-ttu-id="cda07-112">Sizes</span><span class="sxs-lookup"><span data-stu-id="cda07-112">Sizes</span></span>           |    <span data-ttu-id="cda07-113">Description</span><span class="sxs-lookup"><span data-stu-id="cda07-113">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="cda07-114">General purpose</span><span class="sxs-lookup"><span data-stu-id="cda07-114">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="cda07-115">DSv2, Dv2, DS, D, Av2, A0-7,</span><span class="sxs-lookup"><span data-stu-id="cda07-115">DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="cda07-116">Balanced CPU-to-memory ratio.</span><span class="sxs-lookup"><span data-stu-id="cda07-116">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="cda07-117">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span><span class="sxs-lookup"><span data-stu-id="cda07-117">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="cda07-118">Compute optimized</span><span class="sxs-lookup"><span data-stu-id="cda07-118">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="cda07-119">Fs, F</span><span class="sxs-lookup"><span data-stu-id="cda07-119">Fs, F</span></span>             | <span data-ttu-id="cda07-120">High CPU-to-memory ratio.</span><span class="sxs-lookup"><span data-stu-id="cda07-120">High CPU-to-memory ratio.</span></span> <span data-ttu-id="cda07-121">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span><span class="sxs-lookup"><span data-stu-id="cda07-121">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="cda07-122">Memory optimized</span><span class="sxs-lookup"><span data-stu-id="cda07-122">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="cda07-123">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="cda07-123">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="cda07-124">High memory-to-core ratio.</span><span class="sxs-lookup"><span data-stu-id="cda07-124">High memory-to-core ratio.</span></span> <span data-ttu-id="cda07-125">Great for relational database servers, medium to large caches, and in-memory analytics.</span><span class="sxs-lookup"><span data-stu-id="cda07-125">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="cda07-126">Storage optimized</span><span class="sxs-lookup"><span data-stu-id="cda07-126">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="cda07-127">Ls</span><span class="sxs-lookup"><span data-stu-id="cda07-127">Ls</span></span>                | <span data-ttu-id="cda07-128">High disk throughput and IO.</span><span class="sxs-lookup"><span data-stu-id="cda07-128">High disk throughput and IO.</span></span> <span data-ttu-id="cda07-129">Ideal for Big Data, SQL, and NoSQL databases.</span><span class="sxs-lookup"><span data-stu-id="cda07-129">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="cda07-130">GPU</span><span class="sxs-lookup"><span data-stu-id="cda07-130">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="cda07-131">NV, NC</span><span class="sxs-lookup"><span data-stu-id="cda07-131">NV, NC</span></span>            | <span data-ttu-id="cda07-132">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span><span class="sxs-lookup"><span data-stu-id="cda07-132">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="cda07-133">Available with single or multiple GPUs.</span><span class="sxs-lookup"><span data-stu-id="cda07-133">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="cda07-134">High performance compute</span><span class="sxs-lookup"><span data-stu-id="cda07-134">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="cda07-135">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="cda07-135">H, A8-11</span></span>          | <span data-ttu-id="cda07-136">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span><span class="sxs-lookup"><span data-stu-id="cda07-136">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

<span data-ttu-id="cda07-137">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span><span class="sxs-lookup"><span data-stu-id="cda07-137">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>

<span data-ttu-id="cda07-138">Learn more about the different VM sizes that are available:</span><span class="sxs-lookup"><span data-stu-id="cda07-138">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="cda07-139">General purpose</span><span class="sxs-lookup"><span data-stu-id="cda07-139">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="cda07-140">Compute optimized</span><span class="sxs-lookup"><span data-stu-id="cda07-140">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="cda07-141">Memory optimized</span><span class="sxs-lookup"><span data-stu-id="cda07-141">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="cda07-142">Storage optimized</span><span class="sxs-lookup"><span data-stu-id="cda07-142">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="cda07-143">GPU</span><span class="sxs-lookup"><span data-stu-id="cda07-143">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="cda07-144">High performance compute</span><span class="sxs-lookup"><span data-stu-id="cda07-144">High performance compute</span></span>](sizes-hpc.md)



