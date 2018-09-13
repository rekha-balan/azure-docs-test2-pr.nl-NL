---
title: How to use Azure Blob storage (object storage) from Python | Microsoft Docs
description: Store unstructured data in the cloud with Azure Blob storage (object storage).
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 968814db9496fd410162d482191592c8a56101f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549741"
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="d3cb1-103">How to use Azure Blob storage from Python</span><span class="sxs-lookup"><span data-stu-id="d3cb1-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d3cb1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d3cb1-104">Overview</span></span>
<span data-ttu-id="d3cb1-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="d3cb1-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="d3cb1-107">Blob storage is also referred to as object storage.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="d3cb1-108">This article will show you how to perform common scenarios using Blob storage.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="d3cb1-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span><span class="sxs-lookup"><span data-stu-id="d3cb1-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="d3cb1-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="d3cb1-111">Create a container</span><span class="sxs-lookup"><span data-stu-id="d3cb1-111">Create a container</span></span>
<span data-ttu-id="d3cb1-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="d3cb1-113">The following code uses a **BlockBlobService** object.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="d3cb1-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="d3cb1-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="d3cb1-116">Replace 'myaccount' and 'mykey' with your account name and key.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="d3cb1-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="d3cb1-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="d3cb1-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="d3cb1-120">Alternatively, you can modify a container after you have created it using the following code.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="d3cb1-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d3cb1-122">Upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="d3cb1-122">Upload a blob into a container</span></span>
<span data-ttu-id="d3cb1-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="d3cb1-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="d3cb1-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="d3cb1-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span><span class="sxs-lookup"><span data-stu-id="d3cb1-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="d3cb1-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="d3cb1-128">List the blobs in a container</span><span class="sxs-lookup"><span data-stu-id="d3cb1-128">List the blobs in a container</span></span>
<span data-ttu-id="d3cb1-129">To list the blobs in a container, use the **list\_blobs** method.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="d3cb1-130">This method returns a generator.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-130">This method returns a generator.</span></span> <span data-ttu-id="d3cb1-131">The following code outputs the **name** of each blob in a container to the console.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="d3cb1-132">Download blobs</span><span class="sxs-lookup"><span data-stu-id="d3cb1-132">Download blobs</span></span>
<span data-ttu-id="d3cb1-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="d3cb1-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="d3cb1-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="d3cb1-136">Delete a blob</span><span class="sxs-lookup"><span data-stu-id="d3cb1-136">Delete a blob</span></span>
<span data-ttu-id="d3cb1-137">Finally, to delete a blob, call **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="d3cb1-138">Writing to an append blob</span><span class="sxs-lookup"><span data-stu-id="d3cb1-138">Writing to an append blob</span></span>
<span data-ttu-id="d3cb1-139">An append blob is optimized for append operations, such as logging.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="d3cb1-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="d3cb1-141">You cannot update or delete an existing block in an append blob.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="d3cb1-142">The block IDs for an append blob are not exposed as they are for a block blob.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="d3cb1-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="d3cb1-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span><span class="sxs-lookup"><span data-stu-id="d3cb1-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="d3cb1-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="d3cb1-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3cb1-146">Next steps</span></span>
<span data-ttu-id="d3cb1-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="d3cb1-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="d3cb1-148">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="d3cb1-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="d3cb1-149">Azure Storage Services REST API</span><span class="sxs-lookup"><span data-stu-id="d3cb1-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="d3cb1-150">[Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="d3cb1-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="d3cb1-151">[Microsoft Azure Storage SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="d3cb1-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python
