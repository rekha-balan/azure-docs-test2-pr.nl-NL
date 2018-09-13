---
title: How to use File storage from Java | Microsoft Docs
description: Learn how to use the Azure file service to upload, download, list, and delete files. Samples written in Java.
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 49b35ff1b82f5384b105d99ce95773648a11f6f4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553235"
---
# <a name="how-to-use-file-storage-from-java"></a><span data-ttu-id="6ae2d-104">How to use File Storage from Java</span><span class="sxs-lookup"><span data-stu-id="6ae2d-104">How to use File Storage from Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="6ae2d-105">Overview</span><span class="sxs-lookup"><span data-stu-id="6ae2d-105">Overview</span></span>
<span data-ttu-id="6ae2d-106">In this guide you'll learn how to perform basic operations on the  Microsoft Azure File storage service.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-106">In this guide you'll learn how to perform basic operations on the  Microsoft Azure File storage service.</span></span> <span data-ttu-id="6ae2d-107">Through samples written in Java you'll learn how to  create shares and directories, upload, list, and delete files.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-107">Through samples written in Java you'll learn how to  create shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="6ae2d-108">If you are new to Microsoft Azure's File Storage service, going through the concepts in the sections that follow will be very helpful in understanding the samples.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-108">If you are new to Microsoft Azure's File Storage service, going through the concepts in the sections that follow will be very helpful in understanding the samples.</span></span>

