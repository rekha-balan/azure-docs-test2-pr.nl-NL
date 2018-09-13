---
title: Persist job and task output to Azure Storage - Azure Batch | Microsoft Docs
description: Learn how to use Azure Storage as a durable store for your Batch task and job output, and enable viewing this persisted output in the Azure portal.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: ''
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8eb5e17893e4ebb619ba577b19fa1653a310ccda
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661814"
---
# <a name="persist-results-from-completed-jobs-and-tasks-to-azure-storage"></a><span data-ttu-id="042af-103">Persist results from completed jobs and tasks to Azure Storage</span><span class="sxs-lookup"><span data-stu-id="042af-103">Persist results from completed jobs and tasks to Azure Storage</span></span>

<span data-ttu-id="042af-104">The tasks you run in Batch typically produce output that must be stored and then later retrieved by other tasks in the job, the client application that executed the job, or both.</span><span class="sxs-lookup"><span data-stu-id="042af-104">The tasks you run in Batch typically produce output that must be stored and then later retrieved by other tasks in the job, the client application that executed the job, or both.</span></span> <span data-ttu-id="042af-105">This output might be files created by processing input data or log files associated with task execution.</span><span class="sxs-lookup"><span data-stu-id="042af-105">This output might be files created by processing input data or log files associated with task execution.</span></span> <span data-ttu-id="042af-106">This article introduces a .NET class library that uses a conventions-based technique to persist such task output to Azure Blob storage, making it available even after you delete your pools, jobs, and compute nodes.</span><span class="sxs-lookup"><span data-stu-id="042af-106">This article introduces a .NET class library that uses a conventions-based technique to persist such task output to Azure Blob storage, making it available even after you delete your pools, jobs, and compute nodes.</span></span>

<span data-ttu-id="042af-107">By using the technique in this article, you can also view your task output in **Saved output files** and **Saved logs** in the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="042af-107">By using the technique in this article, you can also view your task output in **Saved output files** and **Saved logs** in the [Azure portal][portal].</span></span>

<span data-ttu-id="042af-108">![Saved output files and Saved logs selectors in portal][1]</span><span class="sxs-lookup"><span data-stu-id="042af-108">![Saved output files and Saved logs selectors in portal][1]</span></span>

> [!NOTE]
> <span data-ttu-id="042af-109">The [Azure Batch File Conventions][nuget_package] .NET class library discussed in this article is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="042af-109">The [Azure Batch File Conventions][nuget_package] .NET class library discussed in this article is currently in preview.</span></span> <span data-ttu-id="042af-110">Some of the features described here may change prior to general availability.</span><span class="sxs-lookup"><span data-stu-id="042af-110">Some of the features described here may change prior to general availability.</span></span>
> 
> 

## <a name="task-output-considerations"></a><span data-ttu-id="042af-111">Task output considerations</span><span class="sxs-lookup"><span data-stu-id="042af-111">Task output considerations</span></span>
<span data-ttu-id="042af-112">When you design your Batch solution, you must consider several factors related to job and task outputs.</span><span class="sxs-lookup"><span data-stu-id="042af-112">When you design your Batch solution, you must consider several factors related to job and task outputs.</span></span>

