---
title: Count states for tasks and nodes - Azure Batch | Microsoft Docs
description: Count the state of Azure Batch tasks and compute nodes to help manage and monitor Batch solutions.
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.topic: article
ms.date: 09/07/2018
ms.author: danlep
ms.openlocfilehash: e1d6f2d6181e70fde75907191664dcf6cd0b7252
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871070"
---
# <a name="monitor-batch-solutions-by-counting-tasks-and-nodes-by-state"></a><span data-ttu-id="fa832-103">Monitor Batch solutions by counting tasks and nodes by state</span><span class="sxs-lookup"><span data-stu-id="fa832-103">Monitor Batch solutions by counting tasks and nodes by state</span></span>

<span data-ttu-id="fa832-104">To monitor and manage large-scale Azure Batch solutions, you need accurate counts of resources in various states.</span><span class="sxs-lookup"><span data-stu-id="fa832-104">To monitor and manage large-scale Azure Batch solutions, you need accurate counts of resources in various states.</span></span> <span data-ttu-id="fa832-105">Azure Batch provides efficient operations to get these counts for Batch *tasks* and *compute nodes*.</span><span class="sxs-lookup"><span data-stu-id="fa832-105">Azure Batch provides efficient operations to get these counts for Batch *tasks* and *compute nodes*.</span></span> <span data-ttu-id="fa832-106">Use these operations instead of potentially time-consuming list queries that return detailed information about large collections of tasks or nodes.</span><span class="sxs-lookup"><span data-stu-id="fa832-106">Use these operations instead of potentially time-consuming list queries that return detailed information about large collections of tasks or nodes.</span></span>

* <span data-ttu-id="fa832-107">[Get Task Counts][rest_get_task_counts] gets an aggregate count of active, running, and completed tasks in a job, and of tasks that succeeded or failed.</span><span class="sxs-lookup"><span data-stu-id="fa832-107">[Get Task Counts][rest_get_task_counts] gets an aggregate count of active, running, and completed tasks in a job, and of tasks that succeeded or failed.</span></span> 

  <span data-ttu-id="fa832-108">By counting tasks in each state, you can more easily display job progress to a user, or detect unexpected delays or failures that may affect the job.</span><span class="sxs-lookup"><span data-stu-id="fa832-108">By counting tasks in each state, you can more easily display job progress to a user, or detect unexpected delays or failures that may affect the job.</span></span> <span data-ttu-id="fa832-109">Get Task Counts is available as of Batch Service API version 2017-06-01.5.1 and related SDKs and tools.</span><span class="sxs-lookup"><span data-stu-id="fa832-109">Get Task Counts is available as of Batch Service API version 2017-06-01.5.1 and related SDKs and tools.</span></span>

* <span data-ttu-id="fa832-110">[List Pool Node Counts][rest_get_node_counts] gets the number of dedicated and low-priority compute nodes in each pool that are in various states: creating, idle, offline, preempted, rebooting, reimaging, starting, and others.</span><span class="sxs-lookup"><span data-stu-id="fa832-110">[List Pool Node Counts][rest_get_node_counts] gets the number of dedicated and low-priority compute nodes in each pool that are in various states: creating, idle, offline, preempted, rebooting, reimaging, starting, and others.</span></span> 

  <span data-ttu-id="fa832-111">By counting nodes in each state, you can determine when you have adequate compute resources to run your jobs, and identify potential issues with your pools.</span><span class="sxs-lookup"><span data-stu-id="fa832-111">By counting nodes in each state, you can determine when you have adequate compute resources to run your jobs, and identify potential issues with your pools.</span></span> <span data-ttu-id="fa832-112">List Pool Node Counts is available as of Batch Service API version 2018-03-01.6.1 and related SDKs and tools.</span><span class="sxs-lookup"><span data-stu-id="fa832-112">List Pool Node Counts is available as of Batch Service API version 2018-03-01.6.1 and related SDKs and tools.</span></span>

