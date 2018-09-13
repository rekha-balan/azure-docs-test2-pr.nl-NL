---
title: Azure Quickstart - Run Batch job - .NET
description: Quickly run a Batch job and tasks with the Batch .NET client library.
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 09/06/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d896e0b7c5a270e690adbf929375e56b8599de63
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857353"
---
# <a name="quickstart-run-your-first-azure-batch-job-with-the-net-api"></a><span data-ttu-id="2485a-103">Quickstart: Run your first Azure Batch job with the .NET API</span><span class="sxs-lookup"><span data-stu-id="2485a-103">Quickstart: Run your first Azure Batch job with the .NET API</span></span>

<span data-ttu-id="2485a-104">This quickstart runs an Azure Batch job from a C# application built on the Azure Batch .NET API.</span><span class="sxs-lookup"><span data-stu-id="2485a-104">This quickstart runs an Azure Batch job from a C# application built on the Azure Batch .NET API.</span></span> <span data-ttu-id="2485a-105">The app uploads several input data files to Azure storage and then creates a *pool* of Batch compute nodes (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="2485a-105">The app uploads several input data files to Azure storage and then creates a *pool* of Batch compute nodes (virtual machines).</span></span> <span data-ttu-id="2485a-106">Then, it creates a sample *job* that runs *tasks* to process each input file on the pool using a basic command.</span><span class="sxs-lookup"><span data-stu-id="2485a-106">Then, it creates a sample *job* that runs *tasks* to process each input file on the pool using a basic command.</span></span> <span data-ttu-id="2485a-107">After completing this quickstart, you will understand the key concepts of the Batch service and be ready to try Batch with more realistic workloads at larger scale.</span><span class="sxs-lookup"><span data-stu-id="2485a-107">After completing this quickstart, you will understand the key concepts of the Batch service and be ready to try Batch with more realistic workloads at larger scale.</span></span>

