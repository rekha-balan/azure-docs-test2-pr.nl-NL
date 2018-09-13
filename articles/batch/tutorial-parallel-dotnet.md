---
title: Run a parallel workload - Azure Batch .NET
description: Tutorial - Transcode media files in parallel with ffmpeg in Azure Batch using the Batch .NET client library
services: batch
author: dlepow
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 09/07/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 15b0b41e2727ab8ce4f2e81745b76508e671618a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864518"
---
# <a name="tutorial-run-a-parallel-workload-with-azure-batch-using-the-net-api"></a><span data-ttu-id="2f168-103">Tutorial: Run a parallel workload with Azure Batch using the .NET API</span><span class="sxs-lookup"><span data-stu-id="2f168-103">Tutorial: Run a parallel workload with Azure Batch using the .NET API</span></span>

<span data-ttu-id="2f168-104">Use Azure Batch to run large-scale parallel and high-performance computing (HPC) batch jobs efficiently in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f168-104">Use Azure Batch to run large-scale parallel and high-performance computing (HPC) batch jobs efficiently in Azure.</span></span> <span data-ttu-id="2f168-105">This tutorial walks through a C# example of running a parallel workload using Batch.</span><span class="sxs-lookup"><span data-stu-id="2f168-105">This tutorial walks through a C# example of running a parallel workload using Batch.</span></span> <span data-ttu-id="2f168-106">You learn a common Batch application workflow and how to interact programmatically with Batch and Storage resources.</span><span class="sxs-lookup"><span data-stu-id="2f168-106">You learn a common Batch application workflow and how to interact programmatically with Batch and Storage resources.</span></span> <span data-ttu-id="2f168-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="2f168-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2f168-108">Add an application package to your Batch account</span><span class="sxs-lookup"><span data-stu-id="2f168-108">Add an application package to your Batch account</span></span>
> * <span data-ttu-id="2f168-109">Authenticate with Batch and Storage accounts</span><span class="sxs-lookup"><span data-stu-id="2f168-109">Authenticate with Batch and Storage accounts</span></span>
> * <span data-ttu-id="2f168-110">Upload input files to Storage</span><span class="sxs-lookup"><span data-stu-id="2f168-110">Upload input files to Storage</span></span>
> * <span data-ttu-id="2f168-111">Create a pool of compute nodes to run an application</span><span class="sxs-lookup"><span data-stu-id="2f168-111">Create a pool of compute nodes to run an application</span></span>
> * <span data-ttu-id="2f168-112">Create a job and tasks to process input files</span><span class="sxs-lookup"><span data-stu-id="2f168-112">Create a job and tasks to process input files</span></span>
> * <span data-ttu-id="2f168-113">Monitor task execution</span><span class="sxs-lookup"><span data-stu-id="2f168-113">Monitor task execution</span></span>
> * <span data-ttu-id="2f168-114">Retrieve output files</span><span class="sxs-lookup"><span data-stu-id="2f168-114">Retrieve output files</span></span>

