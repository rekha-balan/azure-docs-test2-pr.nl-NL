---
title: Creating Filters with Azure Media Services REST API | Microsoft Docs
description: This topic describes how to create filters so your client can use them to stream specific sections of a stream. Media Services creates dynamic manifests to achieve this selective streaming.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 8cb98bf2c3528299cd741713cb3410632a475a23
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556270"
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="d54c3-104">Creating Filters with Azure Media Services REST API</span><span class="sxs-lookup"><span data-stu-id="d54c3-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="d54c3-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span><span class="sxs-lookup"><span data-stu-id="d54c3-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="d54c3-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span><span class="sxs-lookup"><span data-stu-id="d54c3-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="d54c3-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span><span class="sxs-lookup"><span data-stu-id="d54c3-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="d54c3-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d54c3-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="d54c3-111">This topic shows how to use REST APIs to create, update, and delete filters.</span><span class="sxs-lookup"><span data-stu-id="d54c3-111">This topic shows how to use REST APIs to create, update, and delete filters.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="d54c3-112">Types used to create filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-112">Types used to create filters</span></span>
<span data-ttu-id="d54c3-113">The following types are used when creating filters:</span><span class="sxs-lookup"><span data-stu-id="d54c3-113">The following types are used when creating filters:</span></span>  

* [<span data-ttu-id="d54c3-114">Filter</span><span class="sxs-lookup"><span data-stu-id="d54c3-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="d54c3-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="d54c3-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="d54c3-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="d54c3-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="d54c3-117">FilterTrackSelect and FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="d54c3-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

> [!NOTE]
> When working with the Media Services REST API, the following considerations apply:
> 
> When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).
> 
> After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI as described in [Connecting to Media Services using REST API](media-services-rest-connect-programmatically.md). 
> 
> 

## <a name="create-filters"></a><span data-ttu-id="d54c3-123">Create filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-123">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="d54c3-124">Create global Filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-124">Create global Filters</span></span>
<span data-ttu-id="d54c3-125">To create a global Filter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="d54c3-125">To create a global Filter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="d54c3-126">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-126">HTTP Request</span></span>
<span data-ttu-id="d54c3-127">Request Headers</span><span class="sxs-lookup"><span data-stu-id="d54c3-127">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="d54c3-128">Request body</span><span class="sxs-lookup"><span data-stu-id="d54c3-128">Request body</span></span> 

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




#### <a name="http-response"></a><span data-ttu-id="d54c3-129">HTTP Response</span><span class="sxs-lookup"><span data-stu-id="d54c3-129">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="d54c3-130">Create local AssetFilters</span><span class="sxs-lookup"><span data-stu-id="d54c3-130">Create local AssetFilters</span></span>
<span data-ttu-id="d54c3-131">To create a local AssetFilter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="d54c3-131">To create a local AssetFilter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="d54c3-132">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-132">HTTP Request</span></span>
<span data-ttu-id="d54c3-133">Request Headers</span><span class="sxs-lookup"><span data-stu-id="d54c3-133">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="d54c3-134">Request body</span><span class="sxs-lookup"><span data-stu-id="d54c3-134">Request body</span></span> 

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