[!INCLUDE [storage-file-concepts-include](../../includes/storage-file-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="6ae2d-109">Create a Java application</span><span class="sxs-lookup"><span data-stu-id="6ae2d-109">Create a Java application</span></span>
<span data-ttu-id="6ae2d-110">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span><span class="sxs-lookup"><span data-stu-id="6ae2d-110">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="6ae2d-111">You should also have created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-111">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-file-storage"></a><span data-ttu-id="6ae2d-112">Setup your application to use File storage</span><span class="sxs-lookup"><span data-stu-id="6ae2d-112">Setup your application to use File storage</span></span>
<span data-ttu-id="6ae2d-113">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-113">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="6ae2d-114">Setup an Azure storage connection string</span><span class="sxs-lookup"><span data-stu-id="6ae2d-114">Setup an Azure storage connection string</span></span>
<span data-ttu-id="6ae2d-115">To use File storage, you need to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-115">To use File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="6ae2d-116">The first step would be to configure a connection string which we'll use to connect to your storage account.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-116">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="6ae2d-117">Let's define a static variable to do that.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-117">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="6ae2d-118">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-118">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="6ae2d-119">Connecting to an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="6ae2d-119">Connecting to an Azure storage account</span></span>
<span data-ttu-id="6ae2d-120">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-120">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="6ae2d-121">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-121">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="how-to-create-a-share"></a><span data-ttu-id="6ae2d-122">How to: Create a Share</span><span class="sxs-lookup"><span data-stu-id="6ae2d-122">How to: Create a Share</span></span>
<span data-ttu-id="6ae2d-123">All files and directories in File storage reside in a container called a **Share**.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-123">All files and directories in File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="6ae2d-124">Your storage account can have as much shares as your account capacity allows.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-124">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="6ae2d-125">To obtain access to a share and its contents, you need to use a File storage client.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-125">To obtain access to a share and its contents, you need to use a File storage client.</span></span>

```java
// Create the file storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="6ae2d-126">Using the File storage client, you can then obtain a reference to a share.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-126">Using the File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="6ae2d-127">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-127">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="6ae2d-128">At this point, **share** holds a reference to a share named **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-128">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="how-to-upload-a-file"></a><span data-ttu-id="6ae2d-129">How to: Upload a file</span><span class="sxs-lookup"><span data-stu-id="6ae2d-129">How to: Upload a file</span></span>
<span data-ttu-id="6ae2d-130">An Azure File Storage Share contains at the very least, a root directory where files can reside.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-130">An Azure File Storage Share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="6ae2d-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="6ae2d-132">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-132">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="6ae2d-133">You do this by calling the **getRootDirectoryReference** method of the share object.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-133">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="6ae2d-134">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-134">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="how-to-create-a-directory"></a><span data-ttu-id="6ae2d-135">How to: Create a Directory</span><span class="sxs-lookup"><span data-stu-id="6ae2d-135">How to: Create a Directory</span></span>
<span data-ttu-id="6ae2d-136">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-136">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="6ae2d-137">The Azure file storage service allows you to create as much directories as your account will allow.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-137">The Azure file storage service allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="6ae2d-138">The code below will create a sub-directory named **sampledir** under the root directory.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-138">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="how-to-list-files-and-directories-in-a-share"></a><span data-ttu-id="6ae2d-139">How to: List files and directories in a share</span><span class="sxs-lookup"><span data-stu-id="6ae2d-139">How to: List files and directories in a share</span></span>
<span data-ttu-id="6ae2d-140">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-140">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="6ae2d-141">The method returns a list of ListFileItem objects which you can iterate on.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-141">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="6ae2d-142">As an example, the following code will list files and directories inside the root directory.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-142">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="how-to-download-a-file"></a><span data-ttu-id="6ae2d-143">How to: Download a file</span><span class="sxs-lookup"><span data-stu-id="6ae2d-143">How to: Download a file</span></span>
<span data-ttu-id="6ae2d-144">One of the more frequent operations you will perform against file storage is to download files.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-144">One of the more frequent operations you will perform against file storage is to download files.</span></span> <span data-ttu-id="6ae2d-145">In the following example, the code downloads SampleFile.txt and displays its contents.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-145">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="how-to-delete-a-file"></a><span data-ttu-id="6ae2d-146">How to: Delete a file</span><span class="sxs-lookup"><span data-stu-id="6ae2d-146">How to: Delete a file</span></span>
<span data-ttu-id="6ae2d-147">Another common file storage operation is file deletion.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-147">Another common file storage operation is file deletion.</span></span> <span data-ttu-id="6ae2d-148">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-148">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="how-to-delete-a-directory"></a><span data-ttu-id="6ae2d-149">How to: Delete a directory</span><span class="sxs-lookup"><span data-stu-id="6ae2d-149">How to: Delete a directory</span></span>
<span data-ttu-id="6ae2d-150">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-150">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="how-to-delete-a-share"></a><span data-ttu-id="6ae2d-151">How to: Delete a Share</span><span class="sxs-lookup"><span data-stu-id="6ae2d-151">How to: Delete a Share</span></span>
<span data-ttu-id="6ae2d-152">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-152">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="6ae2d-153">Here's sample code that does that.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-153">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="6ae2d-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ae2d-154">Next steps</span></span>
<span data-ttu-id="6ae2d-155">If you would like to learn more about other Azure storage APIs, follow these links.</span><span class="sxs-lookup"><span data-stu-id="6ae2d-155">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="6ae2d-156">Java Developer Center</span><span class="sxs-lookup"><span data-stu-id="6ae2d-156">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="6ae2d-157">Azure Storage SDK for Java</span><span class="sxs-lookup"><span data-stu-id="6ae2d-157">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="6ae2d-158">Azure Storage SDK for Android</span><span class="sxs-lookup"><span data-stu-id="6ae2d-158">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="6ae2d-159">Azure Storage Client SDK Reference</span><span class="sxs-lookup"><span data-stu-id="6ae2d-159">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="6ae2d-160">Azure Storage Services REST API</span><span class="sxs-lookup"><span data-stu-id="6ae2d-160">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="6ae2d-161">Azure Storage Team Blog</span><span class="sxs-lookup"><span data-stu-id="6ae2d-161">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="6ae2d-162">Transfer data with the AzCopy Command-Line Utility</span><span class="sxs-lookup"><span data-stu-id="6ae2d-162">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

