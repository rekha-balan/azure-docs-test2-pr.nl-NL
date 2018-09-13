---
title: How to use Azure File storage from Python | Microsoft Docs
description: Learn how to use the Azure File storage from Python to upload, list, download, and delete files.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 6dc82721d2b14dc489e9fce493f54337829af7fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552757"
---
# <a name="how-to-use-azure-file-storage-from-python"></a><span data-ttu-id="bccba-103">How to use Azure File storage from Python</span><span class="sxs-lookup"><span data-stu-id="bccba-103">How to use Azure File storage from Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="overview"></a><span data-ttu-id="bccba-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bccba-104">Overview</span></span>
<span data-ttu-id="bccba-105">This article will show you how to perform common scenarios using File storage.</span><span class="sxs-lookup"><span data-stu-id="bccba-105">This article will show you how to perform common scenarios using File storage.</span></span> <span data-ttu-id="bccba-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span><span class="sxs-lookup"><span data-stu-id="bccba-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="bccba-107">The scenarios covered include uploading, listing, downloading, and deleting files.</span><span class="sxs-lookup"><span data-stu-id="bccba-107">The scenarios covered include uploading, listing, downloading, and deleting files.</span></span>

[!INCLUDE [storage-file-concepts-include](../../includes/storage-file-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-share"></a><span data-ttu-id="bccba-108">Create a share</span><span class="sxs-lookup"><span data-stu-id="bccba-108">Create a share</span></span>
<span data-ttu-id="bccba-109">The **FileService** object lets you work with shares, directories and files.</span><span class="sxs-lookup"><span data-stu-id="bccba-109">The **FileService** object lets you work with shares, directories and files.</span></span> <span data-ttu-id="bccba-110">The following code creates a **FileService** object.</span><span class="sxs-lookup"><span data-stu-id="bccba-110">The following code creates a **FileService** object.</span></span> <span data-ttu-id="bccba-111">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bccba-111">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

<span data-ttu-id="bccba-112">The following code creates a **FileService** object using the storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="bccba-112">The following code creates a **FileService** object using the storage account name and account key.</span></span>  <span data-ttu-id="bccba-113">Replace 'myaccount' and 'mykey' with your account name and key.</span><span class="sxs-lookup"><span data-stu-id="bccba-113">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
file_service = **FileService** (account_name='myaccount', account_key='mykey')
```

<span data-ttu-id="bccba-114">In the following code example, you can use a **FileService** object to create the share if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="bccba-114">In the following code example, you can use a **FileService** object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

## <a name="upload-a-file-into-a-share"></a><span data-ttu-id="bccba-115">Upload a file into a share</span><span class="sxs-lookup"><span data-stu-id="bccba-115">Upload a file into a share</span></span>
<span data-ttu-id="bccba-116">An Azure File Storage Share contains at the very least, a root directory where files can reside.</span><span class="sxs-lookup"><span data-stu-id="bccba-116">An Azure File Storage Share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="bccba-117">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span><span class="sxs-lookup"><span data-stu-id="bccba-117">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="bccba-118">To create a file and upload data, use the **create\_file\_from\_path**, **create\_file\_from\_stream**, **create\_file\_from\_bytes** or **create\_file\_from\_text** methods.</span><span class="sxs-lookup"><span data-stu-id="bccba-118">To create a file and upload data, use the **create\_file\_from\_path**, **create\_file\_from\_stream**, **create\_file\_from\_bytes** or **create\_file\_from\_text** methods.</span></span> <span data-ttu-id="bccba-119">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span><span class="sxs-lookup"><span data-stu-id="bccba-119">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="bccba-120">**create\_file\_from\_path** uploads the contents of a file from the specified path, and **create\_file\_from\_stream** uploads the contents from an already opened file/stream.</span><span class="sxs-lookup"><span data-stu-id="bccba-120">**create\_file\_from\_path** uploads the contents of a file from the specified path, and **create\_file\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="bccba-121">**create\_file\_from\_bytes** uploads an array of bytes, and **create\_file\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span><span class="sxs-lookup"><span data-stu-id="bccba-121">**create\_file\_from\_bytes** uploads an array of bytes, and **create\_file\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="bccba-122">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span><span class="sxs-lookup"><span data-stu-id="bccba-122">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

## <a name="how-to-create-a-directory"></a><span data-ttu-id="bccba-123">How to: Create a Directory</span><span class="sxs-lookup"><span data-stu-id="bccba-123">How to: Create a Directory</span></span>
<span data-ttu-id="bccba-124">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span><span class="sxs-lookup"><span data-stu-id="bccba-124">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="bccba-125">The Azure file storage service allows you to create as many directories as your account will allow.</span><span class="sxs-lookup"><span data-stu-id="bccba-125">The Azure file storage service allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="bccba-126">The code below will create a sub-directory named **sampledir** under the root directory.</span><span class="sxs-lookup"><span data-stu-id="bccba-126">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

## <a name="how-to-list-files-and-directories-in-a-share"></a><span data-ttu-id="bccba-127">How to: List files and directories in a share</span><span class="sxs-lookup"><span data-stu-id="bccba-127">How to: List files and directories in a share</span></span>
<span data-ttu-id="bccba-128">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span><span class="sxs-lookup"><span data-stu-id="bccba-128">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="bccba-129">This method returns a generator.</span><span class="sxs-lookup"><span data-stu-id="bccba-129">This method returns a generator.</span></span> <span data-ttu-id="bccba-130">The following code outputs the **name** of each file and directory in a share to the console.</span><span class="sxs-lookup"><span data-stu-id="bccba-130">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

## <a name="download-files"></a><span data-ttu-id="bccba-131">Download files</span><span class="sxs-lookup"><span data-stu-id="bccba-131">Download files</span></span>
<span data-ttu-id="bccba-132">To download data from a file, use **get\_file\_to\_path**, **get\_file\_to\_stream**, **get\_file\_to\_bytes**, or **get\_file\_to\_text**.</span><span class="sxs-lookup"><span data-stu-id="bccba-132">To download data from a file, use **get\_file\_to\_path**, **get\_file\_to\_stream**, **get\_file\_to\_bytes**, or **get\_file\_to\_text**.</span></span> <span data-ttu-id="bccba-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span><span class="sxs-lookup"><span data-stu-id="bccba-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="bccba-134">The following example demonstrates using **get\_file\_to\_path** to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span><span class="sxs-lookup"><span data-stu-id="bccba-134">The following example demonstrates using **get\_file\_to\_path** to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

## <a name="delete-a-file"></a><span data-ttu-id="bccba-135">Delete a file</span><span class="sxs-lookup"><span data-stu-id="bccba-135">Delete a file</span></span>
<span data-ttu-id="bccba-136">Finally, to delete a file, call **delete_file**.</span><span class="sxs-lookup"><span data-stu-id="bccba-136">Finally, to delete a file, call **delete_file**.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="bccba-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="bccba-137">Next steps</span></span>
<span data-ttu-id="bccba-138">Now that you've learned the basics of File storage, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="bccba-138">Now that you've learned the basics of File storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="bccba-139">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="bccba-139">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="bccba-140">Azure Storage Services REST API</span><span class="sxs-lookup"><span data-stu-id="bccba-140">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="bccba-141">[Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="bccba-141">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="bccba-142">[Microsoft Azure Storage SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="bccba-142">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python
