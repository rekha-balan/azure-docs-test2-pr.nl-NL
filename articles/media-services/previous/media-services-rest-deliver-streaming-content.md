---
title: Publish Azure Media Services content using REST
description: Learn how to create a locator that is used to build a streaming URL. The code uses REST API.
author: Juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2017
ms.author: juliako
ms.openlocfilehash: 8385dedd494c0cef968cb869ded3e92ce213da5e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857739"
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="71303-104">Publish Azure Media Services content using REST</span><span class="sxs-lookup"><span data-stu-id="71303-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [Portal](media-services-portal-publish.md)
> 
> 

<span data-ttu-id="71303-108">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span><span class="sxs-lookup"><span data-stu-id="71303-108">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="71303-109">The [encoding an asset](media-services-rest-encode-asset.md) article shows how to encode into an adaptive bitrate MP4 set.</span><span class="sxs-lookup"><span data-stu-id="71303-109">The [encoding an asset](media-services-rest-encode-asset.md) article shows how to encode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="71303-110">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) article) before creating a locator.</span><span class="sxs-lookup"><span data-stu-id="71303-110">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) article) before creating a locator.</span></span> 

<span data-ttu-id="71303-111">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span><span class="sxs-lookup"><span data-stu-id="71303-111">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="71303-112">This article shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="71303-112">This article shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="71303-113">It also shows hot to build progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="71303-113">It also shows hot to build progressive download URLs.</span></span>

<span data-ttu-id="71303-114">The [following](#types) section shows the enum types whose values are used in the REST calls.</span><span class="sxs-lookup"><span data-stu-id="71303-114">The [following](#types) section shows the enum types whose values are used in the REST calls.</span></span>   

> [!NOTE]
> When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="71303-117">Connect to Media Services</span><span class="sxs-lookup"><span data-stu-id="71303-117">Connect to Media Services</span></span>

<span data-ttu-id="71303-118">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="71303-118">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
>After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="71303-121">Create an OnDemand streaming locator</span><span class="sxs-lookup"><span data-stu-id="71303-121">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="71303-122">To create the OnDemand streaming locator and get URLs, you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="71303-122">To create the OnDemand streaming locator and get URLs, you need to do the following:</span></span>

1. <span data-ttu-id="71303-123">If the content is encrypted, define an access policy.</span><span class="sxs-lookup"><span data-stu-id="71303-123">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="71303-124">Create an OnDemand streaming locator.</span><span class="sxs-lookup"><span data-stu-id="71303-124">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="71303-125">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span><span class="sxs-lookup"><span data-stu-id="71303-125">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="71303-126">If you plan to progressively download, get the names of MP4 files in the asset.</span><span class="sxs-lookup"><span data-stu-id="71303-126">If you plan to progressively download, get the names of MP4 files in the asset.</span></span> 
4. <span data-ttu-id="71303-127">Build URLs to the manifest file or MP4 files.</span><span class="sxs-lookup"><span data-stu-id="71303-127">Build URLs to the manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="71303-128">You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span><span class="sxs-lookup"><span data-stu-id="71303-128">You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="71303-129">Create an access policy</span><span class="sxs-lookup"><span data-stu-id="71303-129">Create an access policy</span></span>

>[!NOTE]
>There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). Use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) article.

<span data-ttu-id="71303-133">Request:</span><span class="sxs-lookup"><span data-stu-id="71303-133">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="71303-134">Response:</span><span class="sxs-lookup"><span data-stu-id="71303-134">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="71303-135">Create an OnDemand streaming locator</span><span class="sxs-lookup"><span data-stu-id="71303-135">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="71303-136">Create the locator for the specified asset and asset policy.</span><span class="sxs-lookup"><span data-stu-id="71303-136">Create the locator for the specified asset and asset policy.</span></span>

<span data-ttu-id="71303-137">Request:</span><span class="sxs-lookup"><span data-stu-id="71303-137">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="71303-138">Response:</span><span class="sxs-lookup"><span data-stu-id="71303-138">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="71303-139">Build streaming URLs</span><span class="sxs-lookup"><span data-stu-id="71303-139">Build streaming URLs</span></span>
<span data-ttu-id="71303-140">Use the **Path** value returned after the creation of the locator to build the Smooth, HLS, and MPEG DASH URLs.</span><span class="sxs-lookup"><span data-stu-id="71303-140">Use the **Path** value returned after the creation of the locator to build the Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="71303-141">Smooth Streaming: **Path** + manifest file name + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="71303-141">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="71303-142">example:</span><span class="sxs-lookup"><span data-stu-id="71303-142">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="71303-143">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="71303-143">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="71303-144">example:</span><span class="sxs-lookup"><span data-stu-id="71303-144">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="71303-145">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="71303-145">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="71303-146">example:</span><span class="sxs-lookup"><span data-stu-id="71303-146">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="71303-147">Build progressive download URLs</span><span class="sxs-lookup"><span data-stu-id="71303-147">Build progressive download URLs</span></span>
<span data-ttu-id="71303-148">Use the **Path** value returned after the creation of the locator to build the progressive download URL.</span><span class="sxs-lookup"><span data-stu-id="71303-148">Use the **Path** value returned after the creation of the locator to build the progressive download URL.</span></span>   

<span data-ttu-id="71303-149">URL: **Path** + asset file mp4 name</span><span class="sxs-lookup"><span data-stu-id="71303-149">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="71303-150">example:</span><span class="sxs-lookup"><span data-stu-id="71303-150">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <a id="types"></a><span data-ttu-id="71303-151">Enum types</span><span class="sxs-lookup"><span data-stu-id="71303-151">Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="71303-152">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="71303-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="71303-153">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="71303-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="71303-154">See also</span><span class="sxs-lookup"><span data-stu-id="71303-154">See also</span></span>
[<span data-ttu-id="71303-155">Media Services operations REST API overview</span><span class="sxs-lookup"><span data-stu-id="71303-155">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="71303-156">Configure asset delivery policy</span><span class="sxs-lookup"><span data-stu-id="71303-156">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

