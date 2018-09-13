---
title: Choose VM sizes for Azure Batch pools | Microsoft Docs
description: How to choose from the available VM sizes for compute nodes in Azure Batch pools
services: batch
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: batch
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2018
ms.author: danlep
ms.openlocfilehash: 1669d5a2237322f72dce3b172c32e7199900a4e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969470"
---
# <a name="choose-a-vm-size-for-compute-nodes-in-an-azure-batch-pool"></a><span data-ttu-id="0a816-103">Choose a VM size for compute nodes in an Azure Batch pool</span><span class="sxs-lookup"><span data-stu-id="0a816-103">Choose a VM size for compute nodes in an Azure Batch pool</span></span>

<span data-ttu-id="0a816-104">When you select a node size for an Azure Batch pool, you can choose from among almost all the VM sizes available in Azure.</span><span class="sxs-lookup"><span data-stu-id="0a816-104">When you select a node size for an Azure Batch pool, you can choose from among almost all the VM sizes available in Azure.</span></span> <span data-ttu-id="0a816-105">Azure offers a range of sizes for Linux and Windows VMs for different workloads.</span><span class="sxs-lookup"><span data-stu-id="0a816-105">Azure offers a range of sizes for Linux and Windows VMs for different workloads.</span></span> 

<span data-ttu-id="0a816-106">There are a few exceptions and limitations to choosing a VM size:</span><span class="sxs-lookup"><span data-stu-id="0a816-106">There are a few exceptions and limitations to choosing a VM size:</span></span>
* <span data-ttu-id="0a816-107">Some VM families or VM sizes are not supported in Batch.</span><span class="sxs-lookup"><span data-stu-id="0a816-107">Some VM families or VM sizes are not supported in Batch.</span></span> 
* <span data-ttu-id="0a816-108">Some VM sizes are restricted and need to be specifically enabled before they can be allocated.</span><span class="sxs-lookup"><span data-stu-id="0a816-108">Some VM sizes are restricted and need to be specifically enabled before they can be allocated.</span></span>


## <a name="supported-vm-families-and-sizes"></a><span data-ttu-id="0a816-109">Supported VM families and sizes</span><span class="sxs-lookup"><span data-stu-id="0a816-109">Supported VM families and sizes</span></span>

### <a name="pools-in-virtual-machine-configuration"></a><span data-ttu-id="0a816-110">Pools in Virtual Machine configuration</span><span class="sxs-lookup"><span data-stu-id="0a816-110">Pools in Virtual Machine configuration</span></span>

<span data-ttu-id="0a816-111">Batch pools in the Virtual Machine configuration support all VM sizes ([Linux](../virtual-machines/linux/sizes.md), [Windows](../virtual-machines/windows/sizes.md)) *except* for the following:</span><span class="sxs-lookup"><span data-stu-id="0a816-111">Batch pools in the Virtual Machine configuration support all VM sizes ([Linux](../virtual-machines/linux/sizes.md), [Windows](../virtual-machines/windows/sizes.md)) *except* for the following:</span></span>

| <span data-ttu-id="0a816-112">Family</span><span class="sxs-lookup"><span data-stu-id="0a816-112">Family</span></span>  | <span data-ttu-id="0a816-113">Unsupported sizes</span><span class="sxs-lookup"><span data-stu-id="0a816-113">Unsupported sizes</span></span>  |
|---------|---------|
| <span data-ttu-id="0a816-114">Basic A-series</span><span class="sxs-lookup"><span data-stu-id="0a816-114">Basic A-series</span></span> | <span data-ttu-id="0a816-115">Basic_A0 (A0)</span><span class="sxs-lookup"><span data-stu-id="0a816-115">Basic_A0 (A0)</span></span> |
| <span data-ttu-id="0a816-116">A-series</span><span class="sxs-lookup"><span data-stu-id="0a816-116">A-series</span></span> | <span data-ttu-id="0a816-117">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="0a816-117">Standard_A0</span></span> |
| <span data-ttu-id="0a816-118">B-series</span><span class="sxs-lookup"><span data-stu-id="0a816-118">B-series</span></span> | <span data-ttu-id="0a816-119">All</span><span class="sxs-lookup"><span data-stu-id="0a816-119">All</span></span> |
| <span data-ttu-id="0a816-120">M-series</span><span class="sxs-lookup"><span data-stu-id="0a816-120">M-series</span></span> | <span data-ttu-id="0a816-121">All</span><span class="sxs-lookup"><span data-stu-id="0a816-121">All</span></span> |



