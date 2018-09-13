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
# <a name="how-to-use-file-storage-from-java"></a>How to use File Storage from Java
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Overview
In this guide you'll learn how to perform basic operations on the  Microsoft Azure File storage service. Through samples written in Java you'll learn how to  create shares and directories, upload, list, and delete files. If you are new to Microsoft Azure's File Storage service, going through the concepts in the sections that follow will be very helpful in understanding the samples.

[!INCLUDE [storage-file-concepts-include](../../includes/storage-file-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Create a Java application
To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][]. You should also have created an Azure storage account.

## <a name="setup-your-application-to-use-file-storage"></a>Setup your application to use File storage
To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Setup an Azure storage connection string
To use File storage, you need to connect to your Azure storage account. The first step would be to configure a connection string which we'll use to connect to your storage account. Let's define a static variable to do that.

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a>Connecting to an Azure storage account
To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.

## <a name="how-to-create-a-share"></a>How to: Create a Share
All files and directories in File storage reside in a container called a **Share**. Your storage account can have as much shares as your account capacity allows. To obtain access to a share and its contents, you need to use a File storage client.

```java
// Create the file storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Using the File storage client, you can then obtain a reference to a share.

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

At this point, **share** holds a reference to a share named **sampleshare**.

## <a name="how-to-upload-a-file"></a>How to: Upload a file
An Azure File Storage Share contains at the very least, a root directory where files can reside. In this section, you'll learn how to upload a file from local storage onto the root directory of a share.

The first step in uploading a file is to obtain a reference to the directory where it should reside. You do this by calling the **getRootDirectoryReference** method of the share object.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="how-to-create-a-directory"></a>How to: Create a Directory
You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory. The Azure file storage service allows you to create as much directories as your account will allow. The code below will create a sub-directory named **sampledir** under the root directory.

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

## <a name="how-to-list-files-and-directories-in-a-share"></a>How to: List files and directories in a share
Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference. The method returns a list of ListFileItem objects which you can iterate on. As an example, the following code will list files and directories inside the root directory.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="how-to-download-a-file"></a>How to: Download a file
One of the more frequent operations you will perform against file storage is to download files. In the following example, the code downloads SampleFile.txt and displays its contents.

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

## <a name="how-to-delete-a-file"></a>How to: Delete a file
Another common file storage operation is file deletion. The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.

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

## <a name="how-to-delete-a-directory"></a>How to: Delete a directory
Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.

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

## <a name="how-to-delete-a-share"></a>How to: Delete a Share
Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object. Here's sample code that does that.

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

## <a name="next-steps"></a>Next steps
If you would like to learn more about other Azure storage APIs, follow these links.

* [Java Developer Center](http://azure.microsoft.com/develop/java/)
* [Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
* [Azure Storage SDK for Android](https://github.com/azure/azure-storage-android)
* [Azure Storage Client SDK Reference](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Storage Services REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)
* [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md)

