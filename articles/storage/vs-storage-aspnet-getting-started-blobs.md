---
title: Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET) | Microsoft Docs
description: How to get started using Azure blob storage in an ASP.NET project in Visual Studio after connecting to a storage account using Visual Studio Connected Services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: 46c8b57acaa4689b979887fe43d091eca40b0659
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662253"
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="7eca2-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7eca2-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="7eca2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7eca2-104">Overview</span></span>

<span data-ttu-id="7eca2-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span><span class="sxs-lookup"><span data-stu-id="7eca2-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="7eca2-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span><span class="sxs-lookup"><span data-stu-id="7eca2-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="7eca2-107">Blob storage is also referred to as object storage.</span><span class="sxs-lookup"><span data-stu-id="7eca2-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="7eca2-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="7eca2-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="7eca2-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span><span class="sxs-lookup"><span data-stu-id="7eca2-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="7eca2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7eca2-110">Prerequisites</span></span>

* [<span data-ttu-id="7eca2-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7eca2-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/visual-studio-homepage-vs.aspx)
* [<span data-ttu-id="7eca2-112">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="7eca2-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="7eca2-113">Create an MVC controller</span><span class="sxs-lookup"><span data-stu-id="7eca2-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="7eca2-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Add a controller to an ASP.NET MVC app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="7eca2-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specify MVC controller type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="7eca2-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span></span>

    ![Name the MVC controller](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="7eca2-120">Add the following *using* directives to the `BlobsController.cs` file:</span><span class="sxs-lookup"><span data-stu-id="7eca2-120">Add the following *using* directives to the `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="7eca2-121">Create a blob container</span><span class="sxs-lookup"><span data-stu-id="7eca2-121">Create a blob container</span></span>

<span data-ttu-id="7eca2-122">A blob container is a nested hierarchy of blobs and folders.</span><span class="sxs-lookup"><span data-stu-id="7eca2-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="7eca2-123">The following steps illustrate how to create a blob container:</span><span class="sxs-lookup"><span data-stu-id="7eca2-123">The following steps illustrate how to create a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="7eca2-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="7eca2-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="7eca2-125">Open the `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7eca2-125">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="7eca2-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="7eca2-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="7eca2-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7eca2-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span><span class="sxs-lookup"><span data-stu-id="7eca2-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span> <span data-ttu-id="7eca2-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="7eca2-130">Get a **CloudBlobClient** object represents a blob service client.</span><span class="sxs-lookup"><span data-stu-id="7eca2-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="7eca2-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span><span class="sxs-lookup"><span data-stu-id="7eca2-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span></span> <span data-ttu-id="7eca2-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span><span class="sxs-lookup"><span data-stu-id="7eca2-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="7eca2-133">The reference is returned whether or not the blob container exists.</span><span class="sxs-lookup"><span data-stu-id="7eca2-133">The reference is returned whether or not the blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="7eca2-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span><span class="sxs-lookup"><span data-stu-id="7eca2-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span></span> <span data-ttu-id="7eca2-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span><span class="sxs-lookup"><span data-stu-id="7eca2-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span></span> <span data-ttu-id="7eca2-136">Otherwise, **false** is returned.</span><span class="sxs-lookup"><span data-stu-id="7eca2-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="7eca2-137">Update the **ViewBag** with the name of the blob container.</span><span class="sxs-lookup"><span data-stu-id="7eca2-137">Update the **ViewBag** with the name of the blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="7eca2-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7eca2-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="7eca2-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="7eca2-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="7eca2-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7eca2-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7eca2-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7eca2-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="7eca2-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="7eca2-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span></span>
  
    ![Create blob container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="7eca2-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span><span class="sxs-lookup"><span data-stu-id="7eca2-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span></span> <span data-ttu-id="7eca2-146">Therefore, if you run the app when the container exists, the method returns **false**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-146">Therefore, if you run the app when the container exists, the method returns **false**.</span></span> <span data-ttu-id="7eca2-147">To run the app multiple times, you must delete the container before running the app again.</span><span class="sxs-lookup"><span data-stu-id="7eca2-147">To run the app multiple times, you must delete the container before running the app again.</span></span> <span data-ttu-id="7eca2-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span><span class="sxs-lookup"><span data-stu-id="7eca2-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="7eca2-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="7eca2-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="7eca2-150">Upload a blob into a blob container</span><span class="sxs-lookup"><span data-stu-id="7eca2-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="7eca2-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span><span class="sxs-lookup"><span data-stu-id="7eca2-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="7eca2-152">This section walks you through uploading a local file to a blob container.</span><span class="sxs-lookup"><span data-stu-id="7eca2-152">This section walks you through uploading a local file to a blob container.</span></span> <span data-ttu-id="7eca2-153">The steps assume you've created a blob container named *test-blob-container*.</span><span class="sxs-lookup"><span data-stu-id="7eca2-153">The steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="7eca2-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="7eca2-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="7eca2-155">Open the `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7eca2-155">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="7eca2-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="7eca2-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="7eca2-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7eca2-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="7eca2-159">Get a **CloudBlobClient** object represents a blob service client.</span><span class="sxs-lookup"><span data-stu-id="7eca2-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="7eca2-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span><span class="sxs-lookup"><span data-stu-id="7eca2-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="7eca2-161">As explained earlier, Azure storage supports different blob types.</span><span class="sxs-lookup"><span data-stu-id="7eca2-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="7eca2-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span><span class="sxs-lookup"><span data-stu-id="7eca2-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="7eca2-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span><span class="sxs-lookup"><span data-stu-id="7eca2-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="7eca2-164">Usually, block blob is the recommended type to use.</span><span class="sxs-lookup"><span data-stu-id="7eca2-164">Usually, block blob is the recommended type to use.</span></span> <span data-ttu-id="7eca2-165">(Change <blob-name>\* to the name you want to give the blob once uploaded.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-165">(Change <blob-name>\* to the name you want to give the blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="7eca2-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span><span class="sxs-lookup"><span data-stu-id="7eca2-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="7eca2-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span><span class="sxs-lookup"><span data-stu-id="7eca2-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="7eca2-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="7eca2-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7eca2-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7eca2-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7eca2-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7eca2-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="7eca2-172">Run the application, and select **Upload blob**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-172">Run the application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="7eca2-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span><span class="sxs-lookup"><span data-stu-id="7eca2-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span></span>    

## <a name="list-the-blobs-in-a-blob-container"></a><span data-ttu-id="7eca2-174">List the blobs in a blob container</span><span class="sxs-lookup"><span data-stu-id="7eca2-174">List the blobs in a blob container</span></span>

<span data-ttu-id="7eca2-175">This section illustrates how to list the blobs in a blob container.</span><span class="sxs-lookup"><span data-stu-id="7eca2-175">This section illustrates how to list the blobs in a blob container.</span></span> <span data-ttu-id="7eca2-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="7eca2-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="7eca2-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="7eca2-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="7eca2-178">Open the `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7eca2-178">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="7eca2-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="7eca2-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="7eca2-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7eca2-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="7eca2-182">Get a **CloudBlobClient** object represents a blob service client.</span><span class="sxs-lookup"><span data-stu-id="7eca2-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="7eca2-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span><span class="sxs-lookup"><span data-stu-id="7eca2-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="7eca2-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span><span class="sxs-lookup"><span data-stu-id="7eca2-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="7eca2-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span><span class="sxs-lookup"><span data-stu-id="7eca2-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="7eca2-186">The following code snippet enumerates all the blobs in a blob container.</span><span class="sxs-lookup"><span data-stu-id="7eca2-186">The following code snippet enumerates all the blobs in a blob container.</span></span> <span data-ttu-id="7eca2-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span><span class="sxs-lookup"><span data-stu-id="7eca2-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="7eca2-188">In addition to blobs, blob containers can contain directories.</span><span class="sxs-lookup"><span data-stu-id="7eca2-188">In addition to blobs, blob containers can contain directories.</span></span> <span data-ttu-id="7eca2-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span><span class="sxs-lookup"><span data-stu-id="7eca2-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="7eca2-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7eca2-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="7eca2-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="7eca2-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="7eca2-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span><span class="sxs-lookup"><span data-stu-id="7eca2-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="7eca2-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span><span class="sxs-lookup"><span data-stu-id="7eca2-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="7eca2-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7eca2-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="7eca2-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="7eca2-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="7eca2-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7eca2-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7eca2-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7eca2-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="7eca2-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="7eca2-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span></span>
  
    ![Blob listing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="7eca2-201">Download blobs</span><span class="sxs-lookup"><span data-stu-id="7eca2-201">Download blobs</span></span>

<span data-ttu-id="7eca2-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span><span class="sxs-lookup"><span data-stu-id="7eca2-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span></span> <span data-ttu-id="7eca2-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="7eca2-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="7eca2-204">Open the `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7eca2-204">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="7eca2-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="7eca2-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="7eca2-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7eca2-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="7eca2-208">Get a **CloudBlobClient** object represents a blob service client.</span><span class="sxs-lookup"><span data-stu-id="7eca2-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="7eca2-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span><span class="sxs-lookup"><span data-stu-id="7eca2-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="7eca2-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span><span class="sxs-lookup"><span data-stu-id="7eca2-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="7eca2-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="7eca2-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span><span class="sxs-lookup"><span data-stu-id="7eca2-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span></span> <span data-ttu-id="7eca2-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="7eca2-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7eca2-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7eca2-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7eca2-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="7eca2-216">Run the application, and select **Download blob** to download the blob.</span><span class="sxs-lookup"><span data-stu-id="7eca2-216">Run the application, and select **Download blob** to download the blob.</span></span> <span data-ttu-id="7eca2-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span><span class="sxs-lookup"><span data-stu-id="7eca2-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="7eca2-218">Delete blobs</span><span class="sxs-lookup"><span data-stu-id="7eca2-218">Delete blobs</span></span>

<span data-ttu-id="7eca2-219">The following steps illustrate how to delete a blob:</span><span class="sxs-lookup"><span data-stu-id="7eca2-219">The following steps illustrate how to delete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="7eca2-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="7eca2-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="7eca2-221">Open the `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7eca2-221">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="7eca2-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7eca2-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="7eca2-223">Get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="7eca2-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7eca2-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="7eca2-225">Get a **CloudBlobClient** object represents a blob service client.</span><span class="sxs-lookup"><span data-stu-id="7eca2-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="7eca2-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span><span class="sxs-lookup"><span data-stu-id="7eca2-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="7eca2-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span><span class="sxs-lookup"><span data-stu-id="7eca2-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="7eca2-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span><span class="sxs-lookup"><span data-stu-id="7eca2-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. To delete a blob, use the **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="7eca2-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7eca2-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7eca2-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7eca2-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="7eca2-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span><span class="sxs-lookup"><span data-stu-id="7eca2-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7eca2-232">Next steps</span><span class="sxs-lookup"><span data-stu-id="7eca2-232">Next steps</span></span>
<span data-ttu-id="7eca2-233">View more feature guides to learn about additional options for storing data in Azure.</span><span class="sxs-lookup"><span data-stu-id="7eca2-233">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="7eca2-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7eca2-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="7eca2-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7eca2-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)




