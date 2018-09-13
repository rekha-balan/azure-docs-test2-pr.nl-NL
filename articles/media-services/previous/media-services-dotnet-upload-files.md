---
title: Upload files into a Media Services account using .NET  | Microsoft Docs
description: Learn how to get media content into Media Services by creating and uploading assets.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2018
ms.author: juliako
ms.openlocfilehash: 9edfa8ea0c9e469d09cef7ddbd1c7edda4484b47
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864435"
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="5411b-103">Upload files into a Media Services account using .NET</span><span class="sxs-lookup"><span data-stu-id="5411b-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="5411b-107">In Media Services, you upload (or ingest) your digital files into an asset.</span><span class="sxs-lookup"><span data-stu-id="5411b-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="5411b-108">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="5411b-108">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="5411b-109">The files in the asset are called **Asset Files**.</span><span class="sxs-lookup"><span data-stu-id="5411b-109">The files in the asset are called **Asset Files**.</span></span> <span data-ttu-id="5411b-110">The **AssetFile** instance and the actual media file are two distinct objects.</span><span class="sxs-lookup"><span data-stu-id="5411b-110">The **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="5411b-111">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span><span class="sxs-lookup"><span data-stu-id="5411b-111">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

> [!NOTE]
> The following considerations apply:
> 
> * Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed. The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]". Also, there can only be one '.' for the file name extension.
> * The length of the name should not be greater than 260 characters.
> * There is a limit to the maximum file size supported for processing in Media Services. See [this](media-services-quotas-and-limitations.md) article for details about the file size limitation.
> * There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) article.
> 

<span data-ttu-id="5411b-122">When you create assets, you can specify the following encryption options:</span><span class="sxs-lookup"><span data-stu-id="5411b-122">When you create assets, you can specify the following encryption options:</span></span>

* <span data-ttu-id="5411b-123">**None** - No encryption is used.</span><span class="sxs-lookup"><span data-stu-id="5411b-123">**None** - No encryption is used.</span></span> <span data-ttu-id="5411b-124">This is the default value.</span><span class="sxs-lookup"><span data-stu-id="5411b-124">This is the default value.</span></span> <span data-ttu-id="5411b-125">When using this option your content is not protected in transit or at rest in storage.</span><span class="sxs-lookup"><span data-stu-id="5411b-125">When using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="5411b-126">If you plan to deliver an MP4 using progressive download, use this option:</span><span class="sxs-lookup"><span data-stu-id="5411b-126">If you plan to deliver an MP4 using progressive download, use this option:</span></span> 
* <span data-ttu-id="5411b-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="5411b-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="5411b-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span><span class="sxs-lookup"><span data-stu-id="5411b-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="5411b-129">Note that the files must have been encoded and encrypted by Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="5411b-129">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="5411b-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="5411b-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="5411b-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span><span class="sxs-lookup"><span data-stu-id="5411b-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="5411b-132">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span><span class="sxs-lookup"><span data-stu-id="5411b-132">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="5411b-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span><span class="sxs-lookup"><span data-stu-id="5411b-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="5411b-134">If your asset is storage encrypted, you must configure asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="5411b-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="5411b-135">For more information, see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="5411b-135">For more information, see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="5411b-136">If you specify for your asset to be encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you need to associate your asset with a **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="5411b-136">If you specify for your asset to be encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you need to associate your asset with a **ContentKey**.</span></span> <span data-ttu-id="5411b-137">For more information, see [How to create a ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="5411b-137">For more information, see [How to create a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="5411b-138">If you specify for your asset to be encrypted with a **StorageEncrypted** option, the Media Services SDK for .NET creates a **StorateEncrypted** **ContentKey** for your asset.</span><span class="sxs-lookup"><span data-stu-id="5411b-138">If you specify for your asset to be encrypted with a **StorageEncrypted** option, the Media Services SDK for .NET creates a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="5411b-139">This article shows how to use Media Services .NET SDK as well as Media Services .NET SDK extensions to upload files into a Media Services asset.</span><span class="sxs-lookup"><span data-stu-id="5411b-139">This article shows how to use Media Services .NET SDK as well as Media Services .NET SDK extensions to upload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="5411b-140">Upload a single file with Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5411b-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="5411b-141">The following code uses .NET to upload a single file.</span><span class="sxs-lookup"><span data-stu-id="5411b-141">The following code uses .NET to upload a single file.</span></span> <span data-ttu-id="5411b-142">The AccessPolicy and Locator are created and destroyed by the Upload function.</span><span class="sxs-lookup"><span data-stu-id="5411b-142">The AccessPolicy and Locator are created and destroyed by the Upload function.</span></span> 

