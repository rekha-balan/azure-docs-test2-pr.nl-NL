---
title: Automatically scale compute nodes in an Azure Batch pool | Microsoft Docs
description: Enable automatic scaling on a cloud pool to dynamically adjust the number of compute nodes in the pool.
services: batch
documentationcenter: ''
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 04/03/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0563f6c3aa4508ef2acac6b17dc85ecbf11bb154
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555294"
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a><span data-ttu-id="1c2ac-103">Create an automatic scaling formula for scaling compute nodes in a Batch pool</span><span class="sxs-lookup"><span data-stu-id="1c2ac-103">Create an automatic scaling formula for scaling compute nodes in a Batch pool</span></span>

<span data-ttu-id="1c2ac-104">With automatic scaling, the Azure Batch service can dynamically add or remove compute nodes in a pool based on parameters that you define.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-104">With automatic scaling, the Azure Batch service can dynamically add or remove compute nodes in a pool based on parameters that you define.</span></span> <span data-ttu-id="1c2ac-105">You can save both time and money by automatically adjusting the number of compute nodes used by your application.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-105">You can save both time and money by automatically adjusting the number of compute nodes used by your application.</span></span> <span data-ttu-id="1c2ac-106">Automatic scaling enables you to add nodes as your job's task demands increase, and remove them when they decrease.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-106">Automatic scaling enables you to add nodes as your job's task demands increase, and remove them when they decrease.</span></span>

<span data-ttu-id="1c2ac-107">You enable automatic scaling on a pool of compute nodes by associating with it an *autoscale formula* that you define.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-107">You enable automatic scaling on a pool of compute nodes by associating with it an *autoscale formula* that you define.</span></span> <span data-ttu-id="1c2ac-108">For example, in Batch .NET, you can use the [PoolOperations.EnableAutoScale][net_enableautoscale] method.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-108">For example, in Batch .NET, you can use the [PoolOperations.EnableAutoScale][net_enableautoscale] method.</span></span> <span data-ttu-id="1c2ac-109">The Batch service uses the autoscale formula to determine the number of compute nodes that are needed to execute your workload.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-109">The Batch service uses the autoscale formula to determine the number of compute nodes that are needed to execute your workload.</span></span> <span data-ttu-id="1c2ac-110">Batch responds to service metrics data that is collected periodically.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-110">Batch responds to service metrics data that is collected periodically.</span></span> <span data-ttu-id="1c2ac-111">Using this metrics data, Batch adjusts the number of compute nodes in the pool based on your formula and at a configurable interval .</span><span class="sxs-lookup"><span data-stu-id="1c2ac-111">Using this metrics data, Batch adjusts the number of compute nodes in the pool based on your formula and at a configurable interval .</span></span>

<span data-ttu-id="1c2ac-112">You can enable automatic scaling when a pool is created, or on an existing pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-112">You can enable automatic scaling when a pool is created, or on an existing pool.</span></span> <span data-ttu-id="1c2ac-113">You can also change an existing formula on a pool that is "autoscale" enabled.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-113">You can also change an existing formula on a pool that is "autoscale" enabled.</span></span> <span data-ttu-id="1c2ac-114">Batch enables you to evaluate your formulas before assigning them to pools and to monitor the status of automatic scaling runs.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-114">Batch enables you to evaluate your formulas before assigning them to pools and to monitor the status of automatic scaling runs.</span></span>

<span data-ttu-id="1c2ac-115">This article discusses the various entities that make up your autoscale formulas, including variables, operators, operations, and functions.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-115">This article discusses the various entities that make up your autoscale formulas, including variables, operators, operations, and functions.</span></span> <span data-ttu-id="1c2ac-116">You'll find out how to obtain various compute resource and task metrics within Batch.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-116">You'll find out how to obtain various compute resource and task metrics within Batch.</span></span> <span data-ttu-id="1c2ac-117">You can use these metrics to intelligently adjust your pool's node count based on resource usage and task status.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-117">You can use these metrics to intelligently adjust your pool's node count based on resource usage and task status.</span></span> <span data-ttu-id="1c2ac-118">You'll then learn how to construct a formula and enable automatic scaling on a pool by using both the Batch REST and .NET APIs.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-118">You'll then learn how to construct a formula and enable automatic scaling on a pool by using both the Batch REST and .NET APIs.</span></span> <span data-ttu-id="1c2ac-119">We'll finish up with a few example formulas.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-119">We'll finish up with a few example formulas.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c2ac-120">Each Azure Batch account is limited to a maximum number of cores (and therefore compute nodes) that can be used for processing.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-120">Each Azure Batch account is limited to a maximum number of cores (and therefore compute nodes) that can be used for processing.</span></span> <span data-ttu-id="1c2ac-121">The Batch service creates new nodes only up to that core limit.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-121">The Batch service creates new nodes only up to that core limit.</span></span> <span data-ttu-id="1c2ac-122">The Batch service may not reach the target number of compute nodes specified by an autoscale formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-122">The Batch service may not reach the target number of compute nodes specified by an autoscale formula.</span></span> <span data-ttu-id="1c2ac-123">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for information on viewing and increasing your account quotas.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-123">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for information on viewing and increasing your account quotas.</span></span>
> 
> 

## <a name="automatic-scaling-formulas"></a><span data-ttu-id="1c2ac-124">Automatic scaling formulas</span><span class="sxs-lookup"><span data-stu-id="1c2ac-124">Automatic scaling formulas</span></span>
<span data-ttu-id="1c2ac-125">An automatic scaling formula is a string value that you define that contains one or more statements.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-125">An automatic scaling formula is a string value that you define that contains one or more statements.</span></span> <span data-ttu-id="1c2ac-126">The autoscale formula is assigned to a pool's [autoScaleFormula][rest_autoscaleformula] element (Batch REST) or [CloudPool.AutoScaleFormula][net_cloudpool_autoscaleformula] property (Batch .NET).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-126">The autoscale formula is assigned to a pool's [autoScaleFormula][rest_autoscaleformula] element (Batch REST) or [CloudPool.AutoScaleFormula][net_cloudpool_autoscaleformula] property (Batch .NET).</span></span> <span data-ttu-id="1c2ac-127">The Batch service uses your formula to determine the target number of compute nodes in the pool for the next interval of processing.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-127">The Batch service uses your formula to determine the target number of compute nodes in the pool for the next interval of processing.</span></span> <span data-ttu-id="1c2ac-128">The formula string cannot exceed 8 KB in size, can include up to 100 statements that are separated by semicolons, and can include line breaks and comments.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-128">The formula string cannot exceed 8 KB in size, can include up to 100 statements that are separated by semicolons, and can include line breaks and comments.</span></span>

<span data-ttu-id="1c2ac-129">You can think of automatic scaling formulas as using a Batch autoscale "language."</span><span class="sxs-lookup"><span data-stu-id="1c2ac-129">You can think of automatic scaling formulas as using a Batch autoscale "language."</span></span> <span data-ttu-id="1c2ac-130">Formula statements are free-formed expressions that can include both service-defined variables (variables defined by the Batch service) and user-defined variables (variables that you define).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-130">Formula statements are free-formed expressions that can include both service-defined variables (variables defined by the Batch service) and user-defined variables (variables that you define).</span></span> <span data-ttu-id="1c2ac-131">They can perform various operations on these values by using built-in types, operators, and functions.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-131">They can perform various operations on these values by using built-in types, operators, and functions.</span></span> <span data-ttu-id="1c2ac-132">For example, a statement might take the following form:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-132">For example, a statement might take the following form:</span></span>

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

<span data-ttu-id="1c2ac-133">Formulas generally contain multiple statements that perform operations on values that are obtained in previous statements.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-133">Formulas generally contain multiple statements that perform operations on values that are obtained in previous statements.</span></span> <span data-ttu-id="1c2ac-134">For example, first we obtain a value for `variable1`, then pass it to a function to populate `variable2`:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-134">For example, first we obtain a value for `variable1`, then pass it to a function to populate `variable2`:</span></span>

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

