---
title: Migrate from Azure Media Services v2 to v3 | Microsoft Docs
description: This article describes changes that were introduced in Azure Media Services v3 and shows differences between two versions.
services: media-services
documentationcenter: na
author: Juliako
manager: cfowler
editor: ''
tags: ''
keywords: azure media services, stream, broadcast, live, offline
ms.service: media-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: media
ms.date: 06/12/2018
ms.author: juliako
ms.openlocfilehash: a382af644d30f9f0ebb586273c982ef1766f50b0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966296"
---
# <a name="migrate-from-media-services-v2-to-v3"></a><span data-ttu-id="e7b04-104">Migrate from Media Services v2 to v3</span><span class="sxs-lookup"><span data-stu-id="e7b04-104">Migrate from Media Services v2 to v3</span></span>

> [!NOTE]
> <span data-ttu-id="e7b04-105">The latest version of Azure Media Services is in Preview and may be referred to as v3.</span><span class="sxs-lookup"><span data-stu-id="e7b04-105">The latest version of Azure Media Services is in Preview and may be referred to as v3.</span></span>

<span data-ttu-id="e7b04-106">This article describes changes that were introduced in Azure Media Services (AMS) v3 and shows differences between two versions.</span><span class="sxs-lookup"><span data-stu-id="e7b04-106">This article describes changes that were introduced in Azure Media Services (AMS) v3 and shows differences between two versions.</span></span>

## <a name="why-should-you-move-to-v3"></a><span data-ttu-id="e7b04-107">Why should you move to v3?</span><span class="sxs-lookup"><span data-stu-id="e7b04-107">Why should you move to v3?</span></span>

### <a name="api-is-more-approachable"></a><span data-ttu-id="e7b04-108">API is more approachable</span><span class="sxs-lookup"><span data-stu-id="e7b04-108">API is more approachable</span></span>

*  <span data-ttu-id="e7b04-109">v3 is based on a unified API surface which exposes both management and operations functionality built on Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e7b04-109">v3 is based on a unified API surface which exposes both management and operations functionality built on Azure Resource Manager.</span></span> <span data-ttu-id="e7b04-110">Azure Resource Manager templates can be used to create and deploy Transforms, Streaming Endpoints, LiveEvents, and more.</span><span class="sxs-lookup"><span data-stu-id="e7b04-110">Azure Resource Manager templates can be used to create and deploy Transforms, Streaming Endpoints, LiveEvents, and more.</span></span>
* <span data-ttu-id="e7b04-111">Open API (aka Swagger) Specification document.</span><span class="sxs-lookup"><span data-stu-id="e7b04-111">Open API (aka Swagger) Specification document.</span></span>
* <span data-ttu-id="e7b04-112">SDKs available for .Net, .Net Core, Node.js, Python, Java, Ruby.</span><span class="sxs-lookup"><span data-stu-id="e7b04-112">SDKs available for .Net, .Net Core, Node.js, Python, Java, Ruby.</span></span>
* <span data-ttu-id="e7b04-113">Azure CLI integration.</span><span class="sxs-lookup"><span data-stu-id="e7b04-113">Azure CLI integration.</span></span>

### <a name="new-features"></a><span data-ttu-id="e7b04-114">New features</span><span class="sxs-lookup"><span data-stu-id="e7b04-114">New features</span></span>

