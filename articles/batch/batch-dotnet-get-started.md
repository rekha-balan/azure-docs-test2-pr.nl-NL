---
title: Tutorial - Use the Azure Batch client library for .NET | Microsoft Docs
description: Learn the basic concepts of Azure Batch and build a simple solution using .NET.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: ''
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 294e731b60667db580ee639607d3ba948435b46d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553008"
---
# <a name="get-started-building-solutions-with-the-batch-client-library-for-net"></a><span data-ttu-id="dbd69-103">Get started building solutions with the Batch client library for .NET</span><span class="sxs-lookup"><span data-stu-id="dbd69-103">Get started building solutions with the Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
>
>

<span data-ttu-id="dbd69-106">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span><span class="sxs-lookup"><span data-stu-id="dbd69-106">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="dbd69-107">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/storage-introduction.md) for file staging and retrieval.</span><span class="sxs-lookup"><span data-stu-id="dbd69-107">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="dbd69-108">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span><span class="sxs-lookup"><span data-stu-id="dbd69-108">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="dbd69-109">![Batch solution workflow (basic)][11]</span><span class="sxs-lookup"><span data-stu-id="dbd69-109">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="dbd69-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dbd69-110">Prerequisites</span></span>
<span data-ttu-id="dbd69-111">This article assumes that you have a working knowledge of C# and Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbd69-111">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="dbd69-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span><span class="sxs-lookup"><span data-stu-id="dbd69-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="dbd69-113">Accounts</span><span class="sxs-lookup"><span data-stu-id="dbd69-113">Accounts</span></span>
* <span data-ttu-id="dbd69-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="dbd69-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="dbd69-115">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dbd69-115">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="dbd69-116">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="dbd69-116">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> Batch currently supports *only* the **General purpose** storage account type, as described in step #5 [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a><span data-ttu-id="dbd69-118">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dbd69-118">Visual Studio</span></span>
<span data-ttu-id="dbd69-119">You must have **Visual Studio 2015 or newer** to build the sample project.</span><span class="sxs-lookup"><span data-stu-id="dbd69-119">You must have **Visual Studio 2015 or newer** to build the sample project.</span></span> <span data-ttu-id="dbd69-120">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="dbd69-120">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="dbd69-121">*DotNetTutorial* code sample</span><span class="sxs-lookup"><span data-stu-id="dbd69-121">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="dbd69-122">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="dbd69-122">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="dbd69-123">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span><span class="sxs-lookup"><span data-stu-id="dbd69-123">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="dbd69-124">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span><span class="sxs-lookup"><span data-stu-id="dbd69-124">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="dbd69-125">Azure Batch Explorer (optional)</span><span class="sxs-lookup"><span data-stu-id="dbd69-125">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="dbd69-126">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="dbd69-126">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="dbd69-127">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span><span class="sxs-lookup"><span data-stu-id="dbd69-127">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="dbd69-128">DotNetTutorial sample project overview</span><span class="sxs-lookup"><span data-stu-id="dbd69-128">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="dbd69-129">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="dbd69-129">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="dbd69-130">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="dbd69-130">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="dbd69-131">DotNetTutorial runs on your local workstation.</span><span class="sxs-lookup"><span data-stu-id="dbd69-131">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="dbd69-132">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span><span class="sxs-lookup"><span data-stu-id="dbd69-132">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="dbd69-133">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span><span class="sxs-lookup"><span data-stu-id="dbd69-133">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="dbd69-134">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span><span class="sxs-lookup"><span data-stu-id="dbd69-134">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="dbd69-135">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-135">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span></span> <span data-ttu-id="dbd69-136">This makes it available to the client application for download.</span><span class="sxs-lookup"><span data-stu-id="dbd69-136">This makes it available to the client application for download.</span></span> <span data-ttu-id="dbd69-137">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="dbd69-137">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span></span>

