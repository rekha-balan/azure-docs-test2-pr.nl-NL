---
title: Overview and comparison of Azure on demand media encoders | Microsoft Docs
description: This topic gives an overview and comparison of Azure on demand media encoders.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 4d35bdd88998d30435e9e5e916a18b3ce3bc7978
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662862"
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="9e638-103">Overview and comparison of Azure on demand media encoders</span><span class="sxs-lookup"><span data-stu-id="9e638-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="9e638-104">Encoding overview</span><span class="sxs-lookup"><span data-stu-id="9e638-104">Encoding overview</span></span>
<span data-ttu-id="9e638-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span><span class="sxs-lookup"><span data-stu-id="9e638-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="9e638-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span><span class="sxs-lookup"><span data-stu-id="9e638-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="9e638-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span><span class="sxs-lookup"><span data-stu-id="9e638-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="9e638-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="9e638-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="9e638-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="9e638-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="9e638-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="9e638-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="9e638-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="9e638-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="9e638-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span><span class="sxs-lookup"><span data-stu-id="9e638-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="9e638-113">Media Services supports the following on demand encoders that are described in this article:</span><span class="sxs-lookup"><span data-stu-id="9e638-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="9e638-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9e638-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="9e638-115">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="9e638-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="9e638-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span><span class="sxs-lookup"><span data-stu-id="9e638-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="9e638-117">The topic also provides comparison of the encoders.</span><span class="sxs-lookup"><span data-stu-id="9e638-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="9e638-118">By default each Media Services account can have one active encoding task at a time.</span><span class="sxs-lookup"><span data-stu-id="9e638-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="9e638-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span><span class="sxs-lookup"><span data-stu-id="9e638-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="9e638-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e638-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="9e638-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9e638-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="9e638-122">How to use</span><span class="sxs-lookup"><span data-stu-id="9e638-122">How to use</span></span>
[<span data-ttu-id="9e638-123">How to encode with Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9e638-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="9e638-124">Formats</span><span class="sxs-lookup"><span data-stu-id="9e638-124">Formats</span></span>
[<span data-ttu-id="9e638-125">Formats and codecs</span><span class="sxs-lookup"><span data-stu-id="9e638-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="9e638-126">Presets</span><span class="sxs-lookup"><span data-stu-id="9e638-126">Presets</span></span>
<span data-ttu-id="9e638-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="9e638-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="9e638-128">Input and output metadata</span><span class="sxs-lookup"><span data-stu-id="9e638-128">Input and output metadata</span></span>
<span data-ttu-id="9e638-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9e638-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="9e638-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9e638-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="9e638-131">Generate thumbnails</span><span class="sxs-lookup"><span data-stu-id="9e638-131">Generate thumbnails</span></span>
<span data-ttu-id="9e638-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="9e638-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="9e638-133">Trim videos (clipping)</span><span class="sxs-lookup"><span data-stu-id="9e638-133">Trim videos (clipping)</span></span>
<span data-ttu-id="9e638-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="9e638-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="9e638-135">Create overlays</span><span class="sxs-lookup"><span data-stu-id="9e638-135">Create overlays</span></span>
<span data-ttu-id="9e638-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="9e638-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="9e638-137">See also</span><span class="sxs-lookup"><span data-stu-id="9e638-137">See also</span></span>
[<span data-ttu-id="9e638-138">The Media Services blog</span><span class="sxs-lookup"><span data-stu-id="9e638-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="9e638-139">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="9e638-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="9e638-140">Overview</span><span class="sxs-lookup"><span data-stu-id="9e638-140">Overview</span></span>
[<span data-ttu-id="9e638-141">Introducing Premium Encoding in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9e638-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="9e638-142">How to use</span><span class="sxs-lookup"><span data-stu-id="9e638-142">How to use</span></span>
<span data-ttu-id="9e638-143">Media Encoder Premium Workflow is configured using complex workflows.</span><span class="sxs-lookup"><span data-stu-id="9e638-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="9e638-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span><span class="sxs-lookup"><span data-stu-id="9e638-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="9e638-145">How to Use Premium Encoding in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9e638-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="9e638-146">Known issues</span><span class="sxs-lookup"><span data-stu-id="9e638-146">Known issues</span></span>
<span data-ttu-id="9e638-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span><span class="sxs-lookup"><span data-stu-id="9e638-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="9e638-148">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="9e638-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9e638-149">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="9e638-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="9e638-150">Related articles</span><span class="sxs-lookup"><span data-stu-id="9e638-150">Related articles</span></span>
* [<span data-ttu-id="9e638-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span><span class="sxs-lookup"><span data-stu-id="9e638-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="9e638-152">Quotas and Limitations</span><span class="sxs-lookup"><span data-stu-id="9e638-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
