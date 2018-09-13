---
title: Media Encoder Premium Workflow formats and codecs | Microsoft Docs
description: This topic gives an overview of Media Encoder Premium Workflow Formats formats and codecs
services: media-services
documentationcenter: ''
author: juliako
manager: erik43
editor: ''
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 8179e955ef0c126acb9dab31226bd1e12278f9b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550115"
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a>Media Encoder Premium Workflow formats and codecs
> [!NOTE]
> For premium encoder questions, email mepd at Microsoft.com.
> 
> Media Encoder Premium Workflow media processor discussed in this topic is not available in China. 
> 
> 

This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.

[Media Encoder Premium Worflow Input Formats and Codecs](#input_formats)

[Media Encoder Premium Worflow Output Formats and Codecs](#output_formats)

**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section. 

## <a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs
The following section lists the codecs and file formats that this media processor supports as input.

### <a name="input-containerfile-formats"></a>Input Container/File Formats
* Adobe® Flash® F4V
* MXF/SMPTE 377M
* GXF
* MPEG-2 Transport Streams
* MPEG-2 Program Streams
* MPEG-4/MP4
* Windows Media/ASF
* AVI (Uncompressed 8bit/10bit)

### <a name="input-video-codecs"></a>Input Video Codecs
* AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra
* Avid DNxHD (in MXF)
* DVCPro/DVCProHD (in MXF)
* JPEG2000
* MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)
* MPEG-1
* Windows Media Video/VC-1

### <a name="input-audio-codecs"></a>Input Audio Codecs
* AES (SMPTE 331M and 302M, AES3-2003)
* Dolby® E
* Dolby® Digital (AC3)
* AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio
* WAV/PCM

## <a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs
The following section lists the codecs and file formats that are supported as output from this media processor.

### <a name="output-containerfile-formats"></a>Output Container/File Formats
* Adobe® Flash® F4V
* MXF (OP1a, XDCAM and AS02)
* DPP (including AS11)
* GXF
* MPEG-4/MP4
* Windows Media/ASF
* AVI (Uncompressed 8bit/10bit)
* Smooth Streaming File Format (PIFF 1.3)
* MPEG-TS 

### <a name="output-video-codecs"></a>Output Video Codecs
* AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)
* Avid DNxHD (in MXF)
* DVCPro/DVCProHD (in MXF)
* MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)
* MPEG-1
* Windows Media Video/VC-1
* JPEG thumbnail creation

### <a name="output-audio-codecs"></a>Output Audio Codecs
* AES (SMPTE 331M and 302M, AES3-2003)
* Dolby® Digital (AC3)
* Dolby® Digital Plus (E-AC3) up to 7.1
* AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio

>[!NOTE]
>If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.

## <a id="closed_captioning"></a>Support for Closed Captioning
On ingest, **Media Encoder Premium Workflow** supports:

1. SCC files
2. SMPTE-TT files
3. CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files
4. STL subtitle files

On output, the following options are available:

1. CEA-608 to CEA-708 translation
2. CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)
3. SCC
4. SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)
5. SRT Subtitle file
6. DVB subtitle streams

Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.

## <a name="known-issues"></a>Known issues
If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file. 

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
