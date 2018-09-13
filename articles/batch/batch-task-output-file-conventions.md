---
title: Persist job and task output to Azure Storage with the File Conventions library for .NET - Azure Batch | Microsoft Docs
description: Learn how to use Azure Batch File Conventions library for .NET to persist Batch task and job output to Azure Storage, and view the persisted output in the Azure portal.
services: batch
documentationcenter: .net
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b4ff1799f77581452859d1dbc0e6e9cc47062e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966798"
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="cd538-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET</span><span class="sxs-lookup"><span data-stu-id="cd538-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="cd538-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="cd538-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="cd538-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span><span class="sxs-lookup"><span data-stu-id="cd538-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="cd538-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span><span class="sxs-lookup"><span data-stu-id="cd538-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="cd538-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span><span class="sxs-lookup"><span data-stu-id="cd538-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="cd538-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span><span class="sxs-lookup"><span data-stu-id="cd538-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="cd538-109">You don't need to know the names or locations of the files.</span><span class="sxs-lookup"><span data-stu-id="cd538-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="cd538-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span><span class="sxs-lookup"><span data-stu-id="cd538-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="cd538-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span><span class="sxs-lookup"><span data-stu-id="cd538-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="cd538-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span><span class="sxs-lookup"><span data-stu-id="cd538-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="cd538-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span><span class="sxs-lookup"><span data-stu-id="cd538-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="cd538-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="cd538-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="cd538-115">When do I use the File Conventions library to persist task output?</span><span class="sxs-lookup"><span data-stu-id="cd538-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="cd538-116">Azure Batch provides more than one way to persist task output.</span><span class="sxs-lookup"><span data-stu-id="cd538-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="cd538-117">The File Conventions is best suited to these scenarios:</span><span class="sxs-lookup"><span data-stu-id="cd538-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="cd538-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span><span class="sxs-lookup"><span data-stu-id="cd538-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="cd538-119">You want to stream data to Azure Storage while the task is still running.</span><span class="sxs-lookup"><span data-stu-id="cd538-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="cd538-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span><span class="sxs-lookup"><span data-stu-id="cd538-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="cd538-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span><span class="sxs-lookup"><span data-stu-id="cd538-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="cd538-122">You want to view task output in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd538-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="cd538-123">If your scenario differs from those listed above, you may need to consider a different approach.</span><span class="sxs-lookup"><span data-stu-id="cd538-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="cd538-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="cd538-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="cd538-125">What is the Batch File Conventions standard?</span><span class="sxs-lookup"><span data-stu-id="cd538-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="cd538-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span><span class="sxs-lookup"><span data-stu-id="cd538-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="cd538-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd538-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="cd538-128">The portal is aware of the naming convention and so can display files that adhere to it.</span><span class="sxs-lookup"><span data-stu-id="cd538-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="cd538-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span><span class="sxs-lookup"><span data-stu-id="cd538-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="cd538-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span><span class="sxs-lookup"><span data-stu-id="cd538-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="cd538-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span><span class="sxs-lookup"><span data-stu-id="cd538-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="cd538-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="cd538-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="cd538-133">Link an Azure Storage account to your Batch account</span><span class="sxs-lookup"><span data-stu-id="cd538-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="cd538-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="cd538-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="cd538-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="cd538-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="cd538-136">Navigate to your Batch account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd538-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="cd538-137">Under **Settings**, select **Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="cd538-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="cd538-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span><span class="sxs-lookup"><span data-stu-id="cd538-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="cd538-139">Select a Storage account from the list for your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd538-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="cd538-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span><span class="sxs-lookup"><span data-stu-id="cd538-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="cd538-141">Persist output data</span><span class="sxs-lookup"><span data-stu-id="cd538-141">Persist output data</span></span>

<span data-ttu-id="cd538-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span><span class="sxs-lookup"><span data-stu-id="cd538-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="cd538-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span><span class="sxs-lookup"><span data-stu-id="cd538-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="cd538-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="cd538-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="cd538-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span><span class="sxs-lookup"><span data-stu-id="cd538-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="cd538-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span><span class="sxs-lookup"><span data-stu-id="cd538-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="cd538-147">Create storage container</span><span class="sxs-lookup"><span data-stu-id="cd538-147">Create storage container</span></span>

<span data-ttu-id="cd538-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="cd538-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="cd538-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span><span class="sxs-lookup"><span data-stu-id="cd538-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="cd538-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span><span class="sxs-lookup"><span data-stu-id="cd538-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="cd538-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span><span class="sxs-lookup"><span data-stu-id="cd538-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

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

### <a name="store-task-outputs"></a><span data-ttu-id="cd538-152">Store task outputs</span><span class="sxs-lookup"><span data-stu-id="cd538-152">Store task outputs</span></span>

<span data-ttu-id="cd538-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span><span class="sxs-lookup"><span data-stu-id="cd538-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="cd538-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cd538-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

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

<span data-ttu-id="cd538-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span><span class="sxs-lookup"><span data-stu-id="cd538-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="cd538-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span><span class="sxs-lookup"><span data-stu-id="cd538-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="cd538-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span><span class="sxs-lookup"><span data-stu-id="cd538-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="cd538-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span><span class="sxs-lookup"><span data-stu-id="cd538-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="cd538-159">For example, "Give me the *preview* output for task *109*."</span><span class="sxs-lookup"><span data-stu-id="cd538-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="cd538-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span><span class="sxs-lookup"><span data-stu-id="cd538-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="cd538-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span><span class="sxs-lookup"><span data-stu-id="cd538-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="cd538-162">Store job outputs</span><span class="sxs-lookup"><span data-stu-id="cd538-162">Store job outputs</span></span>