```csharp
        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }
```


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="5411b-143">Upload multiple files with Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5411b-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="5411b-144">The following code shows how to create an asset and upload multiple files.</span><span class="sxs-lookup"><span data-stu-id="5411b-144">The following code shows how to create an asset and upload multiple files.</span></span>

<span data-ttu-id="5411b-145">The code does the following:</span><span class="sxs-lookup"><span data-stu-id="5411b-145">The code does the following:</span></span>

* <span data-ttu-id="5411b-146">Creates an empty asset using the CreateEmptyAsset method defined in the previous step.</span><span class="sxs-lookup"><span data-stu-id="5411b-146">Creates an empty asset using the CreateEmptyAsset method defined in the previous step.</span></span>
* <span data-ttu-id="5411b-147">Creates an **AccessPolicy** instance that defines the permissions and duration of access to the asset.</span><span class="sxs-lookup"><span data-stu-id="5411b-147">Creates an **AccessPolicy** instance that defines the permissions and duration of access to the asset.</span></span>
* <span data-ttu-id="5411b-148">Creates a **Locator** instance that provides access to the asset.</span><span class="sxs-lookup"><span data-stu-id="5411b-148">Creates a **Locator** instance that provides access to the asset.</span></span>
* <span data-ttu-id="5411b-149">Creates a **BlobTransferClient** instance.</span><span class="sxs-lookup"><span data-stu-id="5411b-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="5411b-150">This type represents a client that operates on the Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="5411b-150">This type represents a client that operates on the Azure blobs.</span></span> <span data-ttu-id="5411b-151">In this example, the client monitors the upload progress.</span><span class="sxs-lookup"><span data-stu-id="5411b-151">In this example, the client monitors the upload progress.</span></span> 
* <span data-ttu-id="5411b-152">Enumerates through files in the specified directory and creates an **AssetFile** instance for each file.</span><span class="sxs-lookup"><span data-stu-id="5411b-152">Enumerates through files in the specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="5411b-153">Uploads the files into Media Services using the **UploadAsync** method.</span><span class="sxs-lookup"><span data-stu-id="5411b-153">Uploads the files into Media Services using the **UploadAsync** method.</span></span> 

> [!NOTE]
> Use the UploadAsync method to ensure that the calls are not blocking and the files are uploaded in parallel.
> 
> 

```csharp
        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended to validate AssetFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading the files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as the upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }
```


<span data-ttu-id="5411b-155">When uploading a large number of assets, consider the following:</span><span class="sxs-lookup"><span data-stu-id="5411b-155">When uploading a large number of assets, consider the following:</span></span>

* <span data-ttu-id="5411b-156">Create a new **CloudMediaContext** object per thread.</span><span class="sxs-lookup"><span data-stu-id="5411b-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="5411b-157">The **CloudMediaContext** class is not thread-safe.</span><span class="sxs-lookup"><span data-stu-id="5411b-157">The **CloudMediaContext** class is not thread-safe.</span></span>
* <span data-ttu-id="5411b-158">Increase NumberOfConcurrentTransfers from the default value of 2 to a higher value like 5.</span><span class="sxs-lookup"><span data-stu-id="5411b-158">Increase NumberOfConcurrentTransfers from the default value of 2 to a higher value like 5.</span></span> <span data-ttu-id="5411b-159">Setting this property affects all instances of **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="5411b-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="5411b-160">Keep ParallelTransferThreadCount at the default value of 10.</span><span class="sxs-lookup"><span data-stu-id="5411b-160">Keep ParallelTransferThreadCount at the default value of 10.</span></span>

