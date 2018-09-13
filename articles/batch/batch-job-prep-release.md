---
title: Create tasks to prepare jobs and complete jobs on compute nodes - Azure Batch | Microsoft Docs
description: Use job-level preparation tasks to minimize data transfer to Azure Batch compute nodes, and release tasks for node cleanup at job completion.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: ''
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9eb64641555c67b4d7c4d998044afeda6233f8ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552870"
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="213a1-103">Run job preparation and job release tasks on Batch compute nodes</span><span class="sxs-lookup"><span data-stu-id="213a1-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="213a1-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span><span class="sxs-lookup"><span data-stu-id="213a1-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="213a1-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span><span class="sxs-lookup"><span data-stu-id="213a1-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="213a1-106">You can use **job preparation** and **job release** tasks to perform these operations.</span><span class="sxs-lookup"><span data-stu-id="213a1-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="213a1-107">What are job preparation and release tasks?</span><span class="sxs-lookup"><span data-stu-id="213a1-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="213a1-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span><span class="sxs-lookup"><span data-stu-id="213a1-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="213a1-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span><span class="sxs-lookup"><span data-stu-id="213a1-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="213a1-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span><span class="sxs-lookup"><span data-stu-id="213a1-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="213a1-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span><span class="sxs-lookup"><span data-stu-id="213a1-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="213a1-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span><span class="sxs-lookup"><span data-stu-id="213a1-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="213a1-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span><span class="sxs-lookup"><span data-stu-id="213a1-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="213a1-114">When to use job preparation and release tasks</span><span class="sxs-lookup"><span data-stu-id="213a1-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="213a1-115">Job preparation and job release tasks are a good fit for the following situations:</span><span class="sxs-lookup"><span data-stu-id="213a1-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="213a1-116">**Download common task data**</span><span class="sxs-lookup"><span data-stu-id="213a1-116">**Download common task data**</span></span>

<span data-ttu-id="213a1-117">Batch jobs often require a common set of data as input for the job's tasks.</span><span class="sxs-lookup"><span data-stu-id="213a1-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="213a1-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span><span class="sxs-lookup"><span data-stu-id="213a1-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="213a1-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span><span class="sxs-lookup"><span data-stu-id="213a1-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="213a1-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span><span class="sxs-lookup"><span data-stu-id="213a1-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="213a1-121">**Delete job and task output**</span><span class="sxs-lookup"><span data-stu-id="213a1-121">**Delete job and task output**</span></span>

<span data-ttu-id="213a1-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span><span class="sxs-lookup"><span data-stu-id="213a1-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="213a1-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span><span class="sxs-lookup"><span data-stu-id="213a1-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="213a1-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span><span class="sxs-lookup"><span data-stu-id="213a1-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="213a1-125">**Log retention**</span><span class="sxs-lookup"><span data-stu-id="213a1-125">**Log retention**</span></span>