<span data-ttu-id="1c2ac-135">Include these statements in your autoscale formula in order to arrive at a number of compute nodes that the pool should be scaled to--the **target** number of **dedicated nodes**.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-135">Include these statements in your autoscale formula in order to arrive at a number of compute nodes that the pool should be scaled to--the **target** number of **dedicated nodes**.</span></span> <span data-ttu-id="1c2ac-136">This number may be higher, lower, or the same as the current number of nodes in the pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-136">This number may be higher, lower, or the same as the current number of nodes in the pool.</span></span> <span data-ttu-id="1c2ac-137">Batch evaluates a pool's autoscale formula at a specific interval ([automatic scaling intervals](#automatic-scaling-interval) are discussed below).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-137">Batch evaluates a pool's autoscale formula at a specific interval ([automatic scaling intervals](#automatic-scaling-interval) are discussed below).</span></span> <span data-ttu-id="1c2ac-138">Batch adjusts the target number of nodes in the pool to the number that your autoscale formula specifies at the time of evaluation.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-138">Batch adjusts the target number of nodes in the pool to the number that your autoscale formula specifies at the time of evaluation.</span></span>

### <a name="sample-autoscale-formula"></a><span data-ttu-id="1c2ac-139">Sample autoscale formula</span><span class="sxs-lookup"><span data-stu-id="1c2ac-139">Sample autoscale formula</span></span>

<span data-ttu-id="1c2ac-140">Here is an example of an autoscale formula that can be adjusted to work for most scenarios.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-140">Here is an example of an autoscale formula that can be adjusted to work for most scenarios.</span></span> <span data-ttu-id="1c2ac-141">The variables `startingNumberOfVMs` and `maxNumberofVMs` in the example formula can be adjusted to your needs.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-141">The variables `startingNumberOfVMs` and `maxNumberofVMs` in the example formula can be adjusted to your needs.</span></span>

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs, pendingTaskSamples);
```

<span data-ttu-id="1c2ac-142">With this autoscale formula, the pool is initially created with a single VM.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-142">With this autoscale formula, the pool is initially created with a single VM.</span></span> <span data-ttu-id="1c2ac-143">The $PendingTasks metric defines the number of tasks that are running or queued.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-143">The $PendingTasks metric defines the number of tasks that are running or queued.</span></span> <span data-ttu-id="1c2ac-144">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-144">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="1c2ac-145">The formula ensures that TargetDedicated never exceeds 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-145">The formula ensures that TargetDedicated never exceeds 25 VMs.</span></span> <span data-ttu-id="1c2ac-146">As new tasks are submitted, the pool automatically grows.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-146">As new tasks are submitted, the pool automatically grows.</span></span> <span data-ttu-id="1c2ac-147">As tasks complete, VMs become free one by one and the autoscaling formula shrinks the pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-147">As tasks complete, VMs become free one by one and the autoscaling formula shrinks the pool.</span></span>

## <a name="variables"></a><span data-ttu-id="1c2ac-148">Variables</span><span class="sxs-lookup"><span data-stu-id="1c2ac-148">Variables</span></span>
<span data-ttu-id="1c2ac-149">You can use both **service-defined** and **user-defined** variables in your autoscale formulas.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-149">You can use both **service-defined** and **user-defined** variables in your autoscale formulas.</span></span> <span data-ttu-id="1c2ac-150">The service-defined variables are built in to the Batch service--some are read-write, and some are read-only.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-150">The service-defined variables are built in to the Batch service--some are read-write, and some are read-only.</span></span> <span data-ttu-id="1c2ac-151">User-defined variables are variables that *you* define.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-151">User-defined variables are variables that *you* define.</span></span> <span data-ttu-id="1c2ac-152">In the example formula shown in the previous section, `$TargetDedicated` and `$PendingTasks` are service-defined variables.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-152">In the example formula shown in the previous section, `$TargetDedicated` and `$PendingTasks` are service-defined variables.</span></span> <span data-ttu-id="1c2ac-153">Variables `startingNumberOfVMs` and `maxNumberofVMs` are user-defined variables.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-153">Variables `startingNumberOfVMs` and `maxNumberofVMs` are user-defined variables.</span></span>

> [!NOTE]
> <span data-ttu-id="1c2ac-154">Service-defined variables are always preceeded by a dollar sign ($).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-154">Service-defined variables are always preceeded by a dollar sign ($).</span></span> <span data-ttu-id="1c2ac-155">For user-defined variables, the dollar sign is optional.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-155">For user-defined variables, the dollar sign is optional.</span></span>
>
>

<span data-ttu-id="1c2ac-156">The tables below show both read-write and read-only variables that are defined by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-156">The tables below show both read-write and read-only variables that are defined by the Batch service.</span></span>

<span data-ttu-id="1c2ac-157">You can **get** and **set** the values of these service-defined variables to manage the number of compute nodes in a pool:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-157">You can **get** and **set** the values of these service-defined variables to manage the number of compute nodes in a pool:</span></span>

| <span data-ttu-id="1c2ac-158">Read-write service-defined variables</span><span class="sxs-lookup"><span data-stu-id="1c2ac-158">Read-write service-defined variables</span></span> | <span data-ttu-id="1c2ac-159">Description</span><span class="sxs-lookup"><span data-stu-id="1c2ac-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c2ac-160">$TargetDedicated</span><span class="sxs-lookup"><span data-stu-id="1c2ac-160">$TargetDedicated</span></span> |<span data-ttu-id="1c2ac-161">The **target** number of **dedicated compute nodes** for the pool is the number of compute nodes that the pool should be scaled to.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-161">The **target** number of **dedicated compute nodes** for the pool is the number of compute nodes that the pool should be scaled to.</span></span> <span data-ttu-id="1c2ac-162">It is a "target" number since it's possible for a pool not to reach the target number of nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-162">It is a "target" number since it's possible for a pool not to reach the target number of nodes.</span></span> <span data-ttu-id="1c2ac-163">For example, if the target number of nodes is modified again by a subsequent autoscale evaluation before the pool has reached the initial target, the pool may not reach the target number of nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-163">For example, if the target number of nodes is modified again by a subsequent autoscale evaluation before the pool has reached the initial target, the pool may not reach the target number of nodes.</span></span> <span data-ttu-id="1c2ac-164">It can also happen if a Batch account node or core quota is reached before the target number of nodes is reached.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-164">It can also happen if a Batch account node or core quota is reached before the target number of nodes is reached.</span></span> |
| <span data-ttu-id="1c2ac-165">$NodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="1c2ac-165">$NodeDeallocationOption</span></span> |<span data-ttu-id="1c2ac-166">The action that occurs when compute nodes are removed from a pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-166">The action that occurs when compute nodes are removed from a pool.</span></span> <span data-ttu-id="1c2ac-167">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-167">Possible values are:</span></span><ul><li><span data-ttu-id="1c2ac-168">**requeue**--Terminates tasks immediately and puts them back on the job queue so that they are rescheduled.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-168">**requeue**--Terminates tasks immediately and puts them back on the job queue so that they are rescheduled.</span></span><li><span data-ttu-id="1c2ac-169">**terminate**--Terminates tasks immediately and removes them from the job queue.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-169">**terminate**--Terminates tasks immediately and removes them from the job queue.</span></span><li><span data-ttu-id="1c2ac-170">**taskcompletion**--Waits for currently running tasks to finish and then removes the node from the pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-170">**taskcompletion**--Waits for currently running tasks to finish and then removes the node from the pool.</span></span><li><span data-ttu-id="1c2ac-171">**retaineddata**--Waits for all the local task-retained data on the node to be cleaned up before removing the node from the pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-171">**retaineddata**--Waits for all the local task-retained data on the node to be cleaned up before removing the node from the pool.</span></span></ul> |

<span data-ttu-id="1c2ac-172">You can **get** the value of these service-defined variables to make adjustments that are based on metrics from the Batch service:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-172">You can **get** the value of these service-defined variables to make adjustments that are based on metrics from the Batch service:</span></span>

| <span data-ttu-id="1c2ac-173">Read-only service-defined variables</span><span class="sxs-lookup"><span data-stu-id="1c2ac-173">Read-only service-defined variables</span></span> | <span data-ttu-id="1c2ac-174">Description</span><span class="sxs-lookup"><span data-stu-id="1c2ac-174">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c2ac-175">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="1c2ac-175">$CPUPercent</span></span> |<span data-ttu-id="1c2ac-176">The average percentage of CPU usage.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-176">The average percentage of CPU usage.</span></span> |
| <span data-ttu-id="1c2ac-177">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="1c2ac-177">$WallClockSeconds</span></span> |<span data-ttu-id="1c2ac-178">The number of seconds consumed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-178">The number of seconds consumed.</span></span> |
| <span data-ttu-id="1c2ac-179">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-179">$MemoryBytes</span></span> |<span data-ttu-id="1c2ac-180">The average number of megabytes used.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-180">The average number of megabytes used.</span></span> |
| <span data-ttu-id="1c2ac-181">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-181">$DiskBytes</span></span> |<span data-ttu-id="1c2ac-182">The average number of gigabytes used on the local disks.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-182">The average number of gigabytes used on the local disks.</span></span> |
| <span data-ttu-id="1c2ac-183">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-183">$DiskReadBytes</span></span> |<span data-ttu-id="1c2ac-184">The number of bytes read.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-184">The number of bytes read.</span></span> |
| <span data-ttu-id="1c2ac-185">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-185">$DiskWriteBytes</span></span> |<span data-ttu-id="1c2ac-186">The number of bytes written.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-186">The number of bytes written.</span></span> |
| <span data-ttu-id="1c2ac-187">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="1c2ac-187">$DiskReadOps</span></span> |<span data-ttu-id="1c2ac-188">The count of read disk operations performed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-188">The count of read disk operations performed.</span></span> |
| <span data-ttu-id="1c2ac-189">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="1c2ac-189">$DiskWriteOps</span></span> |<span data-ttu-id="1c2ac-190">The count of write disk operations performed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-190">The count of write disk operations performed.</span></span> |
| <span data-ttu-id="1c2ac-191">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-191">$NetworkInBytes</span></span> |<span data-ttu-id="1c2ac-192">The number of inbound bytes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-192">The number of inbound bytes.</span></span> |
| <span data-ttu-id="1c2ac-193">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-193">$NetworkOutBytes</span></span> |<span data-ttu-id="1c2ac-194">The number of outbound bytes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-194">The number of outbound bytes.</span></span> |
| <span data-ttu-id="1c2ac-195">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="1c2ac-195">$SampleNodeCount</span></span> |<span data-ttu-id="1c2ac-196">The count of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-196">The count of compute nodes.</span></span> |
| <span data-ttu-id="1c2ac-197">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-197">$ActiveTasks</span></span> |<span data-ttu-id="1c2ac-198">The number of tasks in an active state.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-198">The number of tasks in an active state.</span></span> |
| <span data-ttu-id="1c2ac-199">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-199">$RunningTasks</span></span> |<span data-ttu-id="1c2ac-200">The number of tasks in a running state.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-200">The number of tasks in a running state.</span></span> |
| <span data-ttu-id="1c2ac-201">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-201">$PendingTasks</span></span> |<span data-ttu-id="1c2ac-202">The sum of $ActiveTasks and $RunningTasks.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-202">The sum of $ActiveTasks and $RunningTasks.</span></span> |
| <span data-ttu-id="1c2ac-203">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-203">$SucceededTasks</span></span> |<span data-ttu-id="1c2ac-204">The number of tasks that finished successfully.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-204">The number of tasks that finished successfully.</span></span> |
| <span data-ttu-id="1c2ac-205">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-205">$FailedTasks</span></span> |<span data-ttu-id="1c2ac-206">The number of tasks that failed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-206">The number of tasks that failed.</span></span> |
| <span data-ttu-id="1c2ac-207">$CurrentDedicated</span><span class="sxs-lookup"><span data-stu-id="1c2ac-207">$CurrentDedicated</span></span> |<span data-ttu-id="1c2ac-208">The current number of dedicated compute nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-208">The current number of dedicated compute nodes.</span></span> |

> [!TIP]
> <span data-ttu-id="1c2ac-209">The read-only, service-defined variables that are shown above are *objects* that provide various methods to access data associated with each.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-209">The read-only, service-defined variables that are shown above are *objects* that provide various methods to access data associated with each.</span></span> <span data-ttu-id="1c2ac-210">For more information, see [Obtain sample data](#getsampledata) below.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-210">For more information, see [Obtain sample data](#getsampledata) below.</span></span>
> 
> 

## <a name="types"></a><span data-ttu-id="1c2ac-211">Types</span><span class="sxs-lookup"><span data-stu-id="1c2ac-211">Types</span></span>
<span data-ttu-id="1c2ac-212">These **types** are supported in a formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-212">These **types** are supported in a formula.</span></span>

* <span data-ttu-id="1c2ac-213">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-213">double</span></span>
* <span data-ttu-id="1c2ac-214">doubleVec</span><span class="sxs-lookup"><span data-stu-id="1c2ac-214">doubleVec</span></span>
* <span data-ttu-id="1c2ac-215">doubleVecList</span><span class="sxs-lookup"><span data-stu-id="1c2ac-215">doubleVecList</span></span>
* <span data-ttu-id="1c2ac-216">string</span><span class="sxs-lookup"><span data-stu-id="1c2ac-216">string</span></span>
* <span data-ttu-id="1c2ac-217">timestamp--timestamp is a compound structure that contains the following members:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-217">timestamp--timestamp is a compound structure that contains the following members:</span></span>
  
  * <span data-ttu-id="1c2ac-218">year</span><span class="sxs-lookup"><span data-stu-id="1c2ac-218">year</span></span>
  * <span data-ttu-id="1c2ac-219">month (1-12)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-219">month (1-12)</span></span>
  * <span data-ttu-id="1c2ac-220">day (1-31)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-220">day (1-31)</span></span>
  * <span data-ttu-id="1c2ac-221">weekday (in the format of number, e.g. 1 for Monday)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-221">weekday (in the format of number, e.g. 1 for Monday)</span></span>
  * <span data-ttu-id="1c2ac-222">hour (in 24-hour number format, e.g. 13 means 1 PM)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-222">hour (in 24-hour number format, e.g. 13 means 1 PM)</span></span>
  * <span data-ttu-id="1c2ac-223">minute (00-59)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-223">minute (00-59)</span></span>
  * <span data-ttu-id="1c2ac-224">second (00-59)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-224">second (00-59)</span></span>
* <span data-ttu-id="1c2ac-225">timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-225">timeinterval</span></span>
  
  * <span data-ttu-id="1c2ac-226">TimeInterval_Zero</span><span class="sxs-lookup"><span data-stu-id="1c2ac-226">TimeInterval_Zero</span></span>
  * <span data-ttu-id="1c2ac-227">TimeInterval_100ns</span><span class="sxs-lookup"><span data-stu-id="1c2ac-227">TimeInterval_100ns</span></span>
  * <span data-ttu-id="1c2ac-228">TimeInterval_Microsecond</span><span class="sxs-lookup"><span data-stu-id="1c2ac-228">TimeInterval_Microsecond</span></span>
  * <span data-ttu-id="1c2ac-229">TimeInterval_Millisecond</span><span class="sxs-lookup"><span data-stu-id="1c2ac-229">TimeInterval_Millisecond</span></span>
  * <span data-ttu-id="1c2ac-230">TimeInterval_Second</span><span class="sxs-lookup"><span data-stu-id="1c2ac-230">TimeInterval_Second</span></span>
  * <span data-ttu-id="1c2ac-231">TimeInterval_Minute</span><span class="sxs-lookup"><span data-stu-id="1c2ac-231">TimeInterval_Minute</span></span>
  * <span data-ttu-id="1c2ac-232">TimeInterval_Hour</span><span class="sxs-lookup"><span data-stu-id="1c2ac-232">TimeInterval_Hour</span></span>
  * <span data-ttu-id="1c2ac-233">TimeInterval_Day</span><span class="sxs-lookup"><span data-stu-id="1c2ac-233">TimeInterval_Day</span></span>
  * <span data-ttu-id="1c2ac-234">TimeInterval_Week</span><span class="sxs-lookup"><span data-stu-id="1c2ac-234">TimeInterval_Week</span></span>
  * <span data-ttu-id="1c2ac-235">TimeInterval_Year</span><span class="sxs-lookup"><span data-stu-id="1c2ac-235">TimeInterval_Year</span></span>

## <a name="operations"></a><span data-ttu-id="1c2ac-236">Operations</span><span class="sxs-lookup"><span data-stu-id="1c2ac-236">Operations</span></span>
<span data-ttu-id="1c2ac-237">These **operations** are allowed on the types that are listed above.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-237">These **operations** are allowed on the types that are listed above.</span></span>

| <span data-ttu-id="1c2ac-238">Operation</span><span class="sxs-lookup"><span data-stu-id="1c2ac-238">Operation</span></span> | <span data-ttu-id="1c2ac-239">Supported operators</span><span class="sxs-lookup"><span data-stu-id="1c2ac-239">Supported operators</span></span> | <span data-ttu-id="1c2ac-240">Result type</span><span class="sxs-lookup"><span data-stu-id="1c2ac-240">Result type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1c2ac-241">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-241">double *operator* double</span></span> |<span data-ttu-id="1c2ac-242">+, -, \*, /</span><span class="sxs-lookup"><span data-stu-id="1c2ac-242">+, -, \*, /</span></span> |<span data-ttu-id="1c2ac-243">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-243">double</span></span> |
| <span data-ttu-id="1c2ac-244">double *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-244">double *operator* timeinterval</span></span> |* |<span data-ttu-id="1c2ac-245">timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-245">timeinterval</span></span> |
| <span data-ttu-id="1c2ac-246">doubleVec *operator* double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-246">doubleVec *operator* double</span></span> |<span data-ttu-id="1c2ac-247">+, -, \*, /</span><span class="sxs-lookup"><span data-stu-id="1c2ac-247">+, -, \*, /</span></span> |<span data-ttu-id="1c2ac-248">doubleVec</span><span class="sxs-lookup"><span data-stu-id="1c2ac-248">doubleVec</span></span> |
| <span data-ttu-id="1c2ac-249">doubleVec *operator* doubleVec</span><span class="sxs-lookup"><span data-stu-id="1c2ac-249">doubleVec *operator* doubleVec</span></span> |<span data-ttu-id="1c2ac-250">+, -, \*, /</span><span class="sxs-lookup"><span data-stu-id="1c2ac-250">+, -, \*, /</span></span> |<span data-ttu-id="1c2ac-251">doubleVec</span><span class="sxs-lookup"><span data-stu-id="1c2ac-251">doubleVec</span></span> |
| <span data-ttu-id="1c2ac-252">timeinterval *operator* double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-252">timeinterval *operator* double</span></span> |<span data-ttu-id="1c2ac-253">\*, /</span><span class="sxs-lookup"><span data-stu-id="1c2ac-253">\*, /</span></span> |<span data-ttu-id="1c2ac-254">timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-254">timeinterval</span></span> |
| <span data-ttu-id="1c2ac-255">timeinterval *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-255">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="1c2ac-256">+, -</span><span class="sxs-lookup"><span data-stu-id="1c2ac-256">+, -</span></span> |<span data-ttu-id="1c2ac-257">timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-257">timeinterval</span></span> |
| <span data-ttu-id="1c2ac-258">timeinterval *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="1c2ac-258">timeinterval *operator* timestamp</span></span> |+ |<span data-ttu-id="1c2ac-259">timestamp</span><span class="sxs-lookup"><span data-stu-id="1c2ac-259">timestamp</span></span> |
| <span data-ttu-id="1c2ac-260">timestamp *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-260">timestamp *operator* timeinterval</span></span> |+ |<span data-ttu-id="1c2ac-261">timestamp</span><span class="sxs-lookup"><span data-stu-id="1c2ac-261">timestamp</span></span> |
| <span data-ttu-id="1c2ac-262">timestamp *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="1c2ac-262">timestamp *operator* timestamp</span></span> |- |<span data-ttu-id="1c2ac-263">timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-263">timeinterval</span></span> |
| <span data-ttu-id="1c2ac-264">*operator*double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-264">*operator*double</span></span> |<span data-ttu-id="1c2ac-265">-, !</span><span class="sxs-lookup"><span data-stu-id="1c2ac-265">-, !</span></span> |<span data-ttu-id="1c2ac-266">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-266">double</span></span> |
| <span data-ttu-id="1c2ac-267">*operator*timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-267">*operator*timeinterval</span></span> |- |<span data-ttu-id="1c2ac-268">timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-268">timeinterval</span></span> |
| <span data-ttu-id="1c2ac-269">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-269">double *operator* double</span></span> |<span data-ttu-id="1c2ac-270"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="1c2ac-270"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="1c2ac-271">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-271">double</span></span> |
| <span data-ttu-id="1c2ac-272">string *operator* string</span><span class="sxs-lookup"><span data-stu-id="1c2ac-272">string *operator* string</span></span> |<span data-ttu-id="1c2ac-273"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="1c2ac-273"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="1c2ac-274">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-274">double</span></span> |
| <span data-ttu-id="1c2ac-275">timestamp *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="1c2ac-275">timestamp *operator* timestamp</span></span> |<span data-ttu-id="1c2ac-276"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="1c2ac-276"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="1c2ac-277">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-277">double</span></span> |
| <span data-ttu-id="1c2ac-278">timeinterval *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-278">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="1c2ac-279"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="1c2ac-279"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="1c2ac-280">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-280">double</span></span> |
| <span data-ttu-id="1c2ac-281">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-281">double *operator* double</span></span> |<span data-ttu-id="1c2ac-282">&&, &#124;&#124;</span><span class="sxs-lookup"><span data-stu-id="1c2ac-282">&&, &#124;&#124;</span></span> |<span data-ttu-id="1c2ac-283">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-283">double</span></span> |

<span data-ttu-id="1c2ac-284">When testing a double with a ternary operator (`double ? statement1 : statement2`), nonzero is **true**, and zero is **false**.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-284">When testing a double with a ternary operator (`double ? statement1 : statement2`), nonzero is **true**, and zero is **false**.</span></span>

## <a name="functions"></a><span data-ttu-id="1c2ac-285">Functions</span><span class="sxs-lookup"><span data-stu-id="1c2ac-285">Functions</span></span>
<span data-ttu-id="1c2ac-286">These predefined **functions** are available for you to use in defining an automatic scaling formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-286">These predefined **functions** are available for you to use in defining an automatic scaling formula.</span></span>

| <span data-ttu-id="1c2ac-287">Function</span><span class="sxs-lookup"><span data-stu-id="1c2ac-287">Function</span></span> | <span data-ttu-id="1c2ac-288">Return type</span><span class="sxs-lookup"><span data-stu-id="1c2ac-288">Return type</span></span> | <span data-ttu-id="1c2ac-289">Description</span><span class="sxs-lookup"><span data-stu-id="1c2ac-289">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1c2ac-290">avg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-290">avg(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-291">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-291">double</span></span> |<span data-ttu-id="1c2ac-292">Returns the average value for all values in the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-292">Returns the average value for all values in the doubleVecList.</span></span> |
| <span data-ttu-id="1c2ac-293">len(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-293">len(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-294">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-294">double</span></span> |<span data-ttu-id="1c2ac-295">Returns the length of the vector that is created from the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-295">Returns the length of the vector that is created from the doubleVecList.</span></span> |
| <span data-ttu-id="1c2ac-296">lg(double)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-296">lg(double)</span></span> |<span data-ttu-id="1c2ac-297">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-297">double</span></span> |<span data-ttu-id="1c2ac-298">Returns the log base 2 of the double.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-298">Returns the log base 2 of the double.</span></span> |
| <span data-ttu-id="1c2ac-299">lg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-299">lg(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-300">doubleVec</span><span class="sxs-lookup"><span data-stu-id="1c2ac-300">doubleVec</span></span> |<span data-ttu-id="1c2ac-301">Returns the component-wise log base 2 of the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-301">Returns the component-wise log base 2 of the doubleVecList.</span></span> <span data-ttu-id="1c2ac-302">A vec(double) must be explicitly passed for the parameter.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-302">A vec(double) must be explicitly passed for the parameter.</span></span> <span data-ttu-id="1c2ac-303">Otherwise, the double lg(double) version is assumed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-303">Otherwise, the double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="1c2ac-304">ln(double)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-304">ln(double)</span></span> |<span data-ttu-id="1c2ac-305">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-305">double</span></span> |<span data-ttu-id="1c2ac-306">Returns the natural log of the double.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-306">Returns the natural log of the double.</span></span> |
| <span data-ttu-id="1c2ac-307">ln(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-307">ln(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-308">doubleVec</span><span class="sxs-lookup"><span data-stu-id="1c2ac-308">doubleVec</span></span> |<span data-ttu-id="1c2ac-309">Returns the component-wise log base 2 of the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-309">Returns the component-wise log base 2 of the doubleVecList.</span></span> <span data-ttu-id="1c2ac-310">A vec(double) must be explicitly passed for the parameter.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-310">A vec(double) must be explicitly passed for the parameter.</span></span> <span data-ttu-id="1c2ac-311">Otherwise, the double lg(double) version is assumed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-311">Otherwise, the double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="1c2ac-312">log(double)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-312">log(double)</span></span> |<span data-ttu-id="1c2ac-313">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-313">double</span></span> |<span data-ttu-id="1c2ac-314">Returns the log base 10 of the double.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-314">Returns the log base 10 of the double.</span></span> |
| <span data-ttu-id="1c2ac-315">log(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-315">log(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-316">doubleVec</span><span class="sxs-lookup"><span data-stu-id="1c2ac-316">doubleVec</span></span> |<span data-ttu-id="1c2ac-317">Returns the component-wise log base 10 of the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-317">Returns the component-wise log base 10 of the doubleVecList.</span></span> <span data-ttu-id="1c2ac-318">A vec(double) must be explicitly passed for the single double parameter.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-318">A vec(double) must be explicitly passed for the single double parameter.</span></span> <span data-ttu-id="1c2ac-319">Otherwise, the double log(double) version is assumed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-319">Otherwise, the double log(double) version is assumed.</span></span> |
| <span data-ttu-id="1c2ac-320">max(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-320">max(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-321">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-321">double</span></span> |<span data-ttu-id="1c2ac-322">Returns the maximum value in the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-322">Returns the maximum value in the doubleVecList.</span></span> |
| <span data-ttu-id="1c2ac-323">min(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-323">min(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-324">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-324">double</span></span> |<span data-ttu-id="1c2ac-325">Returns the minimum value in the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-325">Returns the minimum value in the doubleVecList.</span></span> |
| <span data-ttu-id="1c2ac-326">norm(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-326">norm(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-327">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-327">double</span></span> |<span data-ttu-id="1c2ac-328">Returns the two-norm of the vector that is created from the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-328">Returns the two-norm of the vector that is created from the doubleVecList.</span></span> |
| <span data-ttu-id="1c2ac-329">percentile(doubleVec v, double p)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-329">percentile(doubleVec v, double p)</span></span> |<span data-ttu-id="1c2ac-330">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-330">double</span></span> |<span data-ttu-id="1c2ac-331">Returns the percentile element of the vector v.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-331">Returns the percentile element of the vector v.</span></span> |
| <span data-ttu-id="1c2ac-332">rand()</span><span class="sxs-lookup"><span data-stu-id="1c2ac-332">rand()</span></span> |<span data-ttu-id="1c2ac-333">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-333">double</span></span> |<span data-ttu-id="1c2ac-334">Returns a random value between 0.0 and 1.0.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-334">Returns a random value between 0.0 and 1.0.</span></span> |
| <span data-ttu-id="1c2ac-335">range(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-335">range(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-336">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-336">double</span></span> |<span data-ttu-id="1c2ac-337">Returns the difference between the min and max values in the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-337">Returns the difference between the min and max values in the doubleVecList.</span></span> |
| <span data-ttu-id="1c2ac-338">std(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-338">std(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-339">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-339">double</span></span> |<span data-ttu-id="1c2ac-340">Returns the sample standard deviation of the values in the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-340">Returns the sample standard deviation of the values in the doubleVecList.</span></span> |
| <span data-ttu-id="1c2ac-341">stop()</span><span class="sxs-lookup"><span data-stu-id="1c2ac-341">stop()</span></span> | |<span data-ttu-id="1c2ac-342">Stops evaluation of the autoscaling expression.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-342">Stops evaluation of the autoscaling expression.</span></span> |
| <span data-ttu-id="1c2ac-343">sum(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-343">sum(doubleVecList)</span></span> |<span data-ttu-id="1c2ac-344">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-344">double</span></span> |<span data-ttu-id="1c2ac-345">Returns the sum of all the components of the doubleVecList.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-345">Returns the sum of all the components of the doubleVecList.</span></span> |
| <span data-ttu-id="1c2ac-346">time(string dateTime="")</span><span class="sxs-lookup"><span data-stu-id="1c2ac-346">time(string dateTime="")</span></span> |<span data-ttu-id="1c2ac-347">timestamp</span><span class="sxs-lookup"><span data-stu-id="1c2ac-347">timestamp</span></span> |<span data-ttu-id="1c2ac-348">Returns the time stamp of the current time if no parameters are passed, or the time stamp of the dateTime string if it is passed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-348">Returns the time stamp of the current time if no parameters are passed, or the time stamp of the dateTime string if it is passed.</span></span> <span data-ttu-id="1c2ac-349">Supported dateTime formats are W3C-DTF and RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-349">Supported dateTime formats are W3C-DTF and RFC 1123.</span></span> |
| <span data-ttu-id="1c2ac-350">val(doubleVec v, double i)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-350">val(doubleVec v, double i)</span></span> |<span data-ttu-id="1c2ac-351">double</span><span class="sxs-lookup"><span data-stu-id="1c2ac-351">double</span></span> |<span data-ttu-id="1c2ac-352">Returns the value of the element that is at location i in vector v, with a starting index of zero.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-352">Returns the value of the element that is at location i in vector v, with a starting index of zero.</span></span> |

<span data-ttu-id="1c2ac-353">Some of the functions that are described in the table above can accept a list as an argument.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-353">Some of the functions that are described in the table above can accept a list as an argument.</span></span> <span data-ttu-id="1c2ac-354">The comma-separated list is any combination of *double* and *doubleVec*.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-354">The comma-separated list is any combination of *double* and *doubleVec*.</span></span> <span data-ttu-id="1c2ac-355">For example:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-355">For example:</span></span>

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

<span data-ttu-id="1c2ac-356">The *doubleVecList* value is converted to a single *doubleVec* before evaluation.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-356">The *doubleVecList* value is converted to a single *doubleVec* before evaluation.</span></span> <span data-ttu-id="1c2ac-357">For example, if `v = [1,2,3]`, then calling `avg(v)` is equivalent to calling `avg(1,2,3)`.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-357">For example, if `v = [1,2,3]`, then calling `avg(v)` is equivalent to calling `avg(1,2,3)`.</span></span> <span data-ttu-id="1c2ac-358">Calling `avg(v, 7)` is equivalent to calling `avg(1,2,3,7)`.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-358">Calling `avg(v, 7)` is equivalent to calling `avg(1,2,3,7)`.</span></span>

## <a name="getsampledata"></a><span data-ttu-id="1c2ac-359">Obtain sample data</span><span class="sxs-lookup"><span data-stu-id="1c2ac-359">Obtain sample data</span></span>
<span data-ttu-id="1c2ac-360">Autoscale formulas act on metrics data (samples) that is provided by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-360">Autoscale formulas act on metrics data (samples) that is provided by the Batch service.</span></span> <span data-ttu-id="1c2ac-361">A formula grows or shrinks pool size based on the values that it obtains from the service.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-361">A formula grows or shrinks pool size based on the values that it obtains from the service.</span></span> <span data-ttu-id="1c2ac-362">The service-defined variables that are described above are objects that provide various methods to access data that is associated with that object.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-362">The service-defined variables that are described above are objects that provide various methods to access data that is associated with that object.</span></span> <span data-ttu-id="1c2ac-363">For example, the following expression shows a request to get the last five minutes of CPU usage:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-363">For example, the following expression shows a request to get the last five minutes of CPU usage:</span></span>

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| <span data-ttu-id="1c2ac-364">Method</span><span class="sxs-lookup"><span data-stu-id="1c2ac-364">Method</span></span> | <span data-ttu-id="1c2ac-365">Description</span><span class="sxs-lookup"><span data-stu-id="1c2ac-365">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c2ac-366">GetSample()</span><span class="sxs-lookup"><span data-stu-id="1c2ac-366">GetSample()</span></span> |<span data-ttu-id="1c2ac-367">The `GetSample()` method returns a vector of data samples.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-367">The `GetSample()` method returns a vector of data samples.</span></span><br/><br/><span data-ttu-id="1c2ac-368">A sample is 30 seconds worth of metrics data.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-368">A sample is 30 seconds worth of metrics data.</span></span> <span data-ttu-id="1c2ac-369">In other words, samples are obtained every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-369">In other words, samples are obtained every 30 seconds.</span></span> <span data-ttu-id="1c2ac-370">But as noted below, there is a delay between when a sample is collected and when it is available to a formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-370">But as noted below, there is a delay between when a sample is collected and when it is available to a formula.</span></span> <span data-ttu-id="1c2ac-371">As such, not all samples for a given time period may be available for evaluation by a formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-371">As such, not all samples for a given time period may be available for evaluation by a formula.</span></span><ul><li>`doubleVec GetSample(double count)`<br/><span data-ttu-id="1c2ac-372">Specifies the number of samples to obtain from the most recent samples that were collected.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-372">Specifies the number of samples to obtain from the most recent samples that were collected.</span></span><br/><br/><span data-ttu-id="1c2ac-373">`GetSample(1)` returns the last available sample.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-373">`GetSample(1)` returns the last available sample.</span></span> <span data-ttu-id="1c2ac-374">For metrics like `$CPUPercent`, however, this should not be used because it is impossible to know *when* the sample was collected.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-374">For metrics like `$CPUPercent`, however, this should not be used because it is impossible to know *when* the sample was collected.</span></span> <span data-ttu-id="1c2ac-375">It might be recent, or, because of system issues, it might be much older.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-375">It might be recent, or, because of system issues, it might be much older.</span></span> <span data-ttu-id="1c2ac-376">It is better in such cases to use a time interval as shown below.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-376">It is better in such cases to use a time interval as shown below.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/><span data-ttu-id="1c2ac-377">Specifies a time frame for gathering sample data.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-377">Specifies a time frame for gathering sample data.</span></span> <span data-ttu-id="1c2ac-378">Optionally, it also specifies the percentage of samples that must be available in the requested time frame.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-378">Optionally, it also specifies the percentage of samples that must be available in the requested time frame.</span></span><br/><br/><span data-ttu-id="1c2ac-379">`$CPUPercent.GetSample(TimeInterval_Minute * 10)` would return 20 samples if all samples for the last ten minutes are present in the CPUPercent history.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-379">`$CPUPercent.GetSample(TimeInterval_Minute * 10)` would return 20 samples if all samples for the last ten minutes are present in the CPUPercent history.</span></span> <span data-ttu-id="1c2ac-380">If the last minute of history was not available, however, only 18 samples would be returned.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-380">If the last minute of history was not available, however, only 18 samples would be returned.</span></span> <span data-ttu-id="1c2ac-381">In this case:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-381">In this case:</span></span><br/><br/><span data-ttu-id="1c2ac-382">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)` would fail because only 90 percent of the samples are available.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-382">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)` would fail because only 90 percent of the samples are available.</span></span><br/><br/><span data-ttu-id="1c2ac-383">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` would succeed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-383">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` would succeed.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/><span data-ttu-id="1c2ac-384">Specifies a time frame for gathering data, with both a start time and an end time.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-384">Specifies a time frame for gathering data, with both a start time and an end time.</span></span><br/><br/><span data-ttu-id="1c2ac-385">As mentioned above, there is a delay between when a sample is collected and when it is available to a formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-385">As mentioned above, there is a delay between when a sample is collected and when it is available to a formula.</span></span> <span data-ttu-id="1c2ac-386">This must be considered when you use the `GetSample` method.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-386">This must be considered when you use the `GetSample` method.</span></span> <span data-ttu-id="1c2ac-387">See `GetSamplePercent` below.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-387">See `GetSamplePercent` below.</span></span> |
| <span data-ttu-id="1c2ac-388">GetSamplePeriod()</span><span class="sxs-lookup"><span data-stu-id="1c2ac-388">GetSamplePeriod()</span></span> |<span data-ttu-id="1c2ac-389">Returns the period of samples that were taken in a historical sample data set.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-389">Returns the period of samples that were taken in a historical sample data set.</span></span> |
| <span data-ttu-id="1c2ac-390">Count()</span><span class="sxs-lookup"><span data-stu-id="1c2ac-390">Count()</span></span> |<span data-ttu-id="1c2ac-391">Returns the total number of samples in the metric history.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-391">Returns the total number of samples in the metric history.</span></span> |
| <span data-ttu-id="1c2ac-392">HistoryBeginTime()</span><span class="sxs-lookup"><span data-stu-id="1c2ac-392">HistoryBeginTime()</span></span> |<span data-ttu-id="1c2ac-393">Returns the time stamp of the oldest available data sample for the metric.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-393">Returns the time stamp of the oldest available data sample for the metric.</span></span> |
| <span data-ttu-id="1c2ac-394">GetSamplePercent()</span><span class="sxs-lookup"><span data-stu-id="1c2ac-394">GetSamplePercent()</span></span> |<span data-ttu-id="1c2ac-395">Returns the percentage of samples that are available for a given time interval.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-395">Returns the percentage of samples that are available for a given time interval.</span></span> <span data-ttu-id="1c2ac-396">For example:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-396">For example:</span></span><br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/><span data-ttu-id="1c2ac-397">Because the `GetSample` method fails if the percentage of samples returned is less than the `samplePercent` specified, you can use the `GetSamplePercent` method to check first.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-397">Because the `GetSample` method fails if the percentage of samples returned is less than the `samplePercent` specified, you can use the `GetSamplePercent` method to check first.</span></span> <span data-ttu-id="1c2ac-398">Then you can perform an alternate action if insufficient samples are present, without halting the automatic scaling evaluation.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-398">Then you can perform an alternate action if insufficient samples are present, without halting the automatic scaling evaluation.</span></span> |

### <a name="samples-sample-percentage-and-the-getsample-method"></a><span data-ttu-id="1c2ac-399">Samples, sample percentage, and the *GetSample()* method</span><span class="sxs-lookup"><span data-stu-id="1c2ac-399">Samples, sample percentage, and the *GetSample()* method</span></span>
<span data-ttu-id="1c2ac-400">The core operation of an autoscale formula is to obtain task and resource metric data and then adjust pool size based on that data.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-400">The core operation of an autoscale formula is to obtain task and resource metric data and then adjust pool size based on that data.</span></span> <span data-ttu-id="1c2ac-401">As such, it is important to have a clear understanding of how autoscale formulas interact with metrics data, or "samples."</span><span class="sxs-lookup"><span data-stu-id="1c2ac-401">As such, it is important to have a clear understanding of how autoscale formulas interact with metrics data, or "samples."</span></span>

<span data-ttu-id="1c2ac-402">**Samples**</span><span class="sxs-lookup"><span data-stu-id="1c2ac-402">**Samples**</span></span>

<span data-ttu-id="1c2ac-403">The Batch service periodically takes *samples* of task and resource metrics and makes them available to your autoscale formulas.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-403">The Batch service periodically takes *samples* of task and resource metrics and makes them available to your autoscale formulas.</span></span> <span data-ttu-id="1c2ac-404">These samples are recorded every 30 seconds by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-404">These samples are recorded every 30 seconds by the Batch service.</span></span> <span data-ttu-id="1c2ac-405">However, there is typically some latency that causes a delay between when those samples were recorded and when they are made available to (and can be read by) your autoscale formulas.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-405">However, there is typically some latency that causes a delay between when those samples were recorded and when they are made available to (and can be read by) your autoscale formulas.</span></span> <span data-ttu-id="1c2ac-406">Additionally, due to various factors such as network or other infrastructure issues, samples may not have been recorded for a particular interval.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-406">Additionally, due to various factors such as network or other infrastructure issues, samples may not have been recorded for a particular interval.</span></span> <span data-ttu-id="1c2ac-407">This results in "missing" samples.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-407">This results in "missing" samples.</span></span>

<span data-ttu-id="1c2ac-408">**Sample percentage**</span><span class="sxs-lookup"><span data-stu-id="1c2ac-408">**Sample percentage**</span></span>

<span data-ttu-id="1c2ac-409">When `samplePercent` is passed to the `GetSample()` method or the `GetSamplePercent()` method is called, "percent" refers to a comparison between the total *possible* number of samples that are recorded by the Batch service and the number of samples that are actually *available* to your autoscale formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-409">When `samplePercent` is passed to the `GetSample()` method or the `GetSamplePercent()` method is called, "percent" refers to a comparison between the total *possible* number of samples that are recorded by the Batch service and the number of samples that are actually *available* to your autoscale formula.</span></span>

<span data-ttu-id="1c2ac-410">Let's look at a 10-minute timespan as an example.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-410">Let's look at a 10-minute timespan as an example.</span></span> <span data-ttu-id="1c2ac-411">Because samples are recorded every 30 seconds, within a 10 minute timespan, the maximum total number of samples that are recorded by Batch would be 20 samples (2 per minute).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-411">Because samples are recorded every 30 seconds, within a 10 minute timespan, the maximum total number of samples that are recorded by Batch would be 20 samples (2 per minute).</span></span> <span data-ttu-id="1c2ac-412">However, due to the inherent latency of the reporting mechanism or some other issue within the Azure infrastructure, there may be only 15 samples that are available to your autoscale formula for reading.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-412">However, due to the inherent latency of the reporting mechanism or some other issue within the Azure infrastructure, there may be only 15 samples that are available to your autoscale formula for reading.</span></span> <span data-ttu-id="1c2ac-413">This means that, for that 10-minute period, only **75 percent** of the total number of samples recorded are actually available to your formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-413">This means that, for that 10-minute period, only **75 percent** of the total number of samples recorded are actually available to your formula.</span></span>

<span data-ttu-id="1c2ac-414">**GetSample() and sample ranges**</span><span class="sxs-lookup"><span data-stu-id="1c2ac-414">**GetSample() and sample ranges**</span></span>

<span data-ttu-id="1c2ac-415">Your autoscale formulas are going to be growing and shrinking your pools--adding nodes or removing nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-415">Your autoscale formulas are going to be growing and shrinking your pools--adding nodes or removing nodes.</span></span> <span data-ttu-id="1c2ac-416">Because nodes cost you money, you want to ensure that your formulas use an intelligent method of analysis that is based on sufficient data.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-416">Because nodes cost you money, you want to ensure that your formulas use an intelligent method of analysis that is based on sufficient data.</span></span> <span data-ttu-id="1c2ac-417">Therefore, we recommend that you use a trending-type analysis in your formulas.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-417">Therefore, we recommend that you use a trending-type analysis in your formulas.</span></span> <span data-ttu-id="1c2ac-418">This type will grow and shrink your pools based on a *range* of collected samples.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-418">This type will grow and shrink your pools based on a *range* of collected samples.</span></span>

<span data-ttu-id="1c2ac-419">To do so, use `GetSample(interval look-back start, interval look-back end)` to return a **vector** of samples:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-419">To do so, use `GetSample(interval look-back start, interval look-back end)` to return a **vector** of samples:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

<span data-ttu-id="1c2ac-420">When the above line is evaluated by Batch, it returns a range of samples as a vector of values.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-420">When the above line is evaluated by Batch, it returns a range of samples as a vector of values.</span></span> <span data-ttu-id="1c2ac-421">For example:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-421">For example:</span></span>

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

<span data-ttu-id="1c2ac-422">Once you've collected the vector of samples, you can then use functions like `min()`, `max()`, and `avg()` to derive meaningful values from the collected range.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-422">Once you've collected the vector of samples, you can then use functions like `min()`, `max()`, and `avg()` to derive meaningful values from the collected range.</span></span>

<span data-ttu-id="1c2ac-423">For additional security, you can force a formula evaluation to *fail* if less than a certain sample percentage is available for a particular time period.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-423">For additional security, you can force a formula evaluation to *fail* if less than a certain sample percentage is available for a particular time period.</span></span> <span data-ttu-id="1c2ac-424">When you force a formula evaluation to fail, you instruct Batch to cease further evaluation of the formula if the specified percentage of samples is not available.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-424">When you force a formula evaluation to fail, you instruct Batch to cease further evaluation of the formula if the specified percentage of samples is not available.</span></span> <span data-ttu-id="1c2ac-425">In this case, no change is made to the pool size.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-425">In this case, no change is made to the pool size.</span></span> <span data-ttu-id="1c2ac-426">To specify a required percentage of samples for the evaluation to succeed, specify it as the third parameter to `GetSample()`.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-426">To specify a required percentage of samples for the evaluation to succeed, specify it as the third parameter to `GetSample()`.</span></span> <span data-ttu-id="1c2ac-427">Here, a requirement of 75 percent of samples is specified:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-427">Here, a requirement of 75 percent of samples is specified:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

<span data-ttu-id="1c2ac-428">Because there may be a delay in sample availability, it is important to always specify a time range with a look-back start time that is older than one minute.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-428">Because there may be a delay in sample availability, it is important to always specify a time range with a look-back start time that is older than one minute.</span></span> <span data-ttu-id="1c2ac-429">It takes approximately one minute for samples to propagate through the system, so samples in the range `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` may not be available.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-429">It takes approximately one minute for samples to propagate through the system, so samples in the range `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` may not be available.</span></span> <span data-ttu-id="1c2ac-430">Again, you can use the percentage parameter of `GetSample()` to force a particular sample percentage requirement.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-430">Again, you can use the percentage parameter of `GetSample()` to force a particular sample percentage requirement.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c2ac-431">We **strongly recommend** that you **avoid relying *only* on `GetSample(1)` in your autoscale formulas**.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-431">We **strongly recommend** that you **avoid relying *only* on `GetSample(1)` in your autoscale formulas**.</span></span> <span data-ttu-id="1c2ac-432">This is because `GetSample(1)` essentially says to the Batch service, "Give me the last sample you have, no matter how long ago you retrieved it."</span><span class="sxs-lookup"><span data-stu-id="1c2ac-432">This is because `GetSample(1)` essentially says to the Batch service, "Give me the last sample you have, no matter how long ago you retrieved it."</span></span> <span data-ttu-id="1c2ac-433">Since it is only a single sample, and it may be an older sample, it may not be representative of the larger picture of recent task or resource state.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-433">Since it is only a single sample, and it may be an older sample, it may not be representative of the larger picture of recent task or resource state.</span></span> <span data-ttu-id="1c2ac-434">If you do use `GetSample(1)`, make sure that it's part of a larger statement and not the only data point that your formula relies on.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-434">If you do use `GetSample(1)`, make sure that it's part of a larger statement and not the only data point that your formula relies on.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="1c2ac-435">Metrics</span><span class="sxs-lookup"><span data-stu-id="1c2ac-435">Metrics</span></span>
<span data-ttu-id="1c2ac-436">You can use both **resource** and **task** metrics when you're defining a formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-436">You can use both **resource** and **task** metrics when you're defining a formula.</span></span> <span data-ttu-id="1c2ac-437">You adjust the target number of dedicated nodes in the pool based on the metrics data that you obtain and evaluate.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-437">You adjust the target number of dedicated nodes in the pool based on the metrics data that you obtain and evaluate.</span></span> <span data-ttu-id="1c2ac-438">See the [Variables](#variables) section above for more information on each metric.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-438">See the [Variables](#variables) section above for more information on each metric.</span></span>

<table>
  <tr>
    <th><span data-ttu-id="1c2ac-439">Metric</span><span class="sxs-lookup"><span data-stu-id="1c2ac-439">Metric</span></span></th>
    <th><span data-ttu-id="1c2ac-440">Description</span><span class="sxs-lookup"><span data-stu-id="1c2ac-440">Description</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="1c2ac-441"><b>Resource</b></span><span class="sxs-lookup"><span data-stu-id="1c2ac-441"><b>Resource</b></span></span></td>
    <td><p><span data-ttu-id="1c2ac-442"><b>Resource metrics</b> are based on the CPU, bandwidth, and memory usage of compute nodes, as well as the number of nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-442"><b>Resource metrics</b> are based on the CPU, bandwidth, and memory usage of compute nodes, as well as the number of nodes.</span></span></p>
        <p> <span data-ttu-id="1c2ac-443">These service-defined variables are useful for making adjustments based on node count:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-443">These service-defined variables are useful for making adjustments based on node count:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="1c2ac-444">$TargetDedicated</span><span class="sxs-lookup"><span data-stu-id="1c2ac-444">$TargetDedicated</span></span></li>
            <li><span data-ttu-id="1c2ac-445">$CurrentDedicated</span><span class="sxs-lookup"><span data-stu-id="1c2ac-445">$CurrentDedicated</span></span></li>
            <li><span data-ttu-id="1c2ac-446">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="1c2ac-446">$SampleNodeCount</span></span></li>
    </ul></p>
    <p><span data-ttu-id="1c2ac-447">These service-defined variables are useful for making adjustments based on node resource usage:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-447">These service-defined variables are useful for making adjustments based on node resource usage:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="1c2ac-448">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="1c2ac-448">$CPUPercent</span></span></li>
      <li><span data-ttu-id="1c2ac-449">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="1c2ac-449">$WallClockSeconds</span></span></li>
      <li><span data-ttu-id="1c2ac-450">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-450">$MemoryBytes</span></span></li>
      <li><span data-ttu-id="1c2ac-451">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-451">$DiskBytes</span></span></li>
      <li><span data-ttu-id="1c2ac-452">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-452">$DiskReadBytes</span></span></li>
      <li><span data-ttu-id="1c2ac-453">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-453">$DiskWriteBytes</span></span></li>
      <li><span data-ttu-id="1c2ac-454">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="1c2ac-454">$DiskReadOps</span></span></li>
      <li><span data-ttu-id="1c2ac-455">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="1c2ac-455">$DiskWriteOps</span></span></li>
      <li><span data-ttu-id="1c2ac-456">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-456">$NetworkInBytes</span></span></li>
      <li><span data-ttu-id="1c2ac-457">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="1c2ac-457">$NetworkOutBytes</span></span></li></ul></p>
  </tr>
  <tr>
    <td><span data-ttu-id="1c2ac-458"><b>Task</b></span><span class="sxs-lookup"><span data-stu-id="1c2ac-458"><b>Task</b></span></span></td>
    <td><p><span data-ttu-id="1c2ac-459"><b>Task metrics</b> are based on the status of tasks, such as Active, Pending, and Completed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-459"><b>Task metrics</b> are based on the status of tasks, such as Active, Pending, and Completed.</span></span> <span data-ttu-id="1c2ac-460">The following service-defined variables are useful for making pool-size adjustments based on task metrics:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-460">The following service-defined variables are useful for making pool-size adjustments based on task metrics:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="1c2ac-461">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-461">$ActiveTasks</span></span></li>
      <li><span data-ttu-id="1c2ac-462">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-462">$RunningTasks</span></span></li>
      <li><span data-ttu-id="1c2ac-463">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-463">$PendingTasks</span></span></li>
      <li><span data-ttu-id="1c2ac-464">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-464">$SucceededTasks</span></span></li>
            <li><span data-ttu-id="1c2ac-465">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-465">$FailedTasks</span></span></li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a><span data-ttu-id="1c2ac-466">Write an autoscale formula</span><span class="sxs-lookup"><span data-stu-id="1c2ac-466">Write an autoscale formula</span></span>
<span data-ttu-id="1c2ac-467">You build an autoscale formula by forming statements that use the above components, then combine those statements into a complete formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-467">You build an autoscale formula by forming statements that use the above components, then combine those statements into a complete formula.</span></span> <span data-ttu-id="1c2ac-468">In this section, we'll create an example autoscale formula that can perform some real-world scaling decisions.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-468">In this section, we'll create an example autoscale formula that can perform some real-world scaling decisions.</span></span>

<span data-ttu-id="1c2ac-469">First, let's define the requirements for our new autoscale formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-469">First, let's define the requirements for our new autoscale formula.</span></span> <span data-ttu-id="1c2ac-470">The formula should:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-470">The formula should:</span></span>

1. <span data-ttu-id="1c2ac-471">**Increase** the target number of compute nodes in a pool if CPU usage is high.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-471">**Increase** the target number of compute nodes in a pool if CPU usage is high.</span></span>
2. <span data-ttu-id="1c2ac-472">**Decrease** the target number of compute nodes in a pool when CPU usage is low.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-472">**Decrease** the target number of compute nodes in a pool when CPU usage is low.</span></span>
3. <span data-ttu-id="1c2ac-473">Always restrict the **maximum** number of nodes to 400.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-473">Always restrict the **maximum** number of nodes to 400.</span></span>

<span data-ttu-id="1c2ac-474">To *increase* the number of nodes during high CPU usage, we define the statement that populates a user-defined variable (`$totalNodes`) with a value that is 110 percent of the current target number of nodes, but only if the minimum average CPU usage during the last 10 minutes was above 70 percent.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-474">To *increase* the number of nodes during high CPU usage, we define the statement that populates a user-defined variable (`$totalNodes`) with a value that is 110 percent of the current target number of nodes, but only if the minimum average CPU usage during the last 10 minutes was above 70 percent.</span></span> <span data-ttu-id="1c2ac-475">Otherwise, we use the current dedicated value.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-475">Otherwise, we use the current dedicated value.</span></span>

```
$totalNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicated * 1.1) : $CurrentDedicated;
```

<span data-ttu-id="1c2ac-476">To *decrease* the number of nodes during low CPU usage, the next statement in our formula sets the same `$totalNodes` variable to 90 percent of the current target number of nodes if the average CPU usage in the past 60 minutes was under 20 percent.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-476">To *decrease* the number of nodes during low CPU usage, the next statement in our formula sets the same `$totalNodes` variable to 90 percent of the current target number of nodes if the average CPU usage in the past 60 minutes was under 20 percent.</span></span> <span data-ttu-id="1c2ac-477">Otherwise, use the current value of `$totalNodes` that we populated in the statement above.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-477">Otherwise, use the current value of `$totalNodes` that we populated in the statement above.</span></span>

```
$totalNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicated * 0.9) : $totalNodes;
```

<span data-ttu-id="1c2ac-478">Now limit the target number of dedicated compute nodes to a **maximum** of 400:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-478">Now limit the target number of dedicated compute nodes to a **maximum** of 400:</span></span>

```
$TargetDedicated = min(400, $totalNodes)
```

<span data-ttu-id="1c2ac-479">Here's the complete formula:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-479">Here's the complete formula:</span></span>

```
$totalNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicated * 1.1) : $CurrentDedicated;
$totalNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicated * 0.9) : $totalNodes;
$TargetDedicated = min(400, $totalNodes)
```

## <a name="create-an-autoscale-enabled-pool"></a><span data-ttu-id="1c2ac-480">Create an autoscale-enabled pool</span><span class="sxs-lookup"><span data-stu-id="1c2ac-480">Create an autoscale-enabled pool</span></span>
<span data-ttu-id="1c2ac-481">To create a new pool with autoscaling enabled, you can use one of the following techniques:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-481">To create a new pool with autoscaling enabled, you can use one of the following techniques:</span></span>

<span data-ttu-id="1c2ac-482">**Batch .NET**</span><span class="sxs-lookup"><span data-stu-id="1c2ac-482">**Batch .NET**</span></span>

1. <span data-ttu-id="1c2ac-483">Create the pool with [BatchClient.PoolOperations.CreatePool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-483">Create the pool with [BatchClient.PoolOperations.CreatePool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx).</span></span>
2. <span data-ttu-id="1c2ac-484">Set the [CloudPool.AutoScaleEnabled](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoscaleenabled.aspx) property to `true`.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-484">Set the [CloudPool.AutoScaleEnabled](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoscaleenabled.aspx) property to `true`.</span></span>
3. <span data-ttu-id="1c2ac-485">Set the [CloudPool.AutoScaleFormula](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoscaleformula.aspx) property with your autoscale formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-485">Set the [CloudPool.AutoScaleFormula](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoscaleformula.aspx) property with your autoscale formula.</span></span>
4. <span data-ttu-id="1c2ac-486">(Optional) Set the [CloudPool.AutoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoScaleevaluationinterval.aspx) property (default is 15 minutes).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-486">(Optional) Set the [CloudPool.AutoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoScaleevaluationinterval.aspx) property (default is 15 minutes).</span></span>
5. <span data-ttu-id="1c2ac-487">Commit the pool with [CloudPool.Commit](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.commit.aspx) or [CommitAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.commitasync.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-487">Commit the pool with [CloudPool.Commit](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.commit.aspx) or [CommitAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.commitasync.aspx).</span></span>

<span data-ttu-id="1c2ac-488">**Batch REST API**</span><span class="sxs-lookup"><span data-stu-id="1c2ac-488">**Batch REST API**</span></span>

* <span data-ttu-id="1c2ac-489">[Add a pool to an account](https://msdn.microsoft.com/library/azure/dn820174.aspx): Specify the `enableAutoScale` and `autoScaleFormula` elements in your REST API request to configure automatic scaling for a pool when you create it.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-489">[Add a pool to an account](https://msdn.microsoft.com/library/azure/dn820174.aspx): Specify the `enableAutoScale` and `autoScaleFormula` elements in your REST API request to configure automatic scaling for a pool when you create it.</span></span>

<span data-ttu-id="1c2ac-490">The following code snippet creates an autoscale-enabled pool by using the [Batch .NET][net_api] library.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-490">The following code snippet creates an autoscale-enabled pool by using the [Batch .NET][net_api] library.</span></span> <span data-ttu-id="1c2ac-491">The pool's autoscale formula sets the target number of nodes to 5 on Mondays, and 1 on every other day of the week.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-491">The pool's autoscale formula sets the target number of nodes to 5 on Mondays, and 1 on every other day of the week.</span></span> <span data-ttu-id="1c2ac-492">The [automatic scaling interval](#automatic-scaling-interval) is set to 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-492">The [automatic scaling interval](#automatic-scaling-interval) is set to 30 minutes.</span></span> <span data-ttu-id="1c2ac-493">In this and the other C# snippets in this article, "myBatchClient" is a properly initialized instance of [BatchClient][net_batchclient].</span><span class="sxs-lookup"><span data-stu-id="1c2ac-493">In this and the other C# snippets in this article, "myBatchClient" is a properly initialized instance of [BatchClient][net_batchclient].</span></span>

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool("mypool", "3", "small");
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicated = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
pool.Commit();
```

