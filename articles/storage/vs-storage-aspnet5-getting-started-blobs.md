---
title: Get started with blob storage and Visual Studio connected services (ASP.NET Core) | Microsoft Docs
description: How to get started using Azure Blob storage in a Visual Studio ASP.NET Core project after you have created a storage account using Visual Studio connected services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e725015c8be7ecfa908f0ae75986b73f218fa3ae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549653"
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="d724a-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="d724a-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d724a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d724a-104">Overview</span></span>
<span data-ttu-id="d724a-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span><span class="sxs-lookup"><span data-stu-id="d724a-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="d724a-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d724a-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="d724a-107">A single blob can be any size.</span><span class="sxs-lookup"><span data-stu-id="d724a-107">A single blob can be any size.</span></span> <span data-ttu-id="d724a-108">Blobs can be things like images, audio and video files, raw data, and document files.</span><span class="sxs-lookup"><span data-stu-id="d724a-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="d724a-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span><span class="sxs-lookup"><span data-stu-id="d724a-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="d724a-110">Just as files live in folders, storage blobs live in containers.</span><span class="sxs-lookup"><span data-stu-id="d724a-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="d724a-111">After you have created a storage, you create one or more containers in the storage.</span><span class="sxs-lookup"><span data-stu-id="d724a-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="d724a-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span><span class="sxs-lookup"><span data-stu-id="d724a-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="d724a-113">After you create the containers, you can upload individual blob files to them.</span><span class="sxs-lookup"><span data-stu-id="d724a-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="d724a-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span><span class="sxs-lookup"><span data-stu-id="d724a-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="d724a-115">Access blob containers in code</span><span class="sxs-lookup"><span data-stu-id="d724a-115">Access blob containers in code</span></span>
<span data-ttu-id="d724a-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span><span class="sxs-lookup"><span data-stu-id="d724a-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="d724a-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span><span class="sxs-lookup"><span data-stu-id="d724a-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="d724a-118">Get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="d724a-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d724a-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span><span class="sxs-lookup"><span data-stu-id="d724a-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="d724a-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span><span class="sxs-lookup"><span data-stu-id="d724a-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="d724a-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="d724a-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="d724a-122">Create a container in code</span><span class="sxs-lookup"><span data-stu-id="d724a-122">Create a container in code</span></span>
<span data-ttu-id="d724a-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="d724a-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="d724a-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span><span class="sxs-lookup"><span data-stu-id="d724a-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="d724a-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span><span class="sxs-lookup"><span data-stu-id="d724a-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="d724a-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="d724a-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="d724a-127">The code below assumes async programming methods are being used.</span><span class="sxs-lookup"><span data-stu-id="d724a-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="d724a-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span><span class="sxs-lookup"><span data-stu-id="d724a-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d724a-129">Upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="d724a-129">Upload a blob into a container</span></span>
<span data-ttu-id="d724a-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span><span class="sxs-lookup"><span data-stu-id="d724a-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="d724a-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span><span class="sxs-lookup"><span data-stu-id="d724a-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="d724a-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span><span class="sxs-lookup"><span data-stu-id="d724a-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="d724a-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span><span class="sxs-lookup"><span data-stu-id="d724a-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="d724a-134">List the blobs in a container</span><span class="sxs-lookup"><span data-stu-id="d724a-134">List the blobs in a container</span></span>
<span data-ttu-id="d724a-135">To list the blobs in a container, first get a container reference.</span><span class="sxs-lookup"><span data-stu-id="d724a-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="d724a-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span><span class="sxs-lookup"><span data-stu-id="d724a-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="d724a-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span><span class="sxs-lookup"><span data-stu-id="d724a-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="d724a-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span><span class="sxs-lookup"><span data-stu-id="d724a-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="d724a-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span><span class="sxs-lookup"><span data-stu-id="d724a-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
        {
            if (item.GetType() == typeof(CloudBlockBlob))
            {
                CloudBlockBlob blob = (CloudBlockBlob)item;
                Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);
            }

            else if (item.GetType() == typeof(CloudPageBlob))
            {
                CloudPageBlob pageBlob = (CloudPageBlob)item;

                Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);
            }

            else if (item.GetType() == typeof(CloudBlobDirectory))
            {
                CloudBlobDirectory directory = (CloudBlobDirectory)item;

                Console.WriteLine("Directory: {0}", directory.Uri);
            }
        }
    } while (token != null);

<span data-ttu-id="d724a-140">There are others ways to list the contents of a blob container.</span><span class="sxs-lookup"><span data-stu-id="d724a-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="d724a-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span><span class="sxs-lookup"><span data-stu-id="d724a-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="d724a-142">Download a blob</span><span class="sxs-lookup"><span data-stu-id="d724a-142">Download a blob</span></span>
<span data-ttu-id="d724a-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span><span class="sxs-lookup"><span data-stu-id="d724a-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="d724a-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span><span class="sxs-lookup"><span data-stu-id="d724a-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="d724a-145">There are other ways to save blobs as files.</span><span class="sxs-lookup"><span data-stu-id="d724a-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="d724a-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span><span class="sxs-lookup"><span data-stu-id="d724a-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="d724a-147">Delete a blob</span><span class="sxs-lookup"><span data-stu-id="d724a-147">Delete a blob</span></span>
<span data-ttu-id="d724a-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span><span class="sxs-lookup"><span data-stu-id="d724a-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="d724a-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="d724a-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

