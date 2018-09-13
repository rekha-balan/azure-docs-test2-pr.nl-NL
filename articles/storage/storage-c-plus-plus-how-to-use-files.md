---
title: How to use File Storage from C++ | Microsoft Docs
description: Store file data in the cloud with Azure File storage.
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: f8ecb68fddf4293592e546c0c10d0c86664bd090
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563559"
---
# <a name="how-to-use-file-storage-from-c"></a><span data-ttu-id="e889c-103">How to use File Storage from C++</span><span class="sxs-lookup"><span data-stu-id="e889c-103">How to use File Storage from C++</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

[!INCLUDE [storage-file-overview-include](../../includes/storage-file-overview-include.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="e889c-104">About this tutorial</span><span class="sxs-lookup"><span data-stu-id="e889c-104">About this tutorial</span></span>
<span data-ttu-id="e889c-105">In this tutorial, you'll learn how to perform basic operations on the Microsoft Azure File storage service.</span><span class="sxs-lookup"><span data-stu-id="e889c-105">In this tutorial, you'll learn how to perform basic operations on the Microsoft Azure File storage service.</span></span> <span data-ttu-id="e889c-106">Through samples written in C++, you'll learn how to create shares and directories, upload, list, and delete files.</span><span class="sxs-lookup"><span data-stu-id="e889c-106">Through samples written in C++, you'll learn how to create shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="e889c-107">If you are new to Microsoft Azure's File Storage service, going through the concepts in the sections that follow will be helpful in understanding the samples.</span><span class="sxs-lookup"><span data-stu-id="e889c-107">If you are new to Microsoft Azure's File Storage service, going through the concepts in the sections that follow will be helpful in understanding the samples.</span></span>

[!INCLUDE [storage-file-concepts-include](../../includes/storage-file-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="e889c-108">Create a C++ application</span><span class="sxs-lookup"><span data-stu-id="e889c-108">Create a C++ application</span></span>
<span data-ttu-id="e889c-109">To build the samples, you will need to install the Azure Storage Client Library 2.4.0 for C++.</span><span class="sxs-lookup"><span data-stu-id="e889c-109">To build the samples, you will need to install the Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="e889c-110">You should also have created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="e889c-110">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="e889c-111">To install the Azure Storage Client 2.4.0 for C++, you can use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="e889c-111">To install the Azure Storage Client 2.4.0 for C++, you can use one of the following methods:</span></span>

* <span data-ttu-id="e889c-112">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span><span class="sxs-lookup"><span data-stu-id="e889c-112">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="e889c-113">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e889c-113">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="e889c-114">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e889c-114">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-to-use-file-storage"></a><span data-ttu-id="e889c-115">Set up your application to use File storage</span><span class="sxs-lookup"><span data-stu-id="e889c-115">Set up your application to use File storage</span></span>
<span data-ttu-id="e889c-116">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access files:</span><span class="sxs-lookup"><span data-stu-id="e889c-116">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access files:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e889c-117">Set up an Azure storage connection string</span><span class="sxs-lookup"><span data-stu-id="e889c-117">Set up an Azure storage connection string</span></span>
<span data-ttu-id="e889c-118">To use File storage, you need to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="e889c-118">To use File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="e889c-119">The first step would be to configure a connection string, which we'll use to connect to your storage account.</span><span class="sxs-lookup"><span data-stu-id="e889c-119">The first step would be to configure a connection string, which we'll use to connect to your storage account.</span></span> <span data-ttu-id="e889c-120">Let's define a static variable to do that.</span><span class="sxs-lookup"><span data-stu-id="e889c-120">Let's define a static variable to do that.</span></span>

```cpp
// Define the connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="e889c-121">Connecting to an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="e889c-121">Connecting to an Azure storage account</span></span>
<span data-ttu-id="e889c-122">You can use the **cloud_storage_account** class to represent your Storage Account information.</span><span class="sxs-lookup"><span data-stu-id="e889c-122">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="e889c-123">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span><span class="sxs-lookup"><span data-stu-id="e889c-123">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-share"></a><span data-ttu-id="e889c-124">How to: Create a Share</span><span class="sxs-lookup"><span data-stu-id="e889c-124">How to: Create a Share</span></span>
<span data-ttu-id="e889c-125">All files and directories in File storage reside in a container called a **Share**.</span><span class="sxs-lookup"><span data-stu-id="e889c-125">All files and directories in File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="e889c-126">Your storage account can have as many shares as your account capacity allows.</span><span class="sxs-lookup"><span data-stu-id="e889c-126">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="e889c-127">To obtain access to a share and its contents, you need to use a File storage client.</span><span class="sxs-lookup"><span data-stu-id="e889c-127">To obtain access to a share and its contents, you need to use a File storage client.</span></span>

```cpp
// Create the file storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="e889c-128">Using the File storage client, you can then obtain a reference to a share.</span><span class="sxs-lookup"><span data-stu-id="e889c-128">Using the File storage client, you can then obtain a reference to a share.</span></span>

```cpp
// Get a reference to the file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="e889c-129">To create the share, use the **create_if_not_exists** method of the **cloud_file_share** object.</span><span class="sxs-lookup"><span data-stu-id="e889c-129">To create the share, use the **create_if_not_exists** method of the **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="e889c-130">At this point, **share** holds a reference to a share named **my-sample-share**.</span><span class="sxs-lookup"><span data-stu-id="e889c-130">At this point, **share** holds a reference to a share named **my-sample-share**.</span></span>

## <a name="how-to-upload-a-file"></a><span data-ttu-id="e889c-131">How to: Upload a file</span><span class="sxs-lookup"><span data-stu-id="e889c-131">How to: Upload a file</span></span>
<span data-ttu-id="e889c-132">At the very least, an Azure File Storage Share contains a root directory where files can reside.</span><span class="sxs-lookup"><span data-stu-id="e889c-132">At the very least, an Azure File Storage Share contains a root directory where files can reside.</span></span> <span data-ttu-id="e889c-133">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span><span class="sxs-lookup"><span data-stu-id="e889c-133">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="e889c-134">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span><span class="sxs-lookup"><span data-stu-id="e889c-134">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="e889c-135">You do this by calling the **get_root_directory_reference** method of the share object.</span><span class="sxs-lookup"><span data-stu-id="e889c-135">You do this by calling the **get_root_directory_reference** method of the share object.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="e889c-136">Now that you have a reference to the root directory of the share, you can upload a file onto it.</span><span class="sxs-lookup"><span data-stu-id="e889c-136">Now that you have a reference to the root directory of the share, you can upload a file onto it.</span></span> <span data-ttu-id="e889c-137">This example uploads from a file, from text, and from a stream.</span><span class="sxs-lookup"><span data-stu-id="e889c-137">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="how-to-create-a-directory"></a><span data-ttu-id="e889c-138">How to: Create a Directory</span><span class="sxs-lookup"><span data-stu-id="e889c-138">How to: Create a Directory</span></span>
<span data-ttu-id="e889c-139">You can also organize storage by putting files inside subdirectories instead of having all of them in the root directory.</span><span class="sxs-lookup"><span data-stu-id="e889c-139">You can also organize storage by putting files inside subdirectories instead of having all of them in the root directory.</span></span> <span data-ttu-id="e889c-140">The Azure file storage service allows you to create as many directories as your account will allow.</span><span class="sxs-lookup"><span data-stu-id="e889c-140">The Azure file storage service allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="e889c-141">The code below will create a directory named **my-sample-directory** under the root directory as well as a subdirectory named **my-sample-subdirectory**.</span><span class="sxs-lookup"><span data-stu-id="e889c-141">The code below will create a directory named **my-sample-directory** under the root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference to a directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if the share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="how-to-list-files-and-directories-in-a-share"></a><span data-ttu-id="e889c-142">How to: List files and directories in a share</span><span class="sxs-lookup"><span data-stu-id="e889c-142">How to: List files and directories in a share</span></span>
<span data-ttu-id="e889c-143">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span><span class="sxs-lookup"><span data-stu-id="e889c-143">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="e889c-144">To access the rich set of properties and methods for a returned **list_file_and_directory_item**, you must call the **list_file_and_directory_item.as_file** method to get a **cloud_file** object, or the **list_file_and_directory_item.as_directory** method to get a **cloud_file_directory** object.</span><span class="sxs-lookup"><span data-stu-id="e889c-144">To access the rich set of properties and methods for a returned **list_file_and_directory_item**, you must call the **list_file_and_directory_item.as_file** method to get a **cloud_file** object, or the **list_file_and_directory_item.as_directory** method to get a **cloud_file_directory** object.</span></span>

<span data-ttu-id="e889c-145">The following code demonstrates how to retrieve and output the URI of each item in the root directory of the share.</span><span class="sxs-lookup"><span data-stu-id="e889c-145">The following code demonstrates how to retrieve and output the URI of each item in the root directory of the share.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="how-to-download-a-file"></a><span data-ttu-id="e889c-146">How to: Download a file</span><span class="sxs-lookup"><span data-stu-id="e889c-146">How to: Download a file</span></span>
<span data-ttu-id="e889c-147">To download files, first retrieve a file reference and then call the **download_to_stream** method to transfer the file contents to a stream object, which you can then persist to a local file.</span><span class="sxs-lookup"><span data-stu-id="e889c-147">To download files, first retrieve a file reference and then call the **download_to_stream** method to transfer the file contents to a stream object, which you can then persist to a local file.</span></span> <span data-ttu-id="e889c-148">Alternatively, you can use the **download_to_file** method to download the contents of a file to a local file.</span><span class="sxs-lookup"><span data-stu-id="e889c-148">Alternatively, you can use the **download_to_file** method to download the contents of a file to a local file.</span></span> <span data-ttu-id="e889c-149">You can use the **download_text** method to download the contents of a file as a text string.</span><span class="sxs-lookup"><span data-stu-id="e889c-149">You can use the **download_text** method to download the contents of a file as a text string.</span></span>

<span data-ttu-id="e889c-150">The following example uses the **download_to_stream** and **download_text** methods to demonstrate downloading the files, which were created in previous sections.</span><span class="sxs-lookup"><span data-stu-id="e889c-150">The following example uses the **download_to_stream** and **download_text** methods to demonstrate downloading the files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="how-to-delete-a-file"></a><span data-ttu-id="e889c-151">How to: Delete a file</span><span class="sxs-lookup"><span data-stu-id="e889c-151">How to: Delete a file</span></span>
<span data-ttu-id="e889c-152">Another common file storage operation is file deletion.</span><span class="sxs-lookup"><span data-stu-id="e889c-152">Another common file storage operation is file deletion.</span></span> <span data-ttu-id="e889c-153">The following code deletes a file named my-sample-file-3 stored under the root directory.</span><span class="sxs-lookup"><span data-stu-id="e889c-153">The following code deletes a file named my-sample-file-3 stored under the root directory.</span></span>

```cpp
// Get a reference to the root directory for the share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="how-to-delete-a-directory"></a><span data-ttu-id="e889c-154">How to: Delete a directory</span><span class="sxs-lookup"><span data-stu-id="e889c-154">How to: Delete a directory</span></span>
<span data-ttu-id="e889c-155">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span><span class="sxs-lookup"><span data-stu-id="e889c-155">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference to the directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference to the subdirectory you want to delete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete the subdirectory and the sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="how-to-delete-a-share"></a><span data-ttu-id="e889c-156">How to: Delete a Share</span><span class="sxs-lookup"><span data-stu-id="e889c-156">How to: Delete a Share</span></span>
<span data-ttu-id="e889c-157">Deleting a share is done by calling the **delete_if_exists** method on a cloud_file_share object.</span><span class="sxs-lookup"><span data-stu-id="e889c-157">Deleting a share is done by calling the **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="e889c-158">Here's sample code that does that.</span><span class="sxs-lookup"><span data-stu-id="e889c-158">Here's sample code that does that.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete the share if exists
share.delete_share_if_exists();
```

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="e889c-159">Set the maximum size for a file share</span><span class="sxs-lookup"><span data-stu-id="e889c-159">Set the maximum size for a file share</span></span>
<span data-ttu-id="e889c-160">You can set the quota (or maximum size) for a file share, in gigabytes.</span><span class="sxs-lookup"><span data-stu-id="e889c-160">You can set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="e889c-161">You can also check to see how much data is currently stored on the share.</span><span class="sxs-lookup"><span data-stu-id="e889c-161">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="e889c-162">By setting the quota for a share, you can limit the total size of the files stored on the share.</span><span class="sxs-lookup"><span data-stu-id="e889c-162">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="e889c-163">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span><span class="sxs-lookup"><span data-stu-id="e889c-163">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="e889c-164">The example below shows how to check the current usage for a share and how to set the quota for the share.</span><span class="sxs-lookup"><span data-stu-id="e889c-164">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets the quota to 2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="e889c-165">Generate a shared access signature for a file or file share</span><span class="sxs-lookup"><span data-stu-id="e889c-165">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="e889c-166">You can generate a shared access signature (SAS) for a file share or for an individual file.</span><span class="sxs-lookup"><span data-stu-id="e889c-166">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="e889c-167">You can also create a shared access policy on a file share to manage shared access signatures.</span><span class="sxs-lookup"><span data-stu-id="e889c-167">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="e889c-168">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span><span class="sxs-lookup"><span data-stu-id="e889c-168">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="e889c-169">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span><span class="sxs-lookup"><span data-stu-id="e889c-169">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client and get a reference to the share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions to expire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for the share
    azure::storage::file_share_permissions permissions;    

    //retrieve the current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add the new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save the updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve the root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in the share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from the SAS, and write some text to the file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```

<span data-ttu-id="e889c-170">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="e889c-170">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e889c-171">Next Steps</span><span class="sxs-lookup"><span data-stu-id="e889c-171">Next Steps</span></span>
<span data-ttu-id="e889c-172">To learn more about Azure Storage, explore these resources:</span><span class="sxs-lookup"><span data-stu-id="e889c-172">To learn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="e889c-173">Storage Client Library for C++</span><span class="sxs-lookup"><span data-stu-id="e889c-173">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="e889c-174">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="e889c-174">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="e889c-175">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="e889c-175">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="e889c-176">Azure Storage Documentation</span><span class="sxs-lookup"><span data-stu-id="e889c-176">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

