---
title: How to use blob storage (object storage) from C++ | Microsoft Docs
description: Store unstructured data in the cloud with Azure Blob storage (object storage).
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: b2cbb5c0c5d4ba28e492202050b5325d1d374a0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540914"
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="54dc9-103">How to use Blob Storage from C++</span><span class="sxs-lookup"><span data-stu-id="54dc9-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="54dc9-104">Overview</span><span class="sxs-lookup"><span data-stu-id="54dc9-104">Overview</span></span>
<span data-ttu-id="54dc9-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span><span class="sxs-lookup"><span data-stu-id="54dc9-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="54dc9-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span><span class="sxs-lookup"><span data-stu-id="54dc9-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="54dc9-107">Blob storage is also referred to as object storage.</span><span class="sxs-lookup"><span data-stu-id="54dc9-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="54dc9-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span><span class="sxs-lookup"><span data-stu-id="54dc9-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="54dc9-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="54dc9-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="54dc9-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span><span class="sxs-lookup"><span data-stu-id="54dc9-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="54dc9-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span><span class="sxs-lookup"><span data-stu-id="54dc9-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="54dc9-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="54dc9-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="54dc9-113">Create a C++ application</span><span class="sxs-lookup"><span data-stu-id="54dc9-113">Create a C++ application</span></span>
<span data-ttu-id="54dc9-114">In this guide, you will use storage features which can be run within a C++ application.</span><span class="sxs-lookup"><span data-stu-id="54dc9-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="54dc9-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="54dc9-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="54dc9-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span><span class="sxs-lookup"><span data-stu-id="54dc9-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="54dc9-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span><span class="sxs-lookup"><span data-stu-id="54dc9-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="54dc9-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="54dc9-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="54dc9-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="54dc9-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="54dc9-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="54dc9-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="54dc9-121">Configure your application to access Blob Storage</span><span class="sxs-lookup"><span data-stu-id="54dc9-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="54dc9-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span><span class="sxs-lookup"><span data-stu-id="54dc9-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
include <was/storage_account.h>
include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="54dc9-123">Setup an Azure storage connection string</span><span class="sxs-lookup"><span data-stu-id="54dc9-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="54dc9-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span><span class="sxs-lookup"><span data-stu-id="54dc9-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="54dc9-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span><span class="sxs-lookup"><span data-stu-id="54dc9-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="54dc9-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="54dc9-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="54dc9-127">This example shows how you can declare a static field to hold the connection string:</span><span class="sxs-lookup"><span data-stu-id="54dc9-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="54dc9-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="54dc9-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="54dc9-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span><span class="sxs-lookup"><span data-stu-id="54dc9-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="54dc9-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span><span class="sxs-lookup"><span data-stu-id="54dc9-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="54dc9-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span><span class="sxs-lookup"><span data-stu-id="54dc9-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="54dc9-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span><span class="sxs-lookup"><span data-stu-id="54dc9-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="54dc9-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span><span class="sxs-lookup"><span data-stu-id="54dc9-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="54dc9-134">Retrieve your connection string</span><span class="sxs-lookup"><span data-stu-id="54dc9-134">Retrieve your connection string</span></span>
<span data-ttu-id="54dc9-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span><span class="sxs-lookup"><span data-stu-id="54dc9-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="54dc9-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span><span class="sxs-lookup"><span data-stu-id="54dc9-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="54dc9-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span><span class="sxs-lookup"><span data-stu-id="54dc9-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="54dc9-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span><span class="sxs-lookup"><span data-stu-id="54dc9-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="54dc9-139">How to: Create a container</span><span class="sxs-lookup"><span data-stu-id="54dc9-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="54dc9-140">This example shows how to create a container if it does not already exist:</span><span class="sxs-lookup"><span data-stu-id="54dc9-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="54dc9-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span><span class="sxs-lookup"><span data-stu-id="54dc9-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="54dc9-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span><span class="sxs-lookup"><span data-stu-id="54dc9-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="54dc9-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span><span class="sxs-lookup"><span data-stu-id="54dc9-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="54dc9-144">How to: Upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="54dc9-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="54dc9-145">Azure Blob Storage supports block blobs and page blobs.</span><span class="sxs-lookup"><span data-stu-id="54dc9-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="54dc9-146">In the majority of cases, block blob is the recommended type to use.</span><span class="sxs-lookup"><span data-stu-id="54dc9-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="54dc9-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span><span class="sxs-lookup"><span data-stu-id="54dc9-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="54dc9-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span><span class="sxs-lookup"><span data-stu-id="54dc9-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="54dc9-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span><span class="sxs-lookup"><span data-stu-id="54dc9-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="54dc9-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span><span class="sxs-lookup"><span data-stu-id="54dc9-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="54dc9-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span><span class="sxs-lookup"><span data-stu-id="54dc9-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="54dc9-152">How to: List the blobs in a container</span><span class="sxs-lookup"><span data-stu-id="54dc9-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="54dc9-153">To list the blobs in a container, first get a container reference.</span><span class="sxs-lookup"><span data-stu-id="54dc9-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="54dc9-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span><span class="sxs-lookup"><span data-stu-id="54dc9-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="54dc9-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span><span class="sxs-lookup"><span data-stu-id="54dc9-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="54dc9-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span><span class="sxs-lookup"><span data-stu-id="54dc9-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="54dc9-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="54dc9-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="54dc9-158">How to: Download blobs</span><span class="sxs-lookup"><span data-stu-id="54dc9-158">How to: Download blobs</span></span>
<span data-ttu-id="54dc9-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span><span class="sxs-lookup"><span data-stu-id="54dc9-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="54dc9-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span><span class="sxs-lookup"><span data-stu-id="54dc9-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="54dc9-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span><span class="sxs-lookup"><span data-stu-id="54dc9-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="54dc9-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span><span class="sxs-lookup"><span data-stu-id="54dc9-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="54dc9-163">How to: Delete blobs</span><span class="sxs-lookup"><span data-stu-id="54dc9-163">How to: Delete blobs</span></span>
<span data-ttu-id="54dc9-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span><span class="sxs-lookup"><span data-stu-id="54dc9-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="54dc9-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="54dc9-165">Next steps</span></span>
<span data-ttu-id="54dc9-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="54dc9-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="54dc9-167">How to use Queue Storage from C++</span><span class="sxs-lookup"><span data-stu-id="54dc9-167">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="54dc9-168">How to use Table Storage from C++</span><span class="sxs-lookup"><span data-stu-id="54dc9-168">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="54dc9-169">List Azure Storage Resources in C++</span><span class="sxs-lookup"><span data-stu-id="54dc9-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="54dc9-170">Storage Client Library for C++ Reference</span><span class="sxs-lookup"><span data-stu-id="54dc9-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="54dc9-171">Azure Storage Documentation</span><span class="sxs-lookup"><span data-stu-id="54dc9-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="54dc9-172">Transfer data with the AzCopy command-line utility</span><span class="sxs-lookup"><span data-stu-id="54dc9-172">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)

