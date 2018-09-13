---
title: Set and retrieve properties and metadata for objects in Azure Storage | Microsoft Docs
description: Store custom metadata on objects in Azure Storage, and set and retrieve system properties.
services: storage
documentationcenter: ''
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: marsma
ms.openlocfilehash: 7c1ca950c3ab1b8ffb754a74597d45b82777838c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670007"
---
# <a name="set-and-retrieve-properties-and-metadata"></a>Set and Retrieve Properties and Metadata
## <a name="overview"></a>Overview
Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain:

* **System properties.** System properties exist on each storage resource. Some of them can be read or set, while others are read-only. Under the covers, some system properties correspond to certain standard HTTP headers. The Azure storage client library maintains these for you.
* **User-defined metadata.** User-defined metadata is metadata that you specify on a given resource, in the form of a name-value pair. You can use metadata to store additional values with a storage resource; these values are for your own purposes only and do not affect how the resource behaves.

Retrieving property and metadata values for a storage resource is a two-step process. Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.

> [!IMPORTANT]
> Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.
>
> You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters. Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers. It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.
>

## <a name="setting-and-retrieving-properties"></a>Setting and Retrieving Properties
To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.

To set properties on an object, specify the property value, then call the **SetProperties** method.

The following code example creates a container and writes some of its property values to a console window:

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a>Setting and Retrieving Metadata
You can specify metadata as one or more name-value pairs on a blob or container resource. To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.

> [!NOTE]
> The name of your metadata must conform to the naming conventions for C# identifiers.
>
>

The following code example sets metadata on a container. One value is set using the collection's **Add** method. The other value is set using implicit key/value syntax. Both are valid.

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="see-also"></a>See Also
* [Azure Storage Client Library for .NET Reference](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx)
* [Azure Storage Client Library for .NET package](https://www.nuget.org/packages/WindowsAzure.Storage/)

