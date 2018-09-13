---
title: Manage anonymous read access to containers and blobs | Microsoft Docs
description: Learn how to make containers and blobs available for anonymous access, and how to access them programmatically.
services: storage
documentationcenter: ''
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 2ae603811f8e7a6fb27f7ac91dae811c11a4281c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556506"
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="ea51d-103">Manage anonymous read access to containers and blobs</span><span class="sxs-lookup"><span data-stu-id="ea51d-103">Manage anonymous read access to containers and blobs</span></span>
## <a name="overview"></a><span data-ttu-id="ea51d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ea51d-104">Overview</span></span>
<span data-ttu-id="ea51d-105">By default, only the owner of the storage account may access storage resources within that account.</span><span class="sxs-lookup"><span data-stu-id="ea51d-105">By default, only the owner of the storage account may access storage resources within that account.</span></span> <span data-ttu-id="ea51d-106">For Blob storage only, you can set a container's permissions to permit anonymous read access to the container and its blobs, so that you can grant access to those resources without sharing your account key.</span><span class="sxs-lookup"><span data-stu-id="ea51d-106">For Blob storage only, you can set a container's permissions to permit anonymous read access to the container and its blobs, so that you can grant access to those resources without sharing your account key.</span></span>

<span data-ttu-id="ea51d-107">Anonymous access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span><span class="sxs-lookup"><span data-stu-id="ea51d-107">Anonymous access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="ea51d-108">For finer-grained control, you can create a shared access signature, which enables you to delegate restricted access using different permissions and over a specified time interval.</span><span class="sxs-lookup"><span data-stu-id="ea51d-108">For finer-grained control, you can create a shared access signature, which enables you to delegate restricted access using different permissions and over a specified time interval.</span></span> <span data-ttu-id="ea51d-109">For more information about creating shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="ea51d-109">For more information about creating shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="ea51d-110">Grant anonymous users permissions to containers and blobs</span><span class="sxs-lookup"><span data-stu-id="ea51d-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="ea51d-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span><span class="sxs-lookup"><span data-stu-id="ea51d-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="ea51d-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span><span class="sxs-lookup"><span data-stu-id="ea51d-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="ea51d-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span><span class="sxs-lookup"><span data-stu-id="ea51d-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="ea51d-114">Containers provide the following options for managing container access:</span><span class="sxs-lookup"><span data-stu-id="ea51d-114">Containers provide the following options for managing container access:</span></span>

* <span data-ttu-id="ea51d-115">**Full public read access:** Container and blob data can be read via anonymous request.</span><span class="sxs-lookup"><span data-stu-id="ea51d-115">**Full public read access:** Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="ea51d-116">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span><span class="sxs-lookup"><span data-stu-id="ea51d-116">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>
* <span data-ttu-id="ea51d-117">**Public read access for blobs only:** Blob data within this container can be read via anonymous request, but container data is not available.</span><span class="sxs-lookup"><span data-stu-id="ea51d-117">**Public read access for blobs only:** Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="ea51d-118">Clients cannot enumerate blobs within the container via anonymous request.</span><span class="sxs-lookup"><span data-stu-id="ea51d-118">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="ea51d-119">**No public read access:** Container and blob data can be read by the account owner only.</span><span class="sxs-lookup"><span data-stu-id="ea51d-119">**No public read access:** Container and blob data can be read by the account owner only.</span></span>

<span data-ttu-id="ea51d-120">You can set container permissions in the following ways:</span><span class="sxs-lookup"><span data-stu-id="ea51d-120">You can set container permissions in the following ways:</span></span>

* <span data-ttu-id="ea51d-121">From the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea51d-121">From the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="ea51d-122">Programmatically, by using the storage client library or the REST API.</span><span class="sxs-lookup"><span data-stu-id="ea51d-122">Programmatically, by using the storage client library or the REST API.</span></span>
* <span data-ttu-id="ea51d-123">By using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea51d-123">By using PowerShell.</span></span> <span data-ttu-id="ea51d-124">To learn about setting container permissions from Azure PowerShell, see [Using Azure PowerShell with Azure Storage](storage-powershell-guide-full.md#how-to-manage-azure-blobs).</span><span class="sxs-lookup"><span data-stu-id="ea51d-124">To learn about setting container permissions from Azure PowerShell, see [Using Azure PowerShell with Azure Storage](storage-powershell-guide-full.md#how-to-manage-azure-blobs).</span></span>

