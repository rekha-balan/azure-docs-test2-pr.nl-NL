---
title: Encode an asset by using Media Encoder Standard in the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of encoding an asset by using Media Encoder Standard in the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 470eb8613416f441c1becee628acf3c898591c84
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870775"
---
# <a name="encode-an-asset-by-using-media-encoder-standard-in-the-azure-portal"></a><span data-ttu-id="d842f-103">Encode an asset by using Media Encoder Standard in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d842f-103">Encode an asset by using Media Encoder Standard in the Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="d842f-104">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="d842f-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d842f-105">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d842f-105">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="d842f-106">One of the most common scenarios in working with Azure Media Services is delivering adaptive bitrate streaming to your clients.</span><span class="sxs-lookup"><span data-stu-id="d842f-106">One of the most common scenarios in working with Azure Media Services is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="d842f-107">Media Services supports the following adaptive bitrate streaming technologies: Apple HTTP Live Streaming (HLS), Microsoft Smooth Streaming, and Dynamic Adaptive Streaming over HTTP (DASH, also called MPEG-DASH).</span><span class="sxs-lookup"><span data-stu-id="d842f-107">Media Services supports the following adaptive bitrate streaming technologies: Apple HTTP Live Streaming (HLS), Microsoft Smooth Streaming, and Dynamic Adaptive Streaming over HTTP (DASH, also called MPEG-DASH).</span></span> <span data-ttu-id="d842f-108">To prepare your videos for adaptive bitrate streaming, first encode your source video as multi-bitrate files.</span><span class="sxs-lookup"><span data-stu-id="d842f-108">To prepare your videos for adaptive bitrate streaming, first encode your source video as multi-bitrate files.</span></span> <span data-ttu-id="d842f-109">You can use Azure Media Encoder Standard to encode your videos.</span><span class="sxs-lookup"><span data-stu-id="d842f-109">You can use Azure Media Encoder Standard to encode your videos.</span></span>  

<span data-ttu-id="d842f-110">Media Services gives you dynamic packaging.</span><span class="sxs-lookup"><span data-stu-id="d842f-110">Media Services gives you dynamic packaging.</span></span> <span data-ttu-id="d842f-111">With dynamic packaging, you can deliver your multi-bitrate MP4s in HLS, Smooth Streaming, and MPEG-DASH, without repackaging in these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="d842f-111">With dynamic packaging, you can deliver your multi-bitrate MP4s in HLS, Smooth Streaming, and MPEG-DASH, without repackaging in these streaming formats.</span></span> <span data-ttu-id="d842f-112">When you use dynamic packaging, you can store and pay for the files in single-storage format.</span><span class="sxs-lookup"><span data-stu-id="d842f-112">When you use dynamic packaging, you can store and pay for the files in single-storage format.</span></span> <span data-ttu-id="d842f-113">Media Services builds and serves the appropriate response based on a client's request.</span><span class="sxs-lookup"><span data-stu-id="d842f-113">Media Services builds and serves the appropriate response based on a client's request.</span></span>

<span data-ttu-id="d842f-114">To take advantage of dynamic packaging, you must encode your source file into a set of multi-bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="d842f-114">To take advantage of dynamic packaging, you must encode your source file into a set of multi-bitrate MP4 files.</span></span> <span data-ttu-id="d842f-115">The encoding steps are demonstrated later in this article.</span><span class="sxs-lookup"><span data-stu-id="d842f-115">The encoding steps are demonstrated later in this article.</span></span>

<span data-ttu-id="d842f-116">To learn how to scale media processing, see [Scale media processing by using the Azure portal](media-services-portal-scale-media-processing.md).</span><span class="sxs-lookup"><span data-stu-id="d842f-116">To learn how to scale media processing, see [Scale media processing by using the Azure portal](media-services-portal-scale-media-processing.md).</span></span>

## <a name="encode-in-the-azure-portal"></a><span data-ttu-id="d842f-117">Encode in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d842f-117">Encode in the Azure portal</span></span>

<span data-ttu-id="d842f-118">To encode your content by using Media Encoder Standard:</span><span class="sxs-lookup"><span data-stu-id="d842f-118">To encode your content by using Media Encoder Standard:</span></span>

1. <span data-ttu-id="d842f-119">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d842f-119">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="d842f-120">Select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="d842f-120">Select **Settings** > **Assets**.</span></span> <span data-ttu-id="d842f-121">Select the asset that you want to encode.</span><span class="sxs-lookup"><span data-stu-id="d842f-121">Select the asset that you want to encode.</span></span>
3. <span data-ttu-id="d842f-122">Select the **Encode** button.</span><span class="sxs-lookup"><span data-stu-id="d842f-122">Select the **Encode** button.</span></span>
4. <span data-ttu-id="d842f-123">In the **Encode an asset** pane, select the **Media Encoder Standard** processor and a preset.</span><span class="sxs-lookup"><span data-stu-id="d842f-123">In the **Encode an asset** pane, select the **Media Encoder Standard** processor and a preset.</span></span> <span data-ttu-id="d842f-124">For information about presets, see [Auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d842f-124">For information about presets, see [Auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="d842f-125">It's important to choose the preset that will work best for your input video.</span><span class="sxs-lookup"><span data-stu-id="d842f-125">It's important to choose the preset that will work best for your input video.</span></span> <span data-ttu-id="d842f-126">For example, if you know your input video has a resolution of 1920 &#215; 1080 pixels, you might choose the **H264 Multiple Bitrate 1080p** preset.</span><span class="sxs-lookup"><span data-stu-id="d842f-126">For example, if you know your input video has a resolution of 1920 &#215; 1080 pixels, you might choose the **H264 Multiple Bitrate 1080p** preset.</span></span> <span data-ttu-id="d842f-127">If you have a low-resolution (640 &#215; 360) video, you shouldn't use the **H264 Multiple Bitrate 1080p** preset.</span><span class="sxs-lookup"><span data-stu-id="d842f-127">If you have a low-resolution (640 &#215; 360) video, you shouldn't use the **H264 Multiple Bitrate 1080p** preset.</span></span>
   
   <span data-ttu-id="d842f-128">To help you manage your resources, you can edit the name of the output asset and the name of the job.</span><span class="sxs-lookup"><span data-stu-id="d842f-128">To help you manage your resources, you can edit the name of the output asset and the name of the job.</span></span>
   
   ![Encode assets](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="d842f-130">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d842f-130">Select **Create**.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d842f-131">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d842f-131">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d842f-132">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d842f-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d842f-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="d842f-133">Next steps</span></span>
* <span data-ttu-id="d842f-134">[Monitor the progress of your encoding job](media-services-portal-check-job-progress.md) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d842f-134">[Monitor the progress of your encoding job](media-services-portal-check-job-progress.md) in the Azure portal.</span></span>  

