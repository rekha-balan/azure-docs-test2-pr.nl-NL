---
title: Overview and comparison of Azure on demand media encoders | Microsoft Docs
description: This topic gives an overview and comparison of Azure on demand media encoders.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: f44f5cffd105d958c7d6552a170150623a0701ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868755"
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="2fd8a-103">Overview and comparison of Azure on demand media encoders</span><span class="sxs-lookup"><span data-stu-id="2fd8a-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="2fd8a-104">Encoding overview</span><span class="sxs-lookup"><span data-stu-id="2fd8a-104">Encoding overview</span></span>
<span data-ttu-id="2fd8a-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="2fd8a-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="2fd8a-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="2fd8a-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

> [!NOTE]
> <span data-ttu-id="2fd8a-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="2fd8a-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="2fd8a-111">Media Services supports the following on demand encoders that are described in this article:</span><span class="sxs-lookup"><span data-stu-id="2fd8a-111">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="2fd8a-112">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="2fd8a-112">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="2fd8a-113">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="2fd8a-113">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="2fd8a-114">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-114">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="2fd8a-115">The topic also provides comparison of the encoders.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-115">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="2fd8a-116">By default each Media Services account can have one active encoding task at a time.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-116">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="2fd8a-117">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-117">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="2fd8a-118">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2fd8a-118">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="2fd8a-119">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="2fd8a-119">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="2fd8a-120">How to use</span><span class="sxs-lookup"><span data-stu-id="2fd8a-120">How to use</span></span>
[<span data-ttu-id="2fd8a-121">How to encode with Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="2fd8a-121">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="2fd8a-122">Formats</span><span class="sxs-lookup"><span data-stu-id="2fd8a-122">Formats</span></span>
[<span data-ttu-id="2fd8a-123">Formats and codecs</span><span class="sxs-lookup"><span data-stu-id="2fd8a-123">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="2fd8a-124">Presets</span><span class="sxs-lookup"><span data-stu-id="2fd8a-124">Presets</span></span>
<span data-ttu-id="2fd8a-125">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="2fd8a-125">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="2fd8a-126">Input and output metadata</span><span class="sxs-lookup"><span data-stu-id="2fd8a-126">Input and output metadata</span></span>
<span data-ttu-id="2fd8a-127">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2fd8a-127">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="2fd8a-128">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2fd8a-128">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="2fd8a-129">Generate thumbnails</span><span class="sxs-lookup"><span data-stu-id="2fd8a-129">Generate thumbnails</span></span>
<span data-ttu-id="2fd8a-130">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="2fd8a-130">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="2fd8a-131">Trim videos (clipping)</span><span class="sxs-lookup"><span data-stu-id="2fd8a-131">Trim videos (clipping)</span></span>
<span data-ttu-id="2fd8a-132">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="2fd8a-132">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="2fd8a-133">Create overlays</span><span class="sxs-lookup"><span data-stu-id="2fd8a-133">Create overlays</span></span>
<span data-ttu-id="2fd8a-134">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="2fd8a-134">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="2fd8a-135">See also</span><span class="sxs-lookup"><span data-stu-id="2fd8a-135">See also</span></span>
[<span data-ttu-id="2fd8a-136">The Media Services blog</span><span class="sxs-lookup"><span data-stu-id="2fd8a-136">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="2fd8a-137">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="2fd8a-137">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="2fd8a-138">Overview</span><span class="sxs-lookup"><span data-stu-id="2fd8a-138">Overview</span></span>
[<span data-ttu-id="2fd8a-139">Introducing Premium Encoding in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="2fd8a-139">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="2fd8a-140">How to use</span><span class="sxs-lookup"><span data-stu-id="2fd8a-140">How to use</span></span>
<span data-ttu-id="2fd8a-141">Media Encoder Premium Workflow is configured using complex workflows.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-141">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="2fd8a-142">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-142">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="2fd8a-143">How to Use Premium Encoding in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="2fd8a-143">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="2fd8a-144">Known issues</span><span class="sxs-lookup"><span data-stu-id="2fd8a-144">Known issues</span></span>
<span data-ttu-id="2fd8a-145">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span><span class="sxs-lookup"><span data-stu-id="2fd8a-145">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="2fd8a-146">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="2fd8a-146">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2fd8a-147">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="2fd8a-147">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="2fd8a-148">Related articles</span><span class="sxs-lookup"><span data-stu-id="2fd8a-148">Related articles</span></span>
* [<span data-ttu-id="2fd8a-149">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span><span class="sxs-lookup"><span data-stu-id="2fd8a-149">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="2fd8a-150">Quotas and Limitations</span><span class="sxs-lookup"><span data-stu-id="2fd8a-150">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