<span data-ttu-id="2f168-115">In this tutorial, you convert MP4 media files in parallel to MP3 format using the [ffmpeg](http://ffmpeg.org/) open-source tool.</span><span class="sxs-lookup"><span data-stu-id="2f168-115">In this tutorial, you convert MP4 media files in parallel to MP3 format using the [ffmpeg](http://ffmpeg.org/) open-source tool.</span></span> 

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="2f168-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f168-116">Prerequisites</span></span>

* <span data-ttu-id="2f168-117">[Visual Studio 2017](https://www.visualstudio.com/vs), or [.NET Core 2.1](https://www.microsoft.com/net/download/dotnet-core/2.1) for Linux, macOS, or Windows.</span><span class="sxs-lookup"><span data-stu-id="2f168-117">[Visual Studio 2017](https://www.visualstudio.com/vs), or [.NET Core 2.1](https://www.microsoft.com/net/download/dotnet-core/2.1) for Linux, macOS, or Windows.</span></span>

* <span data-ttu-id="2f168-118">A Batch account and a linked Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="2f168-118">A Batch account and a linked Azure Storage account.</span></span> <span data-ttu-id="2f168-119">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2f168-119">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span></span>

* <span data-ttu-id="2f168-120">[Windows 64-bit version of ffmpeg 3.4](https://ffmpeg.zeranoe.com/builds/win64/static/ffmpeg-3.4-win64-static.zip) (.zip).</span><span class="sxs-lookup"><span data-stu-id="2f168-120">[Windows 64-bit version of ffmpeg 3.4](https://ffmpeg.zeranoe.com/builds/win64/static/ffmpeg-3.4-win64-static.zip) (.zip).</span></span> <span data-ttu-id="2f168-121">Download the zip file to your local computer.</span><span class="sxs-lookup"><span data-stu-id="2f168-121">Download the zip file to your local computer.</span></span> <span data-ttu-id="2f168-122">For this tutorial you only need the zip file.</span><span class="sxs-lookup"><span data-stu-id="2f168-122">For this tutorial you only need the zip file.</span></span> <span data-ttu-id="2f168-123">You do not need to unzip the file or install it locally.</span><span class="sxs-lookup"><span data-stu-id="2f168-123">You do not need to unzip the file or install it locally.</span></span> 

## <a name="sign-in-to-azure"></a><span data-ttu-id="2f168-124">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="2f168-124">Sign in to Azure</span></span>

<span data-ttu-id="2f168-125">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f168-125">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

## <a name="add-an-application-package"></a><span data-ttu-id="2f168-126">Add an application package</span><span class="sxs-lookup"><span data-stu-id="2f168-126">Add an application package</span></span>

<span data-ttu-id="2f168-127">Use the Azure portal to add ffmpeg to your Batch account as an [application package](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="2f168-127">Use the Azure portal to add ffmpeg to your Batch account as an [application package](batch-application-packages.md).</span></span> <span data-ttu-id="2f168-128">Application packages help you manage task applications and their deployment to the compute nodes in your pool.</span><span class="sxs-lookup"><span data-stu-id="2f168-128">Application packages help you manage task applications and their deployment to the compute nodes in your pool.</span></span> 

1. <span data-ttu-id="2f168-129">In the Azure portal, click **More services** > **Batch accounts**, and click the name of your Batch account.</span><span class="sxs-lookup"><span data-stu-id="2f168-129">In the Azure portal, click **More services** > **Batch accounts**, and click the name of your Batch account.</span></span>
3. <span data-ttu-id="2f168-130">Click **Applications** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="2f168-130">Click **Applications** > **Add**.</span></span>
4. <span data-ttu-id="2f168-131">For **Application id** enter *ffmpeg*, and a package version of *3.4*.</span><span class="sxs-lookup"><span data-stu-id="2f168-131">For **Application id** enter *ffmpeg*, and a package version of *3.4*.</span></span> <span data-ttu-id="2f168-132">Select the ffmpeg zip file you downloaded previously, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f168-132">Select the ffmpeg zip file you downloaded previously, and then click **OK**.</span></span> <span data-ttu-id="2f168-133">The ffmpeg application package is added to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="2f168-133">The ffmpeg application package is added to your Batch account.</span></span>

![Add application package](./media/tutorial-parallel-dotnet/add-application.png)

[!INCLUDE [batch-common-credentials](../../includes/batch-common-credentials.md)]

## <a name="download-and-run-the-sample"></a><span data-ttu-id="2f168-135">Download and run the sample</span><span class="sxs-lookup"><span data-stu-id="2f168-135">Download and run the sample</span></span>

### <a name="download-the-sample"></a><span data-ttu-id="2f168-136">Download the sample</span><span class="sxs-lookup"><span data-stu-id="2f168-136">Download the sample</span></span>

<span data-ttu-id="2f168-137">[Download or clone the sample app](https://github.com/Azure-Samples/batch-dotnet-ffmpeg-tutorial) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="2f168-137">[Download or clone the sample app](https://github.com/Azure-Samples/batch-dotnet-ffmpeg-tutorial) from GitHub.</span></span> <span data-ttu-id="2f168-138">To clone the sample app repo with a Git client, use the following command:</span><span class="sxs-lookup"><span data-stu-id="2f168-138">To clone the sample app repo with a Git client, use the following command:</span></span>

```
git clone https://github.com/Azure-Samples/batch-dotnet-ffmpeg-tutorial.git
```

<span data-ttu-id="2f168-139">Navigate to the directory that contains the Visual Studio solution file `BatchDotNetFfmpegTutorial.sln`.</span><span class="sxs-lookup"><span data-stu-id="2f168-139">Navigate to the directory that contains the Visual Studio solution file `BatchDotNetFfmpegTutorial.sln`.</span></span>

<span data-ttu-id="2f168-140">Open the solution file in Visual Studio, and update the credential strings in `program.cs` with the values you obtained for your accounts.</span><span class="sxs-lookup"><span data-stu-id="2f168-140">Open the solution file in Visual Studio, and update the credential strings in `program.cs` with the values you obtained for your accounts.</span></span> <span data-ttu-id="2f168-141">For example:</span><span class="sxs-lookup"><span data-stu-id="2f168-141">For example:</span></span>

```csharp
// Batch account credentials
private const string BatchAccountName = "mybatchaccount";
private const string BatchAccountKey  = "xxxxxxxxxxxxxxxxE+yXrRvJAqT9BlXwwo1CwF+SwAYOxxxxxxxxxxxxxxxx43pXi/gdiATkvbpLRl3x14pcEQ==";
private const string BatchAccountUrl  = "https://mybatchaccount.mybatchregion.batch.azure.com";

// Storage account credentials
private const string StorageAccountName = "mystorageaccount";
private const string StorageAccountKey  = "xxxxxxxxxxxxxxxxy4/xxxxxxxxxxxxxxxxfwpbIC5aAWA8wDu+AFXZB827Mt9lybZB1nUcQbQiUrkPtilK5BQ==";
```

<span data-ttu-id="2f168-142">Also, make sure that the ffmpeg application package reference in the solution matches the Id and version of the ffmpeg package that you uploaded to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="2f168-142">Also, make sure that the ffmpeg application package reference in the solution matches the Id and version of the ffmpeg package that you uploaded to your Batch account.</span></span>

```csharp
const string appPackageId = "ffmpeg";
const string appPackageVersion = "3.4";
```

### <a name="build-and-run-the-sample-project"></a><span data-ttu-id="2f168-143">Build and run the sample project</span><span class="sxs-lookup"><span data-stu-id="2f168-143">Build and run the sample project</span></span>

<span data-ttu-id="2f168-144">Build and run the application in Visual Studio, or at the command line with the `dotnet build` and `dotnet run` commands.</span><span class="sxs-lookup"><span data-stu-id="2f168-144">Build and run the application in Visual Studio, or at the command line with the `dotnet build` and `dotnet run` commands.</span></span> <span data-ttu-id="2f168-145">After running the application, review the code to learn what each part of the application does.</span><span class="sxs-lookup"><span data-stu-id="2f168-145">After running the application, review the code to learn what each part of the application does.</span></span> <span data-ttu-id="2f168-146">For example, in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2f168-146">For example, in Visual Studio:</span></span>

* <span data-ttu-id="2f168-147">Right-click the solution in Solution Explorer and click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="2f168-147">Right-click the solution in Solution Explorer and click **Build Solution**.</span></span> 

* <span data-ttu-id="2f168-148">Confirm the restoration of any NuGet packages, if you're prompted.</span><span class="sxs-lookup"><span data-stu-id="2f168-148">Confirm the restoration of any NuGet packages, if you're prompted.</span></span> <span data-ttu-id="2f168-149">If you need to download missing packages, ensure the [NuGet Package Manager](https://docs.nuget.org/consume/installing-nuget) is installed.</span><span class="sxs-lookup"><span data-stu-id="2f168-149">If you need to download missing packages, ensure the [NuGet Package Manager](https://docs.nuget.org/consume/installing-nuget) is installed.</span></span>

<span data-ttu-id="2f168-150">Then run it.</span><span class="sxs-lookup"><span data-stu-id="2f168-150">Then run it.</span></span> <span data-ttu-id="2f168-151">When you run the sample application, the console output is similar to the following.</span><span class="sxs-lookup"><span data-stu-id="2f168-151">When you run the sample application, the console output is similar to the following.</span></span> <span data-ttu-id="2f168-152">During execution, you experience a pause at `Monitoring all tasks for 'Completed' state, timeout in 00:30:00...` while the pool's compute nodes are started.</span><span class="sxs-lookup"><span data-stu-id="2f168-152">During execution, you experience a pause at `Monitoring all tasks for 'Completed' state, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> 

```
Sample start: 12/12/2017 3:20:21 PM

Container [input] created.
Container [output] created.
Uploading file LowPriVMs-1.mp4 to container [input]...
Uploading file LowPriVMs-2.mp4 to container [input]...
Uploading file LowPriVMs-3.mp4 to container [input]...
Uploading file LowPriVMs-4.mp4 to container [input]...
Uploading file LowPriVMs-5.mp4 to container [input]...
Creating pool [WinFFmpegPool]...
Creating job [WinFFmpegJob]...
Adding 5 tasks to job [WinFFmpegJob]...
Monitoring all tasks for 'Completed' state, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Deleting container [input]...

Sample end: 12/12/2017 3:29:36 PM
Elapsed time: 00:09:14.3418742
```


<span data-ttu-id="2f168-153">Go to your Batch account in the Azure portal to monitor the pool, compute nodes, job, and tasks.</span><span class="sxs-lookup"><span data-stu-id="2f168-153">Go to your Batch account in the Azure portal to monitor the pool, compute nodes, job, and tasks.</span></span> <span data-ttu-id="2f168-154">For example, to see a heat map of the compute nodes in your pool, click **Pools** > *WinFFmpegPool*.</span><span class="sxs-lookup"><span data-stu-id="2f168-154">For example, to see a heat map of the compute nodes in your pool, click **Pools** > *WinFFmpegPool*.</span></span>

<span data-ttu-id="2f168-155">When tasks are running, the heat map is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="2f168-155">When tasks are running, the heat map is similar to the following:</span></span>

![Pool heat map](./media/tutorial-parallel-dotnet/pool.png)


<span data-ttu-id="2f168-157">Typical execution time is approximately **10 minutes** when you run the application in its default configuration.</span><span class="sxs-lookup"><span data-stu-id="2f168-157">Typical execution time is approximately **10 minutes** when you run the application in its default configuration.</span></span> <span data-ttu-id="2f168-158">Pool creation takes the most time.</span><span class="sxs-lookup"><span data-stu-id="2f168-158">Pool creation takes the most time.</span></span>

[!INCLUDE [batch-common-tutorial-download](../../includes/batch-common-tutorial-download.md)]

## <a name="review-the-code"></a><span data-ttu-id="2f168-159">Review the code</span><span class="sxs-lookup"><span data-stu-id="2f168-159">Review the code</span></span>

<span data-ttu-id="2f168-160">The following sections break down the sample application into the steps that it performs to process a workload in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="2f168-160">The following sections break down the sample application into the steps that it performs to process a workload in the Batch service.</span></span> <span data-ttu-id="2f168-161">Refer to the file `Program.cs` in the solution while you read the rest of this article, since not every line of code in the sample is discussed.</span><span class="sxs-lookup"><span data-stu-id="2f168-161">Refer to the file `Program.cs` in the solution while you read the rest of this article, since not every line of code in the sample is discussed.</span></span>

### <a name="authenticate-blob-and-batch-clients"></a><span data-ttu-id="2f168-162">Authenticate Blob and Batch clients</span><span class="sxs-lookup"><span data-stu-id="2f168-162">Authenticate Blob and Batch clients</span></span>

<span data-ttu-id="2f168-163">To interact with the linked storage account, the app uses the Azure Storage Client Library for .NET.</span><span class="sxs-lookup"><span data-stu-id="2f168-163">To interact with the linked storage account, the app uses the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="2f168-164">It creates a reference to the account with [CloudStorageAccount](/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount), authenticating using shared key authentication.</span><span class="sxs-lookup"><span data-stu-id="2f168-164">It creates a reference to the account with [CloudStorageAccount](/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount), authenticating using shared key authentication.</span></span> <span data-ttu-id="2f168-165">Then, it creates a [CloudBlobClient](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobclient).</span><span class="sxs-lookup"><span data-stu-id="2f168-165">Then, it creates a [CloudBlobClient](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobclient).</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
                                StorageAccountName, StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConnectionString);

CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="2f168-166">The app creates a [BatchClient](/dotnet/api/microsoft.azure.batch.batchclient) object to create and manage pools, jobs, and tasks in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="2f168-166">The app creates a [BatchClient](/dotnet/api/microsoft.azure.batch.batchclient) object to create and manage pools, jobs, and tasks in the Batch service.</span></span> <span data-ttu-id="2f168-167">The Batch client in the sample uses shared key authentication.</span><span class="sxs-lookup"><span data-stu-id="2f168-167">The Batch client in the sample uses shared key authentication.</span></span> <span data-ttu-id="2f168-168">Batch also supports authentication through [Azure Active Directory](batch-aad-auth.md), to authenticate individual users or an unattended application.</span><span class="sxs-lookup"><span data-stu-id="2f168-168">Batch also supports authentication through [Azure Active Directory](batch-aad-auth.md), to authenticate individual users or an unattended application.</span></span>

```csharp
BatchSharedKeyCredentials sharedKeyCredentials = new BatchSharedKeyCredentials(BatchAccountUrl, BatchAccountName, BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(sharedKeyCredentials))
...
```

### <a name="upload-input-files"></a><span data-ttu-id="2f168-169">Upload input files</span><span class="sxs-lookup"><span data-stu-id="2f168-169">Upload input files</span></span>

<span data-ttu-id="2f168-170">The app passes the `blobClient` object to the `CreateContainerIfNotExistAsync` method to create a storage container for the input files (MP4 format) and a container for the task output.</span><span class="sxs-lookup"><span data-stu-id="2f168-170">The app passes the `blobClient` object to the `CreateContainerIfNotExistAsync` method to create a storage container for the input files (MP4 format) and a container for the task output.</span></span>

```csharp
CreateContainerIfNotExistAsync(blobClient, inputContainerName;
CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

<span data-ttu-id="2f168-171">Then, files are uploaded to the input container from the local `InputFiles` folder.</span><span class="sxs-lookup"><span data-stu-id="2f168-171">Then, files are uploaded to the input container from the local `InputFiles` folder.</span></span> <span data-ttu-id="2f168-172">The files in storage are defined as Batch [ResourceFile](/dotnet/api/microsoft.azure.batch.resourcefile) objects that Batch can later download to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="2f168-172">The files in storage are defined as Batch [ResourceFile](/dotnet/api/microsoft.azure.batch.resourcefile) objects that Batch can later download to compute nodes.</span></span> 

<span data-ttu-id="2f168-173">Two methods in `Program.cs` are involved in uploading the files:</span><span class="sxs-lookup"><span data-stu-id="2f168-173">Two methods in `Program.cs` are involved in uploading the files:</span></span>

* <span data-ttu-id="2f168-174">`UploadResourceFilesToContainerAsync`: Returns a collection of ResourceFile objects and internally calls `UploadResourceFileToContainerAsync` to upload each file that is passed in the `inputFilePaths` parameter.</span><span class="sxs-lookup"><span data-stu-id="2f168-174">`UploadResourceFilesToContainerAsync`: Returns a collection of ResourceFile objects and internally calls `UploadResourceFileToContainerAsync` to upload each file that is passed in the `inputFilePaths` parameter.</span></span>
* <span data-ttu-id="2f168-175">`UploadResourceFileToContainerAsync`: Uploads each file as a blob to the input container.</span><span class="sxs-lookup"><span data-stu-id="2f168-175">`UploadResourceFileToContainerAsync`: Uploads each file as a blob to the input container.</span></span> <span data-ttu-id="2f168-176">After uploading the file, it obtains a shared access signature (SAS) for the blob and returns a ResourceFile object to represent it.</span><span class="sxs-lookup"><span data-stu-id="2f168-176">After uploading the file, it obtains a shared access signature (SAS) for the blob and returns a ResourceFile object to represent it.</span></span> 

```csharp
string inputPath = Path.Combine(Environment.CurrentDirectory, "InputFiles");

List<string> inputFilePaths = new List<string>(Directory.GetFileSystemEntries(inputPath, "*.mp4",
    SearchOption.TopDirectoryOnly));

List<ResourceFile> inputFiles = await UploadResourceFilesToContainerAsync(
  blobClient,
  inputContainerName,
  inputFilePaths);
```

<span data-ttu-id="2f168-177">For details about uploading files as blobs to a storage account with .NET, see [Upload, download, and list blobs using .NET](../storage/blobs/storage-quickstart-blobs-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2f168-177">For details about uploading files as blobs to a storage account with .NET, see [Upload, download, and list blobs using .NET](../storage/blobs/storage-quickstart-blobs-dotnet.md).</span></span>

### <a name="create-a-pool-of-compute-nodes"></a><span data-ttu-id="2f168-178">Create a pool of compute nodes</span><span class="sxs-lookup"><span data-stu-id="2f168-178">Create a pool of compute nodes</span></span>

<span data-ttu-id="2f168-179">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistAsync`.</span><span class="sxs-lookup"><span data-stu-id="2f168-179">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistAsync`.</span></span> <span data-ttu-id="2f168-180">This defined method uses the [BatchClient.PoolOperations.CreatePool](/dotnet/api/microsoft.azure.batch.pooloperations.createpool) method to set the number of nodes, VM size, and a pool configuration.</span><span class="sxs-lookup"><span data-stu-id="2f168-180">This defined method uses the [BatchClient.PoolOperations.CreatePool](/dotnet/api/microsoft.azure.batch.pooloperations.createpool) method to set the number of nodes, VM size, and a pool configuration.</span></span> <span data-ttu-id="2f168-181">Here, a [VirtualMachineConfiguration](/dotnet/api/microsoft.azure.batch.virtualmachineconfiguration) object specifies an [ImageReference](/dotnet/api/microsoft.azure.batch.imagereference) to a Windows Server image published in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2f168-181">Here, a [VirtualMachineConfiguration](/dotnet/api/microsoft.azure.batch.virtualmachineconfiguration) object specifies an [ImageReference](/dotnet/api/microsoft.azure.batch.imagereference) to a Windows Server image published in the Azure Marketplace.</span></span> <span data-ttu-id="2f168-182">Batch supports a wide range of VM images in the Azure Marketplace, as well as custom VM images.</span><span class="sxs-lookup"><span data-stu-id="2f168-182">Batch supports a wide range of VM images in the Azure Marketplace, as well as custom VM images.</span></span>

<span data-ttu-id="2f168-183">The number of nodes and VM size are set using defined constants.</span><span class="sxs-lookup"><span data-stu-id="2f168-183">The number of nodes and VM size are set using defined constants.</span></span> <span data-ttu-id="2f168-184">Batch supports dedicated nodes and [low-priority nodes](batch-low-pri-vms.md), and you can use either or both in your pools.</span><span class="sxs-lookup"><span data-stu-id="2f168-184">Batch supports dedicated nodes and [low-priority nodes](batch-low-pri-vms.md), and you can use either or both in your pools.</span></span> <span data-ttu-id="2f168-185">Dedicated nodes are reserved for your pool.</span><span class="sxs-lookup"><span data-stu-id="2f168-185">Dedicated nodes are reserved for your pool.</span></span> <span data-ttu-id="2f168-186">Low-priority nodes are offered at a reduced price from surplus VM capacity in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f168-186">Low-priority nodes are offered at a reduced price from surplus VM capacity in Azure.</span></span> <span data-ttu-id="2f168-187">Low-priority nodes become unavailable if Azure does not have enough capacity.</span><span class="sxs-lookup"><span data-stu-id="2f168-187">Low-priority nodes become unavailable if Azure does not have enough capacity.</span></span> <span data-ttu-id="2f168-188">The sample by default creates a pool containing only 5 low-priority nodes in size *Standard_A1_v2*.</span><span class="sxs-lookup"><span data-stu-id="2f168-188">The sample by default creates a pool containing only 5 low-priority nodes in size *Standard_A1_v2*.</span></span> 

<span data-ttu-id="2f168-189">The ffmpeg application is deployed to the compute nodes by adding an [ApplicationPackageReference](/dotnet/api/microsoft.azure.batch.applicationpackagereference) to the pool configuration.</span><span class="sxs-lookup"><span data-stu-id="2f168-189">The ffmpeg application is deployed to the compute nodes by adding an [ApplicationPackageReference](/dotnet/api/microsoft.azure.batch.applicationpackagereference) to the pool configuration.</span></span> 

<span data-ttu-id="2f168-190">The [CommitAsync](/dotnet/api/microsoft.azure.batch.cloudpool.commitasync) method submits the pool to the Batch service.</span><span class="sxs-lookup"><span data-stu-id="2f168-190">The [CommitAsync](/dotnet/api/microsoft.azure.batch.cloudpool.commitasync) method submits the pool to the Batch service.</span></span>

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

pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: DedicatedNodeCount,
    targetLowPriorityComputeNodes: LowPriorityNodeCount,
    virtualMachineSize: PoolVMSize,                                                
    virtualMachineConfiguration: virtualMachineConfiguration);

pool.ApplicationPackageReferences = new List<ApplicationPackageReference>
    {
    new ApplicationPackageReference {
    ApplicationId = appPackageId,
    Version = appPackageVersion}};

await pool.CommitAsync();  
```

### <a name="create-a-job"></a><span data-ttu-id="2f168-191">Create a job</span><span class="sxs-lookup"><span data-stu-id="2f168-191">Create a job</span></span>

<span data-ttu-id="2f168-192">A Batch job specifies a pool to run tasks on and optional settings such as a priority and schedule for the work.</span><span class="sxs-lookup"><span data-stu-id="2f168-192">A Batch job specifies a pool to run tasks on and optional settings such as a priority and schedule for the work.</span></span> <span data-ttu-id="2f168-193">The sample creates a job with a call to `CreateJobAsync`.</span><span class="sxs-lookup"><span data-stu-id="2f168-193">The sample creates a job with a call to `CreateJobAsync`.</span></span> <span data-ttu-id="2f168-194">This defined method uses the [BatchClient.JobOperations.CreateJob](/dotnet/api/microsoft.azure.batch.joboperations.createjob) method to create a job on your pool.</span><span class="sxs-lookup"><span data-stu-id="2f168-194">This defined method uses the [BatchClient.JobOperations.CreateJob](/dotnet/api/microsoft.azure.batch.joboperations.createjob) method to create a job on your pool.</span></span> 

<span data-ttu-id="2f168-195">The [CommitAsync](/dotnet/api/microsoft.azure.batch.cloudjob.commitasync) method submits the job to the Batch service.</span><span class="sxs-lookup"><span data-stu-id="2f168-195">The [CommitAsync](/dotnet/api/microsoft.azure.batch.cloudjob.commitasync) method submits the job to the Batch service.</span></span> <span data-ttu-id="2f168-196">Initially the job has no tasks.</span><span class="sxs-lookup"><span data-stu-id="2f168-196">Initially the job has no tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob();
job.Id = JobId;
job.PoolInformation = new PoolInformation { PoolId = PoolId };

await job.CommitAsync();
```

### <a name="create-tasks"></a><span data-ttu-id="2f168-197">Create tasks</span><span class="sxs-lookup"><span data-stu-id="2f168-197">Create tasks</span></span>

<span data-ttu-id="2f168-198">The sample creates tasks in the job with a call to the `AddTasksAsync` method, which creates a list of [CloudTask](/dotnet/api/microsoft.azure.batch.cloudtask) objects.</span><span class="sxs-lookup"><span data-stu-id="2f168-198">The sample creates tasks in the job with a call to the `AddTasksAsync` method, which creates a list of [CloudTask](/dotnet/api/microsoft.azure.batch.cloudtask) objects.</span></span> <span data-ttu-id="2f168-199">Each `CloudTask` runs ffmpeg to process an input `ResourceFile` object using a [CommandLine](/dotnet/api/microsoft.azure.batch.cloudtask.commandline) property.</span><span class="sxs-lookup"><span data-stu-id="2f168-199">Each `CloudTask` runs ffmpeg to process an input `ResourceFile` object using a [CommandLine](/dotnet/api/microsoft.azure.batch.cloudtask.commandline) property.</span></span> <span data-ttu-id="2f168-200">ffmpeg was previously installed on each node when the pool was created.</span><span class="sxs-lookup"><span data-stu-id="2f168-200">ffmpeg was previously installed on each node when the pool was created.</span></span> <span data-ttu-id="2f168-201">Here, the command line runs ffmpeg to convert each input MP4 (video) file to an MP3 (audio) file.</span><span class="sxs-lookup"><span data-stu-id="2f168-201">Here, the command line runs ffmpeg to convert each input MP4 (video) file to an MP3 (audio) file.</span></span>

<span data-ttu-id="2f168-202">The sample creates an [OutputFile](/dotnet/api/microsoft.azure.batch.outputfile) object for the MP3 file after running the command line.</span><span class="sxs-lookup"><span data-stu-id="2f168-202">The sample creates an [OutputFile](/dotnet/api/microsoft.azure.batch.outputfile) object for the MP3 file after running the command line.</span></span> <span data-ttu-id="2f168-203">Each task's output files (one, in this case) are uploaded to a container in the linked storage account, using the task's [OutputFiles](/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles) property.</span><span class="sxs-lookup"><span data-stu-id="2f168-203">Each task's output files (one, in this case) are uploaded to a container in the linked storage account, using the task's [OutputFiles](/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles) property.</span></span>

<span data-ttu-id="2f168-204">Then, the sample adds tasks to the job with the [AddTaskAsync](/dotnet/api/microsoft.azure.batch.joboperations.addtaskasync) method, which queues them to run on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="2f168-204">Then, the sample adds tasks to the job with the [AddTaskAsync](/dotnet/api/microsoft.azure.batch.joboperations.addtaskasync) method, which queues them to run on the compute nodes.</span></span> 

```csharp
for (int i = 0; i < inputFiles.Count; i++)
{
    string taskId = String.Format("Task{0}", i);

    // Define task command line to convert each input file.
    string appPath = String.Format("%AZ_BATCH_APP_PACKAGE_{0}#{1}%", appPackageId, appPackageVersion);
    string inputMediaFile = inputFiles[i].FilePath;
    string outputMediaFile = String.Format("{0}{1}",
        System.IO.Path.GetFileNameWithoutExtension(inputMediaFile),
        ".mp3");
    string taskCommandLine = String.Format("cmd /c {0}\\ffmpeg-3.4-win64-static\\bin\\ffmpeg.exe -i {1} {2}", appPath, inputMediaFile, outputMediaFile);

    // Create a cloud task (with the task ID and command line) 
    CloudTask task = new CloudTask(taskId, taskCommandLine);
    task.ResourceFiles = new List<ResourceFile> { inputFiles[i] };

    // Task output file
    List<OutputFile> outputFileList = new List<OutputFile>();
    OutputFileBlobContainerDestination outputContainer = new OutputFileBlobContainerDestination(outputContainerSasUrl);
    OutputFile outputFile = new OutputFile(outputMediaFile,
       new OutputFileDestination(outputContainer),
       new OutputFileUploadOptions(OutputFileUploadCondition.TaskSuccess));
    outputFileList.Add(outputFile);
    task.OutputFiles = outputFileList;
    tasks.Add(task);
}

// Add tasks as a collection
await batchClient.JobOperations.AddTaskAsync(jobId, tasks);
return tasks
```

### <a name="monitor-tasks"></a><span data-ttu-id="2f168-205">Monitor tasks</span><span class="sxs-lookup"><span data-stu-id="2f168-205">Monitor tasks</span></span>

<span data-ttu-id="2f168-206">When Batch adds tasks to a job, the service automatically queues and schedules them for execution on compute nodes in the associated pool.</span><span class="sxs-lookup"><span data-stu-id="2f168-206">When Batch adds tasks to a job, the service automatically queues and schedules them for execution on compute nodes in the associated pool.</span></span> <span data-ttu-id="2f168-207">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties.</span><span class="sxs-lookup"><span data-stu-id="2f168-207">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties.</span></span> 

<span data-ttu-id="2f168-208">There are many approaches to monitoring task execution.</span><span class="sxs-lookup"><span data-stu-id="2f168-208">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="2f168-209">This sample defines a `MonitorTasks` method to report only on completion and task failure or success states.</span><span class="sxs-lookup"><span data-stu-id="2f168-209">This sample defines a `MonitorTasks` method to report only on completion and task failure or success states.</span></span> <span data-ttu-id="2f168-210">The `MonitorTasks` code specifies an [ODATADetailLevel](/dotnet/api/microsoft.azure.batch.odatadetaillevel) to efficiently select only minimal information about the tasks.</span><span class="sxs-lookup"><span data-stu-id="2f168-210">The `MonitorTasks` code specifies an [ODATADetailLevel](/dotnet/api/microsoft.azure.batch.odatadetaillevel) to efficiently select only minimal information about the tasks.</span></span> <span data-ttu-id="2f168-211">Then, it creates a [TaskStateMonitor](/dotnet/api/microsoft.azure.batch.taskstatemonitor), which provides helper utilities for monitoring task states.</span><span class="sxs-lookup"><span data-stu-id="2f168-211">Then, it creates a [TaskStateMonitor](/dotnet/api/microsoft.azure.batch.taskstatemonitor), which provides helper utilities for monitoring task states.</span></span> <span data-ttu-id="2f168-212">In `MonitorTasks`, the sample waits for all tasks to reach `TaskState.Completed` within a time limit.</span><span class="sxs-lookup"><span data-stu-id="2f168-212">In `MonitorTasks`, the sample waits for all tasks to reach `TaskState.Completed` within a time limit.</span></span> <span data-ttu-id="2f168-213">Then it terminates the job and reports on any tasks that completed but may have encountered a failure such as a non-zero exit code.</span><span class="sxs-lookup"><span data-stu-id="2f168-213">Then it terminates the job and reports on any tasks that completed but may have encountered a failure such as a non-zero exit code.</span></span>

```csharp
TaskStateMonitor taskStateMonitor = batchClient.Utilities.CreateTaskStateMonitor();
try
{
    await taskStateMonitor.WhenAll(addedTasks, TaskState.Completed, timeout);
}
catch (TimeoutException)
{
    batchClient.JobOperations.TerminateJob(jobId);
    Console.WriteLine(incompleteMessage);
    return false;
}
batchClient.JobOperations.TerminateJob(jobId);
 Console.WriteLine(completeMessage);
...

```

## <a name="clean-up-resources"></a><span data-ttu-id="2f168-214">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2f168-214">Clean up resources</span></span>

<span data-ttu-id="2f168-215">After it runs the tasks, the app automatically deletes the input storage container it created, and gives you the option to delete the Batch pool and job.</span><span class="sxs-lookup"><span data-stu-id="2f168-215">After it runs the tasks, the app automatically deletes the input storage container it created, and gives you the option to delete the Batch pool and job.</span></span> <span data-ttu-id="2f168-216">The BatchClient's [JobOperations](/dotnet/api/microsoft.azure.batch.batchclient.joboperations) and [PoolOperations](/dotnet/api/microsoft.azure.batch.batchclient.pooloperations) classes both have corresponding delete methods, which are called if you confirm deletion.</span><span class="sxs-lookup"><span data-stu-id="2f168-216">The BatchClient's [JobOperations](/dotnet/api/microsoft.azure.batch.batchclient.joboperations) and [PoolOperations](/dotnet/api/microsoft.azure.batch.batchclient.pooloperations) classes both have corresponding delete methods, which are called if you confirm deletion.</span></span> <span data-ttu-id="2f168-217">Although you're not charged for jobs and tasks themselves, you are charged for compute nodes.</span><span class="sxs-lookup"><span data-stu-id="2f168-217">Although you're not charged for jobs and tasks themselves, you are charged for compute nodes.</span></span> <span data-ttu-id="2f168-218">Thus, we recommend that you allocate pools only as needed.</span><span class="sxs-lookup"><span data-stu-id="2f168-218">Thus, we recommend that you allocate pools only as needed.</span></span> <span data-ttu-id="2f168-219">When you delete the pool, all task output on the nodes is deleted.</span><span class="sxs-lookup"><span data-stu-id="2f168-219">When you delete the pool, all task output on the nodes is deleted.</span></span> <span data-ttu-id="2f168-220">However, the output files remain in the storage account.</span><span class="sxs-lookup"><span data-stu-id="2f168-220">However, the output files remain in the storage account.</span></span>

<span data-ttu-id="2f168-221">When no longer needed, delete the resource group, Batch account, and storage account.</span><span class="sxs-lookup"><span data-stu-id="2f168-221">When no longer needed, delete the resource group, Batch account, and storage account.</span></span> <span data-ttu-id="2f168-222">To do so in the Azure portal, select the resource group for the Batch account and click **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="2f168-222">To do so in the Azure portal, select the resource group for the Batch account and click **Delete resource group**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f168-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f168-223">Next steps</span></span>

<span data-ttu-id="2f168-224">In this tutorial, you learned about how to:</span><span class="sxs-lookup"><span data-stu-id="2f168-224">In this tutorial, you learned about how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2f168-225">Add an application package to your Batch account</span><span class="sxs-lookup"><span data-stu-id="2f168-225">Add an application package to your Batch account</span></span>
> * <span data-ttu-id="2f168-226">Authenticate with Batch and Storage accounts</span><span class="sxs-lookup"><span data-stu-id="2f168-226">Authenticate with Batch and Storage accounts</span></span>
> * <span data-ttu-id="2f168-227">Upload input files to Storage</span><span class="sxs-lookup"><span data-stu-id="2f168-227">Upload input files to Storage</span></span>
> * <span data-ttu-id="2f168-228">Create a pool of compute nodes to run an application</span><span class="sxs-lookup"><span data-stu-id="2f168-228">Create a pool of compute nodes to run an application</span></span>
> * <span data-ttu-id="2f168-229">Create a job and tasks to process input files</span><span class="sxs-lookup"><span data-stu-id="2f168-229">Create a job and tasks to process input files</span></span>
> * <span data-ttu-id="2f168-230">Monitor task execution</span><span class="sxs-lookup"><span data-stu-id="2f168-230">Monitor task execution</span></span>
> * <span data-ttu-id="2f168-231">Retrieve output files</span><span class="sxs-lookup"><span data-stu-id="2f168-231">Retrieve output files</span></span>

<span data-ttu-id="2f168-232">For more examples of using the .NET API to schedule and process Batch workloads, see the samples on GitHub.</span><span class="sxs-lookup"><span data-stu-id="2f168-232">For more examples of using the .NET API to schedule and process Batch workloads, see the samples on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f168-233">Batch C# samples</span><span class="sxs-lookup"><span data-stu-id="2f168-233">Batch C# samples</span></span>](https://github.com/Azure-Samples/azure-batch-samples/tree/master/CSharp)