### <a name="pools-in-cloud-service-configuration"></a><span data-ttu-id="0a816-122">Pools in Cloud Service configuration</span><span class="sxs-lookup"><span data-stu-id="0a816-122">Pools in Cloud Service configuration</span></span>

<span data-ttu-id="0a816-123">Batch pools in the Cloud Service configuration support all [VM sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) *except* for the following:</span><span class="sxs-lookup"><span data-stu-id="0a816-123">Batch pools in the Cloud Service configuration support all [VM sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) *except* for the following:</span></span>

| <span data-ttu-id="0a816-124">Family</span><span class="sxs-lookup"><span data-stu-id="0a816-124">Family</span></span>  | <span data-ttu-id="0a816-125">Unsupported sizes</span><span class="sxs-lookup"><span data-stu-id="0a816-125">Unsupported sizes</span></span>  |
|---------|---------|
| <span data-ttu-id="0a816-126">A-series</span><span class="sxs-lookup"><span data-stu-id="0a816-126">A-series</span></span> | <span data-ttu-id="0a816-127">ExtraSmall</span><span class="sxs-lookup"><span data-stu-id="0a816-127">ExtraSmall</span></span> |
| <span data-ttu-id="0a816-128">Av2-series</span><span class="sxs-lookup"><span data-stu-id="0a816-128">Av2-series</span></span> | <span data-ttu-id="0a816-129">Standard_A1_v2, Standard_A2_v2, Standard_A2m_v2</span><span class="sxs-lookup"><span data-stu-id="0a816-129">Standard_A1_v2, Standard_A2_v2, Standard_A2m_v2</span></span> |

