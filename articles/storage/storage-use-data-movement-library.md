---
title: Transfer Data with the Microsoft Azure Storage Data Movement Library | Microsoft Docs
description: Use the Data Movement Library to move or copy data to or from blob and file content. Copy data to Azure Storage from local files, or copy data within or between storage accounts. Easily migrate your data to Azure Storage.
services: storage
documentationcenter: ''
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: ''
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 2ba94e4dd931b6d385101c7dadccfa3583b5296e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551879"
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="594fb-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span><span class="sxs-lookup"><span data-stu-id="594fb-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="594fb-106">Overview</span><span class="sxs-lookup"><span data-stu-id="594fb-106">Overview</span></span>
<span data-ttu-id="594fb-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span><span class="sxs-lookup"><span data-stu-id="594fb-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="594fb-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="594fb-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="594fb-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="594fb-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="594fb-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span><span class="sxs-lookup"><span data-stu-id="594fb-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="594fb-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span><span class="sxs-lookup"><span data-stu-id="594fb-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="594fb-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="594fb-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="594fb-113">This library also works for traditional .NET Framework apps for Windows.</span><span class="sxs-lookup"><span data-stu-id="594fb-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="594fb-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="594fb-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="594fb-115">Upload files and directories to Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="594fb-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="594fb-116">Define the number of parallel operations when transferring data.</span><span class="sxs-lookup"><span data-stu-id="594fb-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="594fb-117">Track data transfer progress.</span><span class="sxs-lookup"><span data-stu-id="594fb-117">Track data transfer progress.</span></span>
- <span data-ttu-id="594fb-118">Resume canceled data transfer.</span><span class="sxs-lookup"><span data-stu-id="594fb-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="594fb-119">Copy file from URL to Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="594fb-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="594fb-120">Copy from Blob Storage to Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="594fb-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="594fb-121">**What you need:**</span><span class="sxs-lookup"><span data-stu-id="594fb-121">**What you need:**</span></span>