#### <a name="http-response"></a><span data-ttu-id="d54c3-135">HTTP Response</span><span class="sxs-lookup"><span data-stu-id="d54c3-135">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="d54c3-136">List filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-136">List filters</span></span>
### <a name="get-all-global-filters-in-the-ams-account"></a><span data-ttu-id="d54c3-137">Get all global **Filter**s in the AMS account</span><span class="sxs-lookup"><span data-stu-id="d54c3-137">Get all global **Filter**s in the AMS account</span></span>
<span data-ttu-id="d54c3-138">To list filters, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="d54c3-138">To list filters, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="d54c3-139">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-139">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="d54c3-140">Get **AssetFilter**s associated with an asset</span><span class="sxs-lookup"><span data-stu-id="d54c3-140">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="d54c3-141">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-141">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="d54c3-142">Get an **AssetFilter** based on its Id</span><span class="sxs-lookup"><span data-stu-id="d54c3-142">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="d54c3-143">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-143">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="d54c3-144">Update filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-144">Update filters</span></span>
<span data-ttu-id="d54c3-145">Use PATCH, PUT or MERGE to update a filter with new property values.</span><span class="sxs-lookup"><span data-stu-id="d54c3-145">Use PATCH, PUT or MERGE to update a filter with new property values.</span></span>  <span data-ttu-id="d54c3-146">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="d54c3-146">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="d54c3-147">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span><span class="sxs-lookup"><span data-stu-id="d54c3-147">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="d54c3-148">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span><span class="sxs-lookup"><span data-stu-id="d54c3-148">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="d54c3-149">It is recommend to clear the cache after updating the filter.</span><span class="sxs-lookup"><span data-stu-id="d54c3-149">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="d54c3-150">If this option is not possible, consider using a different filter.</span><span class="sxs-lookup"><span data-stu-id="d54c3-150">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="d54c3-151">Update global Filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-151">Update global Filters</span></span>
<span data-ttu-id="d54c3-152">To update a global filter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="d54c3-152">To update a global filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="d54c3-153">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-153">HTTP Request</span></span>
<span data-ttu-id="d54c3-154">Request headers:</span><span class="sxs-lookup"><span data-stu-id="d54c3-154">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="d54c3-155">Request body:</span><span class="sxs-lookup"><span data-stu-id="d54c3-155">Request body:</span></span> 

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

### <a name="update-local-assetfilters"></a><span data-ttu-id="d54c3-156">Update local AssetFilters</span><span class="sxs-lookup"><span data-stu-id="d54c3-156">Update local AssetFilters</span></span>
<span data-ttu-id="d54c3-157">To update a local filter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="d54c3-157">To update a local filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="d54c3-158">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-158">HTTP Request</span></span>
<span data-ttu-id="d54c3-159">Request headers:</span><span class="sxs-lookup"><span data-stu-id="d54c3-159">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="d54c3-160">Request body:</span><span class="sxs-lookup"><span data-stu-id="d54c3-160">Request body:</span></span> 

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


## <a name="delete-filters"></a><span data-ttu-id="d54c3-161">Delete filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-161">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="d54c3-162">Delete global Filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-162">Delete global Filters</span></span>
<span data-ttu-id="d54c3-163">To delete a global Filter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="d54c3-163">To delete a global Filter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="d54c3-164">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-164">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="d54c3-165">Delete local AssetFilters</span><span class="sxs-lookup"><span data-stu-id="d54c3-165">Delete local AssetFilters</span></span>
<span data-ttu-id="d54c3-166">To delete a local AssetFilter, use the following HTTP requests:</span><span class="sxs-lookup"><span data-stu-id="d54c3-166">To delete a local AssetFilter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="d54c3-167">HTTP Request</span><span class="sxs-lookup"><span data-stu-id="d54c3-167">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="d54c3-168">Build streaming URLs that use filters</span><span class="sxs-lookup"><span data-stu-id="d54c3-168">Build streaming URLs that use filters</span></span>
<span data-ttu-id="d54c3-169">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d54c3-169">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="d54c3-170">The following examples show how to add filters to your streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="d54c3-170">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="d54c3-171">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="d54c3-171">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="d54c3-172">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="d54c3-172">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="d54c3-173">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="d54c3-173">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="d54c3-174">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="d54c3-174">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="d54c3-175">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d54c3-175">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d54c3-176">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d54c3-176">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d54c3-177">See Also</span><span class="sxs-lookup"><span data-stu-id="d54c3-177">See Also</span></span>
[<span data-ttu-id="d54c3-178">Dynamic manifests overview</span><span class="sxs-lookup"><span data-stu-id="d54c3-178">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

