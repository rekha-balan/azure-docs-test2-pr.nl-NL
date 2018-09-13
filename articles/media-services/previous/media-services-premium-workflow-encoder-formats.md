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
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 68ba76ee18b3acc1c2825a217641c21a799132c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865774"
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="72324-103">Media Encoder Premium Workflow formats and codecs</span><span class="sxs-lookup"><span data-stu-id="72324-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="72324-104">For premium encoder questions, email mepd@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="72324-104">For premium encoder questions, email mepd@microsoft.com.</span></span>
> 
> <span data-ttu-id="72324-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span><span class="sxs-lookup"><span data-stu-id="72324-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="72324-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span><span class="sxs-lookup"><span data-stu-id="72324-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="72324-107">Media Encoder Premium Worflow Input Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="72324-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="72324-108">Media Encoder Premium Worflow Output Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="72324-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="72324-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span><span class="sxs-lookup"><span data-stu-id="72324-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <a id="input_formats"></a><span data-ttu-id="72324-110">Media Encoder Premium Workflow Input Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="72324-110">Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="72324-111">The following section lists the codecs and file formats that this media processor supports as input.</span><span class="sxs-lookup"><span data-stu-id="72324-111">The following section lists the codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="72324-112">Input Container/File Formats</span><span class="sxs-lookup"><span data-stu-id="72324-112">Input Container/File Formats</span></span>
* <span data-ttu-id="72324-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="72324-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="72324-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="72324-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="72324-115">GXF</span><span class="sxs-lookup"><span data-stu-id="72324-115">GXF</span></span>
* <span data-ttu-id="72324-116">MPEG-2 Transport Streams</span><span class="sxs-lookup"><span data-stu-id="72324-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="72324-117">MPEG-2 Program Streams</span><span class="sxs-lookup"><span data-stu-id="72324-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="72324-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="72324-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="72324-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="72324-119">Windows Media/ASF</span></span>
* <span data-ttu-id="72324-120">AVI (Uncompressed 8bit/10bit)</span><span class="sxs-lookup"><span data-stu-id="72324-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="72324-121">Input Video Codecs</span><span class="sxs-lookup"><span data-stu-id="72324-121">Input Video Codecs</span></span>
* <span data-ttu-id="72324-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span><span class="sxs-lookup"><span data-stu-id="72324-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="72324-123">Avid DNxHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="72324-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="72324-124">DVCPro/DVCProHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="72324-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="72324-125">HEVC/H.265, Main and Main 10 Profile</span><span class="sxs-lookup"><span data-stu-id="72324-125">HEVC/H.265, Main and Main 10 Profile</span></span>
* <span data-ttu-id="72324-126">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="72324-126">JPEG2000</span></span>
* <span data-ttu-id="72324-127">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span><span class="sxs-lookup"><span data-stu-id="72324-127">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="72324-128">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="72324-128">MPEG-1</span></span>
* <span data-ttu-id="72324-129">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="72324-129">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="72324-130">Input Audio Codecs</span><span class="sxs-lookup"><span data-stu-id="72324-130">Input Audio Codecs</span></span>
* <span data-ttu-id="72324-131">AES (SMPTE 331M and 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="72324-131">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="72324-132">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="72324-132">Dolby® E</span></span>
* <span data-ttu-id="72324-133">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="72324-133">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="72324-134">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span><span class="sxs-lookup"><span data-stu-id="72324-134">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="72324-135">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="72324-135">MPEG Layer 2</span></span>
* <span data-ttu-id="72324-136">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="72324-136">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="72324-137">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="72324-137">Windows Media Audio</span></span>
* <span data-ttu-id="72324-138">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="72324-138">WAV/PCM</span></span>

## <a id="output_format"></a><span data-ttu-id="72324-139">Media Encoder Premium Workflow Output Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="72324-139">Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="72324-140">The following section lists the codecs and file formats that are supported as output from this media processor.</span><span class="sxs-lookup"><span data-stu-id="72324-140">The following section lists the codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="72324-141">Output Container/File Formats</span><span class="sxs-lookup"><span data-stu-id="72324-141">Output Container/File Formats</span></span>
* <span data-ttu-id="72324-142">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="72324-142">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="72324-143">MXF (OP1a, XDCAM and AS02)</span><span class="sxs-lookup"><span data-stu-id="72324-143">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="72324-144">DPP (including AS11)</span><span class="sxs-lookup"><span data-stu-id="72324-144">DPP (including AS11)</span></span>
* <span data-ttu-id="72324-145">GXF</span><span class="sxs-lookup"><span data-stu-id="72324-145">GXF</span></span>
* <span data-ttu-id="72324-146">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="72324-146">MPEG-4/MP4</span></span>
* <span data-ttu-id="72324-147">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="72324-147">Windows Media/ASF</span></span>
* <span data-ttu-id="72324-148">AVI (Uncompressed 8bit/10bit)</span><span class="sxs-lookup"><span data-stu-id="72324-148">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="72324-149">Smooth Streaming File Format (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="72324-149">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="72324-150">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="72324-150">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="72324-151">Output Video Codecs</span><span class="sxs-lookup"><span data-stu-id="72324-151">Output Video Codecs</span></span>
* <span data-ttu-id="72324-152">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span><span class="sxs-lookup"><span data-stu-id="72324-152">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="72324-153">Avid DNxHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="72324-153">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="72324-154">DVCPro/DVCProHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="72324-154">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="72324-155">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span><span class="sxs-lookup"><span data-stu-id="72324-155">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="72324-156">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="72324-156">MPEG-1</span></span>
* <span data-ttu-id="72324-157">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="72324-157">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="72324-158">JPEG thumbnail creation</span><span class="sxs-lookup"><span data-stu-id="72324-158">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="72324-159">Output Audio Codecs</span><span class="sxs-lookup"><span data-stu-id="72324-159">Output Audio Codecs</span></span>
* <span data-ttu-id="72324-160">AES (SMPTE 331M and 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="72324-160">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="72324-161">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="72324-161">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="72324-162">Dolby® Digital Plus (E-AC3) up to 7.1</span><span class="sxs-lookup"><span data-stu-id="72324-162">Dolby® Digital Plus (E-AC3) up to 7.1</span></span>
* <span data-ttu-id="72324-163">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span><span class="sxs-lookup"><span data-stu-id="72324-163">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="72324-164">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="72324-164">MPEG Layer 2</span></span>
* <span data-ttu-id="72324-165">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="72324-165">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="72324-166">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="72324-166">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="72324-167">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span><span class="sxs-lookup"><span data-stu-id="72324-167">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span></span>

## <a id="closed_captioning"></a><span data-ttu-id="72324-168">Support for Closed Captioning</span><span class="sxs-lookup"><span data-stu-id="72324-168">Support for Closed Captioning</span></span>
<span data-ttu-id="72324-169">On ingest, **Media Encoder Premium Workflow** supports:</span><span class="sxs-lookup"><span data-stu-id="72324-169">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="72324-170">SCC files</span><span class="sxs-lookup"><span data-stu-id="72324-170">SCC files</span></span>
2. <span data-ttu-id="72324-171">SMPTE-TT files</span><span class="sxs-lookup"><span data-stu-id="72324-171">SMPTE-TT files</span></span>
3. <span data-ttu-id="72324-172">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span><span class="sxs-lookup"><span data-stu-id="72324-172">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="72324-173">STL subtitle files</span><span class="sxs-lookup"><span data-stu-id="72324-173">STL subtitle files</span></span>

<span data-ttu-id="72324-174">On output, the following options are available:</span><span class="sxs-lookup"><span data-stu-id="72324-174">On output, the following options are available:</span></span>

1. <span data-ttu-id="72324-175">CEA-608 to CEA-708 translation</span><span class="sxs-lookup"><span data-stu-id="72324-175">CEA-608 to CEA-708 translation</span></span>
2. <span data-ttu-id="72324-176">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span><span class="sxs-lookup"><span data-stu-id="72324-176">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="72324-177">SCC</span><span class="sxs-lookup"><span data-stu-id="72324-177">SCC</span></span>
4. <span data-ttu-id="72324-178">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span><span class="sxs-lookup"><span data-stu-id="72324-178">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="72324-179">SRT Subtitle file</span><span class="sxs-lookup"><span data-stu-id="72324-179">SRT Subtitle file</span></span>
6. <span data-ttu-id="72324-180">DVB subtitle streams</span><span class="sxs-lookup"><span data-stu-id="72324-180">DVB subtitle streams</span></span>

<span data-ttu-id="72324-181">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="72324-181">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="72324-182">Known issues</span><span class="sxs-lookup"><span data-stu-id="72324-182">Known issues</span></span>
<span data-ttu-id="72324-183">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span><span class="sxs-lookup"><span data-stu-id="72324-183">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="72324-184">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="72324-184">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="72324-185">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="72324-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

