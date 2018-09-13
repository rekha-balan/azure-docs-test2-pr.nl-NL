---
title: Submit a large number of tasks - Azure Batch | Microsoft Docs
description: How to efficiently submit a very large number of tasks in a single Azure Batch job
services: batch
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: big-compute
ms.date: 08/24/2018
ms.author: danlep
ms.custom: ''
ms.openlocfilehash: 3c683b24db2899ee680988c7bedc760d6bb8ec73
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870132"
---
# <a name="submit-a-large-number-of-tasks-to-a-batch-job"></a><span data-ttu-id="09829-103">Submit a large number of tasks to a Batch job</span><span class="sxs-lookup"><span data-stu-id="09829-103">Submit a large number of tasks to a Batch job</span></span>

<span data-ttu-id="09829-104">When you run large-scale Azure Batch workloads, you might want to submit tens of thousands, hundreds of thousands, or even more tasks to a single job.</span><span class="sxs-lookup"><span data-stu-id="09829-104">When you run large-scale Azure Batch workloads, you might want to submit tens of thousands, hundreds of thousands, or even more tasks to a single job.</span></span> 

<span data-ttu-id="09829-105">This article gives guidance and some code examples to submit large numbers of tasks with substantially increased throughput to a single Batch job.</span><span class="sxs-lookup"><span data-stu-id="09829-105">This article gives guidance and some code examples to submit large numbers of tasks with substantially increased throughput to a single Batch job.</span></span> <span data-ttu-id="09829-106">After tasks are submitted, they enter the Batch queue for processing on the pool you specify for the job.</span><span class="sxs-lookup"><span data-stu-id="09829-106">After tasks are submitted, they enter the Batch queue for processing on the pool you specify for the job.</span></span>

## <a name="use-task-collections"></a><span data-ttu-id="09829-107">Use task collections</span><span class="sxs-lookup"><span data-stu-id="09829-107">Use task collections</span></span>

<span data-ttu-id="09829-108">The Batch APIs provide methods to efficiently add tasks to a job as a *collection*, in addition to one at a time.</span><span class="sxs-lookup"><span data-stu-id="09829-108">The Batch APIs provide methods to efficiently add tasks to a job as a *collection*, in addition to one at a time.</span></span> <span data-ttu-id="09829-109">When adding a large number of tasks, you should use the appropriate methods or overloads to add tasks as a collection.</span><span class="sxs-lookup"><span data-stu-id="09829-109">When adding a large number of tasks, you should use the appropriate methods or overloads to add tasks as a collection.</span></span> <span data-ttu-id="09829-110">Generally, you construct a task collection by defining tasks as you iterate over a set of input files or parameters for your job.</span><span class="sxs-lookup"><span data-stu-id="09829-110">Generally, you construct a task collection by defining tasks as you iterate over a set of input files or parameters for your job.</span></span>

<span data-ttu-id="09829-111">The maximum size of the task collection that you can add in a single call depends on the Batch API you use:</span><span class="sxs-lookup"><span data-stu-id="09829-111">The maximum size of the task collection that you can add in a single call depends on the Batch API you use:</span></span>

