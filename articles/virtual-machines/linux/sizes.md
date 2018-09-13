---
title: Linux VM sizes in Azure | Microsoft Docs
description: Lists the different sizes available for Linux virtual machines in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/06/2018
ms.author: jonbeck
ms.openlocfilehash: 340e12af71fa16c3de21b152830c1f745f0d4399
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804396"
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="12a75-103">Sizes for Linux virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="12a75-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="12a75-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span><span class="sxs-lookup"><span data-stu-id="12a75-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span></span> <span data-ttu-id="12a75-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span><span class="sxs-lookup"><span data-stu-id="12a75-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span> <span data-ttu-id="12a75-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12a75-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="12a75-107">Type</span><span class="sxs-lookup"><span data-stu-id="12a75-107">Type</span></span>                     | <span data-ttu-id="12a75-108">Sizes</span><span class="sxs-lookup"><span data-stu-id="12a75-108">Sizes</span></span>           |    <span data-ttu-id="12a75-109">Description</span><span class="sxs-lookup"><span data-stu-id="12a75-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="12a75-110">General purpose</span><span class="sxs-lookup"><span data-stu-id="12a75-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="12a75-111">B, Dsv3, Dv3, DSv2, Dv2, Av2</span><span class="sxs-lookup"><span data-stu-id="12a75-111">B, Dsv3, Dv3, DSv2, Dv2, Av2</span></span>  | <span data-ttu-id="12a75-112">Balanced CPU-to-memory ratio.</span><span class="sxs-lookup"><span data-stu-id="12a75-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="12a75-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span><span class="sxs-lookup"><span data-stu-id="12a75-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="12a75-114">Compute optimized</span><span class="sxs-lookup"><span data-stu-id="12a75-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="12a75-115">Fsv2, Fs, F</span><span class="sxs-lookup"><span data-stu-id="12a75-115">Fsv2, Fs, F</span></span>             | <span data-ttu-id="12a75-116">High CPU-to-memory ratio.</span><span class="sxs-lookup"><span data-stu-id="12a75-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="12a75-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span><span class="sxs-lookup"><span data-stu-id="12a75-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="12a75-118">Memory optimized</span><span class="sxs-lookup"><span data-stu-id="12a75-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="12a75-119">Esv3, Ev3, M, GS, G, DSv2, Dv2</span><span class="sxs-lookup"><span data-stu-id="12a75-119">Esv3, Ev3, M, GS, G, DSv2, Dv2</span></span>  | <span data-ttu-id="12a75-120">High memory-to-CPU ratio.</span><span class="sxs-lookup"><span data-stu-id="12a75-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="12a75-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span><span class="sxs-lookup"><span data-stu-id="12a75-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="12a75-122">Storage optimized</span><span class="sxs-lookup"><span data-stu-id="12a75-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="12a75-123">Ls</span><span class="sxs-lookup"><span data-stu-id="12a75-123">Ls</span></span>                | <span data-ttu-id="12a75-124">High disk throughput and IO.</span><span class="sxs-lookup"><span data-stu-id="12a75-124">High disk throughput and IO.</span></span> <span data-ttu-id="12a75-125">Ideal for Big Data, SQL, and NoSQL databases.</span><span class="sxs-lookup"><span data-stu-id="12a75-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="12a75-126">GPU</span><span class="sxs-lookup"><span data-stu-id="12a75-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="12a75-127">NV, NC, NCv2, NCv3, ND</span><span class="sxs-lookup"><span data-stu-id="12a75-127">NV, NC, NCv2, NCv3, ND</span></span>            | <span data-ttu-id="12a75-128">Specialized virtual machines targeted for heavy graphic rendering and video editing, as well as model training and inferencing (ND) with deep learning.</span><span class="sxs-lookup"><span data-stu-id="12a75-128">Specialized virtual machines targeted for heavy graphic rendering and video editing, as well as model training and inferencing (ND) with deep learning.</span></span> <span data-ttu-id="12a75-129">Available with single or multiple GPUs.</span><span class="sxs-lookup"><span data-stu-id="12a75-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="12a75-130">High performance compute</span><span class="sxs-lookup"><span data-stu-id="12a75-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="12a75-131">H</span><span class="sxs-lookup"><span data-stu-id="12a75-131">H</span></span>       | <span data-ttu-id="12a75-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span><span class="sxs-lookup"><span data-stu-id="12a75-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="12a75-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="12a75-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="12a75-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="12a75-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="12a75-135">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="12a75-135">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="12a75-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span><span class="sxs-lookup"><span data-stu-id="12a75-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="12a75-137">REST API</span><span class="sxs-lookup"><span data-stu-id="12a75-137">REST API</span></span>

<span data-ttu-id="12a75-138">For information on using the REST API to query for VM sizes, see the following:</span><span class="sxs-lookup"><span data-stu-id="12a75-138">For information on using the REST API to query for VM sizes, see the following:</span></span>

- [<span data-ttu-id="12a75-139">List available virtual machine sizes for resizing</span><span class="sxs-lookup"><span data-stu-id="12a75-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/listavailablesizes)
- [<span data-ttu-id="12a75-140">List available virtual machine sizes for a subscription</span><span class="sxs-lookup"><span data-stu-id="12a75-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/listall)
- [<span data-ttu-id="12a75-141">List available virtual machine sizes in an availability set</span><span class="sxs-lookup"><span data-stu-id="12a75-141">List available virtual machine sizes in an availability set</span></span>](https://docs.microsoft.com/rest/api/compute/availabilitysets/listavailablesizes)

## <a name="acu"></a><span data-ttu-id="12a75-142">ACU</span><span class="sxs-lookup"><span data-stu-id="12a75-142">ACU</span></span>

<span data-ttu-id="12a75-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span><span class="sxs-lookup"><span data-stu-id="12a75-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="benchmark-scores"></a><span data-ttu-id="12a75-144">Benchmark scores</span><span class="sxs-lookup"><span data-stu-id="12a75-144">Benchmark scores</span></span>

<span data-ttu-id="12a75-145">Learn more about compute performance for Linux VMs using the [CoreMark benchmark scores](compute-benchmark-scores.md).</span><span class="sxs-lookup"><span data-stu-id="12a75-145">Learn more about compute performance for Linux VMs using the [CoreMark benchmark scores](compute-benchmark-scores.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12a75-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="12a75-146">Next steps</span></span>

<span data-ttu-id="12a75-147">Learn more about the different VM sizes that are available:</span><span class="sxs-lookup"><span data-stu-id="12a75-147">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="12a75-148">General purpose</span><span class="sxs-lookup"><span data-stu-id="12a75-148">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="12a75-149">Compute optimized</span><span class="sxs-lookup"><span data-stu-id="12a75-149">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="12a75-150">Memory optimized</span><span class="sxs-lookup"><span data-stu-id="12a75-150">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="12a75-151">Storage optimized</span><span class="sxs-lookup"><span data-stu-id="12a75-151">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="12a75-152">GPU</span><span class="sxs-lookup"><span data-stu-id="12a75-152">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="12a75-153">High performance compute</span><span class="sxs-lookup"><span data-stu-id="12a75-153">High performance compute</span></span>](sizes-hpc.md)
- <span data-ttu-id="12a75-154">Check the [Previous generation](sizes-previous-gen.md) page for A Standard, Dv1 (D1-4 and D11-14 v1), and A8-A11 series</span><span class="sxs-lookup"><span data-stu-id="12a75-154">Check the [Previous generation](sizes-previous-gen.md) page for A Standard, Dv1 (D1-4 and D11-14 v1), and A8-A11 series</span></span>



