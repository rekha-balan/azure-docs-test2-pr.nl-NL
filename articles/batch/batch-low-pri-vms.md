---
title: Run Azure Batch workloads on cost-effective low-priority VMs | Microsoft Docs
description: Learn how to provision low-priority VMs to reduce the cost of Azure Batch workloads.
services: batch
author: mscurrell
manager: jeconnoc
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 03/19/2018
ms.author: markscu
ms.openlocfilehash: d42cef944c3b971804ef1417a3877bf919784a02
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869021"
---
# <a name="use-low-priority-vms-with-batch"></a><span data-ttu-id="db312-103">Use low-priority VMs with Batch</span><span class="sxs-lookup"><span data-stu-id="db312-103">Use low-priority VMs with Batch</span></span>

<span data-ttu-id="db312-104">Azure Batch offers low-priority virtual machines (VMs) to reduce the cost of Batch workloads.</span><span class="sxs-lookup"><span data-stu-id="db312-104">Azure Batch offers low-priority virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="db312-105">Low-priority VMs make new types of Batch workloads possible by enabling a large amount of compute power to be used for a very low cost.</span><span class="sxs-lookup"><span data-stu-id="db312-105">Low-priority VMs make new types of Batch workloads possible by enabling a large amount of compute power to be used for a very low cost.</span></span>
 
<span data-ttu-id="db312-106">Low-priority VMs take advantage of surplus capacity in Azure.</span><span class="sxs-lookup"><span data-stu-id="db312-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="db312-107">When you specify low-priority VMs in your pools, Azure Batch can use this surplus, when available.</span><span class="sxs-lookup"><span data-stu-id="db312-107">When you specify low-priority VMs in your pools, Azure Batch can use this surplus, when available.</span></span>
 
<span data-ttu-id="db312-108">The tradeoff for using low-priority VMs is that those VMs may not be available to be allocated or may be preempted at any time, depending on available capacity.</span><span class="sxs-lookup"><span data-stu-id="db312-108">The tradeoff for using low-priority VMs is that those VMs may not be available to be allocated or may be preempted at any time, depending on available capacity.</span></span> <span data-ttu-id="db312-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span><span class="sxs-lookup"><span data-stu-id="db312-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="db312-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span><span class="sxs-lookup"><span data-stu-id="db312-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>
 
<span data-ttu-id="db312-111">Low-priority VMs are offered at a significantly reduced price compared with dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="db312-111">Low-priority VMs are offered at a significantly reduced price compared with dedicated VMs.</span></span> <span data-ttu-id="db312-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="db312-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="db312-113">Use cases for low-priority VMs</span><span class="sxs-lookup"><span data-stu-id="db312-113">Use cases for low-priority VMs</span></span>

<span data-ttu-id="db312-114">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span><span class="sxs-lookup"><span data-stu-id="db312-114">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="db312-115">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span><span class="sxs-lookup"><span data-stu-id="db312-115">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="db312-116">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span><span class="sxs-lookup"><span data-stu-id="db312-116">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="db312-117">Occasionally VMs may not be available or are preempted, which results in reduced capacity for jobs and may lead to task interruption and reruns.</span><span class="sxs-lookup"><span data-stu-id="db312-117">Occasionally VMs may not be available or are preempted, which results in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="db312-118">Jobs must therefore be flexible in the time they can take to run.</span><span class="sxs-lookup"><span data-stu-id="db312-118">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="db312-119">Jobs with longer tasks may be impacted more if interrupted.</span><span class="sxs-lookup"><span data-stu-id="db312-119">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="db312-120">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption is reduced.</span><span class="sxs-lookup"><span data-stu-id="db312-120">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption is reduced.</span></span> <span data-ttu-id="db312-121">Tasks with shorter execution times tend to work best with low-priority VMs, because the impact of interruption is far less.</span><span class="sxs-lookup"><span data-stu-id="db312-121">Tasks with shorter execution times tend to work best with low-priority VMs, because the impact of interruption is far less.</span></span>

-   <span data-ttu-id="db312-122">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs, because one preempted VM can lead to the whole job having to run again.</span><span class="sxs-lookup"><span data-stu-id="db312-122">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs, because one preempted VM can lead to the whole job having to run again.</span></span>

<span data-ttu-id="db312-123">Some examples of batch processing use cases well suited to use low-priority VMs are:</span><span class="sxs-lookup"><span data-stu-id="db312-123">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="db312-124">**Development and testing**: In particular, if large-scale solutions are being developed, significant savings can be realized.</span><span class="sxs-lookup"><span data-stu-id="db312-124">**Development and testing**: In particular, if large-scale solutions are being developed, significant savings can be realized.</span></span> <span data-ttu-id="db312-125">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span><span class="sxs-lookup"><span data-stu-id="db312-125">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="db312-126">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs remains available.</span><span class="sxs-lookup"><span data-stu-id="db312-126">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs remains available.</span></span>

