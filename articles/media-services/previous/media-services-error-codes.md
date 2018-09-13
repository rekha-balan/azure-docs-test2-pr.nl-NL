---
title: Azure Media Services error codes | Microsoft Docs
description: The topic gives an overview of Azure Media Services error codes.
author: Juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 8a374393a6a5b3d563a441654b7b5df8a510f304
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867787"
---
# <a name="azure-media-services-error-codes"></a><span data-ttu-id="b6b25-103">Azure Media Services error codes</span><span class="sxs-lookup"><span data-stu-id="b6b25-103">Azure Media Services error codes</span></span>
<span data-ttu-id="b6b25-104">When using Microsoft Azure Media Services, you may receive HTTP error codes from the service depending on issues such as authentication tokens expiring to actions that are not supported in Media Services.</span><span class="sxs-lookup"><span data-stu-id="b6b25-104">When using Microsoft Azure Media Services, you may receive HTTP error codes from the service depending on issues such as authentication tokens expiring to actions that are not supported in Media Services.</span></span> <span data-ttu-id="b6b25-105">The following is a list of **HTTP error codes** that may be returned by Media Services and the possible causes for them.</span><span class="sxs-lookup"><span data-stu-id="b6b25-105">The following is a list of **HTTP error codes** that may be returned by Media Services and the possible causes for them.</span></span>  

## <a name="400-bad-request"></a><span data-ttu-id="b6b25-106">400 Bad Request</span><span class="sxs-lookup"><span data-stu-id="b6b25-106">400 Bad Request</span></span>
<span data-ttu-id="b6b25-107">The request contains invalid information and is rejected due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b6b25-107">The request contains invalid information and is rejected due to one of the following reasons:</span></span>

* <span data-ttu-id="b6b25-108">An unsupported API version is specified.</span><span class="sxs-lookup"><span data-stu-id="b6b25-108">An unsupported API version is specified.</span></span> <span data-ttu-id="b6b25-109">For the most current version, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b6b25-109">For the most current version, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="b6b25-110">The API version of Media Services is not specified.</span><span class="sxs-lookup"><span data-stu-id="b6b25-110">The API version of Media Services is not specified.</span></span> <span data-ttu-id="b6b25-111">For information on how to specify the API version, see [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="b6b25-111">For information on how to specify the API version, see [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="b6b25-112">If you are using the .NET or Java SDKs to connect to Media Services, the API version is specified for you whenever you try and perform some action against Media Services.</span><span class="sxs-lookup"><span data-stu-id="b6b25-112">If you are using the .NET or Java SDKs to connect to Media Services, the API version is specified for you whenever you try and perform some action against Media Services.</span></span>
  > 
  > 