## <a name="restricted-vm-families"></a><span data-ttu-id="0a816-130">Restricted VM families</span><span class="sxs-lookup"><span data-stu-id="0a816-130">Restricted VM families</span></span>
<span data-ttu-id="0a816-131">The following VM families can be allocated in Batch pools, but you must request a specific quota increase (see [this article](batch-quota-limit.md#increase-a-quota)):</span><span class="sxs-lookup"><span data-stu-id="0a816-131">The following VM families can be allocated in Batch pools, but you must request a specific quota increase (see [this article](batch-quota-limit.md#increase-a-quota)):</span></span>
* <span data-ttu-id="0a816-132">NCv2-series</span><span class="sxs-lookup"><span data-stu-id="0a816-132">NCv2-series</span></span>
* <span data-ttu-id="0a816-133">NCv3-series</span><span class="sxs-lookup"><span data-stu-id="0a816-133">NCv3-series</span></span>
* <span data-ttu-id="0a816-134">ND-series</span><span class="sxs-lookup"><span data-stu-id="0a816-134">ND-series</span></span>

<span data-ttu-id="0a816-135">These sizes can only be used in pools in the Virtual Machine configuration.</span><span class="sxs-lookup"><span data-stu-id="0a816-135">These sizes can only be used in pools in the Virtual Machine configuration.</span></span>

## <a name="size-considerations"></a><span data-ttu-id="0a816-136">Size considerations</span><span class="sxs-lookup"><span data-stu-id="0a816-136">Size considerations</span></span>

* <span data-ttu-id="0a816-137">**Application requirements** - Consider the characteristics and requirements of the application you'll run on the nodes.</span><span class="sxs-lookup"><span data-stu-id="0a816-137">**Application requirements** - Consider the characteristics and requirements of the application you'll run on the nodes.</span></span> <span data-ttu-id="0a816-138">Aspects like whether the application is multithreaded and how much memory it consumes can help determine the most suitable and cost-effective node size.</span><span class="sxs-lookup"><span data-stu-id="0a816-138">Aspects like whether the application is multithreaded and how much memory it consumes can help determine the most suitable and cost-effective node size.</span></span> <span data-ttu-id="0a816-139">For multi-instance [MPI workloads](batch-mpi.md) or CUDA applications, consider specialized [HPC](../virtual-machines/linux/sizes-hpc.md) or [GPU-enabled](../virtual-machines/linux/sizes-gpu.md) VM sizes, respectively.</span><span class="sxs-lookup"><span data-stu-id="0a816-139">For multi-instance [MPI workloads](batch-mpi.md) or CUDA applications, consider specialized [HPC](../virtual-machines/linux/sizes-hpc.md) or [GPU-enabled](../virtual-machines/linux/sizes-gpu.md) VM sizes, respectively.</span></span> <span data-ttu-id="0a816-140">(See [Use RDMA-capable or GPU-enabled instances in Batch pools](batch-pool-compute-intensive-sizes.md).)</span><span class="sxs-lookup"><span data-stu-id="0a816-140">(See [Use RDMA-capable or GPU-enabled instances in Batch pools](batch-pool-compute-intensive-sizes.md).)</span></span> 

* <span data-ttu-id="0a816-141">**Tasks per node** - It's typical to select a node size assuming one task runs on a node at a time.</span><span class="sxs-lookup"><span data-stu-id="0a816-141">**Tasks per node** - It's typical to select a node size assuming one task runs on a node at a time.</span></span> <span data-ttu-id="0a816-142">However, it might be advantageous to have multiple tasks (and therefore multiple application instances) [run in parallel](batch-parallel-node-tasks.md) on compute nodes during job execution.</span><span class="sxs-lookup"><span data-stu-id="0a816-142">However, it might be advantageous to have multiple tasks (and therefore multiple application instances) [run in parallel](batch-parallel-node-tasks.md) on compute nodes during job execution.</span></span> <span data-ttu-id="0a816-143">In this case, it is common to choose a multicore node size to accommodate the increased demand of parallel task execution.</span><span class="sxs-lookup"><span data-stu-id="0a816-143">In this case, it is common to choose a multicore node size to accommodate the increased demand of parallel task execution.</span></span>

* <span data-ttu-id="0a816-144">**Load levels for different tasks** - All of the nodes in a pool are the same size.</span><span class="sxs-lookup"><span data-stu-id="0a816-144">**Load levels for different tasks** - All of the nodes in a pool are the same size.</span></span> <span data-ttu-id="0a816-145">If you intend to run applications with differing system requirements and/or load levels, we recommend that you use separate pools.</span><span class="sxs-lookup"><span data-stu-id="0a816-145">If you intend to run applications with differing system requirements and/or load levels, we recommend that you use separate pools.</span></span> 

* <span data-ttu-id="0a816-146">**Region availability** - A VM family or size might not be available in the regions where you create your Batch accounts.</span><span class="sxs-lookup"><span data-stu-id="0a816-146">**Region availability** - A VM family or size might not be available in the regions where you create your Batch accounts.</span></span> <span data-ttu-id="0a816-147">To check that a size is available, see [Products available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="0a816-147">To check that a size is available, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>

* <span data-ttu-id="0a816-148">**Quotas** - The [cores quotas](batch-quota-limit.md#resource-quotas) in your Batch account can limit the number of nodes of a given size you can add to a Batch pool.</span><span class="sxs-lookup"><span data-stu-id="0a816-148">**Quotas** - The [cores quotas](batch-quota-limit.md#resource-quotas) in your Batch account can limit the number of nodes of a given size you can add to a Batch pool.</span></span> <span data-ttu-id="0a816-149">To request a quota increase, see [this article](batch-quota-limit.md#increase-a-quota).</span><span class="sxs-lookup"><span data-stu-id="0a816-149">To request a quota increase, see [this article](batch-quota-limit.md#increase-a-quota).</span></span> 

* <span data-ttu-id="0a816-150">**Pool configuration** - In general, you have more VM size options when you create a pool in the Virtual Machine configuration, compared with the Cloud Service configuration.</span><span class="sxs-lookup"><span data-stu-id="0a816-150">**Pool configuration** - In general, you have more VM size options when you create a pool in the Virtual Machine configuration, compared with the Cloud Service configuration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a816-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a816-151">Next steps</span></span>

* <span data-ttu-id="0a816-152">For an in-depth overview of Batch, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="0a816-152">For an in-depth overview of Batch, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span></span>
* <span data-ttu-id="0a816-153">For information about using compute-intensive VM sizes, see [Use RDMA-capable or GPU-enabled instances in Batch pools](batch-pool-compute-intensive-sizes.md).</span><span class="sxs-lookup"><span data-stu-id="0a816-153">For information about using compute-intensive VM sizes, see [Use RDMA-capable or GPU-enabled instances in Batch pools](batch-pool-compute-intensive-sizes.md).</span></span> 