<span data-ttu-id="fa832-113">If you're using a version of the service that doesn't support the task count or node count operations, use a list query instead to count these resources.</span><span class="sxs-lookup"><span data-stu-id="fa832-113">If you're using a version of the service that doesn't support the task count or node count operations, use a list query instead to count these resources.</span></span> <span data-ttu-id="fa832-114">Also use a list query to get information about other Batch resources such as applications, files, and jobs.</span><span class="sxs-lookup"><span data-stu-id="fa832-114">Also use a list query to get information about other Batch resources such as applications, files, and jobs.</span></span> <span data-ttu-id="fa832-115">For more information about applying filters to list queries, see [Create queries to list Batch resources efficiently](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="fa832-115">For more information about applying filters to list queries, see [Create queries to list Batch resources efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="task-state-counts"></a><span data-ttu-id="fa832-116">Task state counts</span><span class="sxs-lookup"><span data-stu-id="fa832-116">Task state counts</span></span>

<span data-ttu-id="fa832-117">The Get Task Counts operation counts tasks by the following states:</span><span class="sxs-lookup"><span data-stu-id="fa832-117">The Get Task Counts operation counts tasks by the following states:</span></span>

- <span data-ttu-id="fa832-118">**Active** - A task that is queued and able to run, but is not currently assigned to a compute node.</span><span class="sxs-lookup"><span data-stu-id="fa832-118">**Active** - A task that is queued and able to run, but is not currently assigned to a compute node.</span></span> <span data-ttu-id="fa832-119">A task is also `active` if it is [dependent on a parent task](batch-task-dependencies.md) that has not yet completed.</span><span class="sxs-lookup"><span data-stu-id="fa832-119">A task is also `active` if it is [dependent on a parent task](batch-task-dependencies.md) that has not yet completed.</span></span> 
- <span data-ttu-id="fa832-120">**Running** - A task that has been assigned to a compute node, but has not yet completed.</span><span class="sxs-lookup"><span data-stu-id="fa832-120">**Running** - A task that has been assigned to a compute node, but has not yet completed.</span></span> <span data-ttu-id="fa832-121">A task is counted as `running` when its state is either `preparing` or `running`, as indicated by the [Get information about a task][rest_get_task] operation.</span><span class="sxs-lookup"><span data-stu-id="fa832-121">A task is counted as `running` when its state is either `preparing` or `running`, as indicated by the [Get information about a task][rest_get_task] operation.</span></span>
- <span data-ttu-id="fa832-122">**Completed** - A task that is no longer eligible to run, because it either finished successfully, or finished unsuccessfully and also exhausted its retry limit.</span><span class="sxs-lookup"><span data-stu-id="fa832-122">**Completed** - A task that is no longer eligible to run, because it either finished successfully, or finished unsuccessfully and also exhausted its retry limit.</span></span> 
- <span data-ttu-id="fa832-123">**Succeeded** - A task whose result of task execution is `success`.</span><span class="sxs-lookup"><span data-stu-id="fa832-123">**Succeeded** - A task whose result of task execution is `success`.</span></span> <span data-ttu-id="fa832-124">Batch determines whether a task has succeeded or failed by checking the `TaskExecutionResult` property of the [executionInfo][rest_get_exec_info] property.</span><span class="sxs-lookup"><span data-stu-id="fa832-124">Batch determines whether a task has succeeded or failed by checking the `TaskExecutionResult` property of the [executionInfo][rest_get_exec_info] property.</span></span>
- <span data-ttu-id="fa832-125">**Failed** A task whose result of task execution is `failure`.</span><span class="sxs-lookup"><span data-stu-id="fa832-125">**Failed** A task whose result of task execution is `failure`.</span></span>

<span data-ttu-id="fa832-126">The following .NET code sample shows how to retrieve task counts by state:</span><span class="sxs-lookup"><span data-stu-id="fa832-126">The following .NET code sample shows how to retrieve task counts by state:</span></span> 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
```

<span data-ttu-id="fa832-127">You can use a similar pattern for REST and other supported languages to get task counts for a job.</span><span class="sxs-lookup"><span data-stu-id="fa832-127">You can use a similar pattern for REST and other supported languages to get task counts for a job.</span></span> 

> [!NOTE]
> <span data-ttu-id="fa832-128">Batch Service API versions before 2018-08-01.7.0 also return a `validationStatus` property in the Get Task Counts response.</span><span class="sxs-lookup"><span data-stu-id="fa832-128">Batch Service API versions before 2018-08-01.7.0 also return a `validationStatus` property in the Get Task Counts response.</span></span> <span data-ttu-id="fa832-129">This property indicates whether Batch checked the state counts for consistency with the states reported in the List Tasks API.</span><span class="sxs-lookup"><span data-stu-id="fa832-129">This property indicates whether Batch checked the state counts for consistency with the states reported in the List Tasks API.</span></span> <span data-ttu-id="fa832-130">A value of `validated` indicates only that Batch checked for consistency at least once for the job.</span><span class="sxs-lookup"><span data-stu-id="fa832-130">A value of `validated` indicates only that Batch checked for consistency at least once for the job.</span></span> <span data-ttu-id="fa832-131">The value of the `validationStatus` property does not indicate whether the counts that Get Task Counts returns are currently up-to-date.</span><span class="sxs-lookup"><span data-stu-id="fa832-131">The value of the `validationStatus` property does not indicate whether the counts that Get Task Counts returns are currently up-to-date.</span></span>
>

## <a name="node-state-counts"></a><span data-ttu-id="fa832-132">Node state counts</span><span class="sxs-lookup"><span data-stu-id="fa832-132">Node state counts</span></span>

<span data-ttu-id="fa832-133">The List Pool Node Counts operation counts compute nodes by the following states in each pool.</span><span class="sxs-lookup"><span data-stu-id="fa832-133">The List Pool Node Counts operation counts compute nodes by the following states in each pool.</span></span> <span data-ttu-id="fa832-134">Separate aggregate counts are provided for dedicated nodes and low-priority nodes in each pool.</span><span class="sxs-lookup"><span data-stu-id="fa832-134">Separate aggregate counts are provided for dedicated nodes and low-priority nodes in each pool.</span></span>

- <span data-ttu-id="fa832-135">**Creating** - An Azure-allocated VM that has not yet started to join a pool.</span><span class="sxs-lookup"><span data-stu-id="fa832-135">**Creating** - An Azure-allocated VM that has not yet started to join a pool.</span></span>
- <span data-ttu-id="fa832-136">**Idle** - An available compute node that is not currently running a task.</span><span class="sxs-lookup"><span data-stu-id="fa832-136">**Idle** - An available compute node that is not currently running a task.</span></span>
- <span data-ttu-id="fa832-137">**LeavingPool** - A node that is leaving the pool, either because the user explicitly removed it or because the pool is resizing or autoscaling down.</span><span class="sxs-lookup"><span data-stu-id="fa832-137">**LeavingPool** - A node that is leaving the pool, either because the user explicitly removed it or because the pool is resizing or autoscaling down.</span></span>
- <span data-ttu-id="fa832-138">**Offline** - A node that Batch cannot use to schedule new tasks.</span><span class="sxs-lookup"><span data-stu-id="fa832-138">**Offline** - A node that Batch cannot use to schedule new tasks.</span></span>
- <span data-ttu-id="fa832-139">**Preempted** - A low-priority node that was removed from the pool because Azure reclaimed the VM.</span><span class="sxs-lookup"><span data-stu-id="fa832-139">**Preempted** - A low-priority node that was removed from the pool because Azure reclaimed the VM.</span></span> <span data-ttu-id="fa832-140">A `preempted` node can be reinitialized when replacement low-priority VM capacity is available.</span><span class="sxs-lookup"><span data-stu-id="fa832-140">A `preempted` node can be reinitialized when replacement low-priority VM capacity is available.</span></span>
- <span data-ttu-id="fa832-141">**Rebooting** - A node that is restarting.</span><span class="sxs-lookup"><span data-stu-id="fa832-141">**Rebooting** - A node that is restarting.</span></span>
- <span data-ttu-id="fa832-142">**Reimaging** - A node on which the operating system is being reinstalled.</span><span class="sxs-lookup"><span data-stu-id="fa832-142">**Reimaging** - A node on which the operating system is being reinstalled.</span></span>
- <span data-ttu-id="fa832-143">**Running** - A node that is running one or more tasks (other than the start task).</span><span class="sxs-lookup"><span data-stu-id="fa832-143">**Running** - A node that is running one or more tasks (other than the start task).</span></span>
- <span data-ttu-id="fa832-144">**Starting** - A node on which the Batch service is starting.</span><span class="sxs-lookup"><span data-stu-id="fa832-144">**Starting** - A node on which the Batch service is starting.</span></span> 
- <span data-ttu-id="fa832-145">**StartTaskFailed** - A node on which the [start task][rest_start_task] failed and exhausted all retries, and on which `waitForSuccess` is set on the start task.</span><span class="sxs-lookup"><span data-stu-id="fa832-145">**StartTaskFailed** - A node on which the [start task][rest_start_task] failed and exhausted all retries, and on which `waitForSuccess` is set on the start task.</span></span> <span data-ttu-id="fa832-146">The node is not usable for running tasks.</span><span class="sxs-lookup"><span data-stu-id="fa832-146">The node is not usable for running tasks.</span></span>
- <span data-ttu-id="fa832-147">**Unknown** - A node that lost contact with the Batch service and whose state isn't known.</span><span class="sxs-lookup"><span data-stu-id="fa832-147">**Unknown** - A node that lost contact with the Batch service and whose state isn't known.</span></span>
- <span data-ttu-id="fa832-148">**Unusable** - A node that can't be used for task execution because of errors.</span><span class="sxs-lookup"><span data-stu-id="fa832-148">**Unusable** - A node that can't be used for task execution because of errors.</span></span>
- <span data-ttu-id="fa832-149">**WaitingForStartTask** - A node on which the start task started running, but `waitForSuccess` is set and the start task has not completed.</span><span class="sxs-lookup"><span data-stu-id="fa832-149">**WaitingForStartTask** - A node on which the start task started running, but `waitForSuccess` is set and the start task has not completed.</span></span>

<span data-ttu-id="fa832-150">The following C# snippet shows how to list node counts for all pools in the current account:</span><span class="sxs-lookup"><span data-stu-id="fa832-150">The following C# snippet shows how to list node counts for all pools in the current account:</span></span>

```csharp
foreach (var nodeCounts in batchClient.PoolOperations.ListPoolNodeCounts())
{
    Console.WriteLine("Pool Id: {0}", nodeCounts.PoolId);

    Console.WriteLine("Total dedicated node count: {0}", nodeCounts.Dedicated.Total);

    // Get dedicated node counts in Idle and Offline states; you can get additional states.
    Console.WriteLine("Dedicated node count in Idle state: {0}", nodeCounts.Dedicated.Idle);
    Console.WriteLine("Dedicated node count in Offline state: {0}", nodeCounts.Dedicated.Offline);

    Console.WriteLine("Total low priority node count: {0}", nodeCounts.LowPriority.Total);

    // Get low-priority node counts in Running and Preempted states; you can get additional states.
    Console.WriteLine("Low-priority node count in Running state: {0}", nodeCounts.LowPriority.Running);
    Console.WriteLine("Low-priority node count in Preempted state: {0}", nodeCounts.LowPriority.Preempted);
}
```
<span data-ttu-id="fa832-151">The following C# snippet shows how to list node counts for a given pool in the current account.</span><span class="sxs-lookup"><span data-stu-id="fa832-151">The following C# snippet shows how to list node counts for a given pool in the current account.</span></span>

```csharp
foreach (var nodeCounts in batchClient.PoolOperations.ListPoolNodeCounts(new ODATADetailLevel(filterClause: "poolId eq 'testpool'")))
{
    Console.WriteLine("Pool Id: {0}", nodeCounts.PoolId);

    Console.WriteLine("Total dedicated node count: {0}", nodeCounts.Dedicated.Total);

    // Get dedicated node counts in Idle and Offline states; you can get additional states.
    Console.WriteLine("Dedicated node count in Idle state: {0}", nodeCounts.Dedicated.Idle);
    Console.WriteLine("Dedicated node count in Offline state: {0}", nodeCounts.Dedicated.Offline);

    Console.WriteLine("Total low priority node count: {0}", nodeCounts.LowPriority.Total);

    // Get low-priority node counts in Running and Preempted states; you can get additional states.
    Console.WriteLine("Low-priority node count in Running state: {0}", nodeCounts.LowPriority.Running);
    Console.WriteLine("Low-priority node count in Preempted state: {0}", nodeCounts.LowPriority.Preempted);
}
```
<span data-ttu-id="fa832-152">You can use a similar pattern for REST and other supported languages to get node counts for pools.</span><span class="sxs-lookup"><span data-stu-id="fa832-152">You can use a similar pattern for REST and other supported languages to get node counts for pools.</span></span>
 
## <a name="next-steps"></a><span data-ttu-id="fa832-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa832-153">Next steps</span></span>

* <span data-ttu-id="fa832-154">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span><span class="sxs-lookup"><span data-stu-id="fa832-154">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span></span> <span data-ttu-id="fa832-155">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features.</span><span class="sxs-lookup"><span data-stu-id="fa832-155">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features.</span></span>

* <span data-ttu-id="fa832-156">For information about applying filters to queries that list Batch resources, see [Create queries to list Batch resources efficiently](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="fa832-156">For information about applying filters to queries that list Batch resources, see [Create queries to list Batch resources efficiently](batch-efficient-list-queries.md).</span></span>


[rest_get_task_counts]: /rest/api/batchservice/job/gettaskcounts
[rest_get_node_counts]: /rest/api/batchservice/account/listpoolnodecounts
[rest_get_task]: /rest/api/batchservice/task/get
[rest_list_tasks]: /rest/api/batchservice/task/list
[rest_get_exec_info]: /rest/api/batchservice/task/get#executionInfo
[rest_start_task]: /rest/api/batchservice/pool/add#starttask