-   <span data-ttu-id="db312-127">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs frequently run faster and for a lower cost.</span><span class="sxs-lookup"><span data-stu-id="db312-127">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="db312-128">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span><span class="sxs-lookup"><span data-stu-id="db312-128">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="db312-129">Low-priority VMs can solely be used in a pool.</span><span class="sxs-lookup"><span data-stu-id="db312-129">Low-priority VMs can solely be used in a pool.</span></span> <span data-ttu-id="db312-130">In this case, Batch recovers any preempted capacity when available.</span><span class="sxs-lookup"><span data-stu-id="db312-130">In this case, Batch recovers any preempted capacity when available.</span></span> <span data-ttu-id="db312-131">This configuration is the cheapest way to execute jobs, as only low-priority VMs are used.</span><span class="sxs-lookup"><span data-stu-id="db312-131">This configuration is the cheapest way to execute jobs, as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="db312-132">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="db312-132">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="db312-133">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span><span class="sxs-lookup"><span data-stu-id="db312-133">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="db312-134">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required.</span><span class="sxs-lookup"><span data-stu-id="db312-134">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required.</span></span> <span data-ttu-id="db312-135">This configuration keeps a minimum amount of capacity available to keep the jobs progressing.</span><span class="sxs-lookup"><span data-stu-id="db312-135">This configuration keeps a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="db312-136">Batch support for low-priority VMs</span><span class="sxs-lookup"><span data-stu-id="db312-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="db312-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span><span class="sxs-lookup"><span data-stu-id="db312-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="db312-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span><span class="sxs-lookup"><span data-stu-id="db312-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="db312-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span><span class="sxs-lookup"><span data-stu-id="db312-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="db312-140">Job and task submission can remain unchanged, regardless of the VM types in the pool.</span><span class="sxs-lookup"><span data-stu-id="db312-140">Job and task submission can remain unchanged, regardless of the VM types in the pool.</span></span> <span data-ttu-id="db312-141">You can also configure a pool to completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span><span class="sxs-lookup"><span data-stu-id="db312-141">You can also configure a pool to completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="db312-142">Batch pools automatically seek the target number of low-priority VMs.</span><span class="sxs-lookup"><span data-stu-id="db312-142">Batch pools automatically seek the target number of low-priority VMs.</span></span> <span data-ttu-id="db312-143">If VMs are preempted, then Batch attempts to replace the lost capacity and return to the target.</span><span class="sxs-lookup"><span data-stu-id="db312-143">If VMs are preempted, then Batch attempts to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="db312-144">When tasks are interrupted, Batch detects and automatically requeues tasks to run again.</span><span class="sxs-lookup"><span data-stu-id="db312-144">When tasks are interrupted, Batch detects and automatically requeues tasks to run again.</span></span>

