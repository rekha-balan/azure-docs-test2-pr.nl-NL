---
title: Creating Filters with Azure Media Services REST API | Microsoft Docs
description: This topic describes how to create filters so your client can use them to stream specific sections of a stream. Media Services creates dynamic manifests to achieve this selective streaming.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 12/07/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 396abe0801d76af3820d302d40d2fc076754741b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866856"
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="eba7d-104">Creating Filters with Azure Media Services REST API</span><span class="sxs-lookup"><span data-stu-id="eba7d-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="eba7d-107">Starting with 2.17 release, Media Services enables you to define filters for your assets.</span><span class="sxs-lookup"><span data-stu-id="eba7d-107">Starting with 2.17 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="eba7d-108">These filters are server-side rules that allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span><span class="sxs-lookup"><span data-stu-id="eba7d-108">These filters are server-side rules that allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="eba7d-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span><span class="sxs-lookup"><span data-stu-id="eba7d-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="eba7d-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eba7d-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="eba7d-111">This article shows how to use REST APIs to create, update, and delete filters.</span><span class="sxs-lookup"><span data-stu-id="eba7d-111">This article shows how to use REST APIs to create, update, and delete filters.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="eba7d-112">Types used to create filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-112">Types used to create filters</span></span>
<span data-ttu-id="eba7d-113">The following types are used when creating filters:</span><span class="sxs-lookup"><span data-stu-id="eba7d-113">The following types are used when creating filters:</span></span>  

* [<span data-ttu-id="eba7d-114">Filter</span><span class="sxs-lookup"><span data-stu-id="eba7d-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="eba7d-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="eba7d-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="eba7d-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="eba7d-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="eba7d-117">FilterTrackSelect and FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="eba7d-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

>When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).

## <a name="connect-to-media-services"></a><span data-ttu-id="eba7d-120">Connect to Media Services</span><span class="sxs-lookup"><span data-stu-id="eba7d-120">Connect to Media Services</span></span>

<span data-ttu-id="eba7d-121">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="eba7d-121">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

