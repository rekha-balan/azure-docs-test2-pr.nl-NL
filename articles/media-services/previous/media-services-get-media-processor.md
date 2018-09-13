---
title: How to Create a media processor using the Azure Media Services SDK for .NET| Microsoft Docs
description: Learn how to create a media processor component to encode, convert format, encrypt, or decrypt media content for Azure Media Services. Code samples are written in C# and use the Media Services SDK for .NET.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 60da450c11a2e65d96c15798854adfef371a694f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965517"
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="20359-104">How to: Get a Media Processor Instance</span><span class="sxs-lookup"><span data-stu-id="20359-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="20359-107">Overview</span><span class="sxs-lookup"><span data-stu-id="20359-107">Overview</span></span>
<span data-ttu-id="20359-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span><span class="sxs-lookup"><span data-stu-id="20359-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="20359-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span><span class="sxs-lookup"><span data-stu-id="20359-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="20359-110">Azure media processors</span><span class="sxs-lookup"><span data-stu-id="20359-110">Azure media processors</span></span> 

<span data-ttu-id="20359-111">The following topic provides lists of media processors:</span><span class="sxs-lookup"><span data-stu-id="20359-111">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="20359-112">Encoding media processors</span><span class="sxs-lookup"><span data-stu-id="20359-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="20359-113">Analytics media processors</span><span class="sxs-lookup"><span data-stu-id="20359-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="20359-114">Get Media Processor</span><span class="sxs-lookup"><span data-stu-id="20359-114">Get Media Processor</span></span>

<span data-ttu-id="20359-115">The following method shows how to get a media processor instance.</span><span class="sxs-lookup"><span data-stu-id="20359-115">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="20359-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="20359-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="20359-117">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="20359-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="20359-118">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="20359-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="20359-119">Next Steps</span><span class="sxs-lookup"><span data-stu-id="20359-119">Next Steps</span></span>
<span data-ttu-id="20359-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span><span class="sxs-lookup"><span data-stu-id="20359-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

