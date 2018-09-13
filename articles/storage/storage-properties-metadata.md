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
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="921e6-103">Set and Retrieve Properties and Metadata</span><span class="sxs-lookup"><span data-stu-id="921e6-103">Set and Retrieve Properties and Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="921e6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="921e6-104">Overview</span></span>
<span data-ttu-id="921e6-105">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain:</span><span class="sxs-lookup"><span data-stu-id="921e6-105">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain:</span></span>

* <span data-ttu-id="921e6-106">**System properties.**</span><span class="sxs-lookup"><span data-stu-id="921e6-106">**System properties.**</span></span> <span data-ttu-id="921e6-107">System properties exist on each storage resource.</span><span class="sxs-lookup"><span data-stu-id="921e6-107">System properties exist on each storage resource.</span></span> <span data-ttu-id="921e6-108">Some of them can be read or set, while others are read-only.</span><span class="sxs-lookup"><span data-stu-id="921e6-108">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="921e6-109">Under the covers, some system properties correspond to certain standard HTTP headers.</span><span class="sxs-lookup"><span data-stu-id="921e6-109">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="921e6-110">The Azure storage client library maintains these for you.</span><span class="sxs-lookup"><span data-stu-id="921e6-110">The Azure storage client library maintains these for you.</span></span>
* <span data-ttu-id="921e6-111">**User-defined metadata.**</span><span class="sxs-lookup"><span data-stu-id="921e6-111">**User-defined metadata.**</span></span> <span data-ttu-id="921e6-112">User-defined metadata is metadata that you specify on a given resource, in the form of a name-value pair.</span><span class="sxs-lookup"><span data-stu-id="921e6-112">User-defined metadata is metadata that you specify on a given resource, in the form of a name-value pair.</span></span> <span data-ttu-id="921e6-113">You can use metadata to store additional values with a storage resource; these values are for your own purposes only and do not affect how the resource behaves.</span><span class="sxs-lookup"><span data-stu-id="921e6-113">You can use metadata to store additional values with a storage resource; these values are for your own purposes only and do not affect how the resource behaves.</span></span>

<span data-ttu-id="921e6-114">Retrieving property and metadata values for a storage resource is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="921e6-114">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="921e6-115">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span><span class="sxs-lookup"><span data-stu-id="921e6-115">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="921e6-116">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span><span class="sxs-lookup"><span data-stu-id="921e6-116">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="921e6-117">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span><span class="sxs-lookup"><span data-stu-id="921e6-117">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="921e6-118">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span><span class="sxs-lookup"><span data-stu-id="921e6-118">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="921e6-119">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span><span class="sxs-lookup"><span data-stu-id="921e6-119">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="921e6-120">Setting and Retrieving Properties</span><span class="sxs-lookup"><span data-stu-id="921e6-120">Setting and Retrieving Properties</span></span>
<span data-ttu-id="921e6-121">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span><span class="sxs-lookup"><span data-stu-id="921e6-121">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="921e6-122">To set properties on an object, specify the property value, then call the **SetProperties** method.</span><span class="sxs-lookup"><span data-stu-id="921e6-122">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="921e6-123">The following code example creates a container and writes some of its property values to a console window:</span><span class="sxs-lookup"><span data-stu-id="921e6-123">The following code example creates a container and writes some of its property values to a console window:</span></span>

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

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="921e6-124">Setting and Retrieving Metadata</span><span class="sxs-lookup"><span data-stu-id="921e6-124">Setting and Retrieving Metadata</span></span>
<span data-ttu-id="921e6-125">You can specify metadata as one or more name-value pairs on a blob or container resource.</span><span class="sxs-lookup"><span data-stu-id="921e6-125">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="921e6-126">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span><span class="sxs-lookup"><span data-stu-id="921e6-126">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="921e6-127">The name of your metadata must conform to the naming conventions for C# identifiers.</span><span class="sxs-lookup"><span data-stu-id="921e6-127">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="921e6-128">The following code example sets metadata on a container.</span><span class="sxs-lookup"><span data-stu-id="921e6-128">The following code example sets metadata on a container.</span></span> <span data-ttu-id="921e6-129">One value is set using the collection's **Add** method.</span><span class="sxs-lookup"><span data-stu-id="921e6-129">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="921e6-130">The other value is set using implicit key/value syntax.</span><span class="sxs-lookup"><span data-stu-id="921e6-130">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="921e6-131">Both are valid.</span><span class="sxs-lookup"><span data-stu-id="921e6-131">Both are valid.</span></span>

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

<span data-ttu-id="921e6-132">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span><span class="sxs-lookup"><span data-stu-id="921e6-132">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="921e6-133">See Also</span><span class="sxs-lookup"><span data-stu-id="921e6-133">See Also</span></span>
* [<span data-ttu-id="921e6-134">Azure Storage Client Library for .NET Reference</span><span class="sxs-lookup"><span data-stu-id="921e6-134">Azure Storage Client Library for .NET Reference</span></span>](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx)
* [<span data-ttu-id="921e6-135">Azure Storage Client Library for .NET package</span><span class="sxs-lookup"><span data-stu-id="921e6-135">Azure Storage Client Library for .NET package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)

