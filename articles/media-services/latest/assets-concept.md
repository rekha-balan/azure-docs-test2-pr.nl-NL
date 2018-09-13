---
title: Assets in Azure Media Services | Microsoft Docs
description: This article gives an explanation of what assets are, and how they are used by Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: 61555eb6cca6995215ce43051abbda9aa43539ec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870996"
---
# <a name="assets"></a><span data-ttu-id="dbf06-103">Assets</span><span class="sxs-lookup"><span data-stu-id="dbf06-103">Assets</span></span>

<span data-ttu-id="dbf06-104">An **Asset** contains digital files (including video, audio, images, thumbnail collections, text tracks and closed caption files) and the metadata about these files.</span><span class="sxs-lookup"><span data-stu-id="dbf06-104">An **Asset** contains digital files (including video, audio, images, thumbnail collections, text tracks and closed caption files) and the metadata about these files.</span></span> <span data-ttu-id="dbf06-105">After the digital files are uploaded into an asset, they could be used in the Media Services encoding and streaming workflows.</span><span class="sxs-lookup"><span data-stu-id="dbf06-105">After the digital files are uploaded into an asset, they could be used in the Media Services encoding and streaming workflows.</span></span>

<span data-ttu-id="dbf06-106">An asset is mapped to a blob container in the [Azure Storage account](storage-account-concept.md) and the files in the asset are stored as block blobs in that container.</span><span class="sxs-lookup"><span data-stu-id="dbf06-106">An asset is mapped to a blob container in the [Azure Storage account](storage-account-concept.md) and the files in the asset are stored as block blobs in that container.</span></span> <span data-ttu-id="dbf06-107">You can interact with the Asset files in the containers using the Storage SDK clients.</span><span class="sxs-lookup"><span data-stu-id="dbf06-107">You can interact with the Asset files in the containers using the Storage SDK clients.</span></span>

<span data-ttu-id="dbf06-108">Azure Media Services supports Blob tiers when the account uses General-purpose v2 (GPv2) storage.</span><span class="sxs-lookup"><span data-stu-id="dbf06-108">Azure Media Services supports Blob tiers when the account uses General-purpose v2 (GPv2) storage.</span></span> <span data-ttu-id="dbf06-109">With GPv2, you can move files to cool or cold storage.</span><span class="sxs-lookup"><span data-stu-id="dbf06-109">With GPv2, you can move files to cool or cold storage.</span></span> <span data-ttu-id="dbf06-110">Cold storage is suitable for archiving source files when no longer needed (for example, after they have been encoded.)</span><span class="sxs-lookup"><span data-stu-id="dbf06-110">Cold storage is suitable for archiving source files when no longer needed (for example, after they have been encoded.)</span></span>

