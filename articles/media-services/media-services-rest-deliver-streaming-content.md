---
title: Publish Azure Media Services content using REST
description: Learn how to create a locator that is used to build a streaming URL. The code uses REST API.
author: Juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: juliako
ms.openlocfilehash: bb3ae3d26d174d0f37cc348cde570250699bf067
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671216"
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="efe00-104">Publish Azure Media Services content using REST</span><span class="sxs-lookup"><span data-stu-id="efe00-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [Portal](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="efe00-108">Overview</span><span class="sxs-lookup"><span data-stu-id="efe00-108">Overview</span></span>
<span data-ttu-id="efe00-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span><span class="sxs-lookup"><span data-stu-id="efe00-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="efe00-110">The [encoding an asset](media-services-rest-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span><span class="sxs-lookup"><span data-stu-id="efe00-110">The [encoding an asset](media-services-rest-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="efe00-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span><span class="sxs-lookup"><span data-stu-id="efe00-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="efe00-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span><span class="sxs-lookup"><span data-stu-id="efe00-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="efe00-113">This topic shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="efe00-113">This topic shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="efe00-114">It also shows hot to build progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="efe00-114">It also shows hot to build progressive download URLs.</span></span>

<span data-ttu-id="efe00-115">The [following](#types) section shows the enum types whose values are used in the REST calls.</span><span class="sxs-lookup"><span data-stu-id="efe00-115">The [following](#types) section shows the enum types whose values are used in the REST calls.</span></span>   

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="efe00-116">Create an OnDemand streaming locator</span><span class="sxs-lookup"><span data-stu-id="efe00-116">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="efe00-117">To create the OnDemand streaming locator and get URLs you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="efe00-117">To create the OnDemand streaming locator and get URLs you need to do the following:</span></span>

1. <span data-ttu-id="efe00-118">If the content is encrypted, define an access policy.</span><span class="sxs-lookup"><span data-stu-id="efe00-118">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="efe00-119">Create an OnDemand streaming locator.</span><span class="sxs-lookup"><span data-stu-id="efe00-119">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="efe00-120">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span><span class="sxs-lookup"><span data-stu-id="efe00-120">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="efe00-121">If you plan to progressively download, get the names of MP4 files in the asset.</span><span class="sxs-lookup"><span data-stu-id="efe00-121">If you plan to progressively download, get the names of MP4 files in the asset.</span></span> 
4. <span data-ttu-id="efe00-122">Build URLs to the manifest file or MP4 files.</span><span class="sxs-lookup"><span data-stu-id="efe00-122">Build URLs to the manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="efe00-123">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span><span class="sxs-lookup"><span data-stu-id="efe00-123">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="efe00-124">Create an access policy</span><span class="sxs-lookup"><span data-stu-id="efe00-124">Create an access policy</span></span>

>[!NOTE]
>There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.

<span data-ttu-id="efe00-128">Request:</span><span class="sxs-lookup"><span data-stu-id="efe00-128">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="efe00-129">Response:</span><span class="sxs-lookup"><span data-stu-id="efe00-129">Response:</span></span>

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

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="efe00-130">Create an OnDemand streaming locator</span><span class="sxs-lookup"><span data-stu-id="efe00-130">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="efe00-131">Create the locator for the specified asset and asset policy.</span><span class="sxs-lookup"><span data-stu-id="efe00-131">Create the locator for the specified asset and asset policy.</span></span>

<span data-ttu-id="efe00-132">Request:</span><span class="sxs-lookup"><span data-stu-id="efe00-132">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="efe00-133">Response:</span><span class="sxs-lookup"><span data-stu-id="efe00-133">Response:</span></span>

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

### <a name="build-streaming-urls"></a><span data-ttu-id="efe00-134">Build streaming URLs</span><span class="sxs-lookup"><span data-stu-id="efe00-134">Build streaming URLs</span></span>
<span data-ttu-id="efe00-135">Use the **Path** value returned after the creation of the locator to build the Smooth, HLS, and MPEG DASH URLs.</span><span class="sxs-lookup"><span data-stu-id="efe00-135">Use the **Path** value returned after the creation of the locator to build the Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="efe00-136">Smooth Streaming: **Path** + manifest file name + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="efe00-136">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="efe00-137">example:</span><span class="sxs-lookup"><span data-stu-id="efe00-137">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="efe00-138">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="efe00-138">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="efe00-139">example:</span><span class="sxs-lookup"><span data-stu-id="efe00-139">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="efe00-140">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="efe00-140">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="efe00-141">example:</span><span class="sxs-lookup"><span data-stu-id="efe00-141">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="efe00-142">Build progressive download URLs</span><span class="sxs-lookup"><span data-stu-id="efe00-142">Build progressive download URLs</span></span>
<span data-ttu-id="efe00-143">Use the **Path** value returned after the creation of the locator to build the progressive download URL.</span><span class="sxs-lookup"><span data-stu-id="efe00-143">Use the **Path** value returned after the creation of the locator to build the progressive download URL.</span></span>   

<span data-ttu-id="efe00-144">URL: **Path** + asset file mp4 name</span><span class="sxs-lookup"><span data-stu-id="efe00-144">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="efe00-145">example:</span><span class="sxs-lookup"><span data-stu-id="efe00-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <a id="types"></a><span data-ttu-id="efe00-146">Enum types</span><span class="sxs-lookup"><span data-stu-id="efe00-146">Enum types</span></span>
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="efe00-147">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="efe00-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="efe00-148">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="efe00-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="efe00-149">See also</span><span class="sxs-lookup"><span data-stu-id="efe00-149">See also</span></span>
[<span data-ttu-id="efe00-150">Configure asset delivery policy</span><span class="sxs-lookup"><span data-stu-id="efe00-150">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