* <span data-ttu-id="09829-112">The following Batch APIs limit the collection to **100 tasks**.</span><span class="sxs-lookup"><span data-stu-id="09829-112">The following Batch APIs limit the collection to **100 tasks**.</span></span> <span data-ttu-id="09829-113">The limit could be smaller depending on the size of the tasks - for example, if the tasks have a large number of resource files or environment variables.</span><span class="sxs-lookup"><span data-stu-id="09829-113">The limit could be smaller depending on the size of the tasks - for example, if the tasks have a large number of resource files or environment variables.</span></span>

    * [<span data-ttu-id="09829-114">REST API</span><span class="sxs-lookup"><span data-stu-id="09829-114">REST API</span></span>](/rest/api/batchservice/task/addcollection)
    * [<span data-ttu-id="09829-115">Python API</span><span class="sxs-lookup"><span data-stu-id="09829-115">Python API</span></span>](/python/api/azure-batch/azure.batch.operations.TaskOperations?view=azure-python#azure_batch_operations_TaskOperations_add_collection)
    * [<span data-ttu-id="09829-116">Node.js API</span><span class="sxs-lookup"><span data-stu-id="09829-116">Node.js API</span></span>](/javascript/api/azure-batch/task?view=azure-node-latest#addcollection)

  <span data-ttu-id="09829-117">When using these APIs, you need to provide logic to divide the number of tasks to meet the collection limit, and to handle errors and retries in case addition of tasks fails.</span><span class="sxs-lookup"><span data-stu-id="09829-117">When using these APIs, you need to provide logic to divide the number of tasks to meet the collection limit, and to handle errors and retries in case addition of tasks fails.</span></span> <span data-ttu-id="09829-118">If a task collection is too large to add, the request generates an error and should be retried again with fewer tasks.</span><span class="sxs-lookup"><span data-stu-id="09829-118">If a task collection is too large to add, the request generates an error and should be retried again with fewer tasks.</span></span>

* <span data-ttu-id="09829-119">The following APIs support much larger task collections - limited only by RAM availability on the submitting client.</span><span class="sxs-lookup"><span data-stu-id="09829-119">The following APIs support much larger task collections - limited only by RAM availability on the submitting client.</span></span> <span data-ttu-id="09829-120">These APIs transparently handle dividing the task collection into "chunks" for the lower-level APIs and retries if addition of tasks fails.</span><span class="sxs-lookup"><span data-stu-id="09829-120">These APIs transparently handle dividing the task collection into "chunks" for the lower-level APIs and retries if addition of tasks fails.</span></span>

    * [<span data-ttu-id="09829-121">.NET API</span><span class="sxs-lookup"><span data-stu-id="09829-121">.NET API</span></span>](/dotnet/api/microsoft.azure.batch.cloudjob.addtaskasync?view=azure-dotnet)
    * [<span data-ttu-id="09829-122">Java API</span><span class="sxs-lookup"><span data-stu-id="09829-122">Java API</span></span>](/java/api/com.microsoft.azure.batch.protocol._tasks.addcollectionasync?view=azure-java-stable)
    * <span data-ttu-id="09829-123">[Azure Batch CLI extension](batch-cli-templates.md) with Batch CLI templates</span><span class="sxs-lookup"><span data-stu-id="09829-123">[Azure Batch CLI extension](batch-cli-templates.md) with Batch CLI templates</span></span>
    * [<span data-ttu-id="09829-124">Python SDK extension</span><span class="sxs-lookup"><span data-stu-id="09829-124">Python SDK extension</span></span>](https://pypi.org/project/azure-batch-extensions/)

## <a name="increase-throughput-of-task-submission"></a><span data-ttu-id="09829-125">Increase throughput of task submission</span><span class="sxs-lookup"><span data-stu-id="09829-125">Increase throughput of task submission</span></span>

<span data-ttu-id="09829-126">It can take some time to add a large collection of tasks to a job - for example, up to 1 minute to add 20,000 tasks via the .NET API.</span><span class="sxs-lookup"><span data-stu-id="09829-126">It can take some time to add a large collection of tasks to a job - for example, up to 1 minute to add 20,000 tasks via the .NET API.</span></span> <span data-ttu-id="09829-127">Depending on the Batch API and your workload, you can improve the task throughput by modifying one or more of the following:</span><span class="sxs-lookup"><span data-stu-id="09829-127">Depending on the Batch API and your workload, you can improve the task throughput by modifying one or more of the following:</span></span>

* <span data-ttu-id="09829-128">**Task size** - Adding large tasks takes longer than adding smaller ones.</span><span class="sxs-lookup"><span data-stu-id="09829-128">**Task size** - Adding large tasks takes longer than adding smaller ones.</span></span> <span data-ttu-id="09829-129">To reduce the size of each task in a collection, you can simplify the task command line, reduce the number of environment variables, or handle requirements for task execution more efficiently.</span><span class="sxs-lookup"><span data-stu-id="09829-129">To reduce the size of each task in a collection, you can simplify the task command line, reduce the number of environment variables, or handle requirements for task execution more efficiently.</span></span> <span data-ttu-id="09829-130">For example, instead of using a large number of resource files, install task dependencies using a [start task](batch-api-basics.md#start-task) on the pool or use an [application package](batch-application-packages.md) or [Docker container](batch-docker-container-workloads.md).</span><span class="sxs-lookup"><span data-stu-id="09829-130">For example, instead of using a large number of resource files, install task dependencies using a [start task](batch-api-basics.md#start-task) on the pool or use an [application package](batch-application-packages.md) or [Docker container](batch-docker-container-workloads.md).</span></span>

* <span data-ttu-id="09829-131">**Number of parallel operations** - Depending on the Batch API, increase throughput by increasing the maximum number of concurrent operations by the Batch client.</span><span class="sxs-lookup"><span data-stu-id="09829-131">**Number of parallel operations** - Depending on the Batch API, increase throughput by increasing the maximum number of concurrent operations by the Batch client.</span></span> <span data-ttu-id="09829-132">Configure this setting using the [BatchClientParallelOptions.MaxDegreeOfParallelism](/dotnet/api/microsoft.azure.batch.batchclientparalleloptions.maxdegreeofparallelism) property in the .NET API, or the `threads` parameter of methods such as [TaskOperations.add_collection](/python/api/azure-batch/azure.batch.operations.TaskOperations?view=azure-python#add-collection) in the Batch Python SDK extension.</span><span class="sxs-lookup"><span data-stu-id="09829-132">Configure this setting using the [BatchClientParallelOptions.MaxDegreeOfParallelism](/dotnet/api/microsoft.azure.batch.batchclientparalleloptions.maxdegreeofparallelism) property in the .NET API, or the `threads` parameter of methods such as [TaskOperations.add_collection](/python/api/azure-batch/azure.batch.operations.TaskOperations?view=azure-python#add-collection) in the Batch Python SDK extension.</span></span> <span data-ttu-id="09829-133">(This property is not available in the native Batch Python SDK.) By default, this property is set to 1, but set it higher to improve throughput of operations.</span><span class="sxs-lookup"><span data-stu-id="09829-133">(This property is not available in the native Batch Python SDK.) By default, this property is set to 1, but set it higher to improve throughput of operations.</span></span> <span data-ttu-id="09829-134">You trade off increased throughput by consuming network bandwidth and some CPU performance.</span><span class="sxs-lookup"><span data-stu-id="09829-134">You trade off increased throughput by consuming network bandwidth and some CPU performance.</span></span> <span data-ttu-id="09829-135">Task throughput increases by up to 100 times the `MaxDegreeOfParallelism` or `threads`.</span><span class="sxs-lookup"><span data-stu-id="09829-135">Task throughput increases by up to 100 times the `MaxDegreeOfParallelism` or `threads`.</span></span> <span data-ttu-id="09829-136">In practice, you should set the number of concurrent operations below 100.</span><span class="sxs-lookup"><span data-stu-id="09829-136">In practice, you should set the number of concurrent operations below 100.</span></span> 
 
  <span data-ttu-id="09829-137">The Azure Batch CLI extension with Batch templates increases the number of concurrent operations automatically based on the number of available cores, but this property is not configurable in the CLI.</span><span class="sxs-lookup"><span data-stu-id="09829-137">The Azure Batch CLI extension with Batch templates increases the number of concurrent operations automatically based on the number of available cores, but this property is not configurable in the CLI.</span></span> 

* <span data-ttu-id="09829-138">**HTTP connection limits** - The number of concurrent HTTP connections can throttle the performance of the Batch client when it is adding large numbers of tasks.</span><span class="sxs-lookup"><span data-stu-id="09829-138">**HTTP connection limits** - The number of concurrent HTTP connections can throttle the performance of the Batch client when it is adding large numbers of tasks.</span></span> <span data-ttu-id="09829-139">The number of HTTP connections is limited with certain APIs.</span><span class="sxs-lookup"><span data-stu-id="09829-139">The number of HTTP connections is limited with certain APIs.</span></span> <span data-ttu-id="09829-140">When developing with the .NET API, for example, the [ServicePointManager.DefaultConnectionLimit](/dotnet/api/system.net.servicepointmanager.defaultconnectionlimit) property is set to 2 by default.</span><span class="sxs-lookup"><span data-stu-id="09829-140">When developing with the .NET API, for example, the [ServicePointManager.DefaultConnectionLimit](/dotnet/api/system.net.servicepointmanager.defaultconnectionlimit) property is set to 2 by default.</span></span> <span data-ttu-id="09829-141">We recommend that you increase the value to a number close to or greater than the number of parallel operations.</span><span class="sxs-lookup"><span data-stu-id="09829-141">We recommend that you increase the value to a number close to or greater than the number of parallel operations.</span></span>

## <a name="example-batch-net"></a><span data-ttu-id="09829-142">Example: Batch .NET</span><span class="sxs-lookup"><span data-stu-id="09829-142">Example: Batch .NET</span></span>

<span data-ttu-id="09829-143">The following C# snippets show settings to configure when adding a large number of tasks using the Batch .NET API.</span><span class="sxs-lookup"><span data-stu-id="09829-143">The following C# snippets show settings to configure when adding a large number of tasks using the Batch .NET API.</span></span>

<span data-ttu-id="09829-144">To increase task throughput, increase the value of the [MaxDegreeofParallelism](/dotnet/api/microsoft.azure.batch.batchclientparalleloptions.maxdegreeofparallelism) property of the [BatchClient](/dotnet/api/microsoft.azure.batch.batchclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="09829-144">To increase task throughput, increase the value of the [MaxDegreeofParallelism](/dotnet/api/microsoft.azure.batch.batchclientparalleloptions.maxdegreeofparallelism) property of the [BatchClient](/dotnet/api/microsoft.azure.batch.batchclient?view=azure-dotnet).</span></span> <span data-ttu-id="09829-145">For example:</span><span class="sxs-lookup"><span data-stu-id="09829-145">For example:</span></span>

```csharp
BatchClientParallelOptions parallelOptions = new BatchClientParallelOptions()
  {
    MaxDegreeOfParallelism = 15
  };
...
```
<span data-ttu-id="09829-146">Add a task collection to the job using the appropriate overload of the [AddTaskAsync](/dotnet/api/microsoft.azure.batch.cloudjob.addtaskasync?view=azure-dotnet) or [AddTask](/dotnet/api/microsoft.azure.batch.cloudjob.addtask?view=azure-dotnet
) method.</span><span class="sxs-lookup"><span data-stu-id="09829-146">Add a task collection to the job using the appropriate overload of the [AddTaskAsync](/dotnet/api/microsoft.azure.batch.cloudjob.addtaskasync?view=azure-dotnet) or [AddTask](/dotnet/api/microsoft.azure.batch.cloudjob.addtask?view=azure-dotnet
) method.</span></span> <span data-ttu-id="09829-147">For example:</span><span class="sxs-lookup"><span data-stu-id="09829-147">For example:</span></span>

```csharp
// Add a list of tasks as a collection
List<CloudTask> tasksToAdd = new List<CloudTask>(); // Populate with your tasks
...
await batchClient.JobOperations.AddTaskAsync(jobId, tasksToAdd, parallelOptions);
```


## <a name="example-batch-cli-extension"></a><span data-ttu-id="09829-148">Example: Batch CLI extension</span><span class="sxs-lookup"><span data-stu-id="09829-148">Example: Batch CLI extension</span></span>

<span data-ttu-id="09829-149">Using the Azure Batch CLI extensions with [Batch CLI templates](batch-cli-templates.md), create a job template JSON file that includes a [task factory](https://github.com/Azure/azure-batch-cli-extensions/blob/master/doc/taskFactories.md).</span><span class="sxs-lookup"><span data-stu-id="09829-149">Using the Azure Batch CLI extensions with [Batch CLI templates](batch-cli-templates.md), create a job template JSON file that includes a [task factory](https://github.com/Azure/azure-batch-cli-extensions/blob/master/doc/taskFactories.md).</span></span> <span data-ttu-id="09829-150">The task factory configures a collection of related tasks for a job from a single task definition.</span><span class="sxs-lookup"><span data-stu-id="09829-150">The task factory configures a collection of related tasks for a job from a single task definition.</span></span>  

<span data-ttu-id="09829-151">The following is a sample job template for a one-dimensional parametric sweep job with a large number of tasks - in this case, 250,000.</span><span class="sxs-lookup"><span data-stu-id="09829-151">The following is a sample job template for a one-dimensional parametric sweep job with a large number of tasks - in this case, 250,000.</span></span> <span data-ttu-id="09829-152">The task command line is a simple `echo` command.</span><span class="sxs-lookup"><span data-stu-id="09829-152">The task command line is a simple `echo` command.</span></span>

```json
{
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "myjob",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "mypool"
            },
            "taskFactory": {
                "type": "parametricSweep",
                "parameterSets": [
                    {
                        "start": 1,
                        "end": 250000,
                        "step": 1
                    }
                ],
                "repeatTask": {
                    "commandLine": "/bin/bash -c 'echo Hello world from task {0}'",
                    "constraints": {
                        "retentionTime":"PT1H"
                    }
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```
<span data-ttu-id="09829-153">To run a job with the template, see [Use Azure Batch CLI templates and file transfer](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="09829-153">To run a job with the template, see [Use Azure Batch CLI templates and file transfer](batch-cli-templates.md).</span></span>

## <a name="example-batch-python-sdk-extension"></a><span data-ttu-id="09829-154">Example: Batch Python SDK extension</span><span class="sxs-lookup"><span data-stu-id="09829-154">Example: Batch Python SDK extension</span></span>

<span data-ttu-id="09829-155">To use the Azure Batch Python SDK extension, first install the Python SDK and the extension:</span><span class="sxs-lookup"><span data-stu-id="09829-155">To use the Azure Batch Python SDK extension, first install the Python SDK and the extension:</span></span>

```
pip install azure-batch
pip install azure-batch-extensions
```

<span data-ttu-id="09829-156">Set up a `BatchExtensionsClient` that uses the SDK extension:</span><span class="sxs-lookup"><span data-stu-id="09829-156">Set up a `BatchExtensionsClient` that uses the SDK extension:</span></span>

```python

client = batch.BatchExtensionsClient(base_url=BATCH_ACCOUNT_URL, resource_group=RESOURCE_GROUP_NAME, batch_account=BATCH_ACCOUNT_NAME)
...
```

<span data-ttu-id="09829-157">Create a collection of tasks to add to a job.</span><span class="sxs-lookup"><span data-stu-id="09829-157">Create a collection of tasks to add to a job.</span></span> <span data-ttu-id="09829-158">For example:</span><span class="sxs-lookup"><span data-stu-id="09829-158">For example:</span></span>


```python
tasks=list()
# Populate the list with your tasks
...

```

<span data-ttu-id="09829-159">Add the task collection using [task.add_collection](/python/api/azure-batch/azure.batch.operations.TaskOperations?view=azure-python#add-collection).</span><span class="sxs-lookup"><span data-stu-id="09829-159">Add the task collection using [task.add_collection](/python/api/azure-batch/azure.batch.operations.TaskOperations?view=azure-python#add-collection).</span></span> <span data-ttu-id="09829-160">Set the `threads` parameter to increase the number of concurrent operations:</span><span class="sxs-lookup"><span data-stu-id="09829-160">Set the `threads` parameter to increase the number of concurrent operations:</span></span>

```python
try:
    client.task.add_collection(job_id, threads=100)
except Exception as e:
    raise e
```

<span data-ttu-id="09829-161">The Batch Python SDK extension also supports adding task parameters to job using a JSON specification for a task factory.</span><span class="sxs-lookup"><span data-stu-id="09829-161">The Batch Python SDK extension also supports adding task parameters to job using a JSON specification for a task factory.</span></span> <span data-ttu-id="09829-162">For example, configure job parameters for a parametric sweep similar to the one in the preceding [Batch CLI template](#example-batch-cli-template) example:</span><span class="sxs-lookup"><span data-stu-id="09829-162">For example, configure job parameters for a parametric sweep similar to the one in the preceding [Batch CLI template](#example-batch-cli-template) example:</span></span>

```python
parameter_sweep = {
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "myjob",
            "poolInfo": {
                "poolId": "mypool"
            },
            "taskFactory": {
                "type": "parametricSweep",
                "parameterSets": [
                    {
                        "start": 1,
                        "end": 250000,
                        "step": 1
                    }
                ],
                "repeatTask": {
                    "commandLine": "/bin/bash -c 'echo Hello world from task {0}'",
                    "constraints": {
                        "retentionTime":"PT1H"
                    }
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
...
job_json = client.job.expand_template(parameter_sweep)
job_parameter = client.job.jobparameter_from_json(job_json)
```

<span data-ttu-id="09829-163">Add the job parameters to the job.</span><span class="sxs-lookup"><span data-stu-id="09829-163">Add the job parameters to the job.</span></span> <span data-ttu-id="09829-164">Set the `threads` parameter to increase the number of concurrent operations:</span><span class="sxs-lookup"><span data-stu-id="09829-164">Set the `threads` parameter to increase the number of concurrent operations:</span></span>

```python
try:
    client.job.add(job_parameter, threads=50)
except Exception as e:
    raise e
```

## <a name="next-steps"></a><span data-ttu-id="09829-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="09829-165">Next steps</span></span>

* <span data-ttu-id="09829-166">Learn more about using the Azure Batch CLI extension with [Batch CLI templates](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="09829-166">Learn more about using the Azure Batch CLI extension with [Batch CLI templates](batch-cli-templates.md).</span></span>
* <span data-ttu-id="09829-167">Learn more about the [Batch Python SDK extension](https://pypi.org/project/azure-batch-extensions/).</span><span class="sxs-lookup"><span data-stu-id="09829-167">Learn more about the [Batch Python SDK extension](https://pypi.org/project/azure-batch-extensions/).</span></span>