<span data-ttu-id="dbf06-111">In Media Services v3, the job input can be created from assets or from HTTP(s) URLs.</span><span class="sxs-lookup"><span data-stu-id="dbf06-111">In Media Services v3, the job input can be created from assets or from HTTP(s) URLs.</span></span> <span data-ttu-id="dbf06-112">To create an asset that can be used as an input for your job, see [Create a job input from a local file](job-input-from-local-file-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="dbf06-112">To create an asset that can be used as an input for your job, see [Create a job input from a local file](job-input-from-local-file-how-to.md).</span></span>

<span data-ttu-id="dbf06-113">Also, read about [storage accounts in Media Services](storage-account-concept.md) and [transforms and jobs](transform-concept.md).</span><span class="sxs-lookup"><span data-stu-id="dbf06-113">Also, read about [storage accounts in Media Services](storage-account-concept.md) and [transforms and jobs](transform-concept.md).</span></span>

## <a name="asset-definition"></a><span data-ttu-id="dbf06-114">Asset definition</span><span class="sxs-lookup"><span data-stu-id="dbf06-114">Asset definition</span></span>

<span data-ttu-id="dbf06-115">The following table shows the Asset's properties and gives their definitions.</span><span class="sxs-lookup"><span data-stu-id="dbf06-115">The following table shows the Asset's properties and gives their definitions.</span></span>

|<span data-ttu-id="dbf06-116">Name</span><span class="sxs-lookup"><span data-stu-id="dbf06-116">Name</span></span>|<span data-ttu-id="dbf06-117">Type</span><span class="sxs-lookup"><span data-stu-id="dbf06-117">Type</span></span>|<span data-ttu-id="dbf06-118">Description</span><span class="sxs-lookup"><span data-stu-id="dbf06-118">Description</span></span>|
|---|---|---|
|<span data-ttu-id="dbf06-119">Id</span><span class="sxs-lookup"><span data-stu-id="dbf06-119">Id</span></span>|<span data-ttu-id="dbf06-120">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-120">string</span></span>|<span data-ttu-id="dbf06-121">Fully qualified resource ID for the resource.</span><span class="sxs-lookup"><span data-stu-id="dbf06-121">Fully qualified resource ID for the resource.</span></span>|
|<span data-ttu-id="dbf06-122">name</span><span class="sxs-lookup"><span data-stu-id="dbf06-122">name</span></span>|<span data-ttu-id="dbf06-123">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-123">string</span></span>|<span data-ttu-id="dbf06-124">The name of the resource.</span><span class="sxs-lookup"><span data-stu-id="dbf06-124">The name of the resource.</span></span>|
|<span data-ttu-id="dbf06-125">properties.alternateId</span><span class="sxs-lookup"><span data-stu-id="dbf06-125">properties.alternateId</span></span> |<span data-ttu-id="dbf06-126">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-126">string</span></span>|<span data-ttu-id="dbf06-127">The alternate ID of the Asset.</span><span class="sxs-lookup"><span data-stu-id="dbf06-127">The alternate ID of the Asset.</span></span>|
|<span data-ttu-id="dbf06-128">properties.assetId</span><span class="sxs-lookup"><span data-stu-id="dbf06-128">properties.assetId</span></span> |<span data-ttu-id="dbf06-129">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-129">string</span></span>|<span data-ttu-id="dbf06-130">The Asset ID.</span><span class="sxs-lookup"><span data-stu-id="dbf06-130">The Asset ID.</span></span>|
|<span data-ttu-id="dbf06-131">properties.container</span><span class="sxs-lookup"><span data-stu-id="dbf06-131">properties.container</span></span> |<span data-ttu-id="dbf06-132">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-132">string</span></span>|<span data-ttu-id="dbf06-133">The name of the asset blob container.</span><span class="sxs-lookup"><span data-stu-id="dbf06-133">The name of the asset blob container.</span></span>|
|<span data-ttu-id="dbf06-134">properties.created</span><span class="sxs-lookup"><span data-stu-id="dbf06-134">properties.created</span></span> |<span data-ttu-id="dbf06-135">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-135">string</span></span>|<span data-ttu-id="dbf06-136">The creation date of the Asset.</span><span class="sxs-lookup"><span data-stu-id="dbf06-136">The creation date of the Asset.</span></span>|
|<span data-ttu-id="dbf06-137">properties.description</span><span class="sxs-lookup"><span data-stu-id="dbf06-137">properties.description</span></span> |<span data-ttu-id="dbf06-138">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-138">string</span></span>|<span data-ttu-id="dbf06-139">The Asset description.</span><span class="sxs-lookup"><span data-stu-id="dbf06-139">The Asset description.</span></span>|
|<span data-ttu-id="dbf06-140">properties.lastModified</span><span class="sxs-lookup"><span data-stu-id="dbf06-140">properties.lastModified</span></span> |<span data-ttu-id="dbf06-141">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-141">string</span></span>|<span data-ttu-id="dbf06-142">The last modified date of the Asset.</span><span class="sxs-lookup"><span data-stu-id="dbf06-142">The last modified date of the Asset.</span></span>|
|<span data-ttu-id="dbf06-143">properties.storageAccountName</span><span class="sxs-lookup"><span data-stu-id="dbf06-143">properties.storageAccountName</span></span> |<span data-ttu-id="dbf06-144">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-144">string</span></span>|<span data-ttu-id="dbf06-145">The name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="dbf06-145">The name of the storage account.</span></span>|
|<span data-ttu-id="dbf06-146">properties.storageEncryptionFormat</span><span class="sxs-lookup"><span data-stu-id="dbf06-146">properties.storageEncryptionFormat</span></span> |<span data-ttu-id="dbf06-147">AssetStorageEncryptionFormat</span><span class="sxs-lookup"><span data-stu-id="dbf06-147">AssetStorageEncryptionFormat</span></span> |<span data-ttu-id="dbf06-148">The Asset encryption format.</span><span class="sxs-lookup"><span data-stu-id="dbf06-148">The Asset encryption format.</span></span> <span data-ttu-id="dbf06-149">One of None or MediaStorageEncryption.</span><span class="sxs-lookup"><span data-stu-id="dbf06-149">One of None or MediaStorageEncryption.</span></span>|
|<span data-ttu-id="dbf06-150">type</span><span class="sxs-lookup"><span data-stu-id="dbf06-150">type</span></span>|<span data-ttu-id="dbf06-151">string</span><span class="sxs-lookup"><span data-stu-id="dbf06-151">string</span></span>|<span data-ttu-id="dbf06-152">The type of the resource.</span><span class="sxs-lookup"><span data-stu-id="dbf06-152">The type of the resource.</span></span>|

<span data-ttu-id="dbf06-153">For the full definition, see [Assets](https://docs.microsoft.com/rest/api/media/assets).</span><span class="sxs-lookup"><span data-stu-id="dbf06-153">For the full definition, see [Assets](https://docs.microsoft.com/rest/api/media/assets).</span></span>

## <a name="filtering-ordering-paging"></a><span data-ttu-id="dbf06-154">Filtering, ordering, paging</span><span class="sxs-lookup"><span data-stu-id="dbf06-154">Filtering, ordering, paging</span></span>

<span data-ttu-id="dbf06-155">Media Services supports the following OData query options for Assets:</span><span class="sxs-lookup"><span data-stu-id="dbf06-155">Media Services supports the following OData query options for Assets:</span></span> 

* <span data-ttu-id="dbf06-156">$filter</span><span class="sxs-lookup"><span data-stu-id="dbf06-156">$filter</span></span> 
* <span data-ttu-id="dbf06-157">$orderby</span><span class="sxs-lookup"><span data-stu-id="dbf06-157">$orderby</span></span> 
* <span data-ttu-id="dbf06-158">$top</span><span class="sxs-lookup"><span data-stu-id="dbf06-158">$top</span></span> 
* <span data-ttu-id="dbf06-159">$skiptoken</span><span class="sxs-lookup"><span data-stu-id="dbf06-159">$skiptoken</span></span> 

### <a name="filteringordering"></a><span data-ttu-id="dbf06-160">Filtering/ordering</span><span class="sxs-lookup"><span data-stu-id="dbf06-160">Filtering/ordering</span></span>

<span data-ttu-id="dbf06-161">The following table shows how these options may be applied to the Asset properties:</span><span class="sxs-lookup"><span data-stu-id="dbf06-161">The following table shows how these options may be applied to the Asset properties:</span></span> 

|<span data-ttu-id="dbf06-162">Name</span><span class="sxs-lookup"><span data-stu-id="dbf06-162">Name</span></span>|<span data-ttu-id="dbf06-163">Filter</span><span class="sxs-lookup"><span data-stu-id="dbf06-163">Filter</span></span>|<span data-ttu-id="dbf06-164">Order</span><span class="sxs-lookup"><span data-stu-id="dbf06-164">Order</span></span>|
|---|---|---|
|<span data-ttu-id="dbf06-165">Id</span><span class="sxs-lookup"><span data-stu-id="dbf06-165">Id</span></span>|<span data-ttu-id="dbf06-166">Supports:</span><span class="sxs-lookup"><span data-stu-id="dbf06-166">Supports:</span></span><br/><span data-ttu-id="dbf06-167">Equals</span><span class="sxs-lookup"><span data-stu-id="dbf06-167">Equals</span></span><br/><span data-ttu-id="dbf06-168">Greater than</span><span class="sxs-lookup"><span data-stu-id="dbf06-168">Greater than</span></span><br/><span data-ttu-id="dbf06-169">Less Than</span><span class="sxs-lookup"><span data-stu-id="dbf06-169">Less Than</span></span>|<span data-ttu-id="dbf06-170">Supports:</span><span class="sxs-lookup"><span data-stu-id="dbf06-170">Supports:</span></span><br/><span data-ttu-id="dbf06-171">Ascending</span><span class="sxs-lookup"><span data-stu-id="dbf06-171">Ascending</span></span><br/><span data-ttu-id="dbf06-172">Descending</span><span class="sxs-lookup"><span data-stu-id="dbf06-172">Descending</span></span>|
|<span data-ttu-id="dbf06-173">name</span><span class="sxs-lookup"><span data-stu-id="dbf06-173">name</span></span>|||
|<span data-ttu-id="dbf06-174">properties.alternateId</span><span class="sxs-lookup"><span data-stu-id="dbf06-174">properties.alternateId</span></span> |<span data-ttu-id="dbf06-175">Supports:</span><span class="sxs-lookup"><span data-stu-id="dbf06-175">Supports:</span></span><br/><span data-ttu-id="dbf06-176">Equals</span><span class="sxs-lookup"><span data-stu-id="dbf06-176">Equals</span></span>||
|<span data-ttu-id="dbf06-177">properties.assetId</span><span class="sxs-lookup"><span data-stu-id="dbf06-177">properties.assetId</span></span> |<span data-ttu-id="dbf06-178">Supports:</span><span class="sxs-lookup"><span data-stu-id="dbf06-178">Supports:</span></span><br/><span data-ttu-id="dbf06-179">Equals</span><span class="sxs-lookup"><span data-stu-id="dbf06-179">Equals</span></span>||
|<span data-ttu-id="dbf06-180">properties.container</span><span class="sxs-lookup"><span data-stu-id="dbf06-180">properties.container</span></span> |||
|<span data-ttu-id="dbf06-181">properties.created</span><span class="sxs-lookup"><span data-stu-id="dbf06-181">properties.created</span></span>|<span data-ttu-id="dbf06-182">Supports:</span><span class="sxs-lookup"><span data-stu-id="dbf06-182">Supports:</span></span><br/><span data-ttu-id="dbf06-183">Equals</span><span class="sxs-lookup"><span data-stu-id="dbf06-183">Equals</span></span><br/><span data-ttu-id="dbf06-184">Greater than</span><span class="sxs-lookup"><span data-stu-id="dbf06-184">Greater than</span></span><br/><span data-ttu-id="dbf06-185">Less Than</span><span class="sxs-lookup"><span data-stu-id="dbf06-185">Less Than</span></span>|<span data-ttu-id="dbf06-186">Supports:</span><span class="sxs-lookup"><span data-stu-id="dbf06-186">Supports:</span></span><br/><span data-ttu-id="dbf06-187">Ascending</span><span class="sxs-lookup"><span data-stu-id="dbf06-187">Ascending</span></span><br/><span data-ttu-id="dbf06-188">Descending</span><span class="sxs-lookup"><span data-stu-id="dbf06-188">Descending</span></span>|
|<span data-ttu-id="dbf06-189">properties.description</span><span class="sxs-lookup"><span data-stu-id="dbf06-189">properties.description</span></span> |||
|<span data-ttu-id="dbf06-190">properties.lastModified</span><span class="sxs-lookup"><span data-stu-id="dbf06-190">properties.lastModified</span></span> |||
|<span data-ttu-id="dbf06-191">properties.storageAccountName</span><span class="sxs-lookup"><span data-stu-id="dbf06-191">properties.storageAccountName</span></span> |||
|<span data-ttu-id="dbf06-192">properties.storageEncryptionFormat</span><span class="sxs-lookup"><span data-stu-id="dbf06-192">properties.storageEncryptionFormat</span></span> | ||
|<span data-ttu-id="dbf06-193">type</span><span class="sxs-lookup"><span data-stu-id="dbf06-193">type</span></span>|||

<span data-ttu-id="dbf06-194">The following C# example filters on the created date:</span><span class="sxs-lookup"><span data-stu-id="dbf06-194">The following C# example filters on the created date:</span></span>

```csharp
var odataQuery = new ODataQuery<Asset>("properties/created lt 2018-05-11T17:39:08.387Z");
var firstPage = await MediaServicesArmClient.Assets.ListAsync(CustomerResourceGroup, CustomerAccountName, odataQuery);
```

### <a name="pagination"></a><span data-ttu-id="dbf06-195">Pagination</span><span class="sxs-lookup"><span data-stu-id="dbf06-195">Pagination</span></span>

<span data-ttu-id="dbf06-196">Pagination is supported for each of the four enabled sort orders.</span><span class="sxs-lookup"><span data-stu-id="dbf06-196">Pagination is supported for each of the four enabled sort orders.</span></span> 

<span data-ttu-id="dbf06-197">If a query response contains many (currently over 1000) items, the service returns an "\@odata.nextLink" property to get the next page of results.</span><span class="sxs-lookup"><span data-stu-id="dbf06-197">If a query response contains many (currently over 1000) items, the service returns an "\@odata.nextLink" property to get the next page of results.</span></span> <span data-ttu-id="dbf06-198">This can be used to page through the entire result set.</span><span class="sxs-lookup"><span data-stu-id="dbf06-198">This can be used to page through the entire result set.</span></span> <span data-ttu-id="dbf06-199">The page size is not configurable by the user.</span><span class="sxs-lookup"><span data-stu-id="dbf06-199">The page size is not configurable by the user.</span></span> 

<span data-ttu-id="dbf06-200">If Assets are created or deleted while paging through the collection, the changes are reflected in the returned results (if those changes are in the part of the collection that has not been downloaded.)</span><span class="sxs-lookup"><span data-stu-id="dbf06-200">If Assets are created or deleted while paging through the collection, the changes are reflected in the returned results (if those changes are in the part of the collection that has not been downloaded.)</span></span> 

<span data-ttu-id="dbf06-201">The following C# example shows how to enumerate through all the assets in the account.</span><span class="sxs-lookup"><span data-stu-id="dbf06-201">The following C# example shows how to enumerate through all the assets in the account.</span></span>

```csharp
var firstPage = await MediaServicesArmClient.Assets.ListAsync(CustomerResourceGroup, CustomerAccountName);

var currentPage = firstPage;
while (currentPage.NextPageLink != null)
{
    currentPage = await MediaServicesArmClient.Assets.ListNextAsync(currentPage.NextPageLink);
}
```

<span data-ttu-id="dbf06-202">For REST examples, see [Assets - List](https://docs.microsoft.com/rest/api/media/assets/list)</span><span class="sxs-lookup"><span data-stu-id="dbf06-202">For REST examples, see [Assets - List](https://docs.microsoft.com/rest/api/media/assets/list)</span></span>


## <a name="storage-side-encryption"></a><span data-ttu-id="dbf06-203">Storage side encryption</span><span class="sxs-lookup"><span data-stu-id="dbf06-203">Storage side encryption</span></span>

<span data-ttu-id="dbf06-204">To protect your Assets at rest, the assets should be encrypted by the storage side encryption.</span><span class="sxs-lookup"><span data-stu-id="dbf06-204">To protect your Assets at rest, the assets should be encrypted by the storage side encryption.</span></span> <span data-ttu-id="dbf06-205">The following table shows how the storage side encryption works in Media Services:</span><span class="sxs-lookup"><span data-stu-id="dbf06-205">The following table shows how the storage side encryption works in Media Services:</span></span>

|<span data-ttu-id="dbf06-206">Encryption option</span><span class="sxs-lookup"><span data-stu-id="dbf06-206">Encryption option</span></span>|<span data-ttu-id="dbf06-207">Description</span><span class="sxs-lookup"><span data-stu-id="dbf06-207">Description</span></span>|<span data-ttu-id="dbf06-208">Media Services v2</span><span class="sxs-lookup"><span data-stu-id="dbf06-208">Media Services v2</span></span>|<span data-ttu-id="dbf06-209">Media Services v3</span><span class="sxs-lookup"><span data-stu-id="dbf06-209">Media Services v3</span></span>|
|---|---|---|---|
|<span data-ttu-id="dbf06-210">Media Services Storage Encryption</span><span class="sxs-lookup"><span data-stu-id="dbf06-210">Media Services Storage Encryption</span></span>|<span data-ttu-id="dbf06-211">AES-256 encryption, key managed by Media Services</span><span class="sxs-lookup"><span data-stu-id="dbf06-211">AES-256 encryption, key managed by Media Services</span></span>|<span data-ttu-id="dbf06-212">Supported<sup>(1)</sup></span><span class="sxs-lookup"><span data-stu-id="dbf06-212">Supported<sup>(1)</sup></span></span>|<span data-ttu-id="dbf06-213">Not supported<sup>(2)</sup></span><span class="sxs-lookup"><span data-stu-id="dbf06-213">Not supported<sup>(2)</sup></span></span>|
|[<span data-ttu-id="dbf06-214">Storage Service Encryption for Data at Rest</span><span class="sxs-lookup"><span data-stu-id="dbf06-214">Storage Service Encryption for Data at Rest</span></span>](https://docs.microsoft.com/azure/storage/common/storage-service-encryption)|<span data-ttu-id="dbf06-215">Server-side encryption offered by Azure Storage, key managed by Azure or by customer</span><span class="sxs-lookup"><span data-stu-id="dbf06-215">Server-side encryption offered by Azure Storage, key managed by Azure or by customer</span></span>|<span data-ttu-id="dbf06-216">Supported</span><span class="sxs-lookup"><span data-stu-id="dbf06-216">Supported</span></span>|<span data-ttu-id="dbf06-217">Supported</span><span class="sxs-lookup"><span data-stu-id="dbf06-217">Supported</span></span>|
|[<span data-ttu-id="dbf06-218">Storage Client-Side Encryption</span><span class="sxs-lookup"><span data-stu-id="dbf06-218">Storage Client-Side Encryption</span></span>](https://docs.microsoft.com/azure/storage/common/storage-client-side-encryption)|<span data-ttu-id="dbf06-219">Client-side encryption offered by Azure storage, key managed by customer in Key Vault</span><span class="sxs-lookup"><span data-stu-id="dbf06-219">Client-side encryption offered by Azure storage, key managed by customer in Key Vault</span></span>|<span data-ttu-id="dbf06-220">Not supported</span><span class="sxs-lookup"><span data-stu-id="dbf06-220">Not supported</span></span>|<span data-ttu-id="dbf06-221">Not supported</span><span class="sxs-lookup"><span data-stu-id="dbf06-221">Not supported</span></span>|

<span data-ttu-id="dbf06-222"><sup>1</sup> While Media Services does support handling of content in the clear/without any form of encryption, doing so is not recommended.</span><span class="sxs-lookup"><span data-stu-id="dbf06-222"><sup>1</sup> While Media Services does support handling of content in the clear/without any form of encryption, doing so is not recommended.</span></span>

<span data-ttu-id="dbf06-223"><sup>2</sup> In Media Services v3, storage encryption (AES-256 encryption) is only supported for backwards compatibility when your Assets were created with Media Services v2.</span><span class="sxs-lookup"><span data-stu-id="dbf06-223"><sup>2</sup> In Media Services v3, storage encryption (AES-256 encryption) is only supported for backwards compatibility when your Assets were created with Media Services v2.</span></span> <span data-ttu-id="dbf06-224">Meaning v3 works with existing storage encrypted assets but will not allow creation of new ones.</span><span class="sxs-lookup"><span data-stu-id="dbf06-224">Meaning v3 works with existing storage encrypted assets but will not allow creation of new ones.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbf06-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbf06-225">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dbf06-226">Stream a file</span><span class="sxs-lookup"><span data-stu-id="dbf06-226">Stream a file</span></span>](stream-files-dotnet-quickstart.md)
