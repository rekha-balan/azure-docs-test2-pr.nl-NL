---
title: How to Create a Media Processor | Microsoft Docs
description: Learn how to create a media processor component to encode, convert format, encrypt, or decrypt media content for Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: juliako
ms.openlocfilehash: c208660fc1439ca831ada6c9bb348dbc3eadc18c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549821"
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="619ff-103">How to: Get a Media Processor Instance</span><span class="sxs-lookup"><span data-stu-id="619ff-103">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="619ff-106">Overview</span><span class="sxs-lookup"><span data-stu-id="619ff-106">Overview</span></span>
<span data-ttu-id="619ff-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span><span class="sxs-lookup"><span data-stu-id="619ff-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="619ff-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span><span class="sxs-lookup"><span data-stu-id="619ff-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

<span data-ttu-id="619ff-109">The following table provides the name and description of each available media processor.</span><span class="sxs-lookup"><span data-stu-id="619ff-109">The following table provides the name and description of each available media processor.</span></span>

| <span data-ttu-id="619ff-110">Media Processor Name</span><span class="sxs-lookup"><span data-stu-id="619ff-110">Media Processor Name</span></span> | <span data-ttu-id="619ff-111">Description</span><span class="sxs-lookup"><span data-stu-id="619ff-111">Description</span></span> | <span data-ttu-id="619ff-112">More Information</span><span class="sxs-lookup"><span data-stu-id="619ff-112">More Information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="619ff-113">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="619ff-113">Media Encoder Standard</span></span> |<span data-ttu-id="619ff-114">Provides standard capabilities for on-demand encoding.</span><span class="sxs-lookup"><span data-stu-id="619ff-114">Provides standard capabilities for on-demand encoding.</span></span> |[<span data-ttu-id="619ff-115">Overview and Comparison of Azure On Demand Media Encoders</span><span class="sxs-lookup"><span data-stu-id="619ff-115">Overview and Comparison of Azure On Demand Media Encoders</span></span>](media-services-encode-asset.md) |
| <span data-ttu-id="619ff-116">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="619ff-116">Media Encoder Premium Workflow</span></span> |<span data-ttu-id="619ff-117">Lets you run encoding tasks using Media Encoder Premium Workflow.</span><span class="sxs-lookup"><span data-stu-id="619ff-117">Lets you run encoding tasks using Media Encoder Premium Workflow.</span></span> |[<span data-ttu-id="619ff-118">Overview and Comparison of Azure On Demand Media Encoders</span><span class="sxs-lookup"><span data-stu-id="619ff-118">Overview and Comparison of Azure On Demand Media Encoders</span></span>](media-services-encode-asset.md) |
| <span data-ttu-id="619ff-119">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="619ff-119">Azure Media Indexer</span></span> |<span data-ttu-id="619ff-120">Enables you to make media files and content searchable, as well as generate closed captioning tracks and keywords.</span><span class="sxs-lookup"><span data-stu-id="619ff-120">Enables you to make media files and content searchable, as well as generate closed captioning tracks and keywords.</span></span> |[<span data-ttu-id="619ff-121">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="619ff-121">Azure Media Indexer</span></span>](media-services-index-content.md) |
| <span data-ttu-id="619ff-122">Azure Media Hyperlapse (preview)</span><span class="sxs-lookup"><span data-stu-id="619ff-122">Azure Media Hyperlapse (preview)</span></span> |<span data-ttu-id="619ff-123">Enables you to smooth out the "bumps" in your video with video stabilization.</span><span class="sxs-lookup"><span data-stu-id="619ff-123">Enables you to smooth out the "bumps" in your video with video stabilization.</span></span> <span data-ttu-id="619ff-124">Also allows you to speed up your content into a consumable clip.</span><span class="sxs-lookup"><span data-stu-id="619ff-124">Also allows you to speed up your content into a consumable clip.</span></span> |[<span data-ttu-id="619ff-125">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="619ff-125">Azure Media Hyperlapse</span></span>](media-services-hyperlapse-content.md) |
| <span data-ttu-id="619ff-126">Azure Media Encoder</span><span class="sxs-lookup"><span data-stu-id="619ff-126">Azure Media Encoder</span></span> |<span data-ttu-id="619ff-127">Deprecated</span><span class="sxs-lookup"><span data-stu-id="619ff-127">Deprecated</span></span> | |
| <span data-ttu-id="619ff-128">Storage Decryption</span><span class="sxs-lookup"><span data-stu-id="619ff-128">Storage Decryption</span></span> |<span data-ttu-id="619ff-129">Deprecated</span><span class="sxs-lookup"><span data-stu-id="619ff-129">Deprecated</span></span> | |
| <span data-ttu-id="619ff-130">Azure Media Packager</span><span class="sxs-lookup"><span data-stu-id="619ff-130">Azure Media Packager</span></span> |<span data-ttu-id="619ff-131">Deprecated</span><span class="sxs-lookup"><span data-stu-id="619ff-131">Deprecated</span></span> | |
| <span data-ttu-id="619ff-132">Azure Media Encryptor</span><span class="sxs-lookup"><span data-stu-id="619ff-132">Azure Media Encryptor</span></span> |<span data-ttu-id="619ff-133">Deprecated</span><span class="sxs-lookup"><span data-stu-id="619ff-133">Deprecated</span></span> | |

## <a name="get-mediaprocessor"></a><span data-ttu-id="619ff-134">Get MediaProcessor</span><span class="sxs-lookup"><span data-stu-id="619ff-134">Get MediaProcessor</span></span>
> [!NOTE]
> When working with the Media Services REST API, the following considerations apply:
> 
> When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).
> 
> After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI as described in [Connecting to Media Services using REST API](media-services-rest-connect-programmatically.md). 
> 
> 

<span data-ttu-id="619ff-140">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span><span class="sxs-lookup"><span data-stu-id="619ff-140">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="619ff-141">Request:</span><span class="sxs-lookup"><span data-stu-id="619ff-141">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="619ff-142">Response:</span><span class="sxs-lookup"><span data-stu-id="619ff-142">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="619ff-143">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="619ff-143">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="619ff-144">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="619ff-144">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="619ff-145">Next Steps</span><span class="sxs-lookup"><span data-stu-id="619ff-145">Next Steps</span></span>
<span data-ttu-id="619ff-146">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span><span class="sxs-lookup"><span data-stu-id="619ff-146">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

