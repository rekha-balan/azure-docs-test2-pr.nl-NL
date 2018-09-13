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
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Overview and comparison of Azure on demand media encoders
## <a name="encoding-overview"></a>Encoding overview
Azure Media Services provides multiple options for the encoding of media in the cloud.

When starting out with Media Services, it is important to understand the difference between codecs and file formats.
Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.

Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.

> [!NOTE]
> When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state. To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state. 

Media Services supports the following on demand encoders that are described in this article:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium Workflow](media-services-encode-asset.md#media-encoder-premium-workflow)

This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information. The topic also provides comparison of the encoders.

>[!NOTE]
>By default each Media Services account can have one active encoding task at a time. You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase. For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Media Encoder Standard
### <a name="how-to-use"></a>How to use
[How to encode with Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Formats
[Formats and codecs](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Presets
Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Input and output metadata
The encoders input metadata is described [here](media-services-input-metadata-schema.md).

The encoders output metadata is described [here](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Generate thumbnails
For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>Trim videos (clipping)
For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Create overlays
For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>See also
[The Media Services blog](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Media Encoder Premium Workflow
### <a name="overview"></a>Overview
[Introducing Premium Encoding in Azure Media Services](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a>How to use
Media Encoder Premium Workflow is configured using complex workflows. Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.

[How to Use Premium Encoding in Azure Media Services](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Known issues
If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.


## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Related articles
* [Perform advanced encoding tasks by customizing Media Encoder Standard presets](media-services-custom-mes-presets-with-dotnet.md)
* [Quotas and Limitations](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