* <span data-ttu-id="042af-113">**Compute node lifetime**: Compute nodes are often transient, especially in autoscale-enabled pools.</span><span class="sxs-lookup"><span data-stu-id="042af-113">**Compute node lifetime**: Compute nodes are often transient, especially in autoscale-enabled pools.</span></span> <span data-ttu-id="042af-114">The outputs of the tasks that run on a node are available only while the node exists, and only within the file retention time you've set for the task.</span><span class="sxs-lookup"><span data-stu-id="042af-114">The outputs of the tasks that run on a node are available only while the node exists, and only within the file retention time you've set for the task.</span></span> <span data-ttu-id="042af-115">To ensure that the task output is preserved, your tasks must therefore upload their output files to a durable store, for example, Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="042af-115">To ensure that the task output is preserved, your tasks must therefore upload their output files to a durable store, for example, Azure Storage.</span></span>
* <span data-ttu-id="042af-116">**Output storage**: To persist task output data to durable storage, you can use the [Azure Storage SDK](../storage/storage-dotnet-how-to-use-blobs.md) in your task code to upload the task output to a Blob storage container.</span><span class="sxs-lookup"><span data-stu-id="042af-116">**Output storage**: To persist task output data to durable storage, you can use the [Azure Storage SDK](../storage/storage-dotnet-how-to-use-blobs.md) in your task code to upload the task output to a Blob storage container.</span></span> <span data-ttu-id="042af-117">If you implement a container and file naming convention, your client application or other tasks in the job can then locate and download this output based on the convention.</span><span class="sxs-lookup"><span data-stu-id="042af-117">If you implement a container and file naming convention, your client application or other tasks in the job can then locate and download this output based on the convention.</span></span>
* <span data-ttu-id="042af-118">**Output retrieval**: You can retrieve task output directly from the compute nodes in your pool, or from Azure Storage if your tasks persist their output.</span><span class="sxs-lookup"><span data-stu-id="042af-118">**Output retrieval**: You can retrieve task output directly from the compute nodes in your pool, or from Azure Storage if your tasks persist their output.</span></span> <span data-ttu-id="042af-119">To retrieve a task's output directly from a compute node, you need the file name and its output location on the node.</span><span class="sxs-lookup"><span data-stu-id="042af-119">To retrieve a task's output directly from a compute node, you need the file name and its output location on the node.</span></span> <span data-ttu-id="042af-120">If you persist output to Azure Storage, downstream tasks or your client application must have the full path to the file in Azure Storage to download it by using the Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="042af-120">If you persist output to Azure Storage, downstream tasks or your client application must have the full path to the file in Azure Storage to download it by using the Azure Storage SDK.</span></span>
* <span data-ttu-id="042af-121">**Viewing output**: When you navigate to a Batch task in the Azure portal and select **Files on node**, you are presented with all files associated with the task, not just the output files you're interested in.</span><span class="sxs-lookup"><span data-stu-id="042af-121">**Viewing output**: When you navigate to a Batch task in the Azure portal and select **Files on node**, you are presented with all files associated with the task, not just the output files you're interested in.</span></span> <span data-ttu-id="042af-122">Again, files on compute nodes are available only while the node exists and only within the file retention time you've set for the task.</span><span class="sxs-lookup"><span data-stu-id="042af-122">Again, files on compute nodes are available only while the node exists and only within the file retention time you've set for the task.</span></span> <span data-ttu-id="042af-123">To view task output that you've persisted to Azure Storage in the portal or an application like the [Azure Storage Explorer][storage_explorer], you must know its location and navigate to the file directly.</span><span class="sxs-lookup"><span data-stu-id="042af-123">To view task output that you've persisted to Azure Storage in the portal or an application like the [Azure Storage Explorer][storage_explorer], you must know its location and navigate to the file directly.</span></span>

## <a name="help-for-persisted-output"></a><span data-ttu-id="042af-124">Help for persisted output</span><span class="sxs-lookup"><span data-stu-id="042af-124">Help for persisted output</span></span>
<span data-ttu-id="042af-125">To help you more easily persist job and task output, the Batch team has defined and implemented a set of naming conventions as well as a .NET class library, the [Azure Batch File Conventions][nuget_package] library, that you can use in your Batch applications.</span><span class="sxs-lookup"><span data-stu-id="042af-125">To help you more easily persist job and task output, the Batch team has defined and implemented a set of naming conventions as well as a .NET class library, the [Azure Batch File Conventions][nuget_package] library, that you can use in your Batch applications.</span></span> <span data-ttu-id="042af-126">In addition, the Azure portal is aware of these naming conventions so that you can easily find the files you've stored by using the library.</span><span class="sxs-lookup"><span data-stu-id="042af-126">In addition, the Azure portal is aware of these naming conventions so that you can easily find the files you've stored by using the library.</span></span>

## <a name="using-the-file-conventions-library"></a><span data-ttu-id="042af-127">Using the file conventions library</span><span class="sxs-lookup"><span data-stu-id="042af-127">Using the file conventions library</span></span>
<span data-ttu-id="042af-128">[Azure Batch File Conventions][nuget_package] is a .NET class library that your Batch .NET applications can use to easily store and retrieve task outputs to and from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="042af-128">[Azure Batch File Conventions][nuget_package] is a .NET class library that your Batch .NET applications can use to easily store and retrieve task outputs to and from Azure Storage.</span></span> <span data-ttu-id="042af-129">It is intended for use in both task and client code--in task code for persisting files, and in client code to list and retrieve them.</span><span class="sxs-lookup"><span data-stu-id="042af-129">It is intended for use in both task and client code--in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="042af-130">Your tasks can also use the library for retrieving the outputs of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span><span class="sxs-lookup"><span data-stu-id="042af-130">Your tasks can also use the library for retrieving the outputs of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span>