## <a id="ingest_in_bulk"></a><span data-ttu-id="5411b-161">Ingesting Assets in Bulk using Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5411b-161">Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="5411b-162">Uploading large asset files can be a bottleneck during asset creation.</span><span class="sxs-lookup"><span data-stu-id="5411b-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="5411b-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from the upload process.</span><span class="sxs-lookup"><span data-stu-id="5411b-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from the upload process.</span></span> <span data-ttu-id="5411b-164">To use a bulk ingesting approach, create a manifest (IngestManifest) that describes the asset and its associated files.</span><span class="sxs-lookup"><span data-stu-id="5411b-164">To use a bulk ingesting approach, create a manifest (IngestManifest) that describes the asset and its associated files.</span></span> <span data-ttu-id="5411b-165">Then use the upload method of your choice to upload the associated files to the manifest’s blob container.</span><span class="sxs-lookup"><span data-stu-id="5411b-165">Then use the upload method of your choice to upload the associated files to the manifest’s blob container.</span></span> <span data-ttu-id="5411b-166">Microsoft Azure Media Services watches the blob container associated with the manifest.</span><span class="sxs-lookup"><span data-stu-id="5411b-166">Microsoft Azure Media Services watches the blob container associated with the manifest.</span></span> <span data-ttu-id="5411b-167">Once a file is uploaded to the blob container, Microsoft Azure Media Services completes the asset creation based on the configuration of the asset in the manifest (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="5411b-167">Once a file is uploaded to the blob container, Microsoft Azure Media Services completes the asset creation based on the configuration of the asset in the manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="5411b-168">To create a new IngestManifest, call the Create method exposed by the IngestManifests collection on the CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="5411b-168">To create a new IngestManifest, call the Create method exposed by the IngestManifests collection on the CloudMediaContext.</span></span> <span data-ttu-id="5411b-169">This method creates a new IngestManifest with the manifest name you provide.</span><span class="sxs-lookup"><span data-stu-id="5411b-169">This method creates a new IngestManifest with the manifest name you provide.</span></span>

```csharp
    IIngestManifest manifest = context.IngestManifests.Create(name);
```

<span data-ttu-id="5411b-170">Create the assets that are associated with the bulk IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="5411b-170">Create the assets that are associated with the bulk IngestManifest.</span></span> <span data-ttu-id="5411b-171">Configure the desired encryption options on the asset for bulk ingesting.</span><span class="sxs-lookup"><span data-stu-id="5411b-171">Configure the desired encryption options on the asset for bulk ingesting.</span></span>

```csharp
    // Create the assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);
```

<span data-ttu-id="5411b-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span><span class="sxs-lookup"><span data-stu-id="5411b-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="5411b-173">It also associates the AssetFiles that makes up each Asset.</span><span class="sxs-lookup"><span data-stu-id="5411b-173">It also associates the AssetFiles that makes up each Asset.</span></span> <span data-ttu-id="5411b-174">To create an IngestManifestAsset, use the Create method on the server context.</span><span class="sxs-lookup"><span data-stu-id="5411b-174">To create an IngestManifestAsset, use the Create method on the server context.</span></span>

<span data-ttu-id="5411b-175">The following example demonstrates adding two new IngestManifestAssets that associate the two assets previously created to the bulk ingest manifest.</span><span class="sxs-lookup"><span data-stu-id="5411b-175">The following example demonstrates adding two new IngestManifestAssets that associate the two assets previously created to the bulk ingest manifest.</span></span> <span data-ttu-id="5411b-176">Each IngestManifestAsset also associates a set of files that are uploaded for each asset during bulk ingesting.</span><span class="sxs-lookup"><span data-stu-id="5411b-176">Each IngestManifestAsset also associates a set of files that are uploaded for each asset during bulk ingesting.</span></span>  

```csharp
    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });
```