<span data-ttu-id="213a1-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span><span class="sxs-lookup"><span data-stu-id="213a1-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="213a1-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span><span class="sxs-lookup"><span data-stu-id="213a1-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="213a1-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span><span class="sxs-lookup"><span data-stu-id="213a1-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="213a1-129">Job preparation task</span><span class="sxs-lookup"><span data-stu-id="213a1-129">Job preparation task</span></span>
<span data-ttu-id="213a1-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span><span class="sxs-lookup"><span data-stu-id="213a1-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="213a1-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span><span class="sxs-lookup"><span data-stu-id="213a1-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="213a1-132">However, you can configure the service not to wait.</span><span class="sxs-lookup"><span data-stu-id="213a1-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="213a1-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span><span class="sxs-lookup"><span data-stu-id="213a1-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="213a1-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span><span class="sxs-lookup"><span data-stu-id="213a1-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="213a1-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span><span class="sxs-lookup"><span data-stu-id="213a1-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="213a1-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span><span class="sxs-lookup"><span data-stu-id="213a1-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="213a1-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span><span class="sxs-lookup"><span data-stu-id="213a1-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="213a1-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span><span class="sxs-lookup"><span data-stu-id="213a1-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="213a1-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span><span class="sxs-lookup"><span data-stu-id="213a1-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="213a1-140">Job release task</span><span class="sxs-lookup"><span data-stu-id="213a1-140">Job release task</span></span>
<span data-ttu-id="213a1-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span><span class="sxs-lookup"><span data-stu-id="213a1-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="213a1-142">You mark a job as completed by issuing a terminate request.</span><span class="sxs-lookup"><span data-stu-id="213a1-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="213a1-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span><span class="sxs-lookup"><span data-stu-id="213a1-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="213a1-144">The job then moves to the *completed* state.</span><span class="sxs-lookup"><span data-stu-id="213a1-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="213a1-145">Job deletion also executes the job release task.</span><span class="sxs-lookup"><span data-stu-id="213a1-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="213a1-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span><span class="sxs-lookup"><span data-stu-id="213a1-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="213a1-147">Job prep and release tasks with Batch .NET</span><span class="sxs-lookup"><span data-stu-id="213a1-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="213a1-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span><span class="sxs-lookup"><span data-stu-id="213a1-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="213a1-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span><span class="sxs-lookup"><span data-stu-id="213a1-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="213a1-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span><span class="sxs-lookup"><span data-stu-id="213a1-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="213a1-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span><span class="sxs-lookup"><span data-stu-id="213a1-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="213a1-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="213a1-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="213a1-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="213a1-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="213a1-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span><span class="sxs-lookup"><span data-stu-id="213a1-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="213a1-155">Code sample on GitHub</span><span class="sxs-lookup"><span data-stu-id="213a1-155">Code sample on GitHub</span></span>
<span data-ttu-id="213a1-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span><span class="sxs-lookup"><span data-stu-id="213a1-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="213a1-157">This console application does the following:</span><span class="sxs-lookup"><span data-stu-id="213a1-157">This console application does the following:</span></span>

1. <span data-ttu-id="213a1-158">Creates a pool with two "small" nodes.</span><span class="sxs-lookup"><span data-stu-id="213a1-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="213a1-159">Creates a job with job preparation, release, and standard tasks.</span><span class="sxs-lookup"><span data-stu-id="213a1-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="213a1-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span><span class="sxs-lookup"><span data-stu-id="213a1-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="213a1-161">Runs a task on each node that writes its task ID to the same text file.</span><span class="sxs-lookup"><span data-stu-id="213a1-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="213a1-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span><span class="sxs-lookup"><span data-stu-id="213a1-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="213a1-163">When the job is completed, runs the job release task to delete the file from the node.</span><span class="sxs-lookup"><span data-stu-id="213a1-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="213a1-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span><span class="sxs-lookup"><span data-stu-id="213a1-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="213a1-165">Pauses execution to allow confirmation of job and/or pool deletion.</span><span class="sxs-lookup"><span data-stu-id="213a1-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="213a1-166">Output from the sample application is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="213a1-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob to reach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="213a1-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span><span class="sxs-lookup"><span data-stu-id="213a1-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="213a1-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span><span class="sxs-lookup"><span data-stu-id="213a1-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="213a1-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span><span class="sxs-lookup"><span data-stu-id="213a1-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="213a1-170">Inspect job preparation and release tasks in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="213a1-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="213a1-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span><span class="sxs-lookup"><span data-stu-id="213a1-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="213a1-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span><span class="sxs-lookup"><span data-stu-id="213a1-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="213a1-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span><span class="sxs-lookup"><span data-stu-id="213a1-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Job preparation properties in Azure portal][1]

## <a name="next-steps"></a><span data-ttu-id="213a1-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="213a1-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="213a1-176">Application packages</span><span class="sxs-lookup"><span data-stu-id="213a1-176">Application packages</span></span>
<span data-ttu-id="213a1-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span><span class="sxs-lookup"><span data-stu-id="213a1-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="213a1-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span><span class="sxs-lookup"><span data-stu-id="213a1-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="213a1-179">Installing applications and staging data</span><span class="sxs-lookup"><span data-stu-id="213a1-179">Installing applications and staging data</span></span>
<span data-ttu-id="213a1-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span><span class="sxs-lookup"><span data-stu-id="213a1-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="213a1-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span><span class="sxs-lookup"><span data-stu-id="213a1-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="213a1-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="213a1-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-job-prep-release/portal-jobprep-01.png

