---
title: How to Create a Media Processor | Microsoft Docs
description: Learn how to create a media processor component to encode, convert format, encrypt, or decrypt media content for Azure Media Services. Code samples are written in C# and use the Media Services SDK for .NET.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 88f6e1da090eb6088e54c6f81d0f83b1737d3c2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553081"
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="d12b1-104">How to: Get a Media Processor Instance</span><span class="sxs-lookup"><span data-stu-id="d12b1-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d12b1-107">Overview</span><span class="sxs-lookup"><span data-stu-id="d12b1-107">Overview</span></span>
<span data-ttu-id="d12b1-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span><span class="sxs-lookup"><span data-stu-id="d12b1-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="d12b1-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span><span class="sxs-lookup"><span data-stu-id="d12b1-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

<span data-ttu-id="d12b1-110">The following table provides the name and description of each available media processor.</span><span class="sxs-lookup"><span data-stu-id="d12b1-110">The following table provides the name and description of each available media processor.</span></span>

| <span data-ttu-id="d12b1-111">Media Processor Name</span><span class="sxs-lookup"><span data-stu-id="d12b1-111">Media Processor Name</span></span> | <span data-ttu-id="d12b1-112">Description</span><span class="sxs-lookup"><span data-stu-id="d12b1-112">Description</span></span> | <span data-ttu-id="d12b1-113">More Information</span><span class="sxs-lookup"><span data-stu-id="d12b1-113">More Information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d12b1-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="d12b1-114">Media Encoder Standard</span></span> |<span data-ttu-id="d12b1-115">Provides standard capabilities for on-demand encoding.</span><span class="sxs-lookup"><span data-stu-id="d12b1-115">Provides standard capabilities for on-demand encoding.</span></span> |[<span data-ttu-id="d12b1-116">Overview and Comparison of Azure On Demand Media Encoders</span><span class="sxs-lookup"><span data-stu-id="d12b1-116">Overview and Comparison of Azure On Demand Media Encoders</span></span>](media-services-encode-asset.md) |
| <span data-ttu-id="d12b1-117">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="d12b1-117">Media Encoder Premium Workflow</span></span> |<span data-ttu-id="d12b1-118">Lets you run encoding tasks using Media Encoder Premium Workflow.</span><span class="sxs-lookup"><span data-stu-id="d12b1-118">Lets you run encoding tasks using Media Encoder Premium Workflow.</span></span> |[<span data-ttu-id="d12b1-119">Overview and Comparison of Azure On Demand Media Encoders</span><span class="sxs-lookup"><span data-stu-id="d12b1-119">Overview and Comparison of Azure On Demand Media Encoders</span></span>](media-services-encode-asset.md) |
| <span data-ttu-id="d12b1-120">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="d12b1-120">Azure Media Indexer</span></span> |<span data-ttu-id="d12b1-121">Enables you to make media files and content searchable, as well as generate closed captioning tracks and keywords.</span><span class="sxs-lookup"><span data-stu-id="d12b1-121">Enables you to make media files and content searchable, as well as generate closed captioning tracks and keywords.</span></span> |[<span data-ttu-id="d12b1-122">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="d12b1-122">Azure Media Indexer</span></span>](media-services-index-content.md) |
| <span data-ttu-id="d12b1-123">Azure Media Hyperlapse (preview)</span><span class="sxs-lookup"><span data-stu-id="d12b1-123">Azure Media Hyperlapse (preview)</span></span> |<span data-ttu-id="d12b1-124">Enables you to smooth out the "bumps" in your video with video stabilization.</span><span class="sxs-lookup"><span data-stu-id="d12b1-124">Enables you to smooth out the "bumps" in your video with video stabilization.</span></span> <span data-ttu-id="d12b1-125">Also allows you to speed up your content into a consumable clip.</span><span class="sxs-lookup"><span data-stu-id="d12b1-125">Also allows you to speed up your content into a consumable clip.</span></span> |[<span data-ttu-id="d12b1-126">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="d12b1-126">Azure Media Hyperlapse</span></span>](media-services-hyperlapse-content.md) |
| <span data-ttu-id="d12b1-127">Azure Media Encoder</span><span class="sxs-lookup"><span data-stu-id="d12b1-127">Azure Media Encoder</span></span> |<span data-ttu-id="d12b1-128">Deprecated</span><span class="sxs-lookup"><span data-stu-id="d12b1-128">Deprecated</span></span> | |
| <span data-ttu-id="d12b1-129">Storage Decryption</span><span class="sxs-lookup"><span data-stu-id="d12b1-129">Storage Decryption</span></span> |<span data-ttu-id="d12b1-130">Deprecated</span><span class="sxs-lookup"><span data-stu-id="d12b1-130">Deprecated</span></span> | |
| <span data-ttu-id="d12b1-131">Azure Media Packager</span><span class="sxs-lookup"><span data-stu-id="d12b1-131">Azure Media Packager</span></span> |<span data-ttu-id="d12b1-132">Deprecated</span><span class="sxs-lookup"><span data-stu-id="d12b1-132">Deprecated</span></span> | |
| <span data-ttu-id="d12b1-133">Azure Media Encryptor</span><span class="sxs-lookup"><span data-stu-id="d12b1-133">Azure Media Encryptor</span></span> |<span data-ttu-id="d12b1-134">Deprecated</span><span class="sxs-lookup"><span data-stu-id="d12b1-134">Deprecated</span></span> | |

## <a name="get-media-processor"></a><span data-ttu-id="d12b1-135">Get Media Processor</span><span class="sxs-lookup"><span data-stu-id="d12b1-135">Get Media Processor</span></span>
<span data-ttu-id="d12b1-136">The following method shows how to get a media processor instance.</span><span class="sxs-lookup"><span data-stu-id="d12b1-136">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="d12b1-137">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-dotnet-connect-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="d12b1-137">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-dotnet-connect-programmatically.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="d12b1-138">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d12b1-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d12b1-139">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d12b1-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d12b1-140">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d12b1-140">Next Steps</span></span>
<span data-ttu-id="d12b1-141">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span><span class="sxs-lookup"><span data-stu-id="d12b1-141">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