* <span data-ttu-id="e7b04-115">Encoding now supports HTTPS ingest (Url-based input).</span><span class="sxs-lookup"><span data-stu-id="e7b04-115">Encoding now supports HTTPS ingest (Url-based input).</span></span>
* <span data-ttu-id="e7b04-116">Transforms are new in v3.</span><span class="sxs-lookup"><span data-stu-id="e7b04-116">Transforms are new in v3.</span></span> <span data-ttu-id="e7b04-117">A Transform is used to share configurations, create Azure Resource Manager Templates, and isolate encoding settings for a specific customer or tenant.</span><span class="sxs-lookup"><span data-stu-id="e7b04-117">A Transform is used to share configurations, create Azure Resource Manager Templates, and isolate encoding settings for a specific customer or tenant.</span></span> 
* <span data-ttu-id="e7b04-118">An Asset can have multiple StreamingLocators each with different Dynamic Packaging and Dynamic Encryption settings.</span><span class="sxs-lookup"><span data-stu-id="e7b04-118">An Asset can have multiple StreamingLocators each with different Dynamic Packaging and Dynamic Encryption settings.</span></span>
* <span data-ttu-id="e7b04-119">Content protection supports multi-key features.</span><span class="sxs-lookup"><span data-stu-id="e7b04-119">Content protection supports multi-key features.</span></span> 
* <span data-ttu-id="e7b04-120">LiveEvent Preview supports Dynamic Packaging and Dynamic Encryption.</span><span class="sxs-lookup"><span data-stu-id="e7b04-120">LiveEvent Preview supports Dynamic Packaging and Dynamic Encryption.</span></span> <span data-ttu-id="e7b04-121">This enables content protection on Preview as well as DASH and HLS packaging.</span><span class="sxs-lookup"><span data-stu-id="e7b04-121">This enables content protection on Preview as well as DASH and HLS packaging.</span></span>
* <span data-ttu-id="e7b04-122">LiveOuput is simpler to use than the older Program entity.</span><span class="sxs-lookup"><span data-stu-id="e7b04-122">LiveOuput is simpler to use than the older Program entity.</span></span> 
* <span data-ttu-id="e7b04-123">RBAC support on entities was added.</span><span class="sxs-lookup"><span data-stu-id="e7b04-123">RBAC support on entities was added.</span></span>

## <a name="changes-from-v2"></a><span data-ttu-id="e7b04-124">Changes from v2</span><span class="sxs-lookup"><span data-stu-id="e7b04-124">Changes from v2</span></span>

* <span data-ttu-id="e7b04-125">In Media Services v3, storage encryption (AES-256 encryption) is only supported for backwards compatibility when your Assets were created with Media Services v2.</span><span class="sxs-lookup"><span data-stu-id="e7b04-125">In Media Services v3, storage encryption (AES-256 encryption) is only supported for backwards compatibility when your Assets were created with Media Services v2.</span></span> <span data-ttu-id="e7b04-126">Meaning v3 works with existing storage encrypted assets but will not allow creation of new ones.</span><span class="sxs-lookup"><span data-stu-id="e7b04-126">Meaning v3 works with existing storage encrypted assets but will not allow creation of new ones.</span></span>

    <span data-ttu-id="e7b04-127">For Assets created with v3, Media Services supports the [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) server side storage encryption.</span><span class="sxs-lookup"><span data-stu-id="e7b04-127">For Assets created with v3, Media Services supports the [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) server side storage encryption.</span></span>
    