<span data-ttu-id="042af-131">The conventions library takes care of ensuring that storage containers and task output files are named according to the convention, and are uploaded to the right place when persisted to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="042af-131">The conventions library takes care of ensuring that storage containers and task output files are named according to the convention, and are uploaded to the right place when persisted to Azure Storage.</span></span> <span data-ttu-id="042af-132">When you retrieve outputs, you can easily locate the outputs for a given job or task by listing or retrieving the outputs by ID and purpose, instead of having to know filenames or where it exists in Storage.</span><span class="sxs-lookup"><span data-stu-id="042af-132">When you retrieve outputs, you can easily locate the outputs for a given job or task by listing or retrieving the outputs by ID and purpose, instead of having to know filenames or where it exists in Storage.</span></span>

<span data-ttu-id="042af-133">For example, you can use the library to "list all intermediate files for task 7," or "get me the thumbnail preview for job *mymovie*," without needing to know the file names or location within your Storage account.</span><span class="sxs-lookup"><span data-stu-id="042af-133">For example, you can use the library to "list all intermediate files for task 7," or "get me the thumbnail preview for job *mymovie*," without needing to know the file names or location within your Storage account.</span></span>

### <a name="get-the-library"></a><span data-ttu-id="042af-134">Get the library</span><span class="sxs-lookup"><span data-stu-id="042af-134">Get the library</span></span>
<span data-ttu-id="042af-135">You can obtain the library, which contains new classes and extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods, from [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="042af-135">You can obtain the library, which contains new classes and extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods, from [NuGet][nuget_package].</span></span> <span data-ttu-id="042af-136">You can add it to your Visual Studio project using the [NuGet Library Package Manager][nuget_manager].</span><span class="sxs-lookup"><span data-stu-id="042af-136">You can add it to your Visual Studio project using the [NuGet Library Package Manager][nuget_manager].</span></span>

> [!TIP]
> <span data-ttu-id="042af-137">You can find the [source code][github_file_conventions] for the Azure Batch File Conventions library on GitHub in the Microsoft Azure SDK for .NET repository.</span><span class="sxs-lookup"><span data-stu-id="042af-137">You can find the [source code][github_file_conventions] for the Azure Batch File Conventions library on GitHub in the Microsoft Azure SDK for .NET repository.</span></span>
> 
> 

## <a name="requirement-linked-storage-account"></a><span data-ttu-id="042af-138">Requirement: linked storage account</span><span class="sxs-lookup"><span data-stu-id="042af-138">Requirement: linked storage account</span></span>
<span data-ttu-id="042af-139">To store outputs to durable storage using the file conventions library and view them in the Azure portal, you must [link an Azure Storage account](batch-application-packages.md#link-a-storage-account) to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="042af-139">To store outputs to durable storage using the file conventions library and view them in the Azure portal, you must [link an Azure Storage account](batch-application-packages.md#link-a-storage-account) to your Batch account.</span></span> <span data-ttu-id="042af-140">If you haven't already, link a Storage account to your Batch account by using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="042af-140">If you haven't already, link a Storage account to your Batch account by using the Azure portal:</span></span>

<span data-ttu-id="042af-141">**Batch account** blade > **Settings** > **Storage Account** > **Storage Account** (None) > Select a Storage account in your subscription</span><span class="sxs-lookup"><span data-stu-id="042af-141">**Batch account** blade > **Settings** > **Storage Account** > **Storage Account** (None) > Select a Storage account in your subscription</span></span>

<span data-ttu-id="042af-142">For a more detailed walk-through on linking a Storage account, see [Application deployment with Azure Batch application packages](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="042af-142">For a more detailed walk-through on linking a Storage account, see [Application deployment with Azure Batch application packages](batch-application-packages.md).</span></span>

## <a name="persist-output"></a><span data-ttu-id="042af-143">Persist output</span><span class="sxs-lookup"><span data-stu-id="042af-143">Persist output</span></span>
<span data-ttu-id="042af-144">There are two primary actions to perform when saving job and task output with the file conventions library: create the storage container and save output to the container.</span><span class="sxs-lookup"><span data-stu-id="042af-144">There are two primary actions to perform when saving job and task output with the file conventions library: create the storage container and save output to the container.</span></span>

> [!WARNING]
> <span data-ttu-id="042af-145">Because all job and task outputs are stored in the same container, [storage throttling limits](../storage/storage-performance-checklist.md#blobs) may be enforced if a large number of tasks try to persist files at the same time.</span><span class="sxs-lookup"><span data-stu-id="042af-145">Because all job and task outputs are stored in the same container, [storage throttling limits](../storage/storage-performance-checklist.md#blobs) may be enforced if a large number of tasks try to persist files at the same time.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="042af-146">Create storage container</span><span class="sxs-lookup"><span data-stu-id="042af-146">Create storage container</span></span>
<span data-ttu-id="042af-147">Before your tasks begin persisting output to storage, you must create a blob storage container to which they'll upload their output.</span><span class="sxs-lookup"><span data-stu-id="042af-147">Before your tasks begin persisting output to storage, you must create a blob storage container to which they'll upload their output.</span></span> <span data-ttu-id="042af-148">Do this by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="042af-148">Do this by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="042af-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter, and creates a container named in such a way that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span><span class="sxs-lookup"><span data-stu-id="042af-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter, and creates a container named in such a way that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="042af-150">You typically place this code in your client application--the application that creates your pools, jobs, and tasks.</span><span class="sxs-lookup"><span data-stu-id="042af-150">You typically place this code in your client application--the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="042af-151">Store task outputs</span><span class="sxs-lookup"><span data-stu-id="042af-151">Store task outputs</span></span>
<span data-ttu-id="042af-152">Now that you've prepared a container in blob storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the file conventions library.</span><span class="sxs-lookup"><span data-stu-id="042af-152">Now that you've prepared a container in blob storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the file conventions library.</span></span>

<span data-ttu-id="042af-153">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="042af-153">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="042af-154">The "output kind" parameter categorizes the persisted files.</span><span class="sxs-lookup"><span data-stu-id="042af-154">The "output kind" parameter categorizes the persisted files.</span></span> <span data-ttu-id="042af-155">There are four predefined [TaskOutputKind][net_taskoutputkind] types: "TaskOutput", "TaskPreview", "TaskLog", and "TaskIntermediate."</span><span class="sxs-lookup"><span data-stu-id="042af-155">There are four predefined [TaskOutputKind][net_taskoutputkind] types: "TaskOutput", "TaskPreview", "TaskLog", and "TaskIntermediate."</span></span> <span data-ttu-id="042af-156">You can also define custom kinds if they would be useful in your workflow.</span><span class="sxs-lookup"><span data-stu-id="042af-156">You can also define custom kinds if they would be useful in your workflow.</span></span>

<span data-ttu-id="042af-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span><span class="sxs-lookup"><span data-stu-id="042af-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="042af-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span><span class="sxs-lookup"><span data-stu-id="042af-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="042af-159">For example, "Give me the *preview* output for task *109*."</span><span class="sxs-lookup"><span data-stu-id="042af-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="042af-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span><span class="sxs-lookup"><span data-stu-id="042af-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="042af-161">The output kind also designates where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear in "Task output files", and *TaskLog* files appear in "Task logs."</span><span class="sxs-lookup"><span data-stu-id="042af-161">The output kind also designates where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear in "Task output files", and *TaskLog* files appear in "Task logs."</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="042af-162">Store job outputs</span><span class="sxs-lookup"><span data-stu-id="042af-162">Store job outputs</span></span>
<span data-ttu-id="042af-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span><span class="sxs-lookup"><span data-stu-id="042af-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="042af-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span><span class="sxs-lookup"><span data-stu-id="042af-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="042af-165">When your job is completed, your client application can simply list and retrieve the outputs for the job, and does not need to query the individual tasks.</span><span class="sxs-lookup"><span data-stu-id="042af-165">When your job is completed, your client application can simply list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="042af-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span><span class="sxs-lookup"><span data-stu-id="042af-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```
CloudJob job = await batchClient.JobOperations.GetJobAsync(jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="042af-167">As with TaskOutputKind for task outputs, you use the [JobOutputKind][net_joboutputkind] parameter to categorize a job's persisted files.</span><span class="sxs-lookup"><span data-stu-id="042af-167">As with TaskOutputKind for task outputs, you use the [JobOutputKind][net_joboutputkind] parameter to categorize a job's persisted files.</span></span> <span data-ttu-id="042af-168">This parameter allows you to later query for (list) a specific type of output.</span><span class="sxs-lookup"><span data-stu-id="042af-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="042af-169">The JobOutputKind includes both output and preview types, and supports creating custom types.</span><span class="sxs-lookup"><span data-stu-id="042af-169">The JobOutputKind includes both output and preview types, and supports creating custom types.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="042af-170">Store task logs</span><span class="sxs-lookup"><span data-stu-id="042af-170">Store task logs</span></span>
<span data-ttu-id="042af-171">In addition to persisting a file to durable storage when a task or job completes, you might find it necessary to persist files that are updated during the execution of a task--log files or `stdout.txt` and `stderr.txt`, for example.</span><span class="sxs-lookup"><span data-stu-id="042af-171">In addition to persisting a file to durable storage when a task or job completes, you might find it necessary to persist files that are updated during the execution of a task--log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="042af-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span><span class="sxs-lookup"><span data-stu-id="042af-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="042af-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="042af-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="042af-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span><span class="sxs-lookup"><span data-stu-id="042af-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="042af-175">`Code to process data and produce output file(s)` is simply a placeholder for the code that your task would normally perform.</span><span class="sxs-lookup"><span data-stu-id="042af-175">`Code to process data and produce output file(s)` is simply a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="042af-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span><span class="sxs-lookup"><span data-stu-id="042af-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="042af-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="042af-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="042af-178">The `Task.Delay` is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node (the node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service).</span><span class="sxs-lookup"><span data-stu-id="042af-178">The `Task.Delay` is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node (the node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service).</span></span> <span data-ttu-id="042af-179">Without this delay, it is possible to miss the last few seconds of output.</span><span class="sxs-lookup"><span data-stu-id="042af-179">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="042af-180">This delay may not be required for all files.</span><span class="sxs-lookup"><span data-stu-id="042af-180">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="042af-181">When you enable file tracking with SaveTrackedAsync, only *appends* to the tracked file are persisted to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="042af-181">When you enable file tracking with SaveTrackedAsync, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="042af-182">Use this method only for tracking non-rotating log files or other files that are appended to, that is, data is only added to the end of the file when it's updated.</span><span class="sxs-lookup"><span data-stu-id="042af-182">Use this method only for tracking non-rotating log files or other files that are appended to, that is, data is only added to the end of the file when it's updated.</span></span>
> 
> 

## <a name="retrieve-output"></a><span data-ttu-id="042af-183">Retrieve output</span><span class="sxs-lookup"><span data-stu-id="042af-183">Retrieve output</span></span>
<span data-ttu-id="042af-184">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span><span class="sxs-lookup"><span data-stu-id="042af-184">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="042af-185">You can request the output for given task or job without needing to know its path in blob Storage, or even its file name.</span><span class="sxs-lookup"><span data-stu-id="042af-185">You can request the output for given task or job without needing to know its path in blob Storage, or even its file name.</span></span> <span data-ttu-id="042af-186">You can simply say, "Give me the output files for task *109*."</span><span class="sxs-lookup"><span data-stu-id="042af-186">You can simply say, "Give me the output files for task *109*."</span></span>

<span data-ttu-id="042af-187">The following code snippet iterates through all of a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span><span class="sxs-lookup"><span data-stu-id="042af-187">The following code snippet iterates through all of a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="task-outputs-and-the-azure-portal"></a><span data-ttu-id="042af-188">Task outputs and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="042af-188">Task outputs and the Azure portal</span></span>
<span data-ttu-id="042af-189">The Azure portal displays task outputs and logs that are persisted to a linked Azure Storage account using the naming conventions found in the [Azure Batch File Conventions README][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="042af-189">The Azure portal displays task outputs and logs that are persisted to a linked Azure Storage account using the naming conventions found in the [Azure Batch File Conventions README][github_file_conventions_readme].</span></span> <span data-ttu-id="042af-190">You can implement these conventions yourself in a language of your choosing, or you can use the file conventions library in your .NET applications.</span><span class="sxs-lookup"><span data-stu-id="042af-190">You can implement these conventions yourself in a language of your choosing, or you can use the file conventions library in your .NET applications.</span></span>

### <a name="enable-portal-display"></a><span data-ttu-id="042af-191">Enable portal display</span><span class="sxs-lookup"><span data-stu-id="042af-191">Enable portal display</span></span>
<span data-ttu-id="042af-192">To enable the display of your outputs in the portal, you must satisfy the following requirements:</span><span class="sxs-lookup"><span data-stu-id="042af-192">To enable the display of your outputs in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="042af-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="042af-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="042af-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span><span class="sxs-lookup"><span data-stu-id="042af-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="042af-195">You can find the definition of these conventions in the file conventions library [README][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="042af-195">You can find the definition of these conventions in the file conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="042af-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, this requirement is satisfied.</span><span class="sxs-lookup"><span data-stu-id="042af-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, this requirement is satisfied.</span></span>

### <a name="view-outputs-in-the-portal"></a><span data-ttu-id="042af-197">View outputs in the portal</span><span class="sxs-lookup"><span data-stu-id="042af-197">View outputs in the portal</span></span>
<span data-ttu-id="042af-198">To view task outputs and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span><span class="sxs-lookup"><span data-stu-id="042af-198">To view task outputs and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="042af-199">This image shows the **Saved output files** for the task with ID "007":</span><span class="sxs-lookup"><span data-stu-id="042af-199">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="042af-200">![Task outputs blade in the Azure portal][2]</span><span class="sxs-lookup"><span data-stu-id="042af-200">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="042af-201">Code sample</span><span class="sxs-lookup"><span data-stu-id="042af-201">Code sample</span></span>
<span data-ttu-id="042af-202">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="042af-202">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="042af-203">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span><span class="sxs-lookup"><span data-stu-id="042af-203">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="042af-204">To run the sample, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="042af-204">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="042af-205">Open the project in **Visual Studio 2015 or newer**.</span><span class="sxs-lookup"><span data-stu-id="042af-205">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="042af-206">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span><span class="sxs-lookup"><span data-stu-id="042af-206">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="042af-207">**Build** (but do not run) the solution.</span><span class="sxs-lookup"><span data-stu-id="042af-207">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="042af-208">Restore any NuGet packages if prompted.</span><span class="sxs-lookup"><span data-stu-id="042af-208">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="042af-209">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="042af-209">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="042af-210">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span><span class="sxs-lookup"><span data-stu-id="042af-210">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="042af-211">**Start** (run) the **PersistOutputs** project.</span><span class="sxs-lookup"><span data-stu-id="042af-211">**Start** (run) the **PersistOutputs** project.</span></span>

## <a name="next-steps"></a><span data-ttu-id="042af-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="042af-212">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="042af-213">Application deployment</span><span class="sxs-lookup"><span data-stu-id="042af-213">Application deployment</span></span>
<span data-ttu-id="042af-214">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span><span class="sxs-lookup"><span data-stu-id="042af-214">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="042af-215">Installing applications and staging data</span><span class="sxs-lookup"><span data-stu-id="042af-215">Installing applications and staging data</span></span>
<span data-ttu-id="042af-216">Check out the [Installing applications and staging data on Batch compute nodes][forum_post] post in the Azure Batch forum for an overview of the various methods of preparing your nodes for running tasks.</span><span class="sxs-lookup"><span data-stu-id="042af-216">Check out the [Installing applications and staging data on Batch compute nodes][forum_post] post in the Azure Batch forum for an overview of the various methods of preparing your nodes for running tasks.</span></span> <span data-ttu-id="042af-217">Written by one of the Azure Batch team members, this post is a good primer on the different ways to get files (including both applications and task input data) onto your compute nodes, and some special considerations for each method.</span><span class="sxs-lookup"><span data-stu-id="042af-217">Written by one of the Azure Batch team members, this post is a good primer on the different ways to get files (including both applications and task input data) onto your compute nodes, and some special considerations for each method.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-task-output/task-output-01.png "Saved output files and Saved logs selectors in portal"
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-task-output/task-output-02.png "Task outputs blade in the Azure portal"


