---
title: Azure Media Services dynamic packaging overview | Microsoft Docs
description: The topic gives and overview of dynamic packaging.
author: Juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2017
ms.author: juliako
ms.openlocfilehash: 94f0839af5c777ca3ac4db07c940ad57b472cf36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554116"
---
# <a name="dynamic-packaging"></a><span data-ttu-id="7cc11-103">Dynamic packaging</span><span class="sxs-lookup"><span data-stu-id="7cc11-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="7cc11-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7cc11-104">Overview</span></span>
<span data-ttu-id="7cc11-105">Microsoft Azure Media Services can be used to deliver many media source file formats, media streaming formats, and content protection formats to a variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="7cc11-105">Microsoft Azure Media Services can be used to deliver many media source file formats, media streaming formats, and content protection formats to a variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="7cc11-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="7cc11-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="7cc11-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want to serve to clients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span><span class="sxs-lookup"><span data-stu-id="7cc11-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want to serve to clients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="7cc11-108">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span><span class="sxs-lookup"><span data-stu-id="7cc11-108">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="7cc11-109">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span><span class="sxs-lookup"><span data-stu-id="7cc11-109">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="7cc11-110">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span><span class="sxs-lookup"><span data-stu-id="7cc11-110">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="7cc11-111">The following diagram shows the traditional encoding and static packaging workflow.</span><span class="sxs-lookup"><span data-stu-id="7cc11-111">The following diagram shows the traditional encoding and static packaging workflow.</span></span>

![Static Encoding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="7cc11-113">The following diagram shows the dynamic packaging workflow.</span><span class="sxs-lookup"><span data-stu-id="7cc11-113">The following diagram shows the dynamic packaging workflow.</span></span>

![Dynamic Encoding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="7cc11-115">Common scenario</span><span class="sxs-lookup"><span data-stu-id="7cc11-115">Common scenario</span></span>
1. <span data-ttu-id="7cc11-116">Upload an input file (called a mezzanine file).</span><span class="sxs-lookup"><span data-stu-id="7cc11-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="7cc11-117">For example, H.264, MP4, or WMV (for the list of supported formats see [Formats Supported by the Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="7cc11-117">For example, H.264, MP4, or WMV (for the list of supported formats see [Formats Supported by the Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="7cc11-118">Encode your mezzanine file to H.264 MP4 adaptive bitrate sets.</span><span class="sxs-lookup"><span data-stu-id="7cc11-118">Encode your mezzanine file to H.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="7cc11-119">Publish the asset that contains the adaptive bitrate MP4 set by creating the On-Demand Locator.</span><span class="sxs-lookup"><span data-stu-id="7cc11-119">Publish the asset that contains the adaptive bitrate MP4 set by creating the On-Demand Locator.</span></span>
4. <span data-ttu-id="7cc11-120">Build the streaming URLs to access and stream your content.</span><span class="sxs-lookup"><span data-stu-id="7cc11-120">Build the streaming URLs to access and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="7cc11-121">Preparing assets for dynamic streaming</span><span class="sxs-lookup"><span data-stu-id="7cc11-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="7cc11-122">To prepare your asset for dynamic streaming you have two options:</span><span class="sxs-lookup"><span data-stu-id="7cc11-122">To prepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="7cc11-123">[Upload a master file](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="7cc11-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="7cc11-124">[Use the Media Encoder Standard encoder to produce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="7cc11-124">[Use the Media Encoder Standard encoder to produce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="7cc11-125">[Stream your content](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7cc11-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <a id="unsupported_formats"></a><span data-ttu-id="7cc11-126">Formats that are not supported by dynamic packaging</span><span class="sxs-lookup"><span data-stu-id="7cc11-126">Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="7cc11-127">The following source file formats are not supported by dynamic packaging.</span><span class="sxs-lookup"><span data-stu-id="7cc11-127">The following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="7cc11-128">Dolby digital mp4 files.</span><span class="sxs-lookup"><span data-stu-id="7cc11-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="7cc11-129">Dolby digital smooth files.</span><span class="sxs-lookup"><span data-stu-id="7cc11-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7cc11-130">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="7cc11-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7cc11-131">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="7cc11-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