![Quickstart app workflow](./media/quick-run-dotnet/sampleapp.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="2485a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2485a-109">Prerequisites</span></span>

* <span data-ttu-id="2485a-110">[Visual Studio 2017](https://www.visualstudio.com/vs), or [.NET Core 2.1](https://www.microsoft.com/net/download/dotnet-core/2.1) for Linux, macOS, or Windows.</span><span class="sxs-lookup"><span data-stu-id="2485a-110">[Visual Studio 2017](https://www.visualstudio.com/vs), or [.NET Core 2.1](https://www.microsoft.com/net/download/dotnet-core/2.1) for Linux, macOS, or Windows.</span></span> 

* <span data-ttu-id="2485a-111">A Batch account and a linked Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="2485a-111">A Batch account and a linked Azure Storage account.</span></span> <span data-ttu-id="2485a-112">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2485a-112">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span></span> 

## <a name="sign-in-to-azure"></a><span data-ttu-id="2485a-113">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="2485a-113">Sign in to Azure</span></span>

<span data-ttu-id="2485a-114">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2485a-114">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

[!INCLUDE [batch-common-credentials](../../includes/batch-common-credentials.md)]

## <a name="download-the-sample"></a><span data-ttu-id="2485a-115">Download the sample</span><span class="sxs-lookup"><span data-stu-id="2485a-115">Download the sample</span></span>

<span data-ttu-id="2485a-116">[Download or clone the sample app](https://github.com/Azure-Samples/batch-dotnet-quickstart) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="2485a-116">[Download or clone the sample app](https://github.com/Azure-Samples/batch-dotnet-quickstart) from GitHub.</span></span> <span data-ttu-id="2485a-117">To clone the sample app repo with a Git client, use the following command:</span><span class="sxs-lookup"><span data-stu-id="2485a-117">To clone the sample app repo with a Git client, use the following command:</span></span>

```
git clone https://github.com/Azure-Samples/batch-dotnet-quickstart.git
```

<span data-ttu-id="2485a-118">Navigate to the directory that contains the Visual Studio solution file `BatchDotNetQuickstart.sln`.</span><span class="sxs-lookup"><span data-stu-id="2485a-118">Navigate to the directory that contains the Visual Studio solution file `BatchDotNetQuickstart.sln`.</span></span>

<span data-ttu-id="2485a-119">Open the solution file in Visual Studio, and update the credential strings in `program.cs` with the values you obtained for your accounts.</span><span class="sxs-lookup"><span data-stu-id="2485a-119">Open the solution file in Visual Studio, and update the credential strings in `program.cs` with the values you obtained for your accounts.</span></span> <span data-ttu-id="2485a-120">For example:</span><span class="sxs-lookup"><span data-stu-id="2485a-120">For example:</span></span>

```csharp
// Batch account credentials
private const string BatchAccountName = "mybatchaccount";
private const string BatchAccountKey  = "xxxxxxxxxxxxxxxxE+yXrRvJAqT9BlXwwo1CwF+SwAYOxxxxxxxxxxxxxxxx43pXi/gdiATkvbpLRl3x14pcEQ==";
private const string BatchAccountUrl  = "https://mybatchaccount.mybatchregion.batch.azure.com";

// Storage account credentials
private const string StorageAccountName = "mystorageaccount";
private const string StorageAccountKey  = "xxxxxxxxxxxxxxxxy4/xxxxxxxxxxxxxxxxfwpbIC5aAWA8wDu+AFXZB827Mt9lybZB1nUcQbQiUrkPtilK5BQ==";
```

## <a name="build-and-run-the-app"></a><span data-ttu-id="2485a-121">Build and run the app</span><span class="sxs-lookup"><span data-stu-id="2485a-121">Build and run the app</span></span>

<span data-ttu-id="2485a-122">To see the Batch workflow in action, build and run the application in Visual Studio, or at the command line with the `dotnet build` and `dotnet run` commands.</span><span class="sxs-lookup"><span data-stu-id="2485a-122">To see the Batch workflow in action, build and run the application in Visual Studio, or at the command line with the `dotnet build` and `dotnet run` commands.</span></span> <span data-ttu-id="2485a-123">After running the application, review the code to learn what each part of the application does.</span><span class="sxs-lookup"><span data-stu-id="2485a-123">After running the application, review the code to learn what each part of the application does.</span></span> <span data-ttu-id="2485a-124">For example, in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2485a-124">For example, in Visual Studio:</span></span>

* <span data-ttu-id="2485a-125">Right-click the solution in Solution Explorer, and click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="2485a-125">Right-click the solution in Solution Explorer, and click **Build Solution**.</span></span> 

* <span data-ttu-id="2485a-126">Confirm the restoration of any NuGet packages, if you're prompted.</span><span class="sxs-lookup"><span data-stu-id="2485a-126">Confirm the restoration of any NuGet packages, if you're prompted.</span></span> <span data-ttu-id="2485a-127">If you need to download missing packages, ensure the [NuGet Package Manager](https://docs.nuget.org/consume/installing-nuget) is installed.</span><span class="sxs-lookup"><span data-stu-id="2485a-127">If you need to download missing packages, ensure the [NuGet Package Manager](https://docs.nuget.org/consume/installing-nuget) is installed.</span></span>

<span data-ttu-id="2485a-128">Then run it.</span><span class="sxs-lookup"><span data-stu-id="2485a-128">Then run it.</span></span> <span data-ttu-id="2485a-129">When you run the sample application, the console output is similar to the following.</span><span class="sxs-lookup"><span data-stu-id="2485a-129">When you run the sample application, the console output is similar to the following.</span></span> <span data-ttu-id="2485a-130">During execution, you experience a pause at `Monitoring all tasks for 'Completed' state, timeout in 00:30:00...` while the pool's compute nodes are started.</span><span class="sxs-lookup"><span data-stu-id="2485a-130">During execution, you experience a pause at `Monitoring all tasks for 'Completed' state, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="2485a-131">Tasks are queued to run as soon as the first compute node is running.</span><span class="sxs-lookup"><span data-stu-id="2485a-131">Tasks are queued to run as soon as the first compute node is running.</span></span> <span data-ttu-id="2485a-132">Go to your Batch account in the [Azure portal](https://portal.azure.com) to monitor the pool, compute nodes, job, and tasks.</span><span class="sxs-lookup"><span data-stu-id="2485a-132">Go to your Batch account in the [Azure portal](https://portal.azure.com) to monitor the pool, compute nodes, job, and tasks.</span></span>

```
Sample start: 12/4/2017 4:02:54 PM

Container [input] created.
Uploading file taskdata0.txt to container [input]...
Uploading file taskdata1.txt to container [input]...
Uploading file taskdata2.txt to container [input]...
Creating pool [DotNetQuickstartPool]...
Creating job [DotNetQuickstartJob]...
Adding 3 tasks to job [DotNetQuickstartJob]...
Monitoring all tasks for 'Completed' state, timeout in 00:30:00...
```

<span data-ttu-id="2485a-133">After tasks complete, you see output similar to the following for each task:</span><span class="sxs-lookup"><span data-stu-id="2485a-133">After tasks complete, you see output similar to the following for each task:</span></span>

```
Printing task output.
Task: Task0
Node: tvm-2850684224_3-20171205t000401z
Standard out:
Batch processing began with mainframe computers and punch cards. Today it still plays a central role in business, engineering, science, and other pursuits that require running lots of automated tasks....
stderr:
...
```

<span data-ttu-id="2485a-134">Typical execution time is approximately 5 minutes when you run the application in its default configuration.</span><span class="sxs-lookup"><span data-stu-id="2485a-134">Typical execution time is approximately 5 minutes when you run the application in its default configuration.</span></span> <span data-ttu-id="2485a-135">Initial pool setup takes the most time.</span><span class="sxs-lookup"><span data-stu-id="2485a-135">Initial pool setup takes the most time.</span></span> <span data-ttu-id="2485a-136">To run the job again, delete the job from the previous run and do not delete the pool.</span><span class="sxs-lookup"><span data-stu-id="2485a-136">To run the job again, delete the job from the previous run and do not delete the pool.</span></span> <span data-ttu-id="2485a-137">On a preconfigured pool, the job completes in a few seconds.</span><span class="sxs-lookup"><span data-stu-id="2485a-137">On a preconfigured pool, the job completes in a few seconds.</span></span>


## <a name="review-the-code"></a><span data-ttu-id="2485a-138">Review the code</span><span class="sxs-lookup"><span data-stu-id="2485a-138">Review the code</span></span>

<span data-ttu-id="2485a-139">The .NET app in this quickstart does the following:</span><span class="sxs-lookup"><span data-stu-id="2485a-139">The .NET app in this quickstart does the following:</span></span>

* <span data-ttu-id="2485a-140">Uploads three small text files to a blob container in your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="2485a-140">Uploads three small text files to a blob container in your Azure storage account.</span></span> <span data-ttu-id="2485a-141">These files are inputs for processing by Batch.</span><span class="sxs-lookup"><span data-stu-id="2485a-141">These files are inputs for processing by Batch.</span></span>
* <span data-ttu-id="2485a-142">Creates a pool of compute nodes running Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2485a-142">Creates a pool of compute nodes running Windows Server.</span></span>
* <span data-ttu-id="2485a-143">Creates a job and three tasks to run on the nodes.</span><span class="sxs-lookup"><span data-stu-id="2485a-143">Creates a job and three tasks to run on the nodes.</span></span> <span data-ttu-id="2485a-144">Each task processes one of the input files using a Windows command line.</span><span class="sxs-lookup"><span data-stu-id="2485a-144">Each task processes one of the input files using a Windows command line.</span></span> 
* <span data-ttu-id="2485a-145">Displays files returned by the tasks.</span><span class="sxs-lookup"><span data-stu-id="2485a-145">Displays files returned by the tasks.</span></span>

<span data-ttu-id="2485a-146">See the file `Program.cs` and the following sections for details.</span><span class="sxs-lookup"><span data-stu-id="2485a-146">See the file `Program.cs` and the following sections for details.</span></span> 

### <a name="preliminaries"></a><span data-ttu-id="2485a-147">Preliminaries</span><span class="sxs-lookup"><span data-stu-id="2485a-147">Preliminaries</span></span>

<span data-ttu-id="2485a-148">To interact with a storage account, the app uses the Azure Storage Client Library for .NET.</span><span class="sxs-lookup"><span data-stu-id="2485a-148">To interact with a storage account, the app uses the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="2485a-149">It creates a reference to the account with [CloudStorageAccount](/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount), and from that creates a [CloudBlobClient](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobclient).</span><span class="sxs-lookup"><span data-stu-id="2485a-149">It creates a reference to the account with [CloudStorageAccount](/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount), and from that creates a [CloudBlobClient](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobclient).</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="2485a-150">The app uses the `blobClient` reference to create a container in the storage account and to upload data files to the container.</span><span class="sxs-lookup"><span data-stu-id="2485a-150">The app uses the `blobClient` reference to create a container in the storage account and to upload data files to the container.</span></span> <span data-ttu-id="2485a-151">The files in storage are defined as Batch [ResourceFile](/dotnet/api/microsoft.azure.batch.resourcefile) objects that Batch can later download to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="2485a-151">The files in storage are defined as Batch [ResourceFile](/dotnet/api/microsoft.azure.batch.resourcefile) objects that Batch can later download to compute nodes.</span></span>

```csharp
List<string> inputFilePaths = new List<string>
{
    "taskdata0.txt",
    "taskdata1.txt",
    "taskdata2.txt"
};

List<ResourceFile> inputFiles = new List<ResourceFile>();

foreach (string filePath in inputFilePaths)
{
    inputFiles.Add(UploadFileToContainer(blobClient, inputContainerName, filePath));
}
```

<span data-ttu-id="2485a-152">The app creates a [BatchClient](/dotnet/api/microsoft.azure.batch.batchclient) object to create and manage pools, jobs, and tasks in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="2485a-152">The app creates a [BatchClient](/dotnet/api/microsoft.azure.batch.batchclient) object to create and manage pools, jobs, and tasks in the Batch service.</span></span> <span data-ttu-id="2485a-153">The Batch client in the sample uses shared key authentication.</span><span class="sxs-lookup"><span data-stu-id="2485a-153">The Batch client in the sample uses shared key authentication.</span></span> <span data-ttu-id="2485a-154">(Batch also supports Azure Active Directory authentication.)</span><span class="sxs-lookup"><span data-stu-id="2485a-154">(Batch also supports Azure Active Directory authentication.)</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(BatchAccountUrl, BatchAccountName, BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
...    
```

### <a name="create-a-pool-of-compute-nodes"></a><span data-ttu-id="2485a-155">Create a pool of compute nodes</span><span class="sxs-lookup"><span data-stu-id="2485a-155">Create a pool of compute nodes</span></span>

<span data-ttu-id="2485a-156">To create a Batch pool, the app uses the [BatchClient.PoolOperations.CreatePool](/dotnet/api/microsoft.azure.batch.pooloperations.createpool) method to set the number of nodes, VM size, and a pool configuration.</span><span class="sxs-lookup"><span data-stu-id="2485a-156">To create a Batch pool, the app uses the [BatchClient.PoolOperations.CreatePool](/dotnet/api/microsoft.azure.batch.pooloperations.createpool) method to set the number of nodes, VM size, and a pool configuration.</span></span> <span data-ttu-id="2485a-157">Here, a [VirtualMachineConfiguration](/dotnet/api/microsoft.azure.batch.virtualmachineconfiguration) object specifies an [ImageReference](/dotnet/api/microsoft.azure.batch.imagereference) to a Windows Server image published in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2485a-157">Here, a [VirtualMachineConfiguration](/dotnet/api/microsoft.azure.batch.virtualmachineconfiguration) object specifies an [ImageReference](/dotnet/api/microsoft.azure.batch.imagereference) to a Windows Server image published in the Azure Marketplace.</span></span> <span data-ttu-id="2485a-158">Batch supports a wide range of Linux and Windows Server images in the Azure Marketplace, as well as custom VM images.</span><span class="sxs-lookup"><span data-stu-id="2485a-158">Batch supports a wide range of Linux and Windows Server images in the Azure Marketplace, as well as custom VM images.</span></span>

<span data-ttu-id="2485a-159">The number of nodes (`PoolNodeCount`) and VM size (`PoolVMSize`) are defined constants.</span><span class="sxs-lookup"><span data-stu-id="2485a-159">The number of nodes (`PoolNodeCount`) and VM size (`PoolVMSize`) are defined constants.</span></span> <span data-ttu-id="2485a-160">The sample by default creates a pool of 2 size *Standard_A1_v2* nodes.</span><span class="sxs-lookup"><span data-stu-id="2485a-160">The sample by default creates a pool of 2 size *Standard_A1_v2* nodes.</span></span> <span data-ttu-id="2485a-161">The size suggested offers a good balance of performance versus cost for this quick example.</span><span class="sxs-lookup"><span data-stu-id="2485a-161">The size suggested offers a good balance of performance versus cost for this quick example.</span></span> 

<span data-ttu-id="2485a-162">The [Commit](/dotnet/api/microsoft.azure.batch.cloudpool.commit) method submits the pool to the Batch service.</span><span class="sxs-lookup"><span data-stu-id="2485a-162">The [Commit](/dotnet/api/microsoft.azure.batch.cloudpool.commit) method submits the pool to the Batch service.</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "MicrosoftWindowsServer",
    offer: "WindowsServer",
    sku: "2012-R2-Datacenter-smalldisk",
    version: "latest");

VirtualMachineConfiguration virtualMachineConfiguration =
new VirtualMachineConfiguration(
   imageReference: imageReference,
   nodeAgentSkuId: "batch.node.windows amd64");

try
{
    CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: PoolId,
    targetDedicatedComputeNodes: PoolNodeCount,
    virtualMachineSize: PoolVMSize,
    virtualMachineConfiguration: virtualMachineConfiguration);

    pool.Commit();
}
...

```
### <a name="create-a-batch-job"></a><span data-ttu-id="2485a-163">Create a Batch job</span><span class="sxs-lookup"><span data-stu-id="2485a-163">Create a Batch job</span></span>

<span data-ttu-id="2485a-164">A Batch job is a logical grouping of one or more tasks.</span><span class="sxs-lookup"><span data-stu-id="2485a-164">A Batch job is a logical grouping of one or more tasks.</span></span> <span data-ttu-id="2485a-165">A job includes settings common to the tasks, such as priority and the pool to run tasks on.</span><span class="sxs-lookup"><span data-stu-id="2485a-165">A job includes settings common to the tasks, such as priority and the pool to run tasks on.</span></span> <span data-ttu-id="2485a-166">The app uses the [BatchClient.JobOperations.CreateJob](/dotnet/api/microsoft.azure.batch.joboperations.createjob) method to create a job on your pool.</span><span class="sxs-lookup"><span data-stu-id="2485a-166">The app uses the [BatchClient.JobOperations.CreateJob](/dotnet/api/microsoft.azure.batch.joboperations.createjob) method to create a job on your pool.</span></span> 

<span data-ttu-id="2485a-167">The [Commit](/dotnet/api/microsoft.azure.batch.cloudjob.commit) method submits the job to the Batch service.</span><span class="sxs-lookup"><span data-stu-id="2485a-167">The [Commit](/dotnet/api/microsoft.azure.batch.cloudjob.commit) method submits the job to the Batch service.</span></span> <span data-ttu-id="2485a-168">Initially the job has no tasks.</span><span class="sxs-lookup"><span data-stu-id="2485a-168">Initially the job has no tasks.</span></span>

```csharp
try
{
    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = JobId;
    job.PoolInformation = new PoolInformation { PoolId = PoolId };

    job.Commit(); 
}
...
```

### <a name="create-tasks"></a><span data-ttu-id="2485a-169">Create tasks</span><span class="sxs-lookup"><span data-stu-id="2485a-169">Create tasks</span></span>
<span data-ttu-id="2485a-170">The app creates a list of [CloudTask](/dotnet/api/microsoft.azure.batch.cloudtask) objects.</span><span class="sxs-lookup"><span data-stu-id="2485a-170">The app creates a list of [CloudTask](/dotnet/api/microsoft.azure.batch.cloudtask) objects.</span></span> <span data-ttu-id="2485a-171">Each task processes an input `ResourceFile` object using a [CommandLine](/dotnet/api/microsoft.azure.batch.cloudtask.commandline) property.</span><span class="sxs-lookup"><span data-stu-id="2485a-171">Each task processes an input `ResourceFile` object using a [CommandLine](/dotnet/api/microsoft.azure.batch.cloudtask.commandline) property.</span></span> <span data-ttu-id="2485a-172">In the sample, the command line runs the Windows `type` command to display the input file.</span><span class="sxs-lookup"><span data-stu-id="2485a-172">In the sample, the command line runs the Windows `type` command to display the input file.</span></span> <span data-ttu-id="2485a-173">This command is a simple example for demonstration purposes.</span><span class="sxs-lookup"><span data-stu-id="2485a-173">This command is a simple example for demonstration purposes.</span></span> <span data-ttu-id="2485a-174">When you use Batch, the command line is where you specify your app or script.</span><span class="sxs-lookup"><span data-stu-id="2485a-174">When you use Batch, the command line is where you specify your app or script.</span></span> <span data-ttu-id="2485a-175">Batch provides a number of ways to deploy apps and scripts to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="2485a-175">Batch provides a number of ways to deploy apps and scripts to compute nodes.</span></span>

<span data-ttu-id="2485a-176">Then, the app adds tasks to the job with the [AddTask](/dotnet/api/microsoft.azure.batch.joboperations.addtask) method, which queues them to run on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="2485a-176">Then, the app adds tasks to the job with the [AddTask](/dotnet/api/microsoft.azure.batch.joboperations.addtask) method, which queues them to run on the compute nodes.</span></span> 

```csharp
for (int i = 0; i < inputFiles.Count; i++)
{
    string taskId = String.Format("Task{0}", i);
    string inputFilename = inputFiles[i].FilePath;
    string taskCommandLine = String.Format("cmd /c type {0}", inputFilename);

    CloudTask task = new CloudTask(taskId, taskCommandLine);
    task.ResourceFiles = new List<ResourceFile> { inputFiles[i] };
    tasks.Add(task);
}

batchClient.JobOperations.AddTask(JobId, tasks);
```
 
### <a name="view-task-output"></a><span data-ttu-id="2485a-177">View task output</span><span class="sxs-lookup"><span data-stu-id="2485a-177">View task output</span></span>

<span data-ttu-id="2485a-178">The app creates a [TaskStateMonitor](/dotnet/api/microsoft.azure.batch.taskstatemonitor) to monitor the tasks to make sure they complete.</span><span class="sxs-lookup"><span data-stu-id="2485a-178">The app creates a [TaskStateMonitor](/dotnet/api/microsoft.azure.batch.taskstatemonitor) to monitor the tasks to make sure they complete.</span></span> <span data-ttu-id="2485a-179">Then, the app uses the [CloudTask.ComputeNodeInformation](/dotnet/api/microsoft.azure.batch.cloudtask.computenodeinformation) property to display the `stdout.txt` file generated by each completed task.</span><span class="sxs-lookup"><span data-stu-id="2485a-179">Then, the app uses the [CloudTask.ComputeNodeInformation](/dotnet/api/microsoft.azure.batch.cloudtask.computenodeinformation) property to display the `stdout.txt` file generated by each completed task.</span></span> <span data-ttu-id="2485a-180">When the task runs successfully, the output of the task command is written to `stdout.txt`:</span><span class="sxs-lookup"><span data-stu-id="2485a-180">When the task runs successfully, the output of the task command is written to `stdout.txt`:</span></span>

```csharp
foreach (CloudTask task in completedtasks)
{
    string nodeId = String.Format(task.ComputeNodeInformation.ComputeNodeId);
    Console.WriteLine("Task: {0}", task.Id);
    Console.WriteLine("Node: {0}", nodeId);
    Console.WriteLine("Standard out:");
    Console.WriteLine(task.GetNodeFile(Constants.StandardOutFileName).ReadAsString());
}
```

## <a name="clean-up-resources"></a><span data-ttu-id="2485a-181">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2485a-181">Clean up resources</span></span>

<span data-ttu-id="2485a-182">The app automatically deletes the storage container it creates, and gives you the option to delete the Batch pool and job.</span><span class="sxs-lookup"><span data-stu-id="2485a-182">The app automatically deletes the storage container it creates, and gives you the option to delete the Batch pool and job.</span></span> <span data-ttu-id="2485a-183">You are charged for the pool while the nodes are running, even if no jobs are scheduled.</span><span class="sxs-lookup"><span data-stu-id="2485a-183">You are charged for the pool while the nodes are running, even if no jobs are scheduled.</span></span> <span data-ttu-id="2485a-184">When you no longer need the pool, delete it.</span><span class="sxs-lookup"><span data-stu-id="2485a-184">When you no longer need the pool, delete it.</span></span> <span data-ttu-id="2485a-185">When you delete the pool, all task output on the nodes is deleted.</span><span class="sxs-lookup"><span data-stu-id="2485a-185">When you delete the pool, all task output on the nodes is deleted.</span></span>

<span data-ttu-id="2485a-186">When no longer needed, delete the resource group, Batch account, and storage account.</span><span class="sxs-lookup"><span data-stu-id="2485a-186">When no longer needed, delete the resource group, Batch account, and storage account.</span></span> <span data-ttu-id="2485a-187">To do so in the Azure portal, select the resource group for the Batch account and click **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="2485a-187">To do so in the Azure portal, select the resource group for the Batch account and click **Delete resource group**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2485a-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="2485a-188">Next steps</span></span>

<span data-ttu-id="2485a-189">In this quickstart, you ran a small app built using the Batch .NET API to create a Batch pool and a Batch job.</span><span class="sxs-lookup"><span data-stu-id="2485a-189">In this quickstart, you ran a small app built using the Batch .NET API to create a Batch pool and a Batch job.</span></span> <span data-ttu-id="2485a-190">The job ran sample tasks, and downloaded output created on the nodes.</span><span class="sxs-lookup"><span data-stu-id="2485a-190">The job ran sample tasks, and downloaded output created on the nodes.</span></span> <span data-ttu-id="2485a-191">Now that you understand the key concepts of the Batch service, you are ready to try Batch with more realistic workloads at larger scale.</span><span class="sxs-lookup"><span data-stu-id="2485a-191">Now that you understand the key concepts of the Batch service, you are ready to try Batch with more realistic workloads at larger scale.</span></span> <span data-ttu-id="2485a-192">To learn more about Azure Batch, and walk through a parallel workload with a real-world application, continue to the Batch .NET tutorial.</span><span class="sxs-lookup"><span data-stu-id="2485a-192">To learn more about Azure Batch, and walk through a parallel workload with a real-world application, continue to the Batch .NET tutorial.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="2485a-193">Process a parallel workload with .NET</span><span class="sxs-lookup"><span data-stu-id="2485a-193">Process a parallel workload with .NET</span></span>](tutorial-parallel-dotnet.md)