<span data-ttu-id="5411b-177">You can use any high-speed client application capable of uploading the asset files to the blob storage container URI provided by the **IIngestManifest.BlobStorageUriForUpload** property of the IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="5411b-177">You can use any high-speed client application capable of uploading the asset files to the blob storage container URI provided by the **IIngestManifest.BlobStorageUriForUpload** property of the IngestManifest.</span></span> 

<span data-ttu-id="5411b-178">The following code shows how to use .NET SDK to upload the assets files.</span><span class="sxs-lookup"><span data-stu-id="5411b-178">The following code shows how to use .NET SDK to upload the assets files.</span></span>

```csharp
    static void UploadBlobFile(string containerName, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(containerName);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }
```

<span data-ttu-id="5411b-179">The code for uploading the asset files for the sample used in this article is shown in the following code example:</span><span class="sxs-lookup"><span data-stu-id="5411b-179">The code for uploading the asset files for the sample used in this article is shown in the following code example:</span></span>

```csharp
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);
```

<span data-ttu-id="5411b-180">You can determine the progress of the bulk ingesting for all assets associated with an **IngestManifest** by polling the Statistics property of the **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="5411b-180">You can determine the progress of the bulk ingesting for all assets associated with an **IngestManifest** by polling the Statistics property of the **IngestManifest**.</span></span> <span data-ttu-id="5411b-181">In order to update progress information, you must use a new **CloudMediaContext** each time you poll the Statistics property.</span><span class="sxs-lookup"><span data-stu-id="5411b-181">In order to update progress information, you must use a new **CloudMediaContext** each time you poll the Statistics property.</span></span>

<span data-ttu-id="5411b-182">The following example demonstrates polling an IngestManifest by its **Id**.</span><span class="sxs-lookup"><span data-stu-id="5411b-182">The following example demonstrates polling an IngestManifest by its **Id**.</span></span>

```csharp
    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }
```


## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="5411b-183">Upload files using .NET SDK Extensions</span><span class="sxs-lookup"><span data-stu-id="5411b-183">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="5411b-184">The following example shows how to upload a single file using .NET SDK Extensions.</span><span class="sxs-lookup"><span data-stu-id="5411b-184">The following example shows how to upload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="5411b-185">In this case the **CreateFromFile** method is used, but the asynchronous version is also available (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="5411b-185">In this case the **CreateFromFile** method is used, but the asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="5411b-186">The **CreateFromFile** method lets you specify the file name, encryption option, and a callback in order to report the upload progress of the file.</span><span class="sxs-lookup"><span data-stu-id="5411b-186">The **CreateFromFile** method lets you specify the file name, encryption option, and a callback in order to report the upload progress of the file.</span></span>

```csharp
    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }
```

<span data-ttu-id="5411b-187">The following example calls UploadFile function and specifies storage encryption as the asset creation option.</span><span class="sxs-lookup"><span data-stu-id="5411b-187">The following example calls UploadFile function and specifies storage encryption as the asset creation option.</span></span>  

```csharp
    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);
```

## <a name="next-steps"></a><span data-ttu-id="5411b-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="5411b-188">Next steps</span></span>

<span data-ttu-id="5411b-189">You can now encode your uploaded assets.</span><span class="sxs-lookup"><span data-stu-id="5411b-189">You can now encode your uploaded assets.</span></span> <span data-ttu-id="5411b-190">For more information, see [Encode assets](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="5411b-190">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="5411b-191">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span><span class="sxs-lookup"><span data-stu-id="5411b-191">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="5411b-192">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="5411b-192">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5411b-193">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="5411b-193">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5411b-194">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="5411b-194">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="5411b-195">Next step</span><span class="sxs-lookup"><span data-stu-id="5411b-195">Next step</span></span>
<span data-ttu-id="5411b-196">Now that you have uploaded an asset to Media Services, go to the [How to Get a Media Processor][How to Get a Media Processor] article.</span><span class="sxs-lookup"><span data-stu-id="5411b-196">Now that you have uploaded an asset to Media Services, go to the [How to Get a Media Processor][How to Get a Media Processor] article.</span></span>

[How to Get a Media Processor]: media-services-get-media-processor.md