* <span data-ttu-id="e7b04-128">Media Services SDKs decoupled from the Storage SDK which gives more control over the Storage SDK used and avoids versioning issues.</span><span class="sxs-lookup"><span data-stu-id="e7b04-128">Media Services SDKs decoupled from the Storage SDK which gives more control over the Storage SDK used and avoids versioning issues.</span></span> 
* <span data-ttu-id="e7b04-129">In v3, all of the encoding bit rates are in bits per second.</span><span class="sxs-lookup"><span data-stu-id="e7b04-129">In v3, all of the encoding bit rates are in bits per second.</span></span> <span data-ttu-id="e7b04-130">This is different than the REST v2 Media Encoder Standard presets.</span><span class="sxs-lookup"><span data-stu-id="e7b04-130">This is different than the REST v2 Media Encoder Standard presets.</span></span> <span data-ttu-id="e7b04-131">For example, the bitrate in v2 would be specified as 128, but in v3 it would be 128000.</span><span class="sxs-lookup"><span data-stu-id="e7b04-131">For example, the bitrate in v2 would be specified as 128, but in v3 it would be 128000.</span></span> 
* <span data-ttu-id="e7b04-132">AssetFiles, AccessPolicies, IngestManifests do not exist in v3.</span><span class="sxs-lookup"><span data-stu-id="e7b04-132">AssetFiles, AccessPolicies, IngestManifests do not exist in v3.</span></span>
* <span data-ttu-id="e7b04-133">ContentKeys are no longer an entity, property of the StreamingLocator.</span><span class="sxs-lookup"><span data-stu-id="e7b04-133">ContentKeys are no longer an entity, property of the StreamingLocator.</span></span>
* <span data-ttu-id="e7b04-134">Event Grid support replaces NotificationEndpoints.</span><span class="sxs-lookup"><span data-stu-id="e7b04-134">Event Grid support replaces NotificationEndpoints.</span></span>
* <span data-ttu-id="e7b04-135">Some entities were renamed</span><span class="sxs-lookup"><span data-stu-id="e7b04-135">Some entities were renamed</span></span>

  * <span data-ttu-id="e7b04-136">JobOutput replaces Task, now just part of the Job.</span><span class="sxs-lookup"><span data-stu-id="e7b04-136">JobOutput replaces Task, now just part of the Job.</span></span>
  * <span data-ttu-id="e7b04-137">LiveEvent replaces Channel.</span><span class="sxs-lookup"><span data-stu-id="e7b04-137">LiveEvent replaces Channel.</span></span>
  * <span data-ttu-id="e7b04-138">LiveOutput replaces Program.</span><span class="sxs-lookup"><span data-stu-id="e7b04-138">LiveOutput replaces Program.</span></span>
  * <span data-ttu-id="e7b04-139">StreamingLocator replaces Locator.</span><span class="sxs-lookup"><span data-stu-id="e7b04-139">StreamingLocator replaces Locator.</span></span>

## <a name="code-changes"></a><span data-ttu-id="e7b04-140">Code changes</span><span class="sxs-lookup"><span data-stu-id="e7b04-140">Code changes</span></span>

### <a name="create-an-asset-and-upload-a-file"></a><span data-ttu-id="e7b04-141">Create an asset and upload a file</span><span class="sxs-lookup"><span data-stu-id="e7b04-141">Create an asset and upload a file</span></span> 

#### <a name="v2"></a><span data-ttu-id="e7b04-142">v2</span><span class="sxs-lookup"><span data-stu-id="e7b04-142">v2</span></span>

```csharp
IAsset asset = context.Assets.Create(assetName, storageAccountName, options);

IAssetFile assetFile = asset.AssetFiles.Create(assetFileName);

assetFile.Upload(filePath);
```

#### <a name="v3"></a><span data-ttu-id="e7b04-143">v3</span><span class="sxs-lookup"><span data-stu-id="e7b04-143">v3</span></span>

```csharp
Asset asset = client.Assets.CreateOrUpdate(resourceGroupName, accountName, assetName, new Asset());

var response = client.Assets.ListContainerSas(resourceGroupName, accountName, assetName, permissions: AssetContainerPermission.ReadWrite, expiryTime: DateTime.Now.AddHours(1));

var sasUri = new Uri(response.AssetContainerSasUrls.First());
CloudBlobContainer container = new CloudBlobContainer(sasUri);

var blob = container.GetBlockBlobReference(Path.GetFileName(fileToUpload));
blob.UploadFromFile(fileToUpload);
```

### <a name="submit-a-job"></a><span data-ttu-id="e7b04-144">Submit a job</span><span class="sxs-lookup"><span data-stu-id="e7b04-144">Submit a job</span></span>

#### <a name="v2"></a><span data-ttu-id="e7b04-145">v2</span><span class="sxs-lookup"><span data-stu-id="e7b04-145">v2</span></span>

```csharp
IMediaProcessor processor = context.MediaProcessors.GetLatestMediaProcessorByName(mediaProcessorName);

IJob job = jobs.Create($"Job for {inputAsset.Name}");

ITask task = job.Tasks.AddNew($"Task for {inputAsset.Name}", processor, taskConfiguration);

task.InputAssets.Add(inputAsset);

task.OutputAssets.AddNew(outputAssetName, outputAssetStorageAccountName, outputAssetOptions);

job.Submit();
```