-   <span data-ttu-id="db312-145">Low-priority VMs have a separate vCPU quota that differs from the one for dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="db312-145">Low-priority VMs have a separate vCPU quota that differs from the one for dedicated VMs.</span></span> 
    <span data-ttu-id="db312-146">The quota for low-priority VMs is higher than the quota for dedicated VMs, because low-priority VMs cost less.</span><span class="sxs-lookup"><span data-stu-id="db312-146">The quota for low-priority VMs is higher than the quota for dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="db312-147">For more information, see [Batch service quotas and limits](batch-quota-limit.md#resource-quotas).</span><span class="sxs-lookup"><span data-stu-id="db312-147">For more information, see [Batch service quotas and limits](batch-quota-limit.md#resource-quotas).</span></span>    

> [!NOTE]
> <span data-ttu-id="db312-148">Low-priority VMs are not currently supported for Batch accounts created in [user subscription mode](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="db312-148">Low-priority VMs are not currently supported for Batch accounts created in [user subscription mode](batch-api-basics.md#account).</span></span>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="db312-149">Create and update pools</span><span class="sxs-lookup"><span data-stu-id="db312-149">Create and update pools</span></span>

<span data-ttu-id="db312-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span><span class="sxs-lookup"><span data-stu-id="db312-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="db312-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span><span class="sxs-lookup"><span data-stu-id="db312-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="db312-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span><span class="sxs-lookup"><span data-stu-id="db312-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="db312-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span><span class="sxs-lookup"><span data-stu-id="db312-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5") // WS 2016
);
```

<span data-ttu-id="db312-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span><span class="sxs-lookup"><span data-stu-id="db312-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="db312-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span><span class="sxs-lookup"><span data-stu-id="db312-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="db312-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span><span class="sxs-lookup"><span data-stu-id="db312-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="db312-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool still returns those nodes.</span><span class="sxs-lookup"><span data-stu-id="db312-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool still returns those nodes.</span></span> <span data-ttu-id="db312-158">The current number of low-priority nodes remains unchanged, but those nodes have their state set to the **Preempted** state.</span><span class="sxs-lookup"><span data-stu-id="db312-158">The current number of low-priority nodes remains unchanged, but those nodes have their state set to the **Preempted** state.</span></span> <span data-ttu-id="db312-159">Batch attempts to find replacement VMs and, if successful, the nodes go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span><span class="sxs-lookup"><span data-stu-id="db312-159">Batch attempts to find replacement VMs and, if successful, the nodes go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="db312-160">Scale a pool containing low-priority VMs</span><span class="sxs-lookup"><span data-stu-id="db312-160">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="db312-161">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using autoscale.</span><span class="sxs-lookup"><span data-stu-id="db312-161">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using autoscale.</span></span>

<span data-ttu-id="db312-162">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="db312-162">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="db312-163">The pool autoscale formula supports low-priority VMs as follows:</span><span class="sxs-lookup"><span data-stu-id="db312-163">The pool autoscale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="db312-164">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="db312-164">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="db312-165">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="db312-165">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="db312-166">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="db312-166">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="db312-167">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span><span class="sxs-lookup"><span data-stu-id="db312-167">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="db312-168">Jobs and tasks</span><span class="sxs-lookup"><span data-stu-id="db312-168">Jobs and tasks</span></span>

<span data-ttu-id="db312-169">Jobs and tasks require little additional configuration for low-priority nodes; the only support is as follows:</span><span class="sxs-lookup"><span data-stu-id="db312-169">Jobs and tasks require little additional configuration for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="db312-170">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="db312-170">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="db312-171">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span><span class="sxs-lookup"><span data-stu-id="db312-171">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="db312-172">If this property is false, the job manager task is scheduled to a dedicated node only.</span><span class="sxs-lookup"><span data-stu-id="db312-172">If this property is false, the job manager task is scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="db312-173">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span><span class="sxs-lookup"><span data-stu-id="db312-173">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="db312-174">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="db312-174">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="db312-175">Handling preemption</span><span class="sxs-lookup"><span data-stu-id="db312-175">Handling preemption</span></span>

<span data-ttu-id="db312-176">VMs may occasionally be preempted; when preemption happens, Batch does the following:</span><span class="sxs-lookup"><span data-stu-id="db312-176">VMs may occasionally be preempted; when preemption happens, Batch does the following:</span></span>

-   <span data-ttu-id="db312-177">The preempted VMs have their state updated to **Preempted**.</span><span class="sxs-lookup"><span data-stu-id="db312-177">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="db312-178">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span><span class="sxs-lookup"><span data-stu-id="db312-178">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="db312-179">The VM is effectively deleted, leading to loss of any data stored locally on the VM.</span><span class="sxs-lookup"><span data-stu-id="db312-179">The VM is effectively deleted, leading to loss of any data stored locally on the VM.</span></span>
-   <span data-ttu-id="db312-180">The pool continually attempts to reach the target number of low-priority nodes available.</span><span class="sxs-lookup"><span data-stu-id="db312-180">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="db312-181">When replacement capacity is found, the nodes keep their IDs, but are reinitialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span><span class="sxs-lookup"><span data-stu-id="db312-181">When replacement capacity is found, the nodes keep their IDs, but are reinitialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="db312-182">Preemption counts are available as a metric in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="db312-182">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="db312-183">Metrics</span><span class="sxs-lookup"><span data-stu-id="db312-183">Metrics</span></span>

<span data-ttu-id="db312-184">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span><span class="sxs-lookup"><span data-stu-id="db312-184">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="db312-185">These metrics are:</span><span class="sxs-lookup"><span data-stu-id="db312-185">These metrics are:</span></span>

- <span data-ttu-id="db312-186">Low-Priority Node Count</span><span class="sxs-lookup"><span data-stu-id="db312-186">Low-Priority Node Count</span></span>
- <span data-ttu-id="db312-187">Low-Priority Core Count</span><span class="sxs-lookup"><span data-stu-id="db312-187">Low-Priority Core Count</span></span> 
- <span data-ttu-id="db312-188">Preempted Node Count</span><span class="sxs-lookup"><span data-stu-id="db312-188">Preempted Node Count</span></span>

<span data-ttu-id="db312-189">To view metrics in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="db312-189">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="db312-190">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span><span class="sxs-lookup"><span data-stu-id="db312-190">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="db312-191">Select **Metrics** from the **Monitoring** section.</span><span class="sxs-lookup"><span data-stu-id="db312-191">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="db312-192">Select the metrics you desire from the **Available Metrics** list.</span><span class="sxs-lookup"><span data-stu-id="db312-192">Select the metrics you desire from the **Available Metrics** list.</span></span>

![Metrics for low-priority nodes](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="db312-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="db312-194">Next steps</span></span>

* <span data-ttu-id="db312-195">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span><span class="sxs-lookup"><span data-stu-id="db312-195">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="db312-196">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span><span class="sxs-lookup"><span data-stu-id="db312-196">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="db312-197">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span><span class="sxs-lookup"><span data-stu-id="db312-197">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