<span data-ttu-id="dbd69-138">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="dbd69-138">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span></span> <span data-ttu-id="dbd69-139">This basic workflow is typical of many compute solutions that are created with Batch.</span><span class="sxs-lookup"><span data-stu-id="dbd69-139">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="dbd69-140">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span><span class="sxs-lookup"><span data-stu-id="dbd69-140">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="dbd69-141">![Batch example workflow][8]</span><span class="sxs-lookup"><span data-stu-id="dbd69-141">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="dbd69-142">**Step 1.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-142">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="dbd69-143">Create **containers** in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-143">Create **containers** in Azure Blob Storage.</span></span><br/>
[<span data-ttu-id="dbd69-144">**Step 2.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-144">**Step 2.**</span></span>](#step-2-upload-task-application-and-data-files) <span data-ttu-id="dbd69-145">Upload task application files and input files to containers.</span><span class="sxs-lookup"><span data-stu-id="dbd69-145">Upload task application files and input files to containers.</span></span><br/>
[<span data-ttu-id="dbd69-146">**Step 3.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-146">**Step 3.**</span></span>](#step-3-create-batch-pool) <span data-ttu-id="dbd69-147">Create a Batch **pool**.</span><span class="sxs-lookup"><span data-stu-id="dbd69-147">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="dbd69-148">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-148">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="dbd69-149">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span><span class="sxs-lookup"><span data-stu-id="dbd69-149">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span></span><br/>
[<span data-ttu-id="dbd69-150">**Step 4.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-150">**Step 4.**</span></span>](#step-4-create-batch-job) <span data-ttu-id="dbd69-151">Create a Batch **job**.</span><span class="sxs-lookup"><span data-stu-id="dbd69-151">Create a Batch **job**.</span></span><br/>
[<span data-ttu-id="dbd69-152">**Step 5.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-152">**Step 5.**</span></span>](#step-5-add-tasks-to-job) <span data-ttu-id="dbd69-153">Add **tasks** to the job.</span><span class="sxs-lookup"><span data-stu-id="dbd69-153">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="dbd69-154">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-154">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="dbd69-155">The tasks are scheduled to execute on nodes.</span><span class="sxs-lookup"><span data-stu-id="dbd69-155">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="dbd69-156">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-156">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="dbd69-157">Each task downloads its input data from Azure Storage, then begins execution.</span><span class="sxs-lookup"><span data-stu-id="dbd69-157">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/>
[<span data-ttu-id="dbd69-158">**Step 6.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-158">**Step 6.**</span></span>](#step-6-monitor-tasks) <span data-ttu-id="dbd69-159">Monitor tasks.</span><span class="sxs-lookup"><span data-stu-id="dbd69-159">Monitor tasks.</span></span><br/>
  <span data-ttu-id="dbd69-160">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-160">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="dbd69-161">As tasks are completed, they upload their output data to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-161">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/>
[<span data-ttu-id="dbd69-162">**Step 7.**</span><span class="sxs-lookup"><span data-stu-id="dbd69-162">**Step 7.**</span></span>](#step-7-download-task-output) <span data-ttu-id="dbd69-163">Download task output from Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-163">Download task output from Storage.</span></span>

<span data-ttu-id="dbd69-164">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span><span class="sxs-lookup"><span data-stu-id="dbd69-164">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-the-dotnettutorial-sample-project"></a><span data-ttu-id="dbd69-165">Build the *DotNetTutorial* sample project</span><span class="sxs-lookup"><span data-stu-id="dbd69-165">Build the *DotNetTutorial* sample project</span></span>
<span data-ttu-id="dbd69-166">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="dbd69-166">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="dbd69-167">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span><span class="sxs-lookup"><span data-stu-id="dbd69-167">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="dbd69-168">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span><span class="sxs-lookup"><span data-stu-id="dbd69-168">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="dbd69-169">Open `Program.cs` within the *DotNetTutorial* project.</span><span class="sxs-lookup"><span data-stu-id="dbd69-169">Open `Program.cs` within the *DotNetTutorial* project.</span></span> <span data-ttu-id="dbd69-170">Then add your credentials as specified near the top of the file:</span><span class="sxs-lookup"><span data-stu-id="dbd69-170">Then add your credentials as specified near the top of the file:</span></span>

```csharp
// Update the Batch and Storage account credential strings below with the values
// unique to your accounts. These are used when constructing connection strings
// for the Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> As mentioned above, you must currently specify the credentials for a **General purpose** storage account in Azure Storage. Your Batch applications use blob storage within the **General purpose** storage account. Do not specify the credentials for a Storage account that was created by selecting the *Blob storage* account type.
>
>

<span data-ttu-id="dbd69-174">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="dbd69-174">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="dbd69-175">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span><span class="sxs-lookup"><span data-stu-id="dbd69-175">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="dbd69-176">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="dbd69-176">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="dbd69-177">Confirm the restoration of any NuGet packages, if you're prompted.</span><span class="sxs-lookup"><span data-stu-id="dbd69-177">Confirm the restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> If the NuGet packages are not automatically restored, or if you see errors about a failure to restore the packages, ensure that you have the [NuGet Package Manager][nuget_packagemgr] installed. Then enable the download of missing packages. See [Enabling Package Restore During Build][nuget_restore] to enable package download.
>
>

<span data-ttu-id="dbd69-181">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span><span class="sxs-lookup"><span data-stu-id="dbd69-181">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="dbd69-182">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span><span class="sxs-lookup"><span data-stu-id="dbd69-182">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span></span>

<span data-ttu-id="dbd69-183">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span><span class="sxs-lookup"><span data-stu-id="dbd69-183">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span></span> <span data-ttu-id="dbd69-184">Each step below then roughly follows the progression of method calls in `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="dbd69-184">Each step below then roughly follows the progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="dbd69-185">Step 1: Create Storage containers</span><span class="sxs-lookup"><span data-stu-id="dbd69-185">Step 1: Create Storage containers</span></span>
<span data-ttu-id="dbd69-186">![Create containers in Azure Storage][1]</span><span class="sxs-lookup"><span data-stu-id="dbd69-186">![Create containers in Azure Storage][1]</span></span>
<br/>

<span data-ttu-id="dbd69-187">Batch includes built-in support for interacting with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-187">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="dbd69-188">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span><span class="sxs-lookup"><span data-stu-id="dbd69-188">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="dbd69-189">The containers also provide a place to store the output data that the tasks produce.</span><span class="sxs-lookup"><span data-stu-id="dbd69-189">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="dbd69-190">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="dbd69-190">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/storage-introduction.md):</span></span>

* <span data-ttu-id="dbd69-191">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span><span class="sxs-lookup"><span data-stu-id="dbd69-191">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="dbd69-192">**input**: Tasks will download the data files to process from the *input* container.</span><span class="sxs-lookup"><span data-stu-id="dbd69-192">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="dbd69-193">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span><span class="sxs-lookup"><span data-stu-id="dbd69-193">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="dbd69-194">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="dbd69-194">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="dbd69-195">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="dbd69-195">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create the blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="dbd69-196">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span><span class="sxs-lookup"><span data-stu-id="dbd69-196">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span></span> <span data-ttu-id="dbd69-197">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span><span class="sxs-lookup"><span data-stu-id="dbd69-197">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span></span>

```csharp
// Use the blob client to create the containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="dbd69-198">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span><span class="sxs-lookup"><span data-stu-id="dbd69-198">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> [How to use Blob Storage from .NET](../storage/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs. It should be near the top of your reading list as you start working with Batch.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="dbd69-201">Step 2: Upload task application and data files</span><span class="sxs-lookup"><span data-stu-id="dbd69-201">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="dbd69-202">![Upload task application and input (data) files to containers][2]</span><span class="sxs-lookup"><span data-stu-id="dbd69-202">![Upload task application and input (data) files to containers][2]</span></span>
<br/>

<span data-ttu-id="dbd69-203">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span><span class="sxs-lookup"><span data-stu-id="dbd69-203">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="dbd69-204">Then it uploads these files to the containers that you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="dbd69-204">Then it uploads these files to the containers that you created in the previous step.</span></span>

```csharp
// Paths to the executable and its dependencies that will be executed by the tasks
List<string> applicationFilePaths = new List<string>
{
    // The DotNetTutorial project includes a project reference to TaskApplication,
    // allowing us to determine the path of the task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// The collection of data files that are to be processed by the tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload the application and its dependencies to Azure Storage. This is the
// application that will process the data files, and will be executed by each
// of the tasks on the compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload the data files. This is the data that will be processed by each of
// the tasks that are executed on the compute nodes within the pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="dbd69-205">There are two methods in `Program.cs` that are involved in the upload process:</span><span class="sxs-lookup"><span data-stu-id="dbd69-205">There are two methods in `Program.cs` that are involved in the upload process:</span></span>

* <span data-ttu-id="dbd69-206">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span><span class="sxs-lookup"><span data-stu-id="dbd69-206">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span></span>
* <span data-ttu-id="dbd69-207">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span><span class="sxs-lookup"><span data-stu-id="dbd69-207">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="dbd69-208">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span><span class="sxs-lookup"><span data-stu-id="dbd69-208">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="dbd69-209">Shared access signatures are also discussed below.</span><span class="sxs-lookup"><span data-stu-id="dbd69-209">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} to container [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set the expiry time and permissions for the blob shared access signature.
        // In this case, no start time is specified, so the shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct the SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="dbd69-210">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="dbd69-210">ResourceFiles</span></span>
<span data-ttu-id="dbd69-211">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span><span class="sxs-lookup"><span data-stu-id="dbd69-211">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="dbd69-212">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-212">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="dbd69-213">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span><span class="sxs-lookup"><span data-stu-id="dbd69-213">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="dbd69-214">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span><span class="sxs-lookup"><span data-stu-id="dbd69-214">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="dbd69-215">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="dbd69-215">[CloudTask][net_task]</span></span>
* <span data-ttu-id="dbd69-216">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="dbd69-216">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="dbd69-217">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="dbd69-217">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="dbd69-218">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="dbd69-218">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="dbd69-219">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="dbd69-219">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="dbd69-220">Shared access signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="dbd69-220">Shared access signature (SAS)</span></span>
<span data-ttu-id="dbd69-221">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-221">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="dbd69-222">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span><span class="sxs-lookup"><span data-stu-id="dbd69-222">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="dbd69-223">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span><span class="sxs-lookup"><span data-stu-id="dbd69-223">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="dbd69-224">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span><span class="sxs-lookup"><span data-stu-id="dbd69-224">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="dbd69-225">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="dbd69-225">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="dbd69-226">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-226">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="dbd69-227">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span><span class="sxs-lookup"><span data-stu-id="dbd69-227">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span></span> <span data-ttu-id="dbd69-228">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span><span class="sxs-lookup"><span data-stu-id="dbd69-228">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span></span> <span data-ttu-id="dbd69-229">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span><span class="sxs-lookup"><span data-stu-id="dbd69-229">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span></span> <span data-ttu-id="dbd69-230">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span><span class="sxs-lookup"><span data-stu-id="dbd69-230">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> Check out the two-part series on shared access signatures, [Part 1: Understanding the shared access signature (SAS) model](../storage/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="dbd69-232">Step 3: Create Batch pool</span><span class="sxs-lookup"><span data-stu-id="dbd69-232">Step 3: Create Batch pool</span></span>
<span data-ttu-id="dbd69-233">![Create a Batch pool][3]</span><span class="sxs-lookup"><span data-stu-id="dbd69-233">![Create a Batch pool][3]</span></span>
<br/>

<span data-ttu-id="dbd69-234">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span><span class="sxs-lookup"><span data-stu-id="dbd69-234">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="dbd69-235">After it uploads the application and data files to the Storage account, *DotNetTutorial* starts its interaction with the Batch service by using the Batch .NET library.</span><span class="sxs-lookup"><span data-stu-id="dbd69-235">After it uploads the application and data files to the Storage account, *DotNetTutorial* starts its interaction with the Batch service by using the Batch .NET library.</span></span> <span data-ttu-id="dbd69-236">To do so, a [BatchClient][net_batchclient] is first created:</span><span class="sxs-lookup"><span data-stu-id="dbd69-236">To do so, a [BatchClient][net_batchclient] is first created:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="dbd69-237">Next, a pool of compute nodes is created in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="dbd69-237">Next, a pool of compute nodes is created in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="dbd69-238">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a pool in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="dbd69-238">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a pool in the Batch service.</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create the unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicated: 3,                                                         // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign the StartTask that will be executed when compute nodes join the pool.
        // In this case, we copy the StartTask's resource files (that will be automatically downloaded
        // to the node by the StartTask) into the shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for the StartTask that copies the task application files to the
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need to manually exit with a 0 for Batch to recognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow the specific error code PoolExists since that is expected if the pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("The pool {0} already existed when we tried to create it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="dbd69-239">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span><span class="sxs-lookup"><span data-stu-id="dbd69-239">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span></span> <span data-ttu-id="dbd69-240">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="dbd69-240">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="dbd69-241">However, by specifying a [VirtualMachineConfiguration][net_virtualmachineconfiguration] instead, you can create pools of nodes created from Marketplace images, which includes both Windows and Linux images—see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="dbd69-241">However, by specifying a [VirtualMachineConfiguration][net_virtualmachineconfiguration] instead, you can create pools of nodes created from Marketplace images, which includes both Windows and Linux images—see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>

> [!IMPORTANT]
> You are charged for compute resources in Batch. To minimize costs, you can lower `targetDedicated` to 1 before you run the sample.
>
>

<span data-ttu-id="dbd69-244">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span><span class="sxs-lookup"><span data-stu-id="dbd69-244">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span></span> <span data-ttu-id="dbd69-245">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span><span class="sxs-lookup"><span data-stu-id="dbd69-245">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="dbd69-246">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span><span class="sxs-lookup"><span data-stu-id="dbd69-246">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span></span> <span data-ttu-id="dbd69-247">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="dbd69-247">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span></span>

<span data-ttu-id="dbd69-248">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span><span class="sxs-lookup"><span data-stu-id="dbd69-248">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span></span> <span data-ttu-id="dbd69-249">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span><span class="sxs-lookup"><span data-stu-id="dbd69-249">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

> [!TIP]
> The **application packages** feature of Azure Batch provides another way to get your application onto the compute nodes in a pool. See [Application deployment with Azure Batch application packages](batch-application-packages.md) for details.
>
>

<span data-ttu-id="dbd69-252">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="dbd69-252">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="dbd69-253">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span><span class="sxs-lookup"><span data-stu-id="dbd69-253">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="dbd69-254">Any process that is executed by a task has access to these environment variables.</span><span class="sxs-lookup"><span data-stu-id="dbd69-254">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> To find out more about the environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see the [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in the [Batch feature overview for developers](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="dbd69-256">Step 4: Create Batch job</span><span class="sxs-lookup"><span data-stu-id="dbd69-256">Step 4: Create Batch job</span></span>
<span data-ttu-id="dbd69-257">![Create Batch job][4]</span><span class="sxs-lookup"><span data-stu-id="dbd69-257">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="dbd69-258">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="dbd69-258">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="dbd69-259">The tasks in a job execute on the associated pool's compute nodes.</span><span class="sxs-lookup"><span data-stu-id="dbd69-259">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="dbd69-260">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span><span class="sxs-lookup"><span data-stu-id="dbd69-260">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="dbd69-261">In this example, however, the job is associated only with the pool that was created in step #3.</span><span class="sxs-lookup"><span data-stu-id="dbd69-261">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="dbd69-262">No additional properties are configured.</span><span class="sxs-lookup"><span data-stu-id="dbd69-262">No additional properties are configured.</span></span>

<span data-ttu-id="dbd69-263">All Batch jobs are associated with a specific pool.</span><span class="sxs-lookup"><span data-stu-id="dbd69-263">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="dbd69-264">This association indicates which nodes the job's tasks will execute on.</span><span class="sxs-lookup"><span data-stu-id="dbd69-264">This association indicates which nodes the job's tasks will execute on.</span></span> <span data-ttu-id="dbd69-265">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span><span class="sxs-lookup"><span data-stu-id="dbd69-265">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="dbd69-266">Now that a job has been created, tasks are added to perform the work.</span><span class="sxs-lookup"><span data-stu-id="dbd69-266">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="dbd69-267">Step 5: Add tasks to job</span><span class="sxs-lookup"><span data-stu-id="dbd69-267">Step 5: Add tasks to job</span></span>
<span data-ttu-id="dbd69-268">![Add tasks to job][5]</span><span class="sxs-lookup"><span data-stu-id="dbd69-268">![Add tasks to job][5]</span></span><br/>
<span data-ttu-id="dbd69-269">*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span><span class="sxs-lookup"><span data-stu-id="dbd69-269">*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="dbd69-270">Batch **tasks** are the individual units of work that execute on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="dbd69-270">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="dbd69-271">A task has a command line and runs the scripts or executables that you specify in that command line.</span><span class="sxs-lookup"><span data-stu-id="dbd69-271">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="dbd69-272">To actually perform work, tasks must be added to a job.</span><span class="sxs-lookup"><span data-stu-id="dbd69-272">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="dbd69-273">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span><span class="sxs-lookup"><span data-stu-id="dbd69-273">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="dbd69-274">In the *DotNetTutorial* sample project, each task processes only one file.</span><span class="sxs-lookup"><span data-stu-id="dbd69-274">In the *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="dbd69-275">Thus, its ResourceFiles collection contains a single element.</span><span class="sxs-lookup"><span data-stu-id="dbd69-275">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks to job [{1}]...", inputFiles.Count, jobId);

    // Create a collection to hold the tasks that we'll be adding to the job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of the tasks. Because we copied the task application to the
    // node's shared directory with the pool's StartTask, we can access it via
    // the shared directory on the node that the task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add the tasks as a collection, as opposed to issuing a separate AddTask call
    // for each. Bulk task submission helps to ensure efficient underlying API calls
    // to the Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in the node's `PATH`, task command lines must be prefixed with `cmd /c`. This will explicitly execute the command interpreter and instruct it to terminate after carrying out your command. This requirement is unnecessary if your tasks execute an application in the node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.
>
>

<span data-ttu-id="dbd69-279">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="dbd69-279">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span></span>

1. <span data-ttu-id="dbd69-280">The **first argument** is the path of the file to process.</span><span class="sxs-lookup"><span data-stu-id="dbd69-280">The **first argument** is the path of the file to process.</span></span> <span data-ttu-id="dbd69-281">This is the local path to the file as it exists on the node.</span><span class="sxs-lookup"><span data-stu-id="dbd69-281">This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="dbd69-282">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span><span class="sxs-lookup"><span data-stu-id="dbd69-282">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span></span> <span data-ttu-id="dbd69-283">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="dbd69-283">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="dbd69-284">The **second argument** specifies that the top *N* words should be written to the output file.</span><span class="sxs-lookup"><span data-stu-id="dbd69-284">The **second argument** specifies that the top *N* words should be written to the output file.</span></span> <span data-ttu-id="dbd69-285">In the sample, this is hard-coded so that the top three words are written to the output file.</span><span class="sxs-lookup"><span data-stu-id="dbd69-285">In the sample, this is hard-coded so that the top three words are written to the output file.</span></span>
3. <span data-ttu-id="dbd69-286">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-286">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="dbd69-287">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-287">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span></span> <span data-ttu-id="dbd69-288">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span><span class="sxs-lookup"><span data-stu-id="dbd69-288">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference to the container using the SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload the file (as a new blob) to the container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when the Batch service
                // sets the CloudTask.ExecutionInformation.ExitCode for the task that
                // executed this application, it properly indicates that there was a
                // problem with the task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="dbd69-289">Step 6: Monitor tasks</span><span class="sxs-lookup"><span data-stu-id="dbd69-289">Step 6: Monitor tasks</span></span>
<span data-ttu-id="dbd69-290">![Monitor tasks][6]</span><span class="sxs-lookup"><span data-stu-id="dbd69-290">![Monitor tasks][6]</span></span><br/>
<span data-ttu-id="dbd69-291">*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="dbd69-291">*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="dbd69-292">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span><span class="sxs-lookup"><span data-stu-id="dbd69-292">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="dbd69-293">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span><span class="sxs-lookup"><span data-stu-id="dbd69-293">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="dbd69-294">There are many approaches to monitoring task execution.</span><span class="sxs-lookup"><span data-stu-id="dbd69-294">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="dbd69-295">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span><span class="sxs-lookup"><span data-stu-id="dbd69-295">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="dbd69-296">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span><span class="sxs-lookup"><span data-stu-id="dbd69-296">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="dbd69-297">They are listed below in their order of appearance:</span><span class="sxs-lookup"><span data-stu-id="dbd69-297">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="dbd69-298">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span><span class="sxs-lookup"><span data-stu-id="dbd69-298">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="dbd69-299">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span><span class="sxs-lookup"><span data-stu-id="dbd69-299">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="dbd69-300">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span><span class="sxs-lookup"><span data-stu-id="dbd69-300">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="dbd69-301">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span><span class="sxs-lookup"><span data-stu-id="dbd69-301">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="dbd69-302">Then it terminates the job.</span><span class="sxs-lookup"><span data-stu-id="dbd69-302">Then it terminates the job.</span></span>
3. <span data-ttu-id="dbd69-303">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span><span class="sxs-lookup"><span data-stu-id="dbd69-303">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="dbd69-304">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="dbd69-304">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="dbd69-305">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="dbd69-305">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="dbd69-306">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span><span class="sxs-lookup"><span data-stu-id="dbd69-306">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed to reach the Completed state within the timeout period.";

    // Obtain the collection of tasks currently managed by the job. Note that we use
    // a detail level to  specify that only the "id" property of each task should be
    // populated. Using a detail level for all list operations helps to lower
    // response time from the Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor to monitor the state of our tasks. In this case, we
    // will wait for all tasks to reach the Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached the "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property to ensure that it did not encounter a scheduling error
    // or return a non-zero exit code.

    // Update the detail level to populate only the task id and executionInfo
    // properties. We refresh the tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate the task's properties with the latest info from the
        // Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.SchedulingError != null)
        {
            // A scheduling error indicates a problem starting the task on the node.
            // It is important to note that the task's state can be "Completed," yet
            // still have encountered a scheduling error.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a scheduling error: {1}",
                task.Id,
                task.ExecutionInformation.SchedulingError.Message);
        }
        else if (task.ExecutionInformation.ExitCode != 0)
        {
            // A non-zero exit code may indicate that the application executed by
            // the task encountered an error during execution. As not every
            // application returns non-zero on failure by default (e.g. robocopy),
            // your implementation of error checking may differ from this example.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within the specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="dbd69-307">Step 7: Download task output</span><span class="sxs-lookup"><span data-stu-id="dbd69-307">Step 7: Download task output</span></span>
<span data-ttu-id="dbd69-308">![Download task output from Storage][7]</span><span class="sxs-lookup"><span data-stu-id="dbd69-308">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="dbd69-309">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dbd69-309">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="dbd69-310">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="dbd69-310">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference to a previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all the block blobs in the specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference to the current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents to a file in the specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded to {0}", directoryPath);
}
```

> [!NOTE]
> The call to `DownloadBlobsFromContainerAsync` in the *DotNetTutorial* application specifies that the files should be downloaded to your `%TEMP%` folder. Feel free to modify this output location.
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="dbd69-313">Step 8: Delete containers</span><span class="sxs-lookup"><span data-stu-id="dbd69-313">Step 8: Delete containers</span></span>
<span data-ttu-id="dbd69-314">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span><span class="sxs-lookup"><span data-stu-id="dbd69-314">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="dbd69-315">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="dbd69-315">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="dbd69-316">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="dbd69-316">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="dbd69-317">Step 9: Delete the job and the pool</span><span class="sxs-lookup"><span data-stu-id="dbd69-317">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="dbd69-318">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span><span class="sxs-lookup"><span data-stu-id="dbd69-318">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span></span> <span data-ttu-id="dbd69-319">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span><span class="sxs-lookup"><span data-stu-id="dbd69-319">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="dbd69-320">Thus, we recommend that you allocate nodes only as needed.</span><span class="sxs-lookup"><span data-stu-id="dbd69-320">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="dbd69-321">Deleting unused pools can be part of your maintenance process.</span><span class="sxs-lookup"><span data-stu-id="dbd69-321">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="dbd69-322">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span><span class="sxs-lookup"><span data-stu-id="dbd69-322">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span></span>

```csharp
// Clean up the resources we've created in the Batch account if the user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost. Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.
>
>

## <a name="run-the-dotnettutorial-sample"></a><span data-ttu-id="dbd69-325">Run the *DotNetTutorial* sample</span><span class="sxs-lookup"><span data-stu-id="dbd69-325">Run the *DotNetTutorial* sample</span></span>
<span data-ttu-id="dbd69-326">When you run the sample application, the console output will be similar to the following.</span><span class="sxs-lookup"><span data-stu-id="dbd69-326">When you run the sample application, the console output will be similar to the following.</span></span> <span data-ttu-id="dbd69-327">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span><span class="sxs-lookup"><span data-stu-id="dbd69-327">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="dbd69-328">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span><span class="sxs-lookup"><span data-stu-id="dbd69-328">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="dbd69-329">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span><span class="sxs-lookup"><span data-stu-id="dbd69-329">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

<span data-ttu-id="dbd69-330">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span><span class="sxs-lookup"><span data-stu-id="dbd69-330">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe to container [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll to container [application]...
Uploading file ..\..\taskdata1.txt to container [input]...
Uploading file ..\..\taskdata2.txt to container [input]...
Uploading file ..\..\taskdata3.txt to container [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks to job [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Downloading all files from container [output]...
All files downloaded to C:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="dbd69-331">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbd69-331">Next steps</span></span>
<span data-ttu-id="dbd69-332">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span><span class="sxs-lookup"><span data-stu-id="dbd69-332">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span></span> <span data-ttu-id="dbd69-333">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span><span class="sxs-lookup"><span data-stu-id="dbd69-333">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="dbd69-334">Try adding more tasks or adjusting the number of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="dbd69-334">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="dbd69-335">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="dbd69-335">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="dbd69-336">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span><span class="sxs-lookup"><span data-stu-id="dbd69-336">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="dbd69-337">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span><span class="sxs-lookup"><span data-stu-id="dbd69-337">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="dbd69-338">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="dbd69-338">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="dbd69-339">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span><span class="sxs-lookup"><span data-stu-id="dbd69-339">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_01_sm.png "Create containers in Azure Storage"
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_02_sm.png "Upload task application and input (data) files to containers"
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_03_sm.png "Create Batch pool"
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_04_sm.png "Create Batch job"
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_05_sm.png "Add tasks to job"
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitor tasks"
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_07_sm.png "Download task output from Storage"
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_sm.png "Batch solution workflow (full diagram)"
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/credentials_batch_sm.png "Batch credentials in Portal"
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/credentials_storage_sm.png "Storage credentials in Portal"
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch solution workflow (minimal diagram)"