#### <a name="v3"></a><span data-ttu-id="e7b04-146">v3</span><span class="sxs-lookup"><span data-stu-id="e7b04-146">v3</span></span>

```csharp
client.Assets.CreateOrUpdate(resourceGroupName, accountName, outputAssetName, new Asset());

JobOutput[] jobOutputs = { new JobOutputAsset(outputAssetName)};

JobInput jobInput = JobInputAsset(assetName: assetName);

Job job = client.Jobs.Create(resourceGroupName,
accountName, transformName, jobName,
new Job {Input = jobInput, Outputs = jobOutputs});
```

### <a name="publish-an-asset-with-aes-encryption"></a><span data-ttu-id="e7b04-147">Publish an asset with AES encryption</span><span class="sxs-lookup"><span data-stu-id="e7b04-147">Publish an asset with AES encryption</span></span> 

#### <a name="v2"></a><span data-ttu-id="e7b04-148">v2</span><span class="sxs-lookup"><span data-stu-id="e7b04-148">v2</span></span>

1. <span data-ttu-id="e7b04-149">Create ContentKeyAuthorizationPolicyOption</span><span class="sxs-lookup"><span data-stu-id="e7b04-149">Create ContentKeyAuthorizationPolicyOption</span></span>
2. <span data-ttu-id="e7b04-150">Create ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="e7b04-150">Create ContentKeyAuthorizationPolicy</span></span>
3. <span data-ttu-id="e7b04-151">Create AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="e7b04-151">Create AssetDeliveryPolicy</span></span>
4. <span data-ttu-id="e7b04-152">Create Asset and upload content OR Submit job and use output asset</span><span class="sxs-lookup"><span data-stu-id="e7b04-152">Create Asset and upload content OR Submit job and use output asset</span></span>
5. <span data-ttu-id="e7b04-153">Associate AssetDeliveryPolicy with Asset</span><span class="sxs-lookup"><span data-stu-id="e7b04-153">Associate AssetDeliveryPolicy with Asset</span></span>
6. <span data-ttu-id="e7b04-154">Create ContentKey</span><span class="sxs-lookup"><span data-stu-id="e7b04-154">Create ContentKey</span></span>
7. <span data-ttu-id="e7b04-155">Attach ContentKey to Asset</span><span class="sxs-lookup"><span data-stu-id="e7b04-155">Attach ContentKey to Asset</span></span>
8. <span data-ttu-id="e7b04-156">Create AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="e7b04-156">Create AccessPolicy</span></span>
9. <span data-ttu-id="e7b04-157">Create Locator</span><span class="sxs-lookup"><span data-stu-id="e7b04-157">Create Locator</span></span>

#### <a name="v3"></a><span data-ttu-id="e7b04-158">v3</span><span class="sxs-lookup"><span data-stu-id="e7b04-158">v3</span></span>

1. <span data-ttu-id="e7b04-159">Create Content Key Policy</span><span class="sxs-lookup"><span data-stu-id="e7b04-159">Create Content Key Policy</span></span>
2. <span data-ttu-id="e7b04-160">Create Asset</span><span class="sxs-lookup"><span data-stu-id="e7b04-160">Create Asset</span></span>
3. <span data-ttu-id="e7b04-161">Upload content or use Asset as JobOutput</span><span class="sxs-lookup"><span data-stu-id="e7b04-161">Upload content or use Asset as JobOutput</span></span>
4. <span data-ttu-id="e7b04-162">Create StreamingLocator</span><span class="sxs-lookup"><span data-stu-id="e7b04-162">Create StreamingLocator</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7b04-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="e7b04-163">Next steps</span></span>

<span data-ttu-id="e7b04-164">To see how easy it is to start encoding and streaming video files, check out [Stream files](stream-files-dotnet-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="e7b04-164">To see how easy it is to start encoding and streaming video files, check out [Stream files](stream-files-dotnet-quickstart.md).</span></span> 

