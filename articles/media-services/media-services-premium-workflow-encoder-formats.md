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
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="c29c0-103">Media Encoder Premium Workflow formats and codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="c29c0-104">For premium encoder questions, email mepd at Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="c29c0-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="c29c0-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span><span class="sxs-lookup"><span data-stu-id="c29c0-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="c29c0-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span><span class="sxs-lookup"><span data-stu-id="c29c0-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="c29c0-107">Media Encoder Premium Worflow Input Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="c29c0-108">Media Encoder Premium Worflow Output Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="c29c0-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span><span class="sxs-lookup"><span data-stu-id="c29c0-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <a id="input_formats"></a><span data-ttu-id="c29c0-110">Media Encoder Premium Workflow Input Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-110">Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="c29c0-111">The following section lists the codecs and file formats that this media processor supports as input.</span><span class="sxs-lookup"><span data-stu-id="c29c0-111">The following section lists the codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="c29c0-112">Input Container/File Formats</span><span class="sxs-lookup"><span data-stu-id="c29c0-112">Input Container/File Formats</span></span>
* <span data-ttu-id="c29c0-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="c29c0-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="c29c0-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="c29c0-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="c29c0-115">GXF</span><span class="sxs-lookup"><span data-stu-id="c29c0-115">GXF</span></span>
* <span data-ttu-id="c29c0-116">MPEG-2 Transport Streams</span><span class="sxs-lookup"><span data-stu-id="c29c0-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="c29c0-117">MPEG-2 Program Streams</span><span class="sxs-lookup"><span data-stu-id="c29c0-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="c29c0-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="c29c0-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="c29c0-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="c29c0-119">Windows Media/ASF</span></span>
* <span data-ttu-id="c29c0-120">AVI (Uncompressed 8bit/10bit)</span><span class="sxs-lookup"><span data-stu-id="c29c0-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="c29c0-121">Input Video Codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-121">Input Video Codecs</span></span>
* <span data-ttu-id="c29c0-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span><span class="sxs-lookup"><span data-stu-id="c29c0-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="c29c0-123">Avid DNxHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="c29c0-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="c29c0-124">DVCPro/DVCProHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="c29c0-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="c29c0-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="c29c0-125">JPEG2000</span></span>
* <span data-ttu-id="c29c0-126">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span><span class="sxs-lookup"><span data-stu-id="c29c0-126">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="c29c0-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="c29c0-127">MPEG-1</span></span>
* <span data-ttu-id="c29c0-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="c29c0-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="c29c0-129">Input Audio Codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-129">Input Audio Codecs</span></span>
* <span data-ttu-id="c29c0-130">AES (SMPTE 331M and 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="c29c0-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="c29c0-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="c29c0-131">Dolby® E</span></span>
* <span data-ttu-id="c29c0-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="c29c0-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="c29c0-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span><span class="sxs-lookup"><span data-stu-id="c29c0-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="c29c0-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="c29c0-134">MPEG Layer 2</span></span>
* <span data-ttu-id="c29c0-135">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="c29c0-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="c29c0-136">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="c29c0-136">Windows Media Audio</span></span>
* <span data-ttu-id="c29c0-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="c29c0-137">WAV/PCM</span></span>

## <a id="output_format"></a><span data-ttu-id="c29c0-138">Media Encoder Premium Workflow Output Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-138">Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="c29c0-139">The following section lists the codecs and file formats that are supported as output from this media processor.</span><span class="sxs-lookup"><span data-stu-id="c29c0-139">The following section lists the codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="c29c0-140">Output Container/File Formats</span><span class="sxs-lookup"><span data-stu-id="c29c0-140">Output Container/File Formats</span></span>
* <span data-ttu-id="c29c0-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="c29c0-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="c29c0-142">MXF (OP1a, XDCAM and AS02)</span><span class="sxs-lookup"><span data-stu-id="c29c0-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="c29c0-143">DPP (including AS11)</span><span class="sxs-lookup"><span data-stu-id="c29c0-143">DPP (including AS11)</span></span>
* <span data-ttu-id="c29c0-144">GXF</span><span class="sxs-lookup"><span data-stu-id="c29c0-144">GXF</span></span>
* <span data-ttu-id="c29c0-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="c29c0-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="c29c0-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="c29c0-146">Windows Media/ASF</span></span>
* <span data-ttu-id="c29c0-147">AVI (Uncompressed 8bit/10bit)</span><span class="sxs-lookup"><span data-stu-id="c29c0-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="c29c0-148">Smooth Streaming File Format (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="c29c0-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="c29c0-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="c29c0-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="c29c0-150">Output Video Codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-150">Output Video Codecs</span></span>
* <span data-ttu-id="c29c0-151">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span><span class="sxs-lookup"><span data-stu-id="c29c0-151">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="c29c0-152">Avid DNxHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="c29c0-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="c29c0-153">DVCPro/DVCProHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="c29c0-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="c29c0-154">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span><span class="sxs-lookup"><span data-stu-id="c29c0-154">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="c29c0-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="c29c0-155">MPEG-1</span></span>
* <span data-ttu-id="c29c0-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="c29c0-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="c29c0-157">JPEG thumbnail creation</span><span class="sxs-lookup"><span data-stu-id="c29c0-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="c29c0-158">Output Audio Codecs</span><span class="sxs-lookup"><span data-stu-id="c29c0-158">Output Audio Codecs</span></span>
* <span data-ttu-id="c29c0-159">AES (SMPTE 331M and 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="c29c0-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="c29c0-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="c29c0-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="c29c0-161">Dolby® Digital Plus (E-AC3) up to 7.1</span><span class="sxs-lookup"><span data-stu-id="c29c0-161">Dolby® Digital Plus (E-AC3) up to 7.1</span></span>
* <span data-ttu-id="c29c0-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span><span class="sxs-lookup"><span data-stu-id="c29c0-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="c29c0-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="c29c0-163">MPEG Layer 2</span></span>
* <span data-ttu-id="c29c0-164">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="c29c0-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="c29c0-165">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="c29c0-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="c29c0-166">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span><span class="sxs-lookup"><span data-stu-id="c29c0-166">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span></span>

## <a id="closed_captioning"></a><span data-ttu-id="c29c0-167">Support for Closed Captioning</span><span class="sxs-lookup"><span data-stu-id="c29c0-167">Support for Closed Captioning</span></span>
<span data-ttu-id="c29c0-168">On ingest, **Media Encoder Premium Workflow** supports:</span><span class="sxs-lookup"><span data-stu-id="c29c0-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="c29c0-169">SCC files</span><span class="sxs-lookup"><span data-stu-id="c29c0-169">SCC files</span></span>
2. <span data-ttu-id="c29c0-170">SMPTE-TT files</span><span class="sxs-lookup"><span data-stu-id="c29c0-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="c29c0-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span><span class="sxs-lookup"><span data-stu-id="c29c0-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="c29c0-172">STL subtitle files</span><span class="sxs-lookup"><span data-stu-id="c29c0-172">STL subtitle files</span></span>

<span data-ttu-id="c29c0-173">On output, the following options are available:</span><span class="sxs-lookup"><span data-stu-id="c29c0-173">On output, the following options are available:</span></span>

1. <span data-ttu-id="c29c0-174">CEA-608 to CEA-708 translation</span><span class="sxs-lookup"><span data-stu-id="c29c0-174">CEA-608 to CEA-708 translation</span></span>
2. <span data-ttu-id="c29c0-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span><span class="sxs-lookup"><span data-stu-id="c29c0-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="c29c0-176">SCC</span><span class="sxs-lookup"><span data-stu-id="c29c0-176">SCC</span></span>
4. <span data-ttu-id="c29c0-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span><span class="sxs-lookup"><span data-stu-id="c29c0-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="c29c0-178">SRT Subtitle file</span><span class="sxs-lookup"><span data-stu-id="c29c0-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="c29c0-179">DVB subtitle streams</span><span class="sxs-lookup"><span data-stu-id="c29c0-179">DVB subtitle streams</span></span>

<span data-ttu-id="c29c0-180">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="c29c0-180">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c29c0-181">Known issues</span><span class="sxs-lookup"><span data-stu-id="c29c0-181">Known issues</span></span>
<span data-ttu-id="c29c0-182">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span><span class="sxs-lookup"><span data-stu-id="c29c0-182">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="c29c0-183">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="c29c0-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c29c0-184">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c29c0-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