### <a name="setting-container-permissions-from-the-azure-portal"></a><span data-ttu-id="ea51d-125">Setting container permissions from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ea51d-125">Setting container permissions from the Azure portal</span></span>
<span data-ttu-id="ea51d-126">To set container permissions from the [Azure portal](https://portal.azure.com), follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ea51d-126">To set container permissions from the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="ea51d-127">Navigate to the dashboard for your storage account.</span><span class="sxs-lookup"><span data-stu-id="ea51d-127">Navigate to the dashboard for your storage account.</span></span>
2. <span data-ttu-id="ea51d-128">Select the container name from the list.</span><span class="sxs-lookup"><span data-stu-id="ea51d-128">Select the container name from the list.</span></span> <span data-ttu-id="ea51d-129">Clicking the name exposes the blobs in the chosen container</span><span class="sxs-lookup"><span data-stu-id="ea51d-129">Clicking the name exposes the blobs in the chosen container</span></span>
3. <span data-ttu-id="ea51d-130">Select **Access policy** from the toolbar.</span><span class="sxs-lookup"><span data-stu-id="ea51d-130">Select **Access policy** from the toolbar.</span></span>
4. <span data-ttu-id="ea51d-131">In the **Access type** field, select your desired level of permissions as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="ea51d-131">In the **Access type** field, select your desired level of permissions as shown in the screenshot below.</span></span>

    ![Edit Container Metadata dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="setting-container-permissions-programmatically-using-net"></a><span data-ttu-id="ea51d-133">Setting container permissions programmatically using .NET</span><span class="sxs-lookup"><span data-stu-id="ea51d-133">Setting container permissions programmatically using .NET</span></span>
<span data-ttu-id="ea51d-134">To set permissions for a container using the .NET client library, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span><span class="sxs-lookup"><span data-stu-id="ea51d-134">To set permissions for a container using the .NET client library, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="ea51d-135">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span><span class="sxs-lookup"><span data-stu-id="ea51d-135">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="ea51d-136">Finally, call the **SetPermissions** method with the updated permissions.</span><span class="sxs-lookup"><span data-stu-id="ea51d-136">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="ea51d-137">The following example sets the container's permissions to full public read access.</span><span class="sxs-lookup"><span data-stu-id="ea51d-137">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="ea51d-138">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="ea51d-138">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="ea51d-139">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="ea51d-139">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="ea51d-140">Access containers and blobs anonymously</span><span class="sxs-lookup"><span data-stu-id="ea51d-140">Access containers and blobs anonymously</span></span>
<span data-ttu-id="ea51d-141">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span><span class="sxs-lookup"><span data-stu-id="ea51d-141">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="ea51d-142">The following examples show a few different ways to reference Blob service resources anonymously.</span><span class="sxs-lookup"><span data-stu-id="ea51d-142">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="ea51d-143">Create an anonymous client object</span><span class="sxs-lookup"><span data-stu-id="ea51d-143">Create an anonymous client object</span></span>
<span data-ttu-id="ea51d-144">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span><span class="sxs-lookup"><span data-stu-id="ea51d-144">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="ea51d-145">However, you must also know the name of a container in that account that's available for anonymous access.</span><span class="sxs-lookup"><span data-stu-id="ea51d-145">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="ea51d-146">Reference a container anonymously</span><span class="sxs-lookup"><span data-stu-id="ea51d-146">Reference a container anonymously</span></span>
<span data-ttu-id="ea51d-147">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span><span class="sxs-lookup"><span data-stu-id="ea51d-147">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```


### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="ea51d-148">Reference a blob anonymously</span><span class="sxs-lookup"><span data-stu-id="ea51d-148">Reference a blob anonymously</span></span>
<span data-ttu-id="ea51d-149">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span><span class="sxs-lookup"><span data-stu-id="ea51d-149">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="ea51d-150">Features available to anonymous users</span><span class="sxs-lookup"><span data-stu-id="ea51d-150">Features available to anonymous users</span></span>
<span data-ttu-id="ea51d-151">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span><span class="sxs-lookup"><span data-stu-id="ea51d-151">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="ea51d-152">REST Operation</span><span class="sxs-lookup"><span data-stu-id="ea51d-152">REST Operation</span></span> | <span data-ttu-id="ea51d-153">Permission with full public read access</span><span class="sxs-lookup"><span data-stu-id="ea51d-153">Permission with full public read access</span></span> | <span data-ttu-id="ea51d-154">Permission with public read access for blobs only</span><span class="sxs-lookup"><span data-stu-id="ea51d-154">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ea51d-155">List Containers</span><span class="sxs-lookup"><span data-stu-id="ea51d-155">List Containers</span></span> |<span data-ttu-id="ea51d-156">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-156">Owner only</span></span> |<span data-ttu-id="ea51d-157">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-157">Owner only</span></span> |
| <span data-ttu-id="ea51d-158">Create Container</span><span class="sxs-lookup"><span data-stu-id="ea51d-158">Create Container</span></span> |<span data-ttu-id="ea51d-159">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-159">Owner only</span></span> |<span data-ttu-id="ea51d-160">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-160">Owner only</span></span> |
| <span data-ttu-id="ea51d-161">Get Container Properties</span><span class="sxs-lookup"><span data-stu-id="ea51d-161">Get Container Properties</span></span> |<span data-ttu-id="ea51d-162">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-162">All</span></span> |<span data-ttu-id="ea51d-163">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-163">Owner only</span></span> |
| <span data-ttu-id="ea51d-164">Get Container Metadata</span><span class="sxs-lookup"><span data-stu-id="ea51d-164">Get Container Metadata</span></span> |<span data-ttu-id="ea51d-165">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-165">All</span></span> |<span data-ttu-id="ea51d-166">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-166">Owner only</span></span> |
| <span data-ttu-id="ea51d-167">Set Container Metadata</span><span class="sxs-lookup"><span data-stu-id="ea51d-167">Set Container Metadata</span></span> |<span data-ttu-id="ea51d-168">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-168">Owner only</span></span> |<span data-ttu-id="ea51d-169">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-169">Owner only</span></span> |
| <span data-ttu-id="ea51d-170">Get Container ACL</span><span class="sxs-lookup"><span data-stu-id="ea51d-170">Get Container ACL</span></span> |<span data-ttu-id="ea51d-171">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-171">Owner only</span></span> |<span data-ttu-id="ea51d-172">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-172">Owner only</span></span> |
| <span data-ttu-id="ea51d-173">Set Container ACL</span><span class="sxs-lookup"><span data-stu-id="ea51d-173">Set Container ACL</span></span> |<span data-ttu-id="ea51d-174">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-174">Owner only</span></span> |<span data-ttu-id="ea51d-175">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-175">Owner only</span></span> |
| <span data-ttu-id="ea51d-176">Delete Container</span><span class="sxs-lookup"><span data-stu-id="ea51d-176">Delete Container</span></span> |<span data-ttu-id="ea51d-177">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-177">Owner only</span></span> |<span data-ttu-id="ea51d-178">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-178">Owner only</span></span> |
| <span data-ttu-id="ea51d-179">List Blobs</span><span class="sxs-lookup"><span data-stu-id="ea51d-179">List Blobs</span></span> |<span data-ttu-id="ea51d-180">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-180">All</span></span> |<span data-ttu-id="ea51d-181">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-181">Owner only</span></span> |
| <span data-ttu-id="ea51d-182">Put Blob</span><span class="sxs-lookup"><span data-stu-id="ea51d-182">Put Blob</span></span> |<span data-ttu-id="ea51d-183">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-183">Owner only</span></span> |<span data-ttu-id="ea51d-184">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-184">Owner only</span></span> |
| <span data-ttu-id="ea51d-185">Get Blob</span><span class="sxs-lookup"><span data-stu-id="ea51d-185">Get Blob</span></span> |<span data-ttu-id="ea51d-186">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-186">All</span></span> |<span data-ttu-id="ea51d-187">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-187">All</span></span> |
| <span data-ttu-id="ea51d-188">Get Blob Properties</span><span class="sxs-lookup"><span data-stu-id="ea51d-188">Get Blob Properties</span></span> |<span data-ttu-id="ea51d-189">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-189">All</span></span> |<span data-ttu-id="ea51d-190">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-190">All</span></span> |
| <span data-ttu-id="ea51d-191">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="ea51d-191">Set Blob Properties</span></span> |<span data-ttu-id="ea51d-192">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-192">Owner only</span></span> |<span data-ttu-id="ea51d-193">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-193">Owner only</span></span> |
| <span data-ttu-id="ea51d-194">Get Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="ea51d-194">Get Blob Metadata</span></span> |<span data-ttu-id="ea51d-195">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-195">All</span></span> |<span data-ttu-id="ea51d-196">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-196">All</span></span> |
| <span data-ttu-id="ea51d-197">Set Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="ea51d-197">Set Blob Metadata</span></span> |<span data-ttu-id="ea51d-198">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-198">Owner only</span></span> |<span data-ttu-id="ea51d-199">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-199">Owner only</span></span> |
| <span data-ttu-id="ea51d-200">Put Block</span><span class="sxs-lookup"><span data-stu-id="ea51d-200">Put Block</span></span> |<span data-ttu-id="ea51d-201">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-201">Owner only</span></span> |<span data-ttu-id="ea51d-202">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-202">Owner only</span></span> |
| <span data-ttu-id="ea51d-203">Get Block List (committed blocks only)</span><span class="sxs-lookup"><span data-stu-id="ea51d-203">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="ea51d-204">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-204">All</span></span> |<span data-ttu-id="ea51d-205">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-205">All</span></span> |
| <span data-ttu-id="ea51d-206">Get Block List (uncommitted blocks only or all blocks)</span><span class="sxs-lookup"><span data-stu-id="ea51d-206">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="ea51d-207">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-207">Owner only</span></span> |<span data-ttu-id="ea51d-208">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-208">Owner only</span></span> |
| <span data-ttu-id="ea51d-209">Put Block List</span><span class="sxs-lookup"><span data-stu-id="ea51d-209">Put Block List</span></span> |<span data-ttu-id="ea51d-210">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-210">Owner only</span></span> |<span data-ttu-id="ea51d-211">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-211">Owner only</span></span> |
| <span data-ttu-id="ea51d-212">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="ea51d-212">Delete Blob</span></span> |<span data-ttu-id="ea51d-213">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-213">Owner only</span></span> |<span data-ttu-id="ea51d-214">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-214">Owner only</span></span> |
| <span data-ttu-id="ea51d-215">Copy Blob</span><span class="sxs-lookup"><span data-stu-id="ea51d-215">Copy Blob</span></span> |<span data-ttu-id="ea51d-216">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-216">Owner only</span></span> |<span data-ttu-id="ea51d-217">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-217">Owner only</span></span> |
| <span data-ttu-id="ea51d-218">Snapshot Blob</span><span class="sxs-lookup"><span data-stu-id="ea51d-218">Snapshot Blob</span></span> |<span data-ttu-id="ea51d-219">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-219">Owner only</span></span> |<span data-ttu-id="ea51d-220">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-220">Owner only</span></span> |
| <span data-ttu-id="ea51d-221">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="ea51d-221">Lease Blob</span></span> |<span data-ttu-id="ea51d-222">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-222">Owner only</span></span> |<span data-ttu-id="ea51d-223">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-223">Owner only</span></span> |
| <span data-ttu-id="ea51d-224">Put Page</span><span class="sxs-lookup"><span data-stu-id="ea51d-224">Put Page</span></span> |<span data-ttu-id="ea51d-225">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-225">Owner only</span></span> |<span data-ttu-id="ea51d-226">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-226">Owner only</span></span> |
| <span data-ttu-id="ea51d-227">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="ea51d-227">Get Page Ranges</span></span> |<span data-ttu-id="ea51d-228">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-228">All</span></span> |<span data-ttu-id="ea51d-229">All</span><span class="sxs-lookup"><span data-stu-id="ea51d-229">All</span></span> |
| <span data-ttu-id="ea51d-230">Append Blob</span><span class="sxs-lookup"><span data-stu-id="ea51d-230">Append Blob</span></span> |<span data-ttu-id="ea51d-231">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-231">Owner only</span></span> |<span data-ttu-id="ea51d-232">Owner only</span><span class="sxs-lookup"><span data-stu-id="ea51d-232">Owner only</span></span> |

## <a name="see-also"></a><span data-ttu-id="ea51d-233">See Also</span><span class="sxs-lookup"><span data-stu-id="ea51d-233">See Also</span></span>
* [<span data-ttu-id="ea51d-234">Authentication for the Azure Storage Services</span><span class="sxs-lookup"><span data-stu-id="ea51d-234">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="ea51d-235">Using Shared Access Signatures (SAS)</span><span class="sxs-lookup"><span data-stu-id="ea51d-235">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="ea51d-236">Delegating Access with a Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="ea51d-236">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)


