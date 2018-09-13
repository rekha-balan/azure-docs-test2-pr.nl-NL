---
title: Create a read-only snapshot of a blob in Azure Storage | Microsoft Docs
description: Learn how to create a snapshot of a blob to back up blob data at a given moment in time. Understand how snapshots are billed and how to use them to minimize capacity charges.
services: storage
documentationcenter: ''
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 3926342767463ee5c75a7375aaebc296494e02ab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564236"
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="d1f4d-104">Create a blob snapshot</span><span class="sxs-lookup"><span data-stu-id="d1f4d-104">Create a blob snapshot</span></span>

<span data-ttu-id="d1f4d-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="d1f4d-106">Snapshots are useful for backing up blobs.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="d1f4d-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="d1f4d-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="d1f4d-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="d1f4d-110">All snapshots share the base blob's URI.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="d1f4d-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="d1f4d-112">A blob can have any number of snapshots.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="d1f4d-113">Snapshots persist until they are explicitly deleted.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="d1f4d-114">A snapshot cannot outlive its base blob.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="d1f4d-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="d1f4d-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="d1f4d-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="d1f4d-118">Any leases associated with the base blob do not affect the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="d1f4d-119">You cannot acquire a lease on a snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="d1f4d-120">A VHD file is used to store the current information and status for a VM disk.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="d1f4d-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="d1f4d-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="d1f4d-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="d1f4d-124">Create a snapshot</span><span class="sxs-lookup"><span data-stu-id="d1f4d-124">Create a snapshot</span></span>
<span data-ttu-id="d1f4d-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="d1f4d-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="d1f4d-126">This example specifies additional metadata for the snapshot when it is created.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a><span data-ttu-id="d1f4d-127">Copy snapshots</span><span class="sxs-lookup"><span data-stu-id="d1f4d-127">Copy snapshots</span></span>
<span data-ttu-id="d1f4d-128">Copy operations involving blobs and snapshots follow these rules:</span><span class="sxs-lookup"><span data-stu-id="d1f4d-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="d1f4d-129">You can copy a snapshot over its base blob.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="d1f4d-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="d1f4d-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="d1f4d-132">You can copy a snapshot to a destination blob with a different name.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="d1f4d-133">The resulting destination blob is a writable blob and not a snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="d1f4d-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="d1f4d-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="d1f4d-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="d1f4d-137">Any uncommitted blocks are not copied.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="d1f4d-138">Specify an access condition</span><span class="sxs-lookup"><span data-stu-id="d1f4d-138">Specify an access condition</span></span>
<span data-ttu-id="d1f4d-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="d1f4d-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="d1f4d-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="d1f4d-142">Delete snapshots</span><span class="sxs-lookup"><span data-stu-id="d1f4d-142">Delete snapshots</span></span>
<span data-ttu-id="d1f4d-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="d1f4d-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="d1f4d-145">If you attempt to delete a blob that still has snapshots, an error results.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="d1f4d-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="d1f4d-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="d1f4d-147">Snapshots with Azure Premium Storage</span><span class="sxs-lookup"><span data-stu-id="d1f4d-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="d1f4d-148">When using snapshots with Premium Storage, the following rules apply:</span><span class="sxs-lookup"><span data-stu-id="d1f4d-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="d1f4d-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="d1f4d-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="d1f4d-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="d1f4d-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="d1f4d-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="d1f4d-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="d1f4d-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="d1f4d-154">The destination blob for the copy operation must not have any existing snapshots.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="d1f4d-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="d1f4d-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="d1f4d-156">Return the absolute URI to a snapshot</span><span class="sxs-lookup"><span data-stu-id="d1f4d-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="d1f4d-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="d1f4d-158">Understand how snapshots accrue charges</span><span class="sxs-lookup"><span data-stu-id="d1f4d-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="d1f4d-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="d1f4d-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="d1f4d-161">Important billing considerations</span><span class="sxs-lookup"><span data-stu-id="d1f4d-161">Important billing considerations</span></span>
<span data-ttu-id="d1f4d-162">The following list includes key points to consider when creating a snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="d1f4d-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="d1f4d-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="d1f4d-165">After you update the base blob, it diverges from its snapshots.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="d1f4d-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="d1f4d-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="d1f4d-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="d1f4d-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="d1f4d-170">The same holds true for a page in a page blob that's updated with identical data.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="d1f4d-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="d1f4d-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="d1f4d-173">This is true even if the data in the base blob and the snapshot remain identical.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="d1f4d-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="d1f4d-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="d1f4d-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="d1f4d-177">Minimize cost with snapshot management</span><span class="sxs-lookup"><span data-stu-id="d1f4d-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="d1f4d-178">We recommend managing your snapshots carefully to avoid extra charges.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="d1f4d-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span><span class="sxs-lookup"><span data-stu-id="d1f4d-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="d1f4d-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="d1f4d-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="d1f4d-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="d1f4d-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="d1f4d-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="d1f4d-185">Snapshot billing scenarios</span><span class="sxs-lookup"><span data-stu-id="d1f4d-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="d1f4d-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="d1f4d-187">**Scenario 1**</span><span class="sxs-lookup"><span data-stu-id="d1f4d-187">**Scenario 1**</span></span>

<span data-ttu-id="d1f4d-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure Storage resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="d1f4d-190">**Scenario 2**</span><span class="sxs-lookup"><span data-stu-id="d1f4d-190">**Scenario 2**</span></span>

<span data-ttu-id="d1f4d-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="d1f4d-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="d1f4d-193">As a result, the account is charged for four blocks.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-193">As a result, the account is charged for four blocks.</span></span>

![Azure Storage resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="d1f4d-195">**Scenario 3**</span><span class="sxs-lookup"><span data-stu-id="d1f4d-195">**Scenario 3**</span></span>

<span data-ttu-id="d1f4d-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="d1f4d-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="d1f4d-198">As a result, the account is charged for four blocks.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-198">As a result, the account is charged for four blocks.</span></span>

![Azure Storage resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="d1f4d-200">**Scenario 4**</span><span class="sxs-lookup"><span data-stu-id="d1f4d-200">**Scenario 4**</span></span>

<span data-ttu-id="d1f4d-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="d1f4d-202">As a result, the account is charged for all eight unique blocks.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="d1f4d-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Azure Storage resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="d1f4d-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1f4d-205">Next steps</span></span>

* <span data-ttu-id="d1f4d-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="d1f4d-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="d1f4d-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="d1f4d-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="d1f4d-208">You can download a sample application and run it, or browse the code on GitHub.</span><span class="sxs-lookup"><span data-stu-id="d1f4d-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx



