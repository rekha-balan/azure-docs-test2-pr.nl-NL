---
title: Media Encoder Standard formats and codecs
description: This topic gives an overview of Media Encoder Standard formats and codecs.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: juliako;anilmur
ms.openlocfilehash: 531e6c086cbace2e8d7f24e69a3a473858c55bd7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661347"
---
# <a name="media-encoder-standard-formats-and-codecs"></a>Media Encoder Standard Formats and Codecs
This document contains a list of the most common import and export file formats that you can use with Media Encoder Standard.

## <a name="input-containerfile-formats"></a>Input Container/File Formats
| File formats (file extensions) | Supported |
| --- | --- | --- | --- |
| FLV (with H.264 and AAC codecs) (.flv) |Yes |
| MXF    (.mxf) |Yes |
| GXF    (.gxf) |Yes |
| MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg) |Yes |
| Windows Media Video (WMV)/ASF (.wmv, .asf) |Yes |
| AVI (Uncompressed 8bit/10bit) (.avi) |Yes |
| MP4 (.mp4, .m4a, .m4v)/ISMV (.isma, .ismv) |Yes |
| [Microsoft Digital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |Yes |
| Matroska/WebM (.mkv) |Yes |
| WAVE/WAV (.wav) |Yes |
| QuickTime (.mov) |Yes |

> [!NOTE]
> Above is a list of the more commonly encountered file extensions. Media Encoder Standard does support many others (for example: .m2ts, .mpeg2video, .qt). If you try to encode a file and you get an error message about the format not being supported, please provide a feedback [here](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).
> 
> 

### <a name="audio-formats-in-input-containers"></a>Audio formats in input containers
Media Encoder Standard supports carrying the following audio formats in input containers:

* MXF, GXF and QuickTime files which have audio tracks with interleaved stereo or 5.1 samples

or

* MXF, GXF and QuickTime files where the audio is carried as separate PCM tracks but the channel mapping (to stereo or 5.1) can be deduced from the file metadata

Note that support for explicit/user-supplied channel mapping will be provided in the near future.

## <a name="input-video-codecs"></a>Input Video Codecs
| Input Video Codecs | Supported |
| --- | --- | --- | --- |
| AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra |8 bit 4:2:0 and 4:2:2 |
| Avid DNxHD (in MXF) |Yes |
| DVCPro/DVCProHD (in MXF) |Yes |
| Digital video (DV) (in AVI files) |Yes |
| JPEG 2000 |Yes |
| MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10) |Up to 422 Profile |
| MPEG-1 |Yes |
| VC-1/WMV9 |Yes |
| Canopus HQ/HQX |No |
| MPEG-4 Part 2 |Yes |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Yes |
| YUV420 uncompressed, or mezzanine |Yes |
| Apple ProRes 422 |Yes |
| Apple ProRes 422 LT |Yes |
| Apple ProRes 422 HQ |Yes |
| Apple ProRes Proxy |Yes |
| Apple ProRes 4444 |Yes |
| Apple ProRes 4444 XQ |Yes |

## <a name="input-audio-codecs"></a>Input Audio Codecs
| Input Audio Codecs | Supported |
| --- | --- | --- | --- |
| AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1) |Yes |
| MPEG Layer 2 |Yes |
| MP3 (MPEG-1 Audio Layer 3) |Yes |
| Windows Media Audio |Yes |
| WAV/PCM |Yes |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Yes |
| [Opus](http://go.microsoft.com/fwlink/?LinkId=822667) |Yes |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Yes |
| AMR (adaptive multi-rate) |Yes |
| AES (SMPTE 331M and 302M, AES3-2003) |No |
| Dolby® E |No |
| Dolby® Digital (AC3) |No |
| Dolby® Digital Plus (E-AC3) |No |

## <a name="output-formats-and-codecs"></a>Output Formats and codecs
The following table lists the codecs and file formats that are supported for export.

| File Format | Video Codec | Audio Codec |
| --- | --- | --- |
| MP4 <br/><br/>(including multi-bitrate MP4 containers) |H.264 (High, Main, and Baseline Profiles) |AAC-LC, HE-AAC v1, HE-AAC v2 |
| MPEG2-TS |H.264 (High, Main, and Baseline Profiles) |AAC-LC, HE-AAC v1, HE-AAC v2 |

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>See also
[Encoding On-Demand Content with Azure Media Services](media-services-encode-asset.md)

[How to encode with Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)
