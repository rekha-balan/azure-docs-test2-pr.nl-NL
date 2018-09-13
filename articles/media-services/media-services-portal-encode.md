---
title: Encode an asset using Media Encoder Standard with the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of encoding an asset using Media Encoder Standard with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: juliako
ms.openlocfilehash: 433b1e3aabcd01f0afecba5d3e0a1fd8c9513980
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549642"
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="7e6ff-103">Encode an asset using Media Encoder Standard with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7e6ff-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="7e6ff-104">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="7e6ff-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e6ff-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="7e6ff-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="7e6ff-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="7e6ff-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="7e6ff-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="7e6ff-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="7e6ff-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="7e6ff-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span><span class="sxs-lookup"><span data-stu-id="7e6ff-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="7e6ff-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="7e6ff-114">Encode with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7e6ff-114">Encode with the Azure portal</span></span>
<span data-ttu-id="7e6ff-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="7e6ff-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="7e6ff-117">In the **Settings** window, select **Assets**.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="7e6ff-118">In the **Assets** window, select the asset that you would like to encode.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="7e6ff-119">Press the **Encode** button.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="7e6ff-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="7e6ff-121">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-121">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="7e6ff-122">For more information about presets, see [this](media-services-mes-presets-overview.md) article – it is important to select the preset that is most appropriate for your input video.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-122">For more information about presets, see [this](media-services-mes-presets-overview.md) article – it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="7e6ff-123">If you have a low resolution (640x360) video, then you should not be using the default "H264 Multiple Bitrate 1080p" preset.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-123">If you have a low resolution (640x360) video, then you should not be using the default "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="7e6ff-124">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-124">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Encode assets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="7e6ff-126">Press **Create**.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-126">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="7e6ff-127">Next step</span><span class="sxs-lookup"><span data-stu-id="7e6ff-127">Next step</span></span>
<span data-ttu-id="7e6ff-128">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span><span class="sxs-lookup"><span data-stu-id="7e6ff-128">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="7e6ff-129">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="7e6ff-129">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7e6ff-130">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="7e6ff-130">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


