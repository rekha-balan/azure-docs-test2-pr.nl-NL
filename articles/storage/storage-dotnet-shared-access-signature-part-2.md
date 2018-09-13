---
title: Create and use a SAS with Blob storage | Microsoft Docs
description: This tutorial shows you how to create shared access signatures for use with Blob storage, and how to consume them from your client applications.
services: storage
documentationcenter: ''
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: bd75b180395df3a5b6e90f474d4bccee624452e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663031"
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="a1a12-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span><span class="sxs-lookup"><span data-stu-id="a1a12-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="a1a12-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a1a12-104">Overview</span></span>
<span data-ttu-id="a1a12-105">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span><span class="sxs-lookup"><span data-stu-id="a1a12-105">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="a1a12-106">Part 2 shows you how to generate and then use shared access signatures with Blob storage.</span><span class="sxs-lookup"><span data-stu-id="a1a12-106">Part 2 shows you how to generate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="a1a12-107">The examples are written in C# and use the Azure Storage Client Library for .NET.</span><span class="sxs-lookup"><span data-stu-id="a1a12-107">The examples are written in C# and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="a1a12-108">The scenarios covered include these aspects of working with shared access signatures:</span><span class="sxs-lookup"><span data-stu-id="a1a12-108">The scenarios covered include these aspects of working with shared access signatures:</span></span>

* <span data-ttu-id="a1a12-109">Generating a shared access signature on a container</span><span class="sxs-lookup"><span data-stu-id="a1a12-109">Generating a shared access signature on a container</span></span>
* <span data-ttu-id="a1a12-110">Generating a shared access signature on a blob</span><span class="sxs-lookup"><span data-stu-id="a1a12-110">Generating a shared access signature on a blob</span></span>
* <span data-ttu-id="a1a12-111">Creating a stored access policy to manage signatures on a container's resources</span><span class="sxs-lookup"><span data-stu-id="a1a12-111">Creating a stored access policy to manage signatures on a container's resources</span></span>
* <span data-ttu-id="a1a12-112">Testing the shared access signatures from a client application</span><span class="sxs-lookup"><span data-stu-id="a1a12-112">Testing the shared access signatures from a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="a1a12-113">About this Tutorial</span><span class="sxs-lookup"><span data-stu-id="a1a12-113">About this Tutorial</span></span>
<span data-ttu-id="a1a12-114">In this tutorial, we'll focus on creating shared access signatures for containers and blobs by creating two console applications.</span><span class="sxs-lookup"><span data-stu-id="a1a12-114">In this tutorial, we'll focus on creating shared access signatures for containers and blobs by creating two console applications.</span></span> <span data-ttu-id="a1a12-115">The first console application generates shared access signatures on a container and on a blob.</span><span class="sxs-lookup"><span data-stu-id="a1a12-115">The first console application generates shared access signatures on a container and on a blob.</span></span> <span data-ttu-id="a1a12-116">This application has knowledge of the storage account keys.</span><span class="sxs-lookup"><span data-stu-id="a1a12-116">This application has knowledge of the storage account keys.</span></span> <span data-ttu-id="a1a12-117">The second console application, which will act as a client application, accesses container and blob resources using the shared access signatures created with the first application.</span><span class="sxs-lookup"><span data-stu-id="a1a12-117">The second console application, which will act as a client application, accesses container and blob resources using the shared access signatures created with the first application.</span></span> <span data-ttu-id="a1a12-118">This application uses the shared access signatures only to authenticate its access to the container and blob resources - it does not have knowledge of the account keys.</span><span class="sxs-lookup"><span data-stu-id="a1a12-118">This application uses the shared access signatures only to authenticate its access to the container and blob resources - it does not have knowledge of the account keys.</span></span>

