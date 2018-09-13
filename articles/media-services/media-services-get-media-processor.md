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
# <a name="how-to-get-a-media-processor-instance"></a>How to: Get a Media Processor Instance
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Overview
In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content. You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.

The following table provides the name and description of each available media processor.

| Media Processor Name | Description | More Information |
| --- | --- | --- |
| Media Encoder Standard |Provides standard capabilities for on-demand encoding. |[Overview and Comparison of Azure On Demand Media Encoders](media-services-encode-asset.md) |
| Media Encoder Premium Workflow |Lets you run encoding tasks using Media Encoder Premium Workflow. |[Overview and Comparison of Azure On Demand Media Encoders](media-services-encode-asset.md) |
| Azure Media Indexer |Enables you to make media files and content searchable, as well as generate closed captioning tracks and keywords. |[Azure Media Indexer](media-services-index-content.md) |
| Azure Media Hyperlapse (preview) |Enables you to smooth out the "bumps" in your video with video stabilization. Also allows you to speed up your content into a consumable clip. |[Azure Media Hyperlapse](media-services-hyperlapse-content.md) |
| Azure Media Encoder |Deprecated | |
| Storage Decryption |Deprecated | |
| Azure Media Packager |Deprecated | |
| Azure Media Encryptor |Deprecated | |

## <a name="get-media-processor"></a>Get Media Processor
The following method shows how to get a media processor instance. The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-dotnet-connect-programmatically.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Next Steps
Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.