* [<span data-ttu-id="594fb-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="594fb-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="594fb-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="594fb-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="594fb-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="594fb-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="594fb-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span><span class="sxs-lookup"><span data-stu-id="594fb-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="594fb-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span><span class="sxs-lookup"><span data-stu-id="594fb-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="594fb-127">Setup</span><span class="sxs-lookup"><span data-stu-id="594fb-127">Setup</span></span>  

1. <span data-ttu-id="594fb-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span><span class="sxs-lookup"><span data-stu-id="594fb-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="594fb-129">When selecting your environment, choose the command-line option.</span><span class="sxs-lookup"><span data-stu-id="594fb-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="594fb-130">From the command line, create a directory for your project.</span><span class="sxs-lookup"><span data-stu-id="594fb-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="594fb-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span><span class="sxs-lookup"><span data-stu-id="594fb-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="594fb-132">Open this directory in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="594fb-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="594fb-133">This step can be quickly done via the command line by typing `code .`.</span><span class="sxs-lookup"><span data-stu-id="594fb-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="594fb-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="594fb-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="594fb-135">Restart Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="594fb-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="594fb-136">At this point, you should see two prompts.</span><span class="sxs-lookup"><span data-stu-id="594fb-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="594fb-137">One is for adding "required assets to build and debug."</span><span class="sxs-lookup"><span data-stu-id="594fb-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="594fb-138">Click "yes."</span><span class="sxs-lookup"><span data-stu-id="594fb-138">Click "yes."</span></span> <span data-ttu-id="594fb-139">Another prompt is for restoring unresolved dependencies.</span><span class="sxs-lookup"><span data-stu-id="594fb-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="594fb-140">Click "restore."</span><span class="sxs-lookup"><span data-stu-id="594fb-140">Click "restore."</span></span>
6. <span data-ttu-id="594fb-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span><span class="sxs-lookup"><span data-stu-id="594fb-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="594fb-142">In this file, change the `externalConsole` value to `true`.</span><span class="sxs-lookup"><span data-stu-id="594fb-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="594fb-143">Visual Studio Code allows you to debug .NET Core applications.</span><span class="sxs-lookup"><span data-stu-id="594fb-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="594fb-144">Hit `F5` to run your application and verify that your setup is working.</span><span class="sxs-lookup"><span data-stu-id="594fb-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="594fb-145">You should see "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="594fb-145">You should see "Hello World!"</span></span> <span data-ttu-id="594fb-146">printed to the console.</span><span class="sxs-lookup"><span data-stu-id="594fb-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="594fb-147">Add Data Movement Library to your project</span><span class="sxs-lookup"><span data-stu-id="594fb-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="594fb-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span><span class="sxs-lookup"><span data-stu-id="594fb-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="594fb-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="594fb-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="594fb-150">Add `"portable-net45+win8"` to the `imports` section.</span><span class="sxs-lookup"><span data-stu-id="594fb-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="594fb-151">A prompt should display to restore your project.</span><span class="sxs-lookup"><span data-stu-id="594fb-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="594fb-152">Click the "restore" button.</span><span class="sxs-lookup"><span data-stu-id="594fb-152">Click the "restore" button.</span></span> <span data-ttu-id="594fb-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span><span class="sxs-lookup"><span data-stu-id="594fb-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="594fb-154">Modify `project.json`:</span><span class="sxs-lookup"><span data-stu-id="594fb-154">Modify `project.json`:</span></span>

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="594fb-155">Set up the skeleton of your application</span><span class="sxs-lookup"><span data-stu-id="594fb-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="594fb-156">The first thing we do is set up the "skeleton" code of our application.</span><span class="sxs-lookup"><span data-stu-id="594fb-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="594fb-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span><span class="sxs-lookup"><span data-stu-id="594fb-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="594fb-158">This object is used to interact with our Storage account in all transfer scenarios.</span><span class="sxs-lookup"><span data-stu-id="594fb-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="594fb-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span><span class="sxs-lookup"><span data-stu-id="594fb-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="594fb-160">Modify `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="594fb-160">Modify `Program.cs`:</span></span>

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="594fb-161">Transfer local file to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="594fb-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="594fb-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="594fb-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

<span data-ttu-id="594fb-163">Modify the `TransferLocalFileToAzureBlob` method:</span><span class="sxs-lookup"><span data-stu-id="594fb-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="594fb-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span><span class="sxs-lookup"><span data-stu-id="594fb-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="594fb-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span><span class="sxs-lookup"><span data-stu-id="594fb-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="594fb-166">Hit `F5` to run your application.</span><span class="sxs-lookup"><span data-stu-id="594fb-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="594fb-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="594fb-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="594fb-168">Set number of parallel operations</span><span class="sxs-lookup"><span data-stu-id="594fb-168">Set number of parallel operations</span></span>
<span data-ttu-id="594fb-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span><span class="sxs-lookup"><span data-stu-id="594fb-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="594fb-170">By default, the Data Movement Library sets the number of parallel operations to 8 \* the number of cores on your machine.</span><span class="sxs-lookup"><span data-stu-id="594fb-170">By default, the Data Movement Library sets the number of parallel operations to 8 \* the number of cores on your machine.</span></span> 

<span data-ttu-id="594fb-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span><span class="sxs-lookup"><span data-stu-id="594fb-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="594fb-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span><span class="sxs-lookup"><span data-stu-id="594fb-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="594fb-173">Let's add some code that allows us to set the number of parallel operations.</span><span class="sxs-lookup"><span data-stu-id="594fb-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="594fb-174">Let's also add code that times how long it takes for the transfer to complete.</span><span class="sxs-lookup"><span data-stu-id="594fb-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="594fb-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="594fb-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="594fb-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="594fb-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

<span data-ttu-id="594fb-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span><span class="sxs-lookup"><span data-stu-id="594fb-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a><span data-ttu-id="594fb-178">Track transfer progress</span><span class="sxs-lookup"><span data-stu-id="594fb-178">Track transfer progress</span></span>
<span data-ttu-id="594fb-179">Knowing how long it took for our data to transfer is great.</span><span class="sxs-lookup"><span data-stu-id="594fb-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="594fb-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span><span class="sxs-lookup"><span data-stu-id="594fb-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="594fb-181">To achieve this scenario, we need to create a `TransferContext` object.</span><span class="sxs-lookup"><span data-stu-id="594fb-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="594fb-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="594fb-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="594fb-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span><span class="sxs-lookup"><span data-stu-id="594fb-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="594fb-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="594fb-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

<span data-ttu-id="594fb-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="594fb-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="594fb-186">Resume a canceled transfer</span><span class="sxs-lookup"><span data-stu-id="594fb-186">Resume a canceled transfer</span></span>
<span data-ttu-id="594fb-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span><span class="sxs-lookup"><span data-stu-id="594fb-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="594fb-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span><span class="sxs-lookup"><span data-stu-id="594fb-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="594fb-189">Modify `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="594fb-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="594fb-190">Up until now, our `checkpoint` value has always been set to `null`.</span><span class="sxs-lookup"><span data-stu-id="594fb-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="594fb-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span><span class="sxs-lookup"><span data-stu-id="594fb-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="594fb-192">Transfer local directory to Azure Blob directory</span><span class="sxs-lookup"><span data-stu-id="594fb-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="594fb-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span><span class="sxs-lookup"><span data-stu-id="594fb-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="594fb-194">Luckily, this is not the case.</span><span class="sxs-lookup"><span data-stu-id="594fb-194">Luckily, this is not the case.</span></span> <span data-ttu-id="594fb-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span><span class="sxs-lookup"><span data-stu-id="594fb-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="594fb-196">Let's add some code that allows us to do just that.</span><span class="sxs-lookup"><span data-stu-id="594fb-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="594fb-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="594fb-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

<span data-ttu-id="594fb-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="594fb-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="594fb-199">There are a few differences between this method and the method for uploading a single file.</span><span class="sxs-lookup"><span data-stu-id="594fb-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="594fb-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span><span class="sxs-lookup"><span data-stu-id="594fb-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="594fb-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span><span class="sxs-lookup"><span data-stu-id="594fb-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="594fb-202">Copy file from URL to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="594fb-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="594fb-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="594fb-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="594fb-204">Modify `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="594fb-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="594fb-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span><span class="sxs-lookup"><span data-stu-id="594fb-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="594fb-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span><span class="sxs-lookup"><span data-stu-id="594fb-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="594fb-207">This method also introduces a new boolean parameter.</span><span class="sxs-lookup"><span data-stu-id="594fb-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="594fb-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span><span class="sxs-lookup"><span data-stu-id="594fb-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="594fb-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="594fb-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="594fb-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span><span class="sxs-lookup"><span data-stu-id="594fb-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="594fb-211">Transfer Azure Blob to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="594fb-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="594fb-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span><span class="sxs-lookup"><span data-stu-id="594fb-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="594fb-213">Modify `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="594fb-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="594fb-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span><span class="sxs-lookup"><span data-stu-id="594fb-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="594fb-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="594fb-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="594fb-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span><span class="sxs-lookup"><span data-stu-id="594fb-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="594fb-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span><span class="sxs-lookup"><span data-stu-id="594fb-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="594fb-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span><span class="sxs-lookup"><span data-stu-id="594fb-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="594fb-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span><span class="sxs-lookup"><span data-stu-id="594fb-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="594fb-220">Conclusion</span><span class="sxs-lookup"><span data-stu-id="594fb-220">Conclusion</span></span>
<span data-ttu-id="594fb-221">Our data movement application is now complete.</span><span class="sxs-lookup"><span data-stu-id="594fb-221">Our data movement application is now complete.</span></span> <span data-ttu-id="594fb-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="594fb-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="594fb-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="594fb-223">Next steps</span></span>
<span data-ttu-id="594fb-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="594fb-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="594fb-225">This getting started focused on Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="594fb-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="594fb-226">However, this same knowledge can be applied to File Storage.</span><span class="sxs-lookup"><span data-stu-id="594fb-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="594fb-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="594fb-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