## <a name="part-1-create-a-console-application-to-generate-shared-access-signatures"></a><span data-ttu-id="a1a12-119">Part 1: Create a Console Application to Generate Shared Access Signatures</span><span class="sxs-lookup"><span data-stu-id="a1a12-119">Part 1: Create a Console Application to Generate Shared Access Signatures</span></span>
<span data-ttu-id="a1a12-120">First, ensure that you have the Azure Storage Client Library for .NET installed.</span><span class="sxs-lookup"><span data-stu-id="a1a12-120">First, ensure that you have the Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="a1a12-121">You can install the [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing the most up-to-date assemblies for the client library; this is the recommended method for ensuring that you have the most recent fixes.</span><span class="sxs-lookup"><span data-stu-id="a1a12-121">You can install the [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing the most up-to-date assemblies for the client library; this is the recommended method for ensuring that you have the most recent fixes.</span></span> <span data-ttu-id="a1a12-122">You can also download the client library as part of the most recent version of the [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a1a12-122">You can also download the client library as part of the most recent version of the [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="a1a12-123">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="a1a12-123">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="a1a12-124">Add references to **Microsoft.WindowsAzure.Configuration.dll** and **Microsoft.WindowsAzure.Storage.dll**, using either of the following approaches:</span><span class="sxs-lookup"><span data-stu-id="a1a12-124">Add references to **Microsoft.WindowsAzure.Configuration.dll** and **Microsoft.WindowsAzure.Storage.dll**, using either of the following approaches:</span></span>

* <span data-ttu-id="a1a12-125">If you want to install the NuGet package, first install the [NuGet Client](https://docs.nuget.org/consume/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="a1a12-125">If you want to install the NuGet package, first install the [NuGet Client](https://docs.nuget.org/consume/installing-nuget).</span></span> <span data-ttu-id="a1a12-126">In Visual Studio, select **Project | Manage NuGet Packages**, search online for **Azure Storage**, and follow the instructions to install.</span><span class="sxs-lookup"><span data-stu-id="a1a12-126">In Visual Studio, select **Project | Manage NuGet Packages**, search online for **Azure Storage**, and follow the instructions to install.</span></span>
* <span data-ttu-id="a1a12-127">Alternatively, locate the assemblies in your installation of the Azure SDK and add references to them.</span><span class="sxs-lookup"><span data-stu-id="a1a12-127">Alternatively, locate the assemblies in your installation of the Azure SDK and add references to them.</span></span>

<span data-ttu-id="a1a12-128">At the top of the Program.cs file, add the following **using** statements:</span><span class="sxs-lookup"><span data-stu-id="a1a12-128">At the top of the Program.cs file, add the following **using** statements:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="a1a12-129">Edit the app.config file so that it contains a configuration setting with a connection string that points to your storage account.</span><span class="sxs-lookup"><span data-stu-id="a1a12-129">Edit the app.config file so that it contains a configuration setting with a connection string that points to your storage account.</span></span> <span data-ttu-id="a1a12-130">Your app.config file should look similar to this one:</span><span class="sxs-lookup"><span data-stu-id="a1a12-130">Your app.config file should look similar to this one:</span></span>

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="a1a12-131">Generate a Shared Access Signature URI for a Container</span><span class="sxs-lookup"><span data-stu-id="a1a12-131">Generate a Shared Access Signature URI for a Container</span></span>
<span data-ttu-id="a1a12-132">To begin with, we'll add a method to generate a shared access signature on a new container.</span><span class="sxs-lookup"><span data-stu-id="a1a12-132">To begin with, we'll add a method to generate a shared access signature on a new container.</span></span> <span data-ttu-id="a1a12-133">In this case the signature is not associated with a stored access policy, so it carries on the URI the information indicating its expiry time and the permissions that it grants.</span><span class="sxs-lookup"><span data-stu-id="a1a12-133">In this case the signature is not associated with a stored access policy, so it carries on the URI the information indicating its expiry time and the permissions that it grants.</span></span>

<span data-ttu-id="a1a12-134">First, add code to the **Main()** method to authenticate access to your storage account and create a new container:</span><span class="sxs-lookup"><span data-stu-id="a1a12-134">First, add code to the **Main()** method to authenticate access to your storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls to the methods created below here...

    //Require user input before closing the console window.
    Console.ReadLine();
}
```

<span data-ttu-id="a1a12-135">Next, add a new method that generates the shared access signature for the container and returns the signature URI:</span><span class="sxs-lookup"><span data-stu-id="a1a12-135">Next, add a new method that generates the shared access signature for the container and returns the signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set the expiry time and permissions for the container.
    //In this case no start time is specified, so the shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```


<span data-ttu-id="a1a12-136">Add the following lines at the bottom of the **Main()** method, before the call to **Console.ReadLine()**, to call **GetContainerSasUri()** and write the signature URI to the console window:</span><span class="sxs-lookup"><span data-stu-id="a1a12-136">Add the following lines at the bottom of the **Main()** method, before the call to **Console.ReadLine()**, to call **GetContainerSasUri()** and write the signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for the container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="a1a12-137">Compile and run to output the shared access signature URI for the new container.</span><span class="sxs-lookup"><span data-stu-id="a1a12-137">Compile and run to output the shared access signature URI for the new container.</span></span> <span data-ttu-id="a1a12-138">The URI will be similar to the following URI:</span><span class="sxs-lookup"><span data-stu-id="a1a12-138">The URI will be similar to the following URI:</span></span>

`https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D`

<span data-ttu-id="a1a12-139">Once you have run the code, the shared access signature that you created on the container will be valid for the next twenty-four hours.</span><span class="sxs-lookup"><span data-stu-id="a1a12-139">Once you have run the code, the shared access signature that you created on the container will be valid for the next twenty-four hours.</span></span> <span data-ttu-id="a1a12-140">The signature grants a client permission to list blobs in the container and to write a new blob to the container.</span><span class="sxs-lookup"><span data-stu-id="a1a12-140">The signature grants a client permission to list blobs in the container and to write a new blob to the container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="a1a12-141">Generate a Shared Access Signature URI for a Blob</span><span class="sxs-lookup"><span data-stu-id="a1a12-141">Generate a Shared Access Signature URI for a Blob</span></span>
<span data-ttu-id="a1a12-142">Next, we'll write similar code to create a new blob within the container and generate a shared access signature for it.</span><span class="sxs-lookup"><span data-stu-id="a1a12-142">Next, we'll write similar code to create a new blob within the container and generate a shared access signature for it.</span></span> <span data-ttu-id="a1a12-143">This shared access signature is not associated with a stored access policy, so it includes the start time, expiry time, and permission information on the URI.</span><span class="sxs-lookup"><span data-stu-id="a1a12-143">This shared access signature is not associated with a stored access policy, so it includes the start time, expiry time, and permission information on the URI.</span></span>

<span data-ttu-id="a1a12-144">Add a new method that creates a new blob and write some text to it, then generates a shared access signature and returns the signature URI:</span><span class="sxs-lookup"><span data-stu-id="a1a12-144">Add a new method that creates a new blob and write some text to it, then generates a shared access signature and returns the signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a Shared Access Signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Set the expiry time and permissions for the blob.
    //In this case the start time is specified as a few minutes in the past, to mitigate clock skew.
    //The shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the blob, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="a1a12-145">At the bottom of the **Main()** method, add the following lines to call **GetBlobSasUri()**, before the call to **Console.ReadLine()**, and write the shared access signature URI to the console window:</span><span class="sxs-lookup"><span data-stu-id="a1a12-145">At the bottom of the **Main()** method, add the following lines to call **GetBlobSasUri()**, before the call to **Console.ReadLine()**, and write the shared access signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="a1a12-146">Compile and run to output the shared access signature URI for the new blob.</span><span class="sxs-lookup"><span data-stu-id="a1a12-146">Compile and run to output the shared access signature URI for the new blob.</span></span> <span data-ttu-id="a1a12-147">The URI will be similar to the following URI:</span><span class="sxs-lookup"><span data-stu-id="a1a12-147">The URI will be similar to the following URI:</span></span>

    https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D

### <a name="create-a-stored-access-policy-on-the-container"></a><span data-ttu-id="a1a12-148">Create a Stored Access Policy on the Container</span><span class="sxs-lookup"><span data-stu-id="a1a12-148">Create a Stored Access Policy on the Container</span></span>
<span data-ttu-id="a1a12-149">Now let's create a stored access policy on the container, which will define the constraints for any shared access signatures that are associated with it.</span><span class="sxs-lookup"><span data-stu-id="a1a12-149">Now let's create a stored access policy on the container, which will define the constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="a1a12-150">In the previous examples, we specified the start time (implicitly or explicitly), the expiry time, and the permissions on the shared access signature URI itself.</span><span class="sxs-lookup"><span data-stu-id="a1a12-150">In the previous examples, we specified the start time (implicitly or explicitly), the expiry time, and the permissions on the shared access signature URI itself.</span></span> <span data-ttu-id="a1a12-151">In the following examples, we will specify these on the stored access policy and not on the shared access signature.</span><span class="sxs-lookup"><span data-stu-id="a1a12-151">In the following examples, we will specify these on the stored access policy and not on the shared access signature.</span></span> <span data-ttu-id="a1a12-152">Doing so enables us to change these constraints without reissuing the shared access signature.</span><span class="sxs-lookup"><span data-stu-id="a1a12-152">Doing so enables us to change these constraints without reissuing the shared access signature.</span></span>

<span data-ttu-id="a1a12-153">It's possible to have one or more of the constraints on the shared access signature and the remainder on the stored access policy.</span><span class="sxs-lookup"><span data-stu-id="a1a12-153">It's possible to have one or more of the constraints on the shared access signature and the remainder on the stored access policy.</span></span> <span data-ttu-id="a1a12-154">However, you can only specify the start time, expiry time, and permissions in one place or the other; for example, you can't specify permissions on the shared access signature and also specify them on the stored access policy.</span><span class="sxs-lookup"><span data-stu-id="a1a12-154">However, you can only specify the start time, expiry time, and permissions in one place or the other; for example, you can't specify permissions on the shared access signature and also specify them on the stored access policy.</span></span>

<span data-ttu-id="a1a12-155">Note that when you add an access policy to a container, you must get the container's existing permissions, add the new access policy, and then set the container's permissions.</span><span class="sxs-lookup"><span data-stu-id="a1a12-155">Note that when you add an access policy to a container, you must get the container's existing permissions, add the new access policy, and then set the container's permissions.</span></span>

<span data-ttu-id="a1a12-156">Add a new method that creates a new stored access policy on a container and returns the name of the policy:</span><span class="sxs-lookup"><span data-stu-id="a1a12-156">Add a new method that creates a new stored access policy on a container and returns the name of the policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Get the container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="a1a12-157">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to first clear any existing access policies and then call the **CreateSharedAccessPolicy()** method:</span><span class="sxs-lookup"><span data-stu-id="a1a12-157">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to first clear any existing access policies and then call the **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on the container, which may be optionally used to provide constraints for
//shared access signatures on the container and the blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="a1a12-158">Note that when you clear the access policies on a container, you must first get the container's existing permissions, then clear the permissions, then set the permissions again.</span><span class="sxs-lookup"><span data-stu-id="a1a12-158">Note that when you clear the access policies on a container, you must first get the container's existing permissions, then clear the permissions, then set the permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-the-container-that-uses-an-access-policy"></a><span data-ttu-id="a1a12-159">Generate a Shared Access Signature URI on the Container That Uses an Access Policy</span><span class="sxs-lookup"><span data-stu-id="a1a12-159">Generate a Shared Access Signature URI on the Container That Uses an Access Policy</span></span>
<span data-ttu-id="a1a12-160">Next, we'll create another shared access signature on the container that we created earlier, but this time we'll associate the signature with the access policy that we created in the previous example.</span><span class="sxs-lookup"><span data-stu-id="a1a12-160">Next, we'll create another shared access signature on the container that we created earlier, but this time we'll associate the signature with the access policy that we created in the previous example.</span></span>

<span data-ttu-id="a1a12-161">Add a new method to generate another shared access signature on the container:</span><span class="sxs-lookup"><span data-stu-id="a1a12-161">Add a new method to generate another shared access signature on the container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate the shared access signature on the container. In this case, all of the constraints for the
    //shared access signature are specified on the stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="a1a12-162">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetContainerSasUriWithPolicy** method:</span><span class="sxs-lookup"><span data-stu-id="a1a12-162">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-the-blob-that-uses-an-access-policy"></a><span data-ttu-id="a1a12-163">Generate a Shared Access Signature URI on the Blob That Uses an Access Policy</span><span class="sxs-lookup"><span data-stu-id="a1a12-163">Generate a Shared Access Signature URI on the Blob That Uses an Access Policy</span></span>
<span data-ttu-id="a1a12-164">Finally, we'll add a similar method to create another blob and generate a shared access signature that's associated with an access policy.</span><span class="sxs-lookup"><span data-stu-id="a1a12-164">Finally, we'll add a similar method to create another blob and generate a shared access signature that's associated with an access policy.</span></span>

<span data-ttu-id="a1a12-165">Add a new method to create a blob and generate a shared access signature:</span><span class="sxs-lookup"><span data-stu-id="a1a12-165">Add a new method to create a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature. " +
    "A stored access policy defines the constraints for the signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate the shared access signature on the blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="a1a12-166">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetBlobSasUriWithPolicy** method:</span><span class="sxs-lookup"><span data-stu-id="a1a12-166">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="a1a12-167">The **Main()** method should now look like this in its entirety.</span><span class="sxs-lookup"><span data-stu-id="a1a12-167">The **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="a1a12-168">Run it to write the shared access signature URIs to the console window, then copy and paste them into a text file for use in the second part of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1a12-168">Run it to write the shared access signature URIs to the console window, then copy and paste them into a text file for use in the second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for the container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on the container, which may be optionally used to provide constraints for
    //shared access signatures on the container and the blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="a1a12-169">When you run the GenerateSharedAccessSignatures console application, you'll see output similar to the following in the console window.</span><span class="sxs-lookup"><span data-stu-id="a1a12-169">When you run the GenerateSharedAccessSignatures console application, you'll see output similar to the following in the console window.</span></span> <span data-ttu-id="a1a12-170">These are the shared access signatures that you'll use in Part 2 of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1a12-170">These are the shared access signatures that you'll use in Part 2 of the tutorial.</span></span>

![sas-console-output-1][sas-console-output-1]

## <a name="part-2-create-a-console-application-to-test-the-shared-access-signatures"></a><span data-ttu-id="a1a12-172">Part 2: Create a Console Application to Test the Shared Access Signatures</span><span class="sxs-lookup"><span data-stu-id="a1a12-172">Part 2: Create a Console Application to Test the Shared Access Signatures</span></span>
<span data-ttu-id="a1a12-173">To test the shared access signatures created in the previous examples, we'll create a second console application that uses the signatures to perform operations on the container and on a blob.</span><span class="sxs-lookup"><span data-stu-id="a1a12-173">To test the shared access signatures created in the previous examples, we'll create a second console application that uses the signatures to perform operations on the container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="a1a12-174">If more than 24 hours have passed since you completed the first part of the tutorial, the signatures you generated will no longer be valid.</span><span class="sxs-lookup"><span data-stu-id="a1a12-174">If more than 24 hours have passed since you completed the first part of the tutorial, the signatures you generated will no longer be valid.</span></span> <span data-ttu-id="a1a12-175">In this case, you should run the code in the first console application to generate fresh shared access signatures for use in the second part of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1a12-175">In this case, you should run the code in the first console application to generate fresh shared access signatures for use in the second part of the tutorial.</span></span>
>
>

<span data-ttu-id="a1a12-176">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="a1a12-176">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="a1a12-177">Add references to **Microsoft.WindowsAzure.Configuration.dll** and **Microsoft.WindowsAzure.Storage.dll**, as you did previously.</span><span class="sxs-lookup"><span data-stu-id="a1a12-177">Add references to **Microsoft.WindowsAzure.Configuration.dll** and **Microsoft.WindowsAzure.Storage.dll**, as you did previously.</span></span>

<span data-ttu-id="a1a12-178">At the top of the Program.cs file, add the following **using** statements:</span><span class="sxs-lookup"><span data-stu-id="a1a12-178">At the top of the Program.cs file, add the following **using** statements:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="a1a12-179">In the body of the **Main()** method, add the following constants, and update their values to the shared access signatures that you generated in part 1 of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1a12-179">In the body of the **Main()** method, add the following constants, and update their values to the shared access signatures that you generated in part 1 of the tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-to-try-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="a1a12-180">Add a Method to Try Container Operations Using a Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="a1a12-180">Add a Method to Try Container Operations Using a Shared Access Signature</span></span>
<span data-ttu-id="a1a12-181">Next, we'll add a method that tests some representative container operations using a shared access signature on the container.</span><span class="sxs-lookup"><span data-stu-id="a1a12-181">Next, we'll add a method that tests some representative container operations using a shared access signature on the container.</span></span> <span data-ttu-id="a1a12-182">Note that the shared access signature is used to return a reference to the container, authenticating access to the container based on the signature alone.</span><span class="sxs-lookup"><span data-stu-id="a1a12-182">Note that the shared access signature is used to return a reference to the container, authenticating access to the container based on the signature alone.</span></span>

<span data-ttu-id="a1a12-183">Add the following method to Program.cs:</span><span class="sxs-lookup"><span data-stu-id="a1a12-183">Add the following method to Program.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with the SAS provided.

    //Return a reference to the container using the SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list to store blob URIs returned by a listing operation on the container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob to the container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions to the container. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List the blobs in the container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference to one of the blobs in the container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in the container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="a1a12-184">Update the **Main()** method to call **UseContainerSAS()** with both of the shared access signatures that you created on the container:</span><span class="sxs-lookup"><span data-stu-id="a1a12-184">Update the **Main()** method to call **UseContainerSAS()** with both of the shared access signatures that you created on the container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```


### <a name="add-a-method-to-try-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="a1a12-185">Add a Method to Try Blob Operations Using a Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="a1a12-185">Add a Method to Try Blob Operations Using a Shared Access Signature</span></span>
<span data-ttu-id="a1a12-186">Finally, we'll add a method that tests some representative blob operations using a shared access signature on the blob.</span><span class="sxs-lookup"><span data-stu-id="a1a12-186">Finally, we'll add a method that tests some representative blob operations using a shared access signature on the blob.</span></span> <span data-ttu-id="a1a12-187">In this case we use the constructor **CloudBlockBlob(String)**, passing in the shared access signature, to return a reference to the blob.</span><span class="sxs-lookup"><span data-stu-id="a1a12-187">In this case we use the constructor **CloudBlockBlob(String)**, passing in the shared access signature, to return a reference to the blob.</span></span> <span data-ttu-id="a1a12-188">No other authentication is required; it's based on the signature alone.</span><span class="sxs-lookup"><span data-stu-id="a1a12-188">No other authentication is required; it's based on the signature alone.</span></span>

<span data-ttu-id="a1a12-189">Add the following method to Program.cs:</span><span class="sxs-lookup"><span data-stu-id="a1a12-189">Add the following method to Program.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using the SAS provided.

    //Return a reference to the blob using the SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob to the container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions to the blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read the contents of the blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete the blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="a1a12-190">Update the **Main()** method to call **UseBlobSAS()** with both of the shared access signatures that you created on the blob:</span><span class="sxs-lookup"><span data-stu-id="a1a12-190">Update the **Main()** method to call **UseBlobSAS()** with both of the shared access signatures that you created on the blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call the test methods with the shared access signatures created on the blob, with and without the access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="a1a12-191">Run the console application and observe the output to see which operations are permitted for which signatures.</span><span class="sxs-lookup"><span data-stu-id="a1a12-191">Run the console application and observe the output to see which operations are permitted for which signatures.</span></span> <span data-ttu-id="a1a12-192">The output in the console window will look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="a1a12-192">The output in the console window will look similar to the following:</span></span>

![sas-console-output-2][sas-console-output-2]

## <a name="next-steps"></a><span data-ttu-id="a1a12-194">Next Steps</span><span class="sxs-lookup"><span data-stu-id="a1a12-194">Next Steps</span></span>
[<span data-ttu-id="a1a12-195">Shared Access Signatures, Part 1: Understanding the SAS Model</span><span class="sxs-lookup"><span data-stu-id="a1a12-195">Shared Access Signatures, Part 1: Understanding the SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)

[<span data-ttu-id="a1a12-196">Manage anonymous read access to containers and blobs</span><span class="sxs-lookup"><span data-stu-id="a1a12-196">Manage anonymous read access to containers and blobs</span></span>](storage-manage-access-to-resources.md)

[<span data-ttu-id="a1a12-197">Delegating Access with a Shared Access Signature (REST API)</span><span class="sxs-lookup"><span data-stu-id="a1a12-197">Delegating Access with a Shared Access Signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)

[<span data-ttu-id="a1a12-198">Introducing Table and Queue SAS</span><span class="sxs-lookup"><span data-stu-id="a1a12-198">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-console-output-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-shared-access-signature-part-2/sas-console-output-1.PNG
[sas-console-output-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-shared-access-signature-part-2/sas-console-output-2.PNG


