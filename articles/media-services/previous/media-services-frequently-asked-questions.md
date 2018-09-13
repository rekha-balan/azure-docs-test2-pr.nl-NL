---
title: Azure Media Services frequently asked questions | Microsoft Docs
description: Frequently asked questions (FAQs)
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2017
ms.author: juliako
ms.openlocfilehash: a47163d06e24814ca5724d1fabea84058f8764cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858021"
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="e42c0-103">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="e42c0-103">Frequently asked questions</span></span>

<span data-ttu-id="e42c0-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span><span class="sxs-lookup"><span data-stu-id="e42c0-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="e42c0-105">General AMS FAQs</span><span class="sxs-lookup"><span data-stu-id="e42c0-105">General AMS FAQs</span></span>

<span data-ttu-id="e42c0-106">Q: How do you stream to Apple iOS devices</span><span class="sxs-lookup"><span data-stu-id="e42c0-106">Q: How do you stream to Apple iOS devices</span></span>

<span data-ttu-id="e42c0-107">A: add "(format=m3u8-aapl)" path to the "/Manifest" portion of the URL to tell the streaming origin server to return back HLS content for consumption on Apple iOS native devices (for details, see (delivering content)[media-services-deliver-content-overview.md]),</span><span class="sxs-lookup"><span data-stu-id="e42c0-107">A: add "(format=m3u8-aapl)" path to the "/Manifest" portion of the URL to tell the streaming origin server to return back HLS content for consumption on Apple iOS native devices (for details, see (delivering content)[media-services-deliver-content-overview.md]),</span></span>

<span data-ttu-id="e42c0-108">Q: How do you scale indexing?</span><span class="sxs-lookup"><span data-stu-id="e42c0-108">Q: How do you scale indexing?</span></span>

<span data-ttu-id="e42c0-109">A: The reserved units are the same for Encoding and Indexing tasks.</span><span class="sxs-lookup"><span data-stu-id="e42c0-109">A: The reserved units are the same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="e42c0-110">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e42c0-110">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="e42c0-111">**Note** that Indexer performance is not affected by Reserved Unit Type.</span><span class="sxs-lookup"><span data-stu-id="e42c0-111">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="e42c0-112">Q: I uploaded, encoded, and published a video.</span><span class="sxs-lookup"><span data-stu-id="e42c0-112">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="e42c0-113">What would be the reason the video does not play when I try to stream it?</span><span class="sxs-lookup"><span data-stu-id="e42c0-113">What would be the reason the video does not play when I try to stream it?</span></span>

<span data-ttu-id="e42c0-114">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="e42c0-114">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span></span>  

<span data-ttu-id="e42c0-115">Q: Can I do compositing on a live stream?</span><span class="sxs-lookup"><span data-stu-id="e42c0-115">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="e42c0-116">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span><span class="sxs-lookup"><span data-stu-id="e42c0-116">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span></span>

<span data-ttu-id="e42c0-117">Q: Can I use Azure CDN with Live Streaming?</span><span class="sxs-lookup"><span data-stu-id="e42c0-117">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="e42c0-118">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="e42c0-118">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="e42c0-119">You can use Live streaming with CDN.</span><span class="sxs-lookup"><span data-stu-id="e42c0-119">You can use Live streaming with CDN.</span></span> <span data-ttu-id="e42c0-120">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span><span class="sxs-lookup"><span data-stu-id="e42c0-120">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="e42c0-121">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span><span class="sxs-lookup"><span data-stu-id="e42c0-121">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="e42c0-122">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span><span class="sxs-lookup"><span data-stu-id="e42c0-122">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="e42c0-123">Only data needs to be refreshed is the manifest data.</span><span class="sxs-lookup"><span data-stu-id="e42c0-123">Only data needs to be refreshed is the manifest data.</span></span> <span data-ttu-id="e42c0-124">CDN periodically refreshes manifest data.</span><span class="sxs-lookup"><span data-stu-id="e42c0-124">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="e42c0-125">Q: Does Azure Media services support storing images?</span><span class="sxs-lookup"><span data-stu-id="e42c0-125">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="e42c0-126">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e42c0-126">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="e42c0-127">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span><span class="sxs-lookup"><span data-stu-id="e42c0-127">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="e42c0-128">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span><span class="sxs-lookup"><span data-stu-id="e42c0-128">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="e42c0-129">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="e42c0-129">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="e42c0-130">Q: How can I copy assets from one Media Services account to another.</span><span class="sxs-lookup"><span data-stu-id="e42c0-130">Q: How can I copy assets from one Media Services account to another.</span></span>

<span data-ttu-id="e42c0-131">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span><span class="sxs-lookup"><span data-stu-id="e42c0-131">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="e42c0-132">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span><span class="sxs-lookup"><span data-stu-id="e42c0-132">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="e42c0-133">Q: What are the supported characters for naming files when working with AMS?</span><span class="sxs-lookup"><span data-stu-id="e42c0-133">Q: What are the supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="e42c0-134">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span><span class="sxs-lookup"><span data-stu-id="e42c0-134">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="e42c0-135">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !\*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="e42c0-135">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !\*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="e42c0-136">Also, there can only be one ‘.’</span><span class="sxs-lookup"><span data-stu-id="e42c0-136">Also, there can only be one ‘.’</span></span> <span data-ttu-id="e42c0-137">for the file name extension.</span><span class="sxs-lookup"><span data-stu-id="e42c0-137">for the file name extension.</span></span>

<span data-ttu-id="e42c0-138">Q: How to connect using REST?</span><span class="sxs-lookup"><span data-stu-id="e42c0-138">Q: How to connect using REST?</span></span>

<span data-ttu-id="e42c0-139">A: For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="e42c0-139">A: For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="e42c0-140">Q: How can I rotate a video during the encoding process.</span><span class="sxs-lookup"><span data-stu-id="e42c0-140">Q: How can I rotate a video during the encoding process.</span></span>

<span data-ttu-id="e42c0-141">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span><span class="sxs-lookup"><span data-stu-id="e42c0-141">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="e42c0-142">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span><span class="sxs-lookup"><span data-stu-id="e42c0-142">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="e42c0-143">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="e42c0-143">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="e42c0-144">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="e42c0-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e42c0-145">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="e42c0-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
