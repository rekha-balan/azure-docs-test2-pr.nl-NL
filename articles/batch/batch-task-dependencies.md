---
title: Use task dependencies to run tasks based on the completion of other tasks - Azure Batch | Microsoft Docs
description: Create tasks that depend on the completion of other tasks for processing MapReduce style and similar big data workloads in Azure Batch.
services: batch
documentationcenter: .net
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a9b44ed56774466bae2f0f5d48b5e012382721b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44771699"
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="b0a93-103">Create task dependencies to run tasks that depend on other tasks</span><span class="sxs-lookup"><span data-stu-id="b0a93-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="b0a93-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span><span class="sxs-lookup"><span data-stu-id="b0a93-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="b0a93-105">Some scenarios where task dependencies are useful include:</span><span class="sxs-lookup"><span data-stu-id="b0a93-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="b0a93-106">MapReduce-style workloads in the cloud.</span><span class="sxs-lookup"><span data-stu-id="b0a93-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="b0a93-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span><span class="sxs-lookup"><span data-stu-id="b0a93-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="b0a93-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span><span class="sxs-lookup"><span data-stu-id="b0a93-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="b0a93-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span><span class="sxs-lookup"><span data-stu-id="b0a93-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="b0a93-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span><span class="sxs-lookup"><span data-stu-id="b0a93-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="b0a93-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span><span class="sxs-lookup"><span data-stu-id="b0a93-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="b0a93-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span><span class="sxs-lookup"><span data-stu-id="b0a93-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="b0a93-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="b0a93-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="b0a93-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span><span class="sxs-lookup"><span data-stu-id="b0a93-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="b0a93-115">See the [Dependency actions](#dependency-actions) section for details.</span><span class="sxs-lookup"><span data-stu-id="b0a93-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="b0a93-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span><span class="sxs-lookup"><span data-stu-id="b0a93-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="b0a93-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span><span class="sxs-lookup"><span data-stu-id="b0a93-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="b0a93-118">You can combine these three basic scenarios to create many-to-many relationships.</span><span class="sxs-lookup"><span data-stu-id="b0a93-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="b0a93-119">Task dependencies with Batch .NET</span><span class="sxs-lookup"><span data-stu-id="b0a93-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="b0a93-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span><span class="sxs-lookup"><span data-stu-id="b0a93-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="b0a93-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="b0a93-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="b0a93-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span><span class="sxs-lookup"><span data-stu-id="b0a93-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="b0a93-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span><span class="sxs-lookup"><span data-stu-id="b0a93-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="b0a93-124">Enable task dependencies</span><span class="sxs-lookup"><span data-stu-id="b0a93-124">Enable task dependencies</span></span>
<span data-ttu-id="b0a93-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span><span class="sxs-lookup"><span data-stu-id="b0a93-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="b0a93-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span><span class="sxs-lookup"><span data-stu-id="b0a93-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="b0a93-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span><span class="sxs-lookup"><span data-stu-id="b0a93-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="b0a93-128">Create dependent tasks</span><span class="sxs-lookup"><span data-stu-id="b0a93-128">Create dependent tasks</span></span>
<span data-ttu-id="b0a93-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span><span class="sxs-lookup"><span data-stu-id="b0a93-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="b0a93-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span><span class="sxs-lookup"><span data-stu-id="b0a93-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="b0a93-131">This code snippet creates a dependent task with task ID "Flowers".</span><span class="sxs-lookup"><span data-stu-id="b0a93-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="b0a93-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span><span class="sxs-lookup"><span data-stu-id="b0a93-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="b0a93-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span><span class="sxs-lookup"><span data-stu-id="b0a93-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="b0a93-134">By default, a task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span><span class="sxs-lookup"><span data-stu-id="b0a93-134">By default, a task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="b0a93-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span><span class="sxs-lookup"><span data-stu-id="b0a93-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span> <span data-ttu-id="b0a93-136">For how to change this, see the [Dependency actions](#dependency-actions) section.</span><span class="sxs-lookup"><span data-stu-id="b0a93-136">For how to change this, see the [Dependency actions](#dependency-actions) section.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="b0a93-137">Dependency scenarios</span><span class="sxs-lookup"><span data-stu-id="b0a93-137">Dependency scenarios</span></span>
<span data-ttu-id="b0a93-138">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span><span class="sxs-lookup"><span data-stu-id="b0a93-138">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="b0a93-139">These can be combined to provide a fourth scenario, many-to-many.</span><span class="sxs-lookup"><span data-stu-id="b0a93-139">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="b0a93-140">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="b0a93-140">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="b0a93-141">Example</span><span class="sxs-lookup"><span data-stu-id="b0a93-141">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="b0a93-142">One-to-one</span><span class="sxs-lookup"><span data-stu-id="b0a93-142">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="b0a93-143">*taskB* depends on *taskA*</span><span class="sxs-lookup"><span data-stu-id="b0a93-143">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="b0a93-144">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span><span class="sxs-lookup"><span data-stu-id="b0a93-144">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="b0a93-145">![Diagram: one-to-one task dependency][1]</span><span class="sxs-lookup"><span data-stu-id="b0a93-145">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="b0a93-146">One-to-many</span><span class="sxs-lookup"><span data-stu-id="b0a93-146">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="b0a93-147">*taskC* depends on both *taskA* and *taskB*</span><span class="sxs-lookup"><span data-stu-id="b0a93-147">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="b0a93-148">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span><span class="sxs-lookup"><span data-stu-id="b0a93-148">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="b0a93-149">![Diagram: one-to-many task dependency][2]</span><span class="sxs-lookup"><span data-stu-id="b0a93-149">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="b0a93-150">Task ID range</span><span class="sxs-lookup"><span data-stu-id="b0a93-150">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="b0a93-151">*taskD* depends on a range of tasks</span><span class="sxs-lookup"><span data-stu-id="b0a93-151">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="b0a93-152">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span><span class="sxs-lookup"><span data-stu-id="b0a93-152">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="b0a93-153">![Diagram: Task id range dependency][3]</span><span class="sxs-lookup"><span data-stu-id="b0a93-153">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="b0a93-154">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span><span class="sxs-lookup"><span data-stu-id="b0a93-154">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="b0a93-155">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span><span class="sxs-lookup"><span data-stu-id="b0a93-155">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="b0a93-156">This behavior is the default behavior for a dependent task.</span><span class="sxs-lookup"><span data-stu-id="b0a93-156">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="b0a93-157">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span><span class="sxs-lookup"><span data-stu-id="b0a93-157">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="b0a93-158">See the [Dependency actions](#dependency-actions) section for details.</span><span class="sxs-lookup"><span data-stu-id="b0a93-158">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="b0a93-159">One-to-one</span><span class="sxs-lookup"><span data-stu-id="b0a93-159">One-to-one</span></span>
<span data-ttu-id="b0a93-160">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span><span class="sxs-lookup"><span data-stu-id="b0a93-160">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="b0a93-161">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="b0a93-161">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="b0a93-162">One-to-many</span><span class="sxs-lookup"><span data-stu-id="b0a93-162">One-to-many</span></span>
<span data-ttu-id="b0a93-163">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span><span class="sxs-lookup"><span data-stu-id="b0a93-163">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="b0a93-164">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="b0a93-164">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="b0a93-165">Task ID range</span><span class="sxs-lookup"><span data-stu-id="b0a93-165">Task ID range</span></span>
<span data-ttu-id="b0a93-166">In a dependency on a range of parent tasks, a task depends on the completion of tasks whose IDs lie within a range.</span><span class="sxs-lookup"><span data-stu-id="b0a93-166">In a dependency on a range of parent tasks, a task depends on the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="b0a93-167">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="b0a93-167">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0a93-168">When you use task ID ranges for your dependencies, only tasks with IDs representing integer values will be selected by the range.</span><span class="sxs-lookup"><span data-stu-id="b0a93-168">When you use task ID ranges for your dependencies, only tasks with IDs representing integer values will be selected by the range.</span></span> <span data-ttu-id="b0a93-169">So the range `1..10` will select tasks `3` and `7`, but not `5flamingoes`.</span><span class="sxs-lookup"><span data-stu-id="b0a93-169">So the range `1..10` will select tasks `3` and `7`, but not `5flamingoes`.</span></span> 
> 
> <span data-ttu-id="b0a93-170">Leading zeroes are not signficant when evaluating range dependencies, so tasks with string identifiers `4`, `04` and `004` will all be *within* the range and they will all be treated as task `4`, so the first one to complete will satisfy the dependency.</span><span class="sxs-lookup"><span data-stu-id="b0a93-170">Leading zeroes are not signficant when evaluating range dependencies, so tasks with string identifiers `4`, `04` and `004` will all be *within* the range and they will all be treated as task `4`, so the first one to complete will satisfy the dependency.</span></span>
> 
> <span data-ttu-id="b0a93-171">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="b0a93-171">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="b0a93-172">See the [Dependency actions](#dependency-actions) section for details.</span><span class="sxs-lookup"><span data-stu-id="b0a93-172">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="b0a93-173">Dependency actions</span><span class="sxs-lookup"><span data-stu-id="b0a93-173">Dependency actions</span></span>

<span data-ttu-id="b0a93-174">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="b0a93-174">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="b0a93-175">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span><span class="sxs-lookup"><span data-stu-id="b0a93-175">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="b0a93-176">You can override the default behavior by specifying a dependency action.</span><span class="sxs-lookup"><span data-stu-id="b0a93-176">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="b0a93-177">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span><span class="sxs-lookup"><span data-stu-id="b0a93-177">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="b0a93-178">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span><span class="sxs-lookup"><span data-stu-id="b0a93-178">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="b0a93-179">If the upstream task fails, the dependent task may still be able to run using older data.</span><span class="sxs-lookup"><span data-stu-id="b0a93-179">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="b0a93-180">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span><span class="sxs-lookup"><span data-stu-id="b0a93-180">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="b0a93-181">A dependency action is based on an exit condition for the parent task.</span><span class="sxs-lookup"><span data-stu-id="b0a93-181">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="b0a93-182">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span><span class="sxs-lookup"><span data-stu-id="b0a93-182">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="b0a93-183">When a pre-processing error occurs.</span><span class="sxs-lookup"><span data-stu-id="b0a93-183">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="b0a93-184">When a file upload error occurs.</span><span class="sxs-lookup"><span data-stu-id="b0a93-184">When a file upload error occurs.</span></span> <span data-ttu-id="b0a93-185">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span><span class="sxs-lookup"><span data-stu-id="b0a93-185">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="b0a93-186">When the task exits with an exit code defined by the **ExitCodes** property.</span><span class="sxs-lookup"><span data-stu-id="b0a93-186">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="b0a93-187">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span><span class="sxs-lookup"><span data-stu-id="b0a93-187">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="b0a93-188">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span><span class="sxs-lookup"><span data-stu-id="b0a93-188">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="b0a93-189">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span><span class="sxs-lookup"><span data-stu-id="b0a93-189">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="b0a93-190">The **DependencyAction** property takes one of two values:</span><span class="sxs-lookup"><span data-stu-id="b0a93-190">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="b0a93-191">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span><span class="sxs-lookup"><span data-stu-id="b0a93-191">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="b0a93-192">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span><span class="sxs-lookup"><span data-stu-id="b0a93-192">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="b0a93-193">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span><span class="sxs-lookup"><span data-stu-id="b0a93-193">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="b0a93-194">The following code snippet sets the **DependencyAction** property for a parent task.</span><span class="sxs-lookup"><span data-stu-id="b0a93-194">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="b0a93-195">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span><span class="sxs-lookup"><span data-stu-id="b0a93-195">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="b0a93-196">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span><span class="sxs-lookup"><span data-stu-id="b0a93-196">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="b0a93-197">Code sample</span><span class="sxs-lookup"><span data-stu-id="b0a93-197">Code sample</span></span>
<span data-ttu-id="b0a93-198">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="b0a93-198">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="b0a93-199">This Visual Studio solution demonstrates:</span><span class="sxs-lookup"><span data-stu-id="b0a93-199">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="b0a93-200">How to enable task dependency on a job</span><span class="sxs-lookup"><span data-stu-id="b0a93-200">How to enable task dependency on a job</span></span>
- <span data-ttu-id="b0a93-201">How to create tasks that depend on other tasks</span><span class="sxs-lookup"><span data-stu-id="b0a93-201">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="b0a93-202">How to execute those tasks on a pool of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b0a93-202">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0a93-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0a93-203">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="b0a93-204">Application deployment</span><span class="sxs-lookup"><span data-stu-id="b0a93-204">Application deployment</span></span>
<span data-ttu-id="b0a93-205">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b0a93-205">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="b0a93-206">Installing applications and staging data</span><span class="sxs-lookup"><span data-stu-id="b0a93-206">Installing applications and staging data</span></span>
<span data-ttu-id="b0a93-207">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span><span class="sxs-lookup"><span data-stu-id="b0a93-207">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="b0a93-208">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b0a93-208">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"