<span data-ttu-id="cd538-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span><span class="sxs-lookup"><span data-stu-id="cd538-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="cd538-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span><span class="sxs-lookup"><span data-stu-id="cd538-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="cd538-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span><span class="sxs-lookup"><span data-stu-id="cd538-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="cd538-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span><span class="sxs-lookup"><span data-stu-id="cd538-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="cd538-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span><span class="sxs-lookup"><span data-stu-id="cd538-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="cd538-168">This parameter allows you to later query for (list) a specific type of output.</span><span class="sxs-lookup"><span data-stu-id="cd538-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="cd538-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span><span class="sxs-lookup"><span data-stu-id="cd538-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="cd538-170">Store task logs</span><span class="sxs-lookup"><span data-stu-id="cd538-170">Store task logs</span></span>

<span data-ttu-id="cd538-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span><span class="sxs-lookup"><span data-stu-id="cd538-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="cd538-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span><span class="sxs-lookup"><span data-stu-id="cd538-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="cd538-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cd538-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="cd538-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span><span class="sxs-lookup"><span data-stu-id="cd538-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

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

<span data-ttu-id="cd538-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span><span class="sxs-lookup"><span data-stu-id="cd538-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="cd538-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span><span class="sxs-lookup"><span data-stu-id="cd538-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="cd538-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="cd538-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="cd538-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span><span class="sxs-lookup"><span data-stu-id="cd538-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="cd538-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span><span class="sxs-lookup"><span data-stu-id="cd538-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="cd538-180">Without this delay, it is possible to miss the last few seconds of output.</span><span class="sxs-lookup"><span data-stu-id="cd538-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="cd538-181">This delay may not be required for all files.</span><span class="sxs-lookup"><span data-stu-id="cd538-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="cd538-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cd538-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="cd538-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span><span class="sxs-lookup"><span data-stu-id="cd538-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="cd538-184">Retrieve output data</span><span class="sxs-lookup"><span data-stu-id="cd538-184">Retrieve output data</span></span>

<span data-ttu-id="cd538-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span><span class="sxs-lookup"><span data-stu-id="cd538-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="cd538-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span><span class="sxs-lookup"><span data-stu-id="cd538-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="cd538-187">Instead, you can request output files by task or job ID.</span><span class="sxs-lookup"><span data-stu-id="cd538-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="cd538-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span><span class="sxs-lookup"><span data-stu-id="cd538-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="cd538-189">View output files in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cd538-189">View output files in the Azure portal</span></span>

<span data-ttu-id="cd538-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="cd538-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="cd538-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span><span class="sxs-lookup"><span data-stu-id="cd538-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="cd538-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span><span class="sxs-lookup"><span data-stu-id="cd538-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="cd538-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="cd538-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="cd538-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span><span class="sxs-lookup"><span data-stu-id="cd538-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="cd538-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="cd538-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="cd538-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span><span class="sxs-lookup"><span data-stu-id="cd538-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="cd538-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span><span class="sxs-lookup"><span data-stu-id="cd538-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="cd538-198">This image shows the **Saved output files** for the task with ID "007":</span><span class="sxs-lookup"><span data-stu-id="cd538-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="cd538-199">![Task outputs blade in the Azure portal][2]</span><span class="sxs-lookup"><span data-stu-id="cd538-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="cd538-200">Code sample</span><span class="sxs-lookup"><span data-stu-id="cd538-200">Code sample</span></span>

<span data-ttu-id="cd538-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="cd538-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="cd538-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span><span class="sxs-lookup"><span data-stu-id="cd538-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="cd538-203">To run the sample, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="cd538-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="cd538-204">Open the project in **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="cd538-204">Open the project in **Visual Studio 2017**.</span></span>
2. <span data-ttu-id="cd538-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span><span class="sxs-lookup"><span data-stu-id="cd538-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="cd538-206">**Build** (but do not run) the solution.</span><span class="sxs-lookup"><span data-stu-id="cd538-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="cd538-207">Restore any NuGet packages if prompted.</span><span class="sxs-lookup"><span data-stu-id="cd538-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="cd538-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="cd538-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="cd538-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span><span class="sxs-lookup"><span data-stu-id="cd538-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="cd538-210">**Start** (run) the **PersistOutputs** project.</span><span class="sxs-lookup"><span data-stu-id="cd538-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="cd538-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span><span class="sxs-lookup"><span data-stu-id="cd538-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cd538-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd538-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="cd538-213">Get the Batch File Conventions library for .NET</span><span class="sxs-lookup"><span data-stu-id="cd538-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="cd538-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="cd538-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="cd538-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span><span class="sxs-lookup"><span data-stu-id="cd538-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="cd538-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span><span class="sxs-lookup"><span data-stu-id="cd538-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="cd538-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span><span class="sxs-lookup"><span data-stu-id="cd538-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="cd538-218">Explore other approaches for persisting output data</span><span class="sxs-lookup"><span data-stu-id="cd538-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="cd538-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span><span class="sxs-lookup"><span data-stu-id="cd538-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="cd538-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span><span class="sxs-lookup"><span data-stu-id="cd538-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

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

[1]: ./media/batch-task-output/task-output-01.png "Saved output files and Saved logs selectors in portal"
[2]: ./media/batch-task-output/task-output-02.png "Task outputs blade in the Azure portal"
