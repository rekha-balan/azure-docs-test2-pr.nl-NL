---
title: Run tasks in parallel to use compute resources efficiently - Azure Batch | Microsoft Docs
description: Increase efficiency and lower costs by using fewer compute nodes and running concurrent tasks on each node in an Azure Batch pool
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: ''
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8c0a963ffb5f2cf09dbb02f99dd106950e054cc1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553445"
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="6a2fb-103">Run tasks concurrently to maximize usage of Batch compute nodes</span><span class="sxs-lookup"><span data-stu-id="6a2fb-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="6a2fb-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="6a2fb-105">For some workloads, this can result in shorter job times and lower cost.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="6a2fb-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span><span class="sxs-lookup"><span data-stu-id="6a2fb-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="6a2fb-107">**Minimizing data transfer** when tasks are able to share data.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="6a2fb-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="6a2fb-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="6a2fb-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="6a2fb-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="6a2fb-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="6a2fb-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="6a2fb-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="6a2fb-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="6a2fb-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="6a2fb-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="6a2fb-118">Example scenario</span><span class="sxs-lookup"><span data-stu-id="6a2fb-118">Example scenario</span></span>
<span data-ttu-id="6a2fb-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="6a2fb-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="6a2fb-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="6a2fb-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="6a2fb-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="6a2fb-124">Enable parallel task execution</span><span class="sxs-lookup"><span data-stu-id="6a2fb-124">Enable parallel task execution</span></span>
<span data-ttu-id="6a2fb-125">You configure compute nodes for parallel task execution at the pool level.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="6a2fb-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="6a2fb-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="6a2fb-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="6a2fb-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="6a2fb-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="6a2fb-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="6a2fb-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="6a2fb-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="6a2fb-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="6a2fb-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="6a2fb-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="6a2fb-135">Distribution of tasks</span><span class="sxs-lookup"><span data-stu-id="6a2fb-135">Distribution of tasks</span></span>
<span data-ttu-id="6a2fb-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="6a2fb-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span><span class="sxs-lookup"><span data-stu-id="6a2fb-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="6a2fb-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span><span class="sxs-lookup"><span data-stu-id="6a2fb-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="6a2fb-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="6a2fb-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span><span class="sxs-lookup"><span data-stu-id="6a2fb-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="6a2fb-141">This minimizes resource usage and saves money.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="6a2fb-142">Batch .NET example</span><span class="sxs-lookup"><span data-stu-id="6a2fb-142">Batch .NET example</span></span>
<span data-ttu-id="6a2fb-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="6a2fb-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="6a2fb-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="6a2fb-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicated: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a><span data-ttu-id="6a2fb-146">Batch REST example</span><span class="sxs-lookup"><span data-stu-id="6a2fb-146">Batch REST example</span></span>
<span data-ttu-id="6a2fb-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="6a2fb-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="6a2fb-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicated":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> <span data-ttu-id="6a2fb-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="6a2fb-150">They cannot be modified after a pool has already been created.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="6a2fb-151">Code sample</span><span class="sxs-lookup"><span data-stu-id="6a2fb-151">Code sample</span></span>
<span data-ttu-id="6a2fb-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="6a2fb-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="6a2fb-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="6a2fb-155">Output from the application specifies which nodes executed each task.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="6a2fb-156">The application also provides a summary of the job parameters and duration.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="6a2fb-157">The summary portion of the output from two different runs of the sample application appears below.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="6a2fb-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="6a2fb-159">The second run of the sample shows a significant decrease in job duration.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="6a2fb-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="6a2fb-161">The job durations in the summaries above do not include pool creation time.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="6a2fb-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6a2fb-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a2fb-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="6a2fb-164">Batch Explorer Heat Map</span><span class="sxs-lookup"><span data-stu-id="6a2fb-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="6a2fb-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="6a2fb-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span><span class="sxs-lookup"><span data-stu-id="6a2fb-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Batch Explorer Heat Map][1]

<span data-ttu-id="6a2fb-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span><span class="sxs-lookup"><span data-stu-id="6a2fb-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-parallel-node-tasks/heat_map.png

