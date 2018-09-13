---
title: Azure Media Services frequently asked questions | Microsoft Docs
description: Frequently asked questions (FAQs)
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 9a6d772bddc4417004c99f319ec7592d026efdb1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662710"
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="3b663-103">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="3b663-103">Frequently asked questions</span></span>

<span data-ttu-id="3b663-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span><span class="sxs-lookup"><span data-stu-id="3b663-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="3b663-105">General AMS FAQs</span><span class="sxs-lookup"><span data-stu-id="3b663-105">General AMS FAQs</span></span>
<span data-ttu-id="3b663-106">Q: How do you scale indexing?</span><span class="sxs-lookup"><span data-stu-id="3b663-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="3b663-107">A: The reserved units are the same for Encoding and Indexing tasks.</span><span class="sxs-lookup"><span data-stu-id="3b663-107">A: The reserved units are the same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="3b663-108">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b663-108">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="3b663-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span><span class="sxs-lookup"><span data-stu-id="3b663-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="3b663-110">Q: I uploaded, encoded, and published a video.</span><span class="sxs-lookup"><span data-stu-id="3b663-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="3b663-111">What would be the reason the video does not play when I try to stream it?</span><span class="sxs-lookup"><span data-stu-id="3b663-111">What would be the reason the video does not play when I try to stream it?</span></span>

<span data-ttu-id="3b663-112">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="3b663-112">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span></span>  

<span data-ttu-id="3b663-113">Q: Can I do compositing on a live stream?</span><span class="sxs-lookup"><span data-stu-id="3b663-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="3b663-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span><span class="sxs-lookup"><span data-stu-id="3b663-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span></span>

<span data-ttu-id="3b663-115">Q: Can I use Azure CDN with Live Streaming?</span><span class="sxs-lookup"><span data-stu-id="3b663-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="3b663-116">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="3b663-116">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="3b663-117">You can use Live streaming with CDN.</span><span class="sxs-lookup"><span data-stu-id="3b663-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="3b663-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span><span class="sxs-lookup"><span data-stu-id="3b663-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="3b663-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span><span class="sxs-lookup"><span data-stu-id="3b663-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="3b663-120">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span><span class="sxs-lookup"><span data-stu-id="3b663-120">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="3b663-121">Only data needs to be refreshed is the manifest data.</span><span class="sxs-lookup"><span data-stu-id="3b663-121">Only data needs to be refreshed is the manifest data.</span></span> <span data-ttu-id="3b663-122">CDN periodically refreshes manifest data.</span><span class="sxs-lookup"><span data-stu-id="3b663-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="3b663-123">Q: Does Azure Media services support storing images?</span><span class="sxs-lookup"><span data-stu-id="3b663-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="3b663-124">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3b663-124">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="3b663-125">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span><span class="sxs-lookup"><span data-stu-id="3b663-125">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="3b663-126">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span><span class="sxs-lookup"><span data-stu-id="3b663-126">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="3b663-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="3b663-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="3b663-128">Q: How can I copy assets from one Media Services account to another.</span><span class="sxs-lookup"><span data-stu-id="3b663-128">Q: How can I copy assets from one Media Services account to another.</span></span>

<span data-ttu-id="3b663-129">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span><span class="sxs-lookup"><span data-stu-id="3b663-129">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="3b663-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span><span class="sxs-lookup"><span data-stu-id="3b663-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="3b663-131">Q: What are the supported characters for naming files when working with AMS?</span><span class="sxs-lookup"><span data-stu-id="3b663-131">Q: What are the supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="3b663-132">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span><span class="sxs-lookup"><span data-stu-id="3b663-132">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="3b663-133">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !\*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="3b663-133">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !\*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="3b663-134">Also, there can only be one ‘.’</span><span class="sxs-lookup"><span data-stu-id="3b663-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="3b663-135">for the file name extension.</span><span class="sxs-lookup"><span data-stu-id="3b663-135">for the file name extension.</span></span>

<span data-ttu-id="3b663-136">Q: How to connect using REST?</span><span class="sxs-lookup"><span data-stu-id="3b663-136">Q: How to connect using REST?</span></span>

<span data-ttu-id="3b663-137">A: After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span><span class="sxs-lookup"><span data-stu-id="3b663-137">A: After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="3b663-138">You must make subsequent calls to the new URI as described in [Connecting to Media Services using REST API](media-services-rest-connect-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="3b663-138">You must make subsequent calls to the new URI as described in [Connecting to Media Services using REST API](media-services-rest-connect-programmatically.md).</span></span>

<span data-ttu-id="3b663-139">Q: How can I rotate a video during the encoding process.</span><span class="sxs-lookup"><span data-stu-id="3b663-139">Q: How can I rotate a video during the encoding process.</span></span>

<span data-ttu-id="3b663-140">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span><span class="sxs-lookup"><span data-stu-id="3b663-140">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="3b663-141">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span><span class="sxs-lookup"><span data-stu-id="3b663-141">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="3b663-142">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="3b663-142">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span></span>

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




## <a name="media-services-learning-paths"></a><span data-ttu-id="3b663-143">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="3b663-143">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3b663-144">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="3b663-144">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