* <span data-ttu-id="b6b25-113">An undefined property has been specified.</span><span class="sxs-lookup"><span data-stu-id="b6b25-113">An undefined property has been specified.</span></span> <span data-ttu-id="b6b25-114">The property name is in the error message.</span><span class="sxs-lookup"><span data-stu-id="b6b25-114">The property name is in the error message.</span></span> <span data-ttu-id="b6b25-115">Only those properties that are members of a given entity can be specified.</span><span class="sxs-lookup"><span data-stu-id="b6b25-115">Only those properties that are members of a given entity can be specified.</span></span> <span data-ttu-id="b6b25-116">See [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) for a list of entities and their properties.</span><span class="sxs-lookup"><span data-stu-id="b6b25-116">See [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) for a list of entities and their properties.</span></span>
* <span data-ttu-id="b6b25-117">An invalid property value has been specified.</span><span class="sxs-lookup"><span data-stu-id="b6b25-117">An invalid property value has been specified.</span></span> <span data-ttu-id="b6b25-118">The property name is in the error message.</span><span class="sxs-lookup"><span data-stu-id="b6b25-118">The property name is in the error message.</span></span> <span data-ttu-id="b6b25-119">See the previous link for valid property types and their values.</span><span class="sxs-lookup"><span data-stu-id="b6b25-119">See the previous link for valid property types and their values.</span></span>
* <span data-ttu-id="b6b25-120">A property value is missing and is required.</span><span class="sxs-lookup"><span data-stu-id="b6b25-120">A property value is missing and is required.</span></span>
* <span data-ttu-id="b6b25-121">Part of the URL specified contains a bad value.</span><span class="sxs-lookup"><span data-stu-id="b6b25-121">Part of the URL specified contains a bad value.</span></span>
* <span data-ttu-id="b6b25-122">An attempt was made to update a WriteOnce property.</span><span class="sxs-lookup"><span data-stu-id="b6b25-122">An attempt was made to update a WriteOnce property.</span></span>
* <span data-ttu-id="b6b25-123">An attempt was made to create a Job that has an input Asset with a primary AssetFile that was not specified or could not be determined.</span><span class="sxs-lookup"><span data-stu-id="b6b25-123">An attempt was made to create a Job that has an input Asset with a primary AssetFile that was not specified or could not be determined.</span></span>
* <span data-ttu-id="b6b25-124">An attempt was made to update a SAS Locator.</span><span class="sxs-lookup"><span data-stu-id="b6b25-124">An attempt was made to update a SAS Locator.</span></span> <span data-ttu-id="b6b25-125">SAS locators can only be created or deleted.</span><span class="sxs-lookup"><span data-stu-id="b6b25-125">SAS locators can only be created or deleted.</span></span> <span data-ttu-id="b6b25-126">Streaming locators can be updated.</span><span class="sxs-lookup"><span data-stu-id="b6b25-126">Streaming locators can be updated.</span></span> <span data-ttu-id="b6b25-127">For more information, see [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="b6b25-127">For more information, see [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>
* <span data-ttu-id="b6b25-128">An unsupported operation or query was submitted.</span><span class="sxs-lookup"><span data-stu-id="b6b25-128">An unsupported operation or query was submitted.</span></span>

## <a name="401-unauthorized"></a><span data-ttu-id="b6b25-129">401 Unauthorized</span><span class="sxs-lookup"><span data-stu-id="b6b25-129">401 Unauthorized</span></span>
<span data-ttu-id="b6b25-130">The request could not be authenticated (before it can be authorized) due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b6b25-130">The request could not be authenticated (before it can be authorized) due to one of the following reasons:</span></span>

* <span data-ttu-id="b6b25-131">Missing authentication header.</span><span class="sxs-lookup"><span data-stu-id="b6b25-131">Missing authentication header.</span></span>
* <span data-ttu-id="b6b25-132">Bad authentication header value.</span><span class="sxs-lookup"><span data-stu-id="b6b25-132">Bad authentication header value.</span></span>
  * <span data-ttu-id="b6b25-133">The token has expired.</span><span class="sxs-lookup"><span data-stu-id="b6b25-133">The token has expired.</span></span> 
  * <span data-ttu-id="b6b25-134">The token contains an invalid signature.</span><span class="sxs-lookup"><span data-stu-id="b6b25-134">The token contains an invalid signature.</span></span>

## <a name="403-forbidden"></a><span data-ttu-id="b6b25-135">403 Forbidden</span><span class="sxs-lookup"><span data-stu-id="b6b25-135">403 Forbidden</span></span>
<span data-ttu-id="b6b25-136">The request is not allowed due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b6b25-136">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="b6b25-137">The Media Services account cannot be found or has been deleted.</span><span class="sxs-lookup"><span data-stu-id="b6b25-137">The Media Services account cannot be found or has been deleted.</span></span>
* <span data-ttu-id="b6b25-138">The Media Services account is disabled and the request type is not HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="b6b25-138">The Media Services account is disabled and the request type is not HTTP GET.</span></span> <span data-ttu-id="b6b25-139">Service operations will return a 403 response as well.</span><span class="sxs-lookup"><span data-stu-id="b6b25-139">Service operations will return a 403 response as well.</span></span>
* <span data-ttu-id="b6b25-140">The authentication token does not contain the user’s credential information: AccountName and/or SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="b6b25-140">The authentication token does not contain the user’s credential information: AccountName and/or SubscriptionId.</span></span> <span data-ttu-id="b6b25-141">You can find this information in the Media Services UI extension for your Media Services account in the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="b6b25-141">You can find this information in the Media Services UI extension for your Media Services account in the Azure Management Portal.</span></span>
* <span data-ttu-id="b6b25-142">The resource cannot be accessed.</span><span class="sxs-lookup"><span data-stu-id="b6b25-142">The resource cannot be accessed.</span></span>
  
  * <span data-ttu-id="b6b25-143">An attempt was made to use a MediaProcessor that is not available for your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="b6b25-143">An attempt was made to use a MediaProcessor that is not available for your Media Services account.</span></span>
  * <span data-ttu-id="b6b25-144">An attempt was made to update a JobTemplate defined by Media Services.</span><span class="sxs-lookup"><span data-stu-id="b6b25-144">An attempt was made to update a JobTemplate defined by Media Services.</span></span>
  * <span data-ttu-id="b6b25-145">An attempt was made to overwrite some other Media Services account's Locator.</span><span class="sxs-lookup"><span data-stu-id="b6b25-145">An attempt was made to overwrite some other Media Services account's Locator.</span></span>
  * <span data-ttu-id="b6b25-146">An attempt was made to overwrite some other Media Services account's ContentKey.</span><span class="sxs-lookup"><span data-stu-id="b6b25-146">An attempt was made to overwrite some other Media Services account's ContentKey.</span></span>
* <span data-ttu-id="b6b25-147">The resource could not be created due to a service quota that was reached for the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="b6b25-147">The resource could not be created due to a service quota that was reached for the Media Services account.</span></span> <span data-ttu-id="b6b25-148">For more information on the service quotas, see [Quotas and Limitations](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="b6b25-148">For more information on the service quotas, see [Quotas and Limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="404-not-found"></a><span data-ttu-id="b6b25-149">404 Not Found</span><span class="sxs-lookup"><span data-stu-id="b6b25-149">404 Not Found</span></span>
<span data-ttu-id="b6b25-150">The request is not allowed on a resource due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b6b25-150">The request is not allowed on a resource due to one of the following reasons:</span></span>

* <span data-ttu-id="b6b25-151">An attempt was made to update an entity that does not exist.</span><span class="sxs-lookup"><span data-stu-id="b6b25-151">An attempt was made to update an entity that does not exist.</span></span>
* <span data-ttu-id="b6b25-152">An attempt was made to delete an entity that does not exist.</span><span class="sxs-lookup"><span data-stu-id="b6b25-152">An attempt was made to delete an entity that does not exist.</span></span>
* <span data-ttu-id="b6b25-153">An attempt was made to create an entity that links to an entity that does not exist.</span><span class="sxs-lookup"><span data-stu-id="b6b25-153">An attempt was made to create an entity that links to an entity that does not exist.</span></span>
* <span data-ttu-id="b6b25-154">An attempt was made to GET an entity that does not exist.</span><span class="sxs-lookup"><span data-stu-id="b6b25-154">An attempt was made to GET an entity that does not exist.</span></span>
* <span data-ttu-id="b6b25-155">An attempt was made to specify a storage account that is not associated with the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="b6b25-155">An attempt was made to specify a storage account that is not associated with the Media Services account.</span></span>  

## <a name="409-conflict"></a><span data-ttu-id="b6b25-156">409 Conflict</span><span class="sxs-lookup"><span data-stu-id="b6b25-156">409 Conflict</span></span>
<span data-ttu-id="b6b25-157">The request is not allowed due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b6b25-157">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="b6b25-158">More than one AssetFile has the specified name within the Asset.</span><span class="sxs-lookup"><span data-stu-id="b6b25-158">More than one AssetFile has the specified name within the Asset.</span></span>
* <span data-ttu-id="b6b25-159">An attempt was made to create a second primary AssetFile within the Asset.</span><span class="sxs-lookup"><span data-stu-id="b6b25-159">An attempt was made to create a second primary AssetFile within the Asset.</span></span>
* <span data-ttu-id="b6b25-160">An attempt was made to create a ContentKey with the specified Id already used.</span><span class="sxs-lookup"><span data-stu-id="b6b25-160">An attempt was made to create a ContentKey with the specified Id already used.</span></span>
* <span data-ttu-id="b6b25-161">An attempt was made to create a Locator with the specified Id already used.</span><span class="sxs-lookup"><span data-stu-id="b6b25-161">An attempt was made to create a Locator with the specified Id already used.</span></span>
* <span data-ttu-id="b6b25-162">More than one IngestManifestFile has the specified name within the IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="b6b25-162">More than one IngestManifestFile has the specified name within the IngestManifest.</span></span>
* <span data-ttu-id="b6b25-163">An attempt was made to link a second storage encryption ContentKey to the storage-encrypted Asset.</span><span class="sxs-lookup"><span data-stu-id="b6b25-163">An attempt was made to link a second storage encryption ContentKey to the storage-encrypted Asset.</span></span>
* <span data-ttu-id="b6b25-164">An attempt was made to link the same ContentKey to the Asset.</span><span class="sxs-lookup"><span data-stu-id="b6b25-164">An attempt was made to link the same ContentKey to the Asset.</span></span>
* <span data-ttu-id="b6b25-165">An attempt was made to create a locator to an Asset whose storage container is missing or is no longer associated with the Asset.</span><span class="sxs-lookup"><span data-stu-id="b6b25-165">An attempt was made to create a locator to an Asset whose storage container is missing or is no longer associated with the Asset.</span></span>
* <span data-ttu-id="b6b25-166">An attempt was made to create a locator to an Asset which already has 5 locators in use.</span><span class="sxs-lookup"><span data-stu-id="b6b25-166">An attempt was made to create a locator to an Asset which already has 5 locators in use.</span></span> <span data-ttu-id="b6b25-167">(Azure Storage enforces the limit of five shared access policies on one storage container.)</span><span class="sxs-lookup"><span data-stu-id="b6b25-167">(Azure Storage enforces the limit of five shared access policies on one storage container.)</span></span>
* <span data-ttu-id="b6b25-168">Linking storage account of an Asset to an IngestManifestAsset is not the same as the storage account used by the parent IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="b6b25-168">Linking storage account of an Asset to an IngestManifestAsset is not the same as the storage account used by the parent IngestManifest.</span></span>  

## <a name="500-internal-server-error"></a><span data-ttu-id="b6b25-169">500 Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="b6b25-169">500 Internal Server Error</span></span>
<span data-ttu-id="b6b25-170">During the processing of the request, Media Services encounters some error that prevents the processing from continuing.</span><span class="sxs-lookup"><span data-stu-id="b6b25-170">During the processing of the request, Media Services encounters some error that prevents the processing from continuing.</span></span> <span data-ttu-id="b6b25-171">This could be due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b6b25-171">This could be due to one of the following reasons:</span></span>

* <span data-ttu-id="b6b25-172">Creating an Asset or Job fails because the Media Services account's service quota information is temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="b6b25-172">Creating an Asset or Job fails because the Media Services account's service quota information is temporarily unavailable.</span></span>
* <span data-ttu-id="b6b25-173">Creating an Asset or IngestManifest blob storage container fails because the account's storage account information is temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="b6b25-173">Creating an Asset or IngestManifest blob storage container fails because the account's storage account information is temporarily unavailable.</span></span>
* <span data-ttu-id="b6b25-174">Other unexpected error.</span><span class="sxs-lookup"><span data-stu-id="b6b25-174">Other unexpected error.</span></span>

## <a name="503-service-unavailable"></a><span data-ttu-id="b6b25-175">503 Service Unavailable</span><span class="sxs-lookup"><span data-stu-id="b6b25-175">503 Service Unavailable</span></span>
<span data-ttu-id="b6b25-176">The server is currently unable to receive requests.</span><span class="sxs-lookup"><span data-stu-id="b6b25-176">The server is currently unable to receive requests.</span></span> <span data-ttu-id="b6b25-177">This error may be caused by excessive requests to the service.</span><span class="sxs-lookup"><span data-stu-id="b6b25-177">This error may be caused by excessive requests to the service.</span></span> <span data-ttu-id="b6b25-178">Media Services throttling mechanism restricts the resource usage for applications that make excessive request to the service.</span><span class="sxs-lookup"><span data-stu-id="b6b25-178">Media Services throttling mechanism restricts the resource usage for applications that make excessive request to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="b6b25-179">Check the error message and error code string to get more detailed information about the reason you got the 503 error.</span><span class="sxs-lookup"><span data-stu-id="b6b25-179">Check the error message and error code string to get more detailed information about the reason you got the 503 error.</span></span> <span data-ttu-id="b6b25-180">This error does not always mean throttling.</span><span class="sxs-lookup"><span data-stu-id="b6b25-180">This error does not always mean throttling.</span></span>
> 
> 

<span data-ttu-id="b6b25-181">Possible status descriptions are:</span><span class="sxs-lookup"><span data-stu-id="b6b25-181">Possible status descriptions are:</span></span>

* <span data-ttu-id="b6b25-182">"Server is busy.</span><span class="sxs-lookup"><span data-stu-id="b6b25-182">"Server is busy.</span></span> <span data-ttu-id="b6b25-183">Previous runs of this type of request took more than {0} seconds."</span><span class="sxs-lookup"><span data-stu-id="b6b25-183">Previous runs of this type of request took more than {0} seconds."</span></span>
* <span data-ttu-id="b6b25-184">"Server is busy.</span><span class="sxs-lookup"><span data-stu-id="b6b25-184">"Server is busy.</span></span> <span data-ttu-id="b6b25-185">More than {0} requests per second can be throttled."</span><span class="sxs-lookup"><span data-stu-id="b6b25-185">More than {0} requests per second can be throttled."</span></span>
* <span data-ttu-id="b6b25-186">"Server is busy.</span><span class="sxs-lookup"><span data-stu-id="b6b25-186">"Server is busy.</span></span> <span data-ttu-id="b6b25-187">More than {0} requests within {1} seconds can be throttled."</span><span class="sxs-lookup"><span data-stu-id="b6b25-187">More than {0} requests within {1} seconds can be throttled."</span></span>

<span data-ttu-id="b6b25-188">To handle this error, we recommend using exponential back-off retry logic.</span><span class="sxs-lookup"><span data-stu-id="b6b25-188">To handle this error, we recommend using exponential back-off retry logic.</span></span> <span data-ttu-id="b6b25-189">That means using progressively longer waits between retries for consecutive error responses.</span><span class="sxs-lookup"><span data-stu-id="b6b25-189">That means using progressively longer waits between retries for consecutive error responses.</span></span>  <span data-ttu-id="b6b25-190">For more information, see [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6b25-190">For more information, see [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b6b25-191">If you are using [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), the retry logic for the 503 error has been implemented by the SDK.</span><span class="sxs-lookup"><span data-stu-id="b6b25-191">If you are using [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), the retry logic for the 503 error has been implemented by the SDK.</span></span>  
> 
> 

## <a name="see-also"></a><span data-ttu-id="b6b25-192">See Also</span><span class="sxs-lookup"><span data-stu-id="b6b25-192">See Also</span></span>
[<span data-ttu-id="b6b25-193">Media Services Management Error Codes</span><span class="sxs-lookup"><span data-stu-id="b6b25-193">Media Services Management Error Codes</span></span>](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a><span data-ttu-id="b6b25-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6b25-194">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b6b25-195">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="b6b25-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

