---
title: Publish Azure Media Services content using .NET
description: Learn how to create a locator that is used to build a streaming URL. Code samples are written in C# and use the Media Services SDK for .NET.
author: juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: juliako
ms.openlocfilehash: ebabd813b427ad04c978adcfe936a718ad302d7b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555378"
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="78e92-104">Publish Azure Media Services content using .NET</span><span class="sxs-lookup"><span data-stu-id="78e92-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [Portal](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="78e92-108">Overview</span><span class="sxs-lookup"><span data-stu-id="78e92-108">Overview</span></span>
<span data-ttu-id="78e92-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span><span class="sxs-lookup"><span data-stu-id="78e92-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="78e92-110">The [encoding an asset](media-services-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span><span class="sxs-lookup"><span data-stu-id="78e92-110">The [encoding an asset](media-services-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator. 
> 
> 

<span data-ttu-id="78e92-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span><span class="sxs-lookup"><span data-stu-id="78e92-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="78e92-113">This topic shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="78e92-113">This topic shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="78e92-114">It also shows hot to build progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="78e92-114">It also shows hot to build progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="78e92-115">Create an OnDemand streaming locator</span><span class="sxs-lookup"><span data-stu-id="78e92-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="78e92-116">To create the OnDemand streaming locator and get URLs you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="78e92-116">To create the OnDemand streaming locator and get URLs you need to do the following:</span></span>

1. <span data-ttu-id="78e92-117">If the content is encrypted, define an access policy.</span><span class="sxs-lookup"><span data-stu-id="78e92-117">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="78e92-118">Create an OnDemand streaming locator.</span><span class="sxs-lookup"><span data-stu-id="78e92-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="78e92-119">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span><span class="sxs-lookup"><span data-stu-id="78e92-119">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="78e92-120">If you plan to progressively download, get the names of MP4 files in the asset.</span><span class="sxs-lookup"><span data-stu-id="78e92-120">If you plan to progressively download, get the names of MP4 files in the asset.</span></span>  
4. <span data-ttu-id="78e92-121">Build URLs to the manifest file or MP4 files.</span><span class="sxs-lookup"><span data-stu-id="78e92-121">Build URLs to the manifest file or MP4 files.</span></span> 


>[!NOTE]
>There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="78e92-125">Use Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="78e92-125">Use Media Services .NET SDK</span></span>
<span data-ttu-id="78e92-126">Build Streaming URLs</span><span class="sxs-lookup"><span data-stu-id="78e92-126">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator to the streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference to the streaming manifest file from the  
        // collection of files in the asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL to the manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL to manifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL to manifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL to manifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="78e92-127">The code  outputs:</span><span class="sxs-lookup"><span data-stu-id="78e92-127">The code  outputs:</span></span>

    URL to manifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL to manifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL to manifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> You can also stream your content over an SSL connection. To do this, make sure your streaming URLs start with HTTPS. Note that, currently, AMS doesn�t support SSL with custom domains.  
> 
> 

<span data-ttu-id="78e92-131">Build progressive download URLs</span><span class="sxs-lookup"><span data-stu-id="78e92-131">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator to the asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL to the MP4 files. Use this to progressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="78e92-132">The code outputs:</span><span class="sxs-lookup"><span data-stu-id="78e92-132">The code outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="78e92-133">Use Media Services .NET SDK Extensions</span><span class="sxs-lookup"><span data-stu-id="78e92-133">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="78e92-134">The following code calls .NET SDK extensions methods that create a locator and generate the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming.</span><span class="sxs-lookup"><span data-stu-id="78e92-134">The following code calls .NET SDK extensions methods that create a locator and generate the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get the streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="78e92-135">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="78e92-135">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="78e92-136">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="78e92-136">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="78e92-137">See Also</span><span class="sxs-lookup"><span data-stu-id="78e92-137">See Also</span></span>
<span data-ttu-id="78e92-138">[Download assets](media-services-deliver-asset-download.md)
[Configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md)</span><span class="sxs-lookup"><span data-stu-id="78e92-138">[Download assets](media-services-deliver-asset-download.md)
[Configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md)</span></span>