## <a name="create-filters"></a><span data-ttu-id="eba7d-122">Create filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-122">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="eba7d-123">Create global Filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-123">Create global Filters</span></span>
<span data-ttu-id="eba7d-124">To create a global Filter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="eba7d-124">To create a global Filter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="eba7d-125">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-125">HTTP Request</span></span>
<span data-ttu-id="eba7d-126">Request Headers</span><span class="sxs-lookup"><span data-stu-id="eba7d-126">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="eba7d-127">Request body</span><span class="sxs-lookup"><span data-stu-id="eba7d-127">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="eba7d-128">HTTP Response</span><span class="sxs-lookup"><span data-stu-id="eba7d-128">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="eba7d-129">Create local AssetFilters</span><span class="sxs-lookup"><span data-stu-id="eba7d-129">Create local AssetFilters</span></span>
<span data-ttu-id="eba7d-130">To create a local AssetFilter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="eba7d-130">To create a local AssetFilter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="eba7d-131">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-131">HTTP Request</span></span>
<span data-ttu-id="eba7d-132">Request Headers</span><span class="sxs-lookup"><span data-stu-id="eba7d-132">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="eba7d-133">Request body</span><span class="sxs-lookup"><span data-stu-id="eba7d-133">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="eba7d-134">HTTP Response</span><span class="sxs-lookup"><span data-stu-id="eba7d-134">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="eba7d-135">List filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-135">List filters</span></span>
### <a name="get-all-global-filters-in-the-ams-account"></a><span data-ttu-id="eba7d-136">Get all global **Filter**s in the AMS account</span><span class="sxs-lookup"><span data-stu-id="eba7d-136">Get all global **Filter**s in the AMS account</span></span>
<span data-ttu-id="eba7d-137">To list filters, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="eba7d-137">To list filters, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="eba7d-138">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-138">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="eba7d-139">Get **AssetFilter**s associated with an asset</span><span class="sxs-lookup"><span data-stu-id="eba7d-139">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="eba7d-140">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="eba7d-141">Get an **AssetFilter** based on its Id</span><span class="sxs-lookup"><span data-stu-id="eba7d-141">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="eba7d-142">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-142">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="eba7d-143">Update filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-143">Update filters</span></span>
<span data-ttu-id="eba7d-144">Use PATCH, PUT, or MERGE to update a filter with new property values.</span><span class="sxs-lookup"><span data-stu-id="eba7d-144">Use PATCH, PUT, or MERGE to update a filter with new property values.</span></span>  <span data-ttu-id="eba7d-145">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="eba7d-145">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="eba7d-146">If you update a filter, it can take up to two minutes for streaming endpoint to refresh the rules.</span><span class="sxs-lookup"><span data-stu-id="eba7d-146">If you update a filter, it can take up to two minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="eba7d-147">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span><span class="sxs-lookup"><span data-stu-id="eba7d-147">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="eba7d-148">Clear the cache after updating the filter.</span><span class="sxs-lookup"><span data-stu-id="eba7d-148">Clear the cache after updating the filter.</span></span> <span data-ttu-id="eba7d-149">If this option is not possible, consider using a different filter.</span><span class="sxs-lookup"><span data-stu-id="eba7d-149">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="eba7d-150">Update global Filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-150">Update global Filters</span></span>
<span data-ttu-id="eba7d-151">To update a global filter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="eba7d-151">To update a global filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="eba7d-152">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-152">HTTP Request</span></span>
<span data-ttu-id="eba7d-153">Request headers:</span><span class="sxs-lookup"><span data-stu-id="eba7d-153">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="eba7d-154">Request body:</span><span class="sxs-lookup"><span data-stu-id="eba7d-154">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="eba7d-155">Update local AssetFilters</span><span class="sxs-lookup"><span data-stu-id="eba7d-155">Update local AssetFilters</span></span>
<span data-ttu-id="eba7d-156">To update a local filter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="eba7d-156">To update a local filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="eba7d-157">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-157">HTTP Request</span></span>
<span data-ttu-id="eba7d-158">Request headers:</span><span class="sxs-lookup"><span data-stu-id="eba7d-158">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="eba7d-159">Request body:</span><span class="sxs-lookup"><span data-stu-id="eba7d-159">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="eba7d-160">Delete filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-160">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="eba7d-161">Delete global Filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-161">Delete global Filters</span></span>
<span data-ttu-id="eba7d-162">To delete a global Filter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="eba7d-162">To delete a global Filter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="eba7d-163">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-163">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN>  
    x-ms-version: 2.17 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="eba7d-164">Delete local AssetFilters</span><span class="sxs-lookup"><span data-stu-id="eba7d-164">Delete local AssetFilters</span></span>
<span data-ttu-id="eba7d-165">To delete a local AssetFilter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="eba7d-165">To delete a local AssetFilter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="eba7d-166">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="eba7d-166">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="eba7d-167">Build streaming URLs that use filters</span><span class="sxs-lookup"><span data-stu-id="eba7d-167">Build streaming URLs that use filters</span></span>
<span data-ttu-id="eba7d-168">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eba7d-168">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="eba7d-169">The following examples show how to add filters to your streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="eba7d-169">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="eba7d-170">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="eba7d-170">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="eba7d-171">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="eba7d-171">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="eba7d-172">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="eba7d-172">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="eba7d-173">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="eba7d-173">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="eba7d-174">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="eba7d-174">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="eba7d-175">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="eba7d-175">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="eba7d-176">See Also</span><span class="sxs-lookup"><span data-stu-id="eba7d-176">See Also</span></span>
[<span data-ttu-id="eba7d-177">Dynamic manifests overview</span><span class="sxs-lookup"><span data-stu-id="eba7d-177">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