<span data-ttu-id="1c2ac-494">In addition to the Batch REST API and .NET SDK, you can use any of the other [Batch SDKs](batch-apis-tools.md#batch-development-apis), [Batch PowerShell cmdlets](batch-powershell-cmdlets-get-started.md), and the [Batch CLI](batch-cli-get-started.md) to work with autoscaling.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-494">In addition to the Batch REST API and .NET SDK, you can use any of the other [Batch SDKs](batch-apis-tools.md#batch-development-apis), [Batch PowerShell cmdlets](batch-powershell-cmdlets-get-started.md), and the [Batch CLI](batch-cli-get-started.md) to work with autoscaling.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c2ac-495">When you create an autoscale-enabled pool, you must **not** specify the `targetDedicated` parameter.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-495">When you create an autoscale-enabled pool, you must **not** specify the `targetDedicated` parameter.</span></span> <span data-ttu-id="1c2ac-496">Also, if you want to manually resize an autoscale-enabled pool (for example, with [BatchClient.PoolOperations.ResizePool][net_poolops_resizepool]), then you must first **disable** automatic scaling on the pool, then resize it.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-496">Also, if you want to manually resize an autoscale-enabled pool (for example, with [BatchClient.PoolOperations.ResizePool][net_poolops_resizepool]), then you must first **disable** automatic scaling on the pool, then resize it.</span></span>
> 
> 

### <a name="automatic-scaling-interval"></a><span data-ttu-id="1c2ac-497">Automatic scaling interval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-497">Automatic scaling interval</span></span>
<span data-ttu-id="1c2ac-498">By default, the Batch service adjusts a pool's size according to its autoscale formula every **15 minutes**.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-498">By default, the Batch service adjusts a pool's size according to its autoscale formula every **15 minutes**.</span></span> <span data-ttu-id="1c2ac-499">This interval is configurable, however, by using the following pool properties:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-499">This interval is configurable, however, by using the following pool properties:</span></span>

* <span data-ttu-id="1c2ac-500">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-500">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span></span>
* <span data-ttu-id="1c2ac-501">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-501">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span></span>

<span data-ttu-id="1c2ac-502">The minimum interval is five minutes, and the maximum is 168 hours.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-502">The minimum interval is five minutes, and the maximum is 168 hours.</span></span> <span data-ttu-id="1c2ac-503">If an interval outside this range is specified, the Batch service will return a Bad Request (400) error.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-503">If an interval outside this range is specified, the Batch service will return a Bad Request (400) error.</span></span>

> [!NOTE]
> <span data-ttu-id="1c2ac-504">Autoscaling is not currently intended to respond to changes in less than a minute, but rather is intended to adjust the size of your pool gradually as you run a workload.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-504">Autoscaling is not currently intended to respond to changes in less than a minute, but rather is intended to adjust the size of your pool gradually as you run a workload.</span></span>
> 
> 

## <a name="enable-autoscaling-on-an-existing-pool"></a><span data-ttu-id="1c2ac-505">Enable autoscaling on an existing pool</span><span class="sxs-lookup"><span data-stu-id="1c2ac-505">Enable autoscaling on an existing pool</span></span>
<span data-ttu-id="1c2ac-506">If you've already created a pool with a set number of compute nodes by using the *targetDedicated* parameter, you can still enable autoscaling on the pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-506">If you've already created a pool with a set number of compute nodes by using the *targetDedicated* parameter, you can still enable autoscaling on the pool.</span></span> <span data-ttu-id="1c2ac-507">Each Batch SDK provides an "enable autoscale" operation, for example:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-507">Each Batch SDK provides an "enable autoscale" operation, for example:</span></span>

* <span data-ttu-id="1c2ac-508">[BatchClient.PoolOperations.EnableAutoScale][net_enableautoscale] (Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-508">[BatchClient.PoolOperations.EnableAutoScale][net_enableautoscale] (Batch .NET)</span></span>
* <span data-ttu-id="1c2ac-509">[Enable automatic scaling on a pool][rest_enableautoscale] (REST API)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-509">[Enable automatic scaling on a pool][rest_enableautoscale] (REST API)</span></span>

<span data-ttu-id="1c2ac-510">When you enable autoscaling on an existing pool, the following applies:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-510">When you enable autoscaling on an existing pool, the following applies:</span></span>

* <span data-ttu-id="1c2ac-511">If automatic scaling is currently **disabled** on the pool when you issue the "enable autoscale" request, you *must* specify a valid autoscale formula when you issue the request.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-511">If automatic scaling is currently **disabled** on the pool when you issue the "enable autoscale" request, you *must* specify a valid autoscale formula when you issue the request.</span></span> <span data-ttu-id="1c2ac-512">You can *optionally* specify an autoscale evaluation interval.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-512">You can *optionally* specify an autoscale evaluation interval.</span></span> <span data-ttu-id="1c2ac-513">If you do not specify an interval, the default value of 15 minutes is used.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-513">If you do not specify an interval, the default value of 15 minutes is used.</span></span>
* <span data-ttu-id="1c2ac-514">If autoscale is currently **enabled** on the pool, you can specify an autoscale formula, an evaluation interval, or both.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-514">If autoscale is currently **enabled** on the pool, you can specify an autoscale formula, an evaluation interval, or both.</span></span> <span data-ttu-id="1c2ac-515">You can't omit both properties.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-515">You can't omit both properties.</span></span>
  
  * <span data-ttu-id="1c2ac-516">If you specify a new autoscale evaluation interval, then the existing evaluation schedule is stopped and a new schedule is started.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-516">If you specify a new autoscale evaluation interval, then the existing evaluation schedule is stopped and a new schedule is started.</span></span> <span data-ttu-id="1c2ac-517">The new schedule's start time is the time at which the "enable autoscale" request was issued.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-517">The new schedule's start time is the time at which the "enable autoscale" request was issued.</span></span>
  * <span data-ttu-id="1c2ac-518">If you omit either the autoscale formula or evaluation interval, the Batch service continues to use the current value of that setting.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-518">If you omit either the autoscale formula or evaluation interval, the Batch service continues to use the current value of that setting.</span></span>

> [!NOTE]
> <span data-ttu-id="1c2ac-519">If a value was specified for the *targetDedicated* parameter when the pool was created, it is ignored when the automatic scaling formula is evaluated.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-519">If a value was specified for the *targetDedicated* parameter when the pool was created, it is ignored when the automatic scaling formula is evaluated.</span></span>
> 
> 

<span data-ttu-id="1c2ac-520">This C# code snippet uses the [Batch .NET][net_api] library to enable autoscaling on an existing pool:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-520">This C# code snippet uses the [Batch .NET][net_api] library to enable autoscaling on an existing pool:</span></span>

```csharp
// Define the autoscaling formula. This formula sets the target number of nodes
// to 5 on Mondays, and 1 on every other day of the week
string myAutoScaleFormula = "$TargetDedicated = (time().weekday == 1 ? 5:1);";

// Set the autoscale formula on the existing pool
myBatchClient.PoolOperations.EnableAutoScale(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a><span data-ttu-id="1c2ac-521">Update an autoscale formula</span><span class="sxs-lookup"><span data-stu-id="1c2ac-521">Update an autoscale formula</span></span>
<span data-ttu-id="1c2ac-522">You use the same "enable autoscale" request to *update* the formula on an existing autoscale-enabled pool (for example, with [EnableAutoScale][net_enableautoscale] in Batch .NET).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-522">You use the same "enable autoscale" request to *update* the formula on an existing autoscale-enabled pool (for example, with [EnableAutoScale][net_enableautoscale] in Batch .NET).</span></span> <span data-ttu-id="1c2ac-523">There is no special "update autoscale" operation.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-523">There is no special "update autoscale" operation.</span></span> <span data-ttu-id="1c2ac-524">For example, if autoscaling is already enabled on "myexistingpool" when the following code is executed, its autoscale formula is replaced with the contents of `myNewFormula`.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-524">For example, if autoscaling is already enabled on "myexistingpool" when the following code is executed, its autoscale formula is replaced with the contents of `myNewFormula`.</span></span>

```csharp
myBatchClient.PoolOperations.EnableAutoScale(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-the-autoscale-interval"></a><span data-ttu-id="1c2ac-525">Update the autoscale interval</span><span class="sxs-lookup"><span data-stu-id="1c2ac-525">Update the autoscale interval</span></span>
<span data-ttu-id="1c2ac-526">As with updating an autoscale formula, you use the same [EnableAutoScale][net_enableautoscale] method to change the autoscale evaluation interval of an existing autoscale-enabled pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-526">As with updating an autoscale formula, you use the same [EnableAutoScale][net_enableautoscale] method to change the autoscale evaluation interval of an existing autoscale-enabled pool.</span></span> <span data-ttu-id="1c2ac-527">For example, to set the autoscale evaluation interval to 60 minutes for a pool that's already autoscale-enabled:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-527">For example, to set the autoscale evaluation interval to 60 minutes for a pool that's already autoscale-enabled:</span></span>

```csharp
myBatchClient.PoolOperations.EnableAutoScale(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a><span data-ttu-id="1c2ac-528">Evaluate an autoscale formula</span><span class="sxs-lookup"><span data-stu-id="1c2ac-528">Evaluate an autoscale formula</span></span>
<span data-ttu-id="1c2ac-529">You can evaluate a formula before applying it to a pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-529">You can evaluate a formula before applying it to a pool.</span></span> <span data-ttu-id="1c2ac-530">In this way, you can perform a "test run" of the formula to see how its statements evaluate before you put the formula into production.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-530">In this way, you can perform a "test run" of the formula to see how its statements evaluate before you put the formula into production.</span></span>

<span data-ttu-id="1c2ac-531">To evaluate an autoscale formula, you must first **enable autoscaling** on the pool with a **valid formula**.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-531">To evaluate an autoscale formula, you must first **enable autoscaling** on the pool with a **valid formula**.</span></span> <span data-ttu-id="1c2ac-532">If you want to test a formula on a pool that doesn't yet have autoscaling enabled, you can use the one-line formula `$TargetDedicated = 0` when you first enable autoscaling.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-532">If you want to test a formula on a pool that doesn't yet have autoscaling enabled, you can use the one-line formula `$TargetDedicated = 0` when you first enable autoscaling.</span></span> <span data-ttu-id="1c2ac-533">Then, use one of the following to evaluate the formula you want to test:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-533">Then, use one of the following to evaluate the formula you want to test:</span></span>

* <span data-ttu-id="1c2ac-534">[BatchClient.PoolOperations.EvaluateAutoScale](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.evaluateautoscale.aspx) or [EvaluateAutoScaleAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.evaluateautoscaleasync.aspx)</span><span class="sxs-lookup"><span data-stu-id="1c2ac-534">[BatchClient.PoolOperations.EvaluateAutoScale](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.evaluateautoscale.aspx) or [EvaluateAutoScaleAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.evaluateautoscaleasync.aspx)</span></span>
  
    <span data-ttu-id="1c2ac-535">These Batch .NET methods require the ID of an existing pool and a string containing the autoscale formula to evaluate.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-535">These Batch .NET methods require the ID of an existing pool and a string containing the autoscale formula to evaluate.</span></span> <span data-ttu-id="1c2ac-536">The evaluation results are contained in the returned [AutoScaleEvaluation](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.autoscaleevaluation.aspx) instance.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-536">The evaluation results are contained in the returned [AutoScaleEvaluation](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.autoscaleevaluation.aspx) instance.</span></span>
* [<span data-ttu-id="1c2ac-537">Evaluate an automatic scaling formula</span><span class="sxs-lookup"><span data-stu-id="1c2ac-537">Evaluate an automatic scaling formula</span></span>](https://msdn.microsoft.com/library/azure/dn820183.aspx)
  
    <span data-ttu-id="1c2ac-538">In this REST API request, specify the pool ID in the URI, and the autoscale formula in the *autoScaleFormula* element of the request body.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-538">In this REST API request, specify the pool ID in the URI, and the autoscale formula in the *autoScaleFormula* element of the request body.</span></span> <span data-ttu-id="1c2ac-539">The response of the operation contains any error information that might be related to the formula.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-539">The response of the operation contains any error information that might be related to the formula.</span></span>

<span data-ttu-id="1c2ac-540">In this [Batch .NET][net_api] code snippet, we evaluate a formula prior to applying it to the [CloudPool][net_cloudpool].</span><span class="sxs-lookup"><span data-stu-id="1c2ac-540">In this [Batch .NET][net_api] code snippet, we evaluate a formula prior to applying it to the [CloudPool][net_cloudpool].</span></span> <span data-ttu-id="1c2ac-541">If the pool does not have autoscaling enabled, we enable it first.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-541">If the pool does not have autoscaling enabled, we enable it first.</span></span>

```csharp
// First obtain a reference to an existing pool
CloudPool pool = batchClient.PoolOperations.GetPool("myExistingPool");

// If autoscaling isn't already enabled on the pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula to enable autoscaling on the
    // pool. This formula is valid, but won't resize the pool:
    pool.EnableAutoScale(
        autoscaleFormula: $"$TargetDedicated = {pool.CurrentDedicated};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScale calls to once every 30 seconds.
    // Because we want to apply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here to ensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh the properties of the pool so that we've got the
    // latest value for AutoScaleEnabled
    pool.Refresh();
}

// We must ensure that autoscaling is enabled on the pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // The formula to evaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicated = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform the autoscale formula evaluation. Note that this does not
    // actually apply the formula to the pool.
    AutoScaleRun eval =
        batchClient.PoolOperations.EvaluateAutoScale(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print the results of the AutoScaleRun.
        // This will display the values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply the formula to the pool since it evaluated successfully
        batchClient.PoolOperations.EnableAutoScale(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output the message associated with the error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

<span data-ttu-id="1c2ac-542">Successful evaluation of the formula in this snippet will result in output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-542">Successful evaluation of the formula in this snippet will result in output similar to the following:</span></span>

```
AutoScaleRun.Results:
    $TargetDedicated=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a><span data-ttu-id="1c2ac-543">Get information about autoscale runs</span><span class="sxs-lookup"><span data-stu-id="1c2ac-543">Get information about autoscale runs</span></span>
<span data-ttu-id="1c2ac-544">To ensure your formula is performing as expected, we recommend you periodically check the results of the autoscaling "runs" Batch performs on your pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-544">To ensure your formula is performing as expected, we recommend you periodically check the results of the autoscaling "runs" Batch performs on your pool.</span></span> <span data-ttu-id="1c2ac-545">To do so, get (or refresh) a reference to the pool, and examine the properties of its last autoscale run.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-545">To do so, get (or refresh) a reference to the pool, and examine the properties of its last autoscale run.</span></span>

<span data-ttu-id="1c2ac-546">In Batch .NET, the [CloudPool.AutoScaleRun](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoscalerun.aspx) property has several properties providing information about the latest automatic scaling run performed on the pool by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-546">In Batch .NET, the [CloudPool.AutoScaleRun](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoscalerun.aspx) property has several properties providing information about the latest automatic scaling run performed on the pool by the Batch service.</span></span>

* [<span data-ttu-id="1c2ac-547">AutoScaleRun.Timestamp</span><span class="sxs-lookup"><span data-stu-id="1c2ac-547">AutoScaleRun.Timestamp</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.autoscalerun.timestamp.aspx)
* [<span data-ttu-id="1c2ac-548">AutoScaleRun.Results</span><span class="sxs-lookup"><span data-stu-id="1c2ac-548">AutoScaleRun.Results</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.autoscalerun.results.aspx)
* [<span data-ttu-id="1c2ac-549">AutoScaleRun.Error</span><span class="sxs-lookup"><span data-stu-id="1c2ac-549">AutoScaleRun.Error</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.autoscalerun.error.aspx)

<span data-ttu-id="1c2ac-550">In the REST API, the [Get information about a pool](https://msdn.microsoft.com/library/dn820165.aspx) request returns information about the pool, which includes the latest automatic scaling run information in [autoScaleRun](https://msdn.microsoft.com/library/dn820165.aspx#bk_autrun).</span><span class="sxs-lookup"><span data-stu-id="1c2ac-550">In the REST API, the [Get information about a pool](https://msdn.microsoft.com/library/dn820165.aspx) request returns information about the pool, which includes the latest automatic scaling run information in [autoScaleRun](https://msdn.microsoft.com/library/dn820165.aspx#bk_autrun).</span></span>

<span data-ttu-id="1c2ac-551">The following C# code snippet uses the Batch .NET library to print information about the last autoscaling run on pool "myPool":</span><span class="sxs-lookup"><span data-stu-id="1c2ac-551">The following C# code snippet uses the Batch .NET library to print information about the last autoscaling run on pool "myPool":</span></span>

```csharp
Cloud pool = myBatchClient.PoolOperations.GetPool("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

<span data-ttu-id="1c2ac-552">Sample output of the preceding snippet:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-552">Sample output of the preceding snippet:</span></span>

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicated=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a><span data-ttu-id="1c2ac-553">Example autoscale formulas</span><span class="sxs-lookup"><span data-stu-id="1c2ac-553">Example autoscale formulas</span></span>
<span data-ttu-id="1c2ac-554">Let's take a look at a few formulas that show different ways to adjust the amount of compute resources in a pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-554">Let's take a look at a few formulas that show different ways to adjust the amount of compute resources in a pool.</span></span>

### <a name="example-1-time-based-adjustment"></a><span data-ttu-id="1c2ac-555">Example 1: Time-based adjustment</span><span class="sxs-lookup"><span data-stu-id="1c2ac-555">Example 1: Time-based adjustment</span></span>
<span data-ttu-id="1c2ac-556">Perhaps you want to adjust the pool size based on the day of the week and time of day, to increase or decrease the number of nodes in the pool accordingly.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-556">Perhaps you want to adjust the pool size based on the day of the week and time of day, to increase or decrease the number of nodes in the pool accordingly.</span></span>

<span data-ttu-id="1c2ac-557">This formula first obtains the current time.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-557">This formula first obtains the current time.</span></span> <span data-ttu-id="1c2ac-558">If it's a weekday (1-5) and within working hours (8 AM to 6 PM), the target pool size is set to 20 nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-558">If it's a weekday (1-5) and within working hours (8 AM to 6 PM), the target pool size is set to 20 nodes.</span></span> <span data-ttu-id="1c2ac-559">Otherwise, it's set to 10 nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-559">Otherwise, it's set to 10 nodes.</span></span>

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicated = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a><span data-ttu-id="1c2ac-560">Example 2: Task-based adjustment</span><span class="sxs-lookup"><span data-stu-id="1c2ac-560">Example 2: Task-based adjustment</span></span>
<span data-ttu-id="1c2ac-561">In this example, the pool size is adjusted based on the number of tasks in the queue.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-561">In this example, the pool size is adjusted based on the number of tasks in the queue.</span></span> <span data-ttu-id="1c2ac-562">Note that both comments and line breaks are acceptable in formula strings.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-562">Note that both comments and line breaks are acceptable in formula strings.</span></span>

```csharp
// Get pending tasks for the past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use the last sample point,
// otherwise we use the maximum of last sample point and the history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM to pending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicated/2);
// The pool size is capped at 20, if target VM value is more than that, set it
// to 20. This value should be adjusted according to your use case.
$TargetDedicated = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a><span data-ttu-id="1c2ac-563">Example 3: Accounting for parallel tasks</span><span class="sxs-lookup"><span data-stu-id="1c2ac-563">Example 3: Accounting for parallel tasks</span></span>
<span data-ttu-id="1c2ac-564">This is another example that adjusts the pool size based on the number of tasks.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-564">This is another example that adjusts the pool size based on the number of tasks.</span></span> <span data-ttu-id="1c2ac-565">This formula also takes into account the [MaxTasksPerComputeNode][net_maxtasks] value that has been set for the pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-565">This formula also takes into account the [MaxTasksPerComputeNode][net_maxtasks] value that has been set for the pool.</span></span> <span data-ttu-id="1c2ac-566">This is particularly useful in situations where [parallel task execution](batch-parallel-node-tasks.md) has been enabled on your pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-566">This is particularly useful in situations where [parallel task execution](batch-parallel-node-tasks.md) has been enabled on your pool.</span></span>

```csharp
// Determine whether 70 percent of the samples have been recorded in the past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set the number of nodes to add to one-fourth the number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set to 4, adjust this number
// for your use case)
$cores = $TargetDedicated * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicated + $extraVMs);
// Attempt to grow the number of compute nodes to match the number of active
// tasks, with a maximum of 3
$TargetDedicated = max(0,min($targetVMs,3));
// Keep the nodes active until the tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a><span data-ttu-id="1c2ac-567">Example 4: Setting an initial pool size</span><span class="sxs-lookup"><span data-stu-id="1c2ac-567">Example 4: Setting an initial pool size</span></span>
<span data-ttu-id="1c2ac-568">This example shows a C# code snippet with an autoscale formula that sets the pool size to a certain number of nodes for an initial time period.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-568">This example shows a C# code snippet with an autoscale formula that sets the pool size to a certain number of nodes for an initial time period.</span></span> <span data-ttu-id="1c2ac-569">Then it adjusts the pool size based on the number of running and active tasks after the initial time period has elapsed.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-569">Then it adjusts the pool size based on the number of running and active tasks after the initial time period has elapsed.</span></span>

<span data-ttu-id="1c2ac-570">The formula in the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="1c2ac-570">The formula in the following code snippet:</span></span>

* <span data-ttu-id="1c2ac-571">Sets the initial pool size to four nodes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-571">Sets the initial pool size to four nodes.</span></span>
* <span data-ttu-id="1c2ac-572">Does not adjust the pool size within the first 10 minutes of the pool's lifecycle.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-572">Does not adjust the pool size within the first 10 minutes of the pool's lifecycle.</span></span>
* <span data-ttu-id="1c2ac-573">After 10 minutes, obtains the max value of the number of running and active tasks within the past 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-573">After 10 minutes, obtains the max value of the number of running and active tasks within the past 60 minutes.</span></span>
  * <span data-ttu-id="1c2ac-574">If both values are 0 (indicating that no tasks were running or active in the last 60 minutes), the pool size is set to 0.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-574">If both values are 0 (indicating that no tasks were running or active in the last 60 minutes), the pool size is set to 0.</span></span>
  * <span data-ttu-id="1c2ac-575">If either value is greater than zero, no change is made.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-575">If either value is greater than zero, no change is made.</span></span>

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicated = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicated = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicated) : {1});
    ", now, 4);
```

## <a name="next-steps"></a><span data-ttu-id="1c2ac-576">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c2ac-576">Next steps</span></span>
* <span data-ttu-id="1c2ac-577">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) contains details about how you can execute multiple tasks simultaneously on the compute nodes in your pool.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-577">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) contains details about how you can execute multiple tasks simultaneously on the compute nodes in your pool.</span></span> <span data-ttu-id="1c2ac-578">In addition to autoscaling, this feature may help to lower job duration for some workloads, saving you money.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-578">In addition to autoscaling, this feature may help to lower job duration for some workloads, saving you money.</span></span>
* <span data-ttu-id="1c2ac-579">For another efficiency booster, ensure that your Batch application queries the Batch service in the most optimal way.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-579">For another efficiency booster, ensure that your Batch application queries the Batch service in the most optimal way.</span></span> <span data-ttu-id="1c2ac-580">In [Query the Azure Batch service efficiently](batch-efficient-list-queries.md), you'll learn how to limit the amount of data that crosses the wire when you query the status of potentially thousands of compute nodes or tasks.</span><span class="sxs-lookup"><span data-stu-id="1c2ac-580">In [Query the Azure Batch service efficiently](batch-efficient-list-queries.md), you'll learn how to limit the amount of data that crosses the wire when you query the status of potentially thousands of compute nodes or tasks.</span></span>

[net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_batchclient]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_autoscaleformula]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoscaleformula.aspx
[net_cloudpool_autoscaleevalinterval]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval.aspx
[net_enableautoscale]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.enableautoscale.aspx
[net_maxtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[net_poolops_resizepool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.resizepool.aspx

[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_autoscaleformula]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[rest_autoscaleinterval]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[rest_enableautoscale]: https://msdn.microsoft.com/library/azure/dn820173.aspx
