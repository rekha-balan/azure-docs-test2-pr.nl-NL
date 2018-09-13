---
title: Azure Media Services output metadata schema | Microsoft Docs
description: The topic gives an overview of Azure Media Services output metadata schema.
author: Juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 4babceb9454a229903c54aab7083c5e5ed138b8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864929"
---
# <a name="output-metadata"></a><span data-ttu-id="e78b5-103">Output Metadata</span><span class="sxs-lookup"><span data-stu-id="e78b5-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="e78b5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e78b5-104">Overview</span></span>
<span data-ttu-id="e78b5-105">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span><span class="sxs-lookup"><span data-stu-id="e78b5-105">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span> <span data-ttu-id="e78b5-106">For example, encode an MP4 file to H.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span><span class="sxs-lookup"><span data-stu-id="e78b5-106">For example, encode an MP4 file to H.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="e78b5-107">Upon completion of a task, an output asset is produced.</span><span class="sxs-lookup"><span data-stu-id="e78b5-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="e78b5-108">The output asset contains video, audio, thumbnails, etc. The output asset also contains a file with metadata about the output asset.</span><span class="sxs-lookup"><span data-stu-id="e78b5-108">The output asset contains video, audio, thumbnails, etc. The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="e78b5-109">The name of the metadata XML file has the following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-109">The name of the metadata XML file has the following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="e78b5-110">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span><span class="sxs-lookup"><span data-stu-id="e78b5-110">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span>  

<span data-ttu-id="e78b5-111">This article discusses the elements and types of the XML schema on which the output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span><span class="sxs-lookup"><span data-stu-id="e78b5-111">This article discusses the elements and types of the XML schema on which the output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="e78b5-112">For information about the file that contains metadata about the input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e78b5-112">For information about the file that contains metadata about the input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="e78b5-113">You can find the complete schema code and XML example at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="e78b5-113">You can find the complete schema code and XML example at the end of this article.</span></span>  
>
>

## <a name="AssetFiles "></a> <span data-ttu-id="e78b5-114">AssetFiles root element</span><span class="sxs-lookup"><span data-stu-id="e78b5-114">AssetFiles root element</span></span>
<span data-ttu-id="e78b5-115">Collection of AssetFile entries for the encoding job.</span><span class="sxs-lookup"><span data-stu-id="e78b5-115">Collection of AssetFile entries for the encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="e78b5-116">Child elements</span><span class="sxs-lookup"><span data-stu-id="e78b5-116">Child elements</span></span>
| <span data-ttu-id="e78b5-117">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-117">Name</span></span> | <span data-ttu-id="e78b5-118">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e78b5-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="e78b5-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="e78b5-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="e78b5-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="e78b5-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of the AssetFiles collection.</span><span class="sxs-lookup"><span data-stu-id="e78b5-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of the AssetFiles collection.</span></span> |

## <a name="AssetFile "></a> <span data-ttu-id="e78b5-122">AssetFile element</span><span class="sxs-lookup"><span data-stu-id="e78b5-122">AssetFile element</span></span>
<span data-ttu-id="e78b5-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e78b5-124">Attributes</span><span class="sxs-lookup"><span data-stu-id="e78b5-124">Attributes</span></span>
| <span data-ttu-id="e78b5-125">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-125">Name</span></span> | <span data-ttu-id="e78b5-126">Type</span><span class="sxs-lookup"><span data-stu-id="e78b5-126">Type</span></span> | <span data-ttu-id="e78b5-127">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e78b5-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="e78b5-128">**Name**</span></span><br/><br/> <span data-ttu-id="e78b5-129">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-129">Required</span></span> |<span data-ttu-id="e78b5-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-130">**xs:string**</span></span> |<span data-ttu-id="e78b5-131">The media asset file name.</span><span class="sxs-lookup"><span data-stu-id="e78b5-131">The media asset file name.</span></span> |
| <span data-ttu-id="e78b5-132">**Size**</span><span class="sxs-lookup"><span data-stu-id="e78b5-132">**Size**</span></span><br/><br/> <span data-ttu-id="e78b5-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-134">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-134">Required</span></span> |<span data-ttu-id="e78b5-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="e78b5-135">**xs:long**</span></span> |<span data-ttu-id="e78b5-136">Size of the asset file in bytes.</span><span class="sxs-lookup"><span data-stu-id="e78b5-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="e78b5-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="e78b5-137">**Duration**</span></span><br/><br/> <span data-ttu-id="e78b5-138">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-138">Required</span></span> |<span data-ttu-id="e78b5-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="e78b5-139">**xs:duration**</span></span> |<span data-ttu-id="e78b5-140">Content play back duration.</span><span class="sxs-lookup"><span data-stu-id="e78b5-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="e78b5-141">Child elements</span><span class="sxs-lookup"><span data-stu-id="e78b5-141">Child elements</span></span>
| <span data-ttu-id="e78b5-142">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-142">Name</span></span> | <span data-ttu-id="e78b5-143">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e78b5-144">**Sources**</span><span class="sxs-lookup"><span data-stu-id="e78b5-144">**Sources**</span></span> |<span data-ttu-id="e78b5-145">Collection of input/source media files, that was processed in order to produce this AssetFile.</span><span class="sxs-lookup"><span data-stu-id="e78b5-145">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span> <span data-ttu-id="e78b5-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e78b5-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="e78b5-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="e78b5-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="e78b5-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="e78b5-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="e78b5-149">Each physical AssetFile can contain in it zero or more videos tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="e78b5-149">Each physical AssetFile can contain in it zero or more videos tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="e78b5-150">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e78b5-150">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="e78b5-151">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="e78b5-151">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="e78b5-152">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="e78b5-152">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="e78b5-153">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="e78b5-153">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="e78b5-154">This is the collection of all those audio tracks.</span><span class="sxs-lookup"><span data-stu-id="e78b5-154">This is the collection of all those audio tracks.</span></span> <span data-ttu-id="e78b5-155">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e78b5-155">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <a name="Sources "></a> <span data-ttu-id="e78b5-156">Sources element</span><span class="sxs-lookup"><span data-stu-id="e78b5-156">Sources element</span></span>
<span data-ttu-id="e78b5-157">Collection of input/source media files, that was processed in order to produce this AssetFile.</span><span class="sxs-lookup"><span data-stu-id="e78b5-157">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span>  

<span data-ttu-id="e78b5-158">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-158">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="e78b5-159">Child elements</span><span class="sxs-lookup"><span data-stu-id="e78b5-159">Child elements</span></span>
| <span data-ttu-id="e78b5-160">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-160">Name</span></span> | <span data-ttu-id="e78b5-161">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-161">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e78b5-162">**Source**</span><span class="sxs-lookup"><span data-stu-id="e78b5-162">**Source**</span></span><br/><br/> <span data-ttu-id="e78b5-163">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="e78b5-163">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="e78b5-164">An input/source file used when generating this asset.</span><span class="sxs-lookup"><span data-stu-id="e78b5-164">An input/source file used when generating this asset.</span></span> <span data-ttu-id="e78b5-165">For more information, see [Source element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e78b5-165">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <a name="Source "></a> <span data-ttu-id="e78b5-166">Source element</span><span class="sxs-lookup"><span data-stu-id="e78b5-166">Source element</span></span>
<span data-ttu-id="e78b5-167">An input/source file used when generating this asset.</span><span class="sxs-lookup"><span data-stu-id="e78b5-167">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="e78b5-168">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-168">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e78b5-169">Attributes</span><span class="sxs-lookup"><span data-stu-id="e78b5-169">Attributes</span></span>
| <span data-ttu-id="e78b5-170">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-170">Name</span></span> | <span data-ttu-id="e78b5-171">Type</span><span class="sxs-lookup"><span data-stu-id="e78b5-171">Type</span></span> | <span data-ttu-id="e78b5-172">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-172">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e78b5-173">**Name**</span><span class="sxs-lookup"><span data-stu-id="e78b5-173">**Name**</span></span><br/><br/> <span data-ttu-id="e78b5-174">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-174">Required</span></span> |<span data-ttu-id="e78b5-175">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-175">**xs:string**</span></span> |<span data-ttu-id="e78b5-176">Input source file name.</span><span class="sxs-lookup"><span data-stu-id="e78b5-176">Input source file name.</span></span> |

## <a name="VideoTracks "></a> <span data-ttu-id="e78b5-177">VideoTracks element</span><span class="sxs-lookup"><span data-stu-id="e78b5-177">VideoTracks element</span></span>
<span data-ttu-id="e78b5-178">Each physical AssetFile can contain in it zero or more videos tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="e78b5-178">Each physical AssetFile can contain in it zero or more videos tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="e78b5-179">The **VideoTracks** element represents a collection of all the video tracks.</span><span class="sxs-lookup"><span data-stu-id="e78b5-179">The **VideoTracks** element represents a collection of all the video tracks.</span></span>  

<span data-ttu-id="e78b5-180">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-180">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="e78b5-181">Child elements</span><span class="sxs-lookup"><span data-stu-id="e78b5-181">Child elements</span></span>
| <span data-ttu-id="e78b5-182">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-182">Name</span></span> | <span data-ttu-id="e78b5-183">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e78b5-184">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="e78b5-184">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="e78b5-185">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="e78b5-185">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="e78b5-186">A specific video track in the parent AssetFile.</span><span class="sxs-lookup"><span data-stu-id="e78b5-186">A specific video track in the parent AssetFile.</span></span> <span data-ttu-id="e78b5-187">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="e78b5-187">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <a name="VideoTrack"></a> <span data-ttu-id="e78b5-188">VideoTrack element</span><span class="sxs-lookup"><span data-stu-id="e78b5-188">VideoTrack element</span></span>
<span data-ttu-id="e78b5-189">A specific video track in the parent AssetFile.</span><span class="sxs-lookup"><span data-stu-id="e78b5-189">A specific video track in the parent AssetFile.</span></span>  

<span data-ttu-id="e78b5-190">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-190">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e78b5-191">Attributes</span><span class="sxs-lookup"><span data-stu-id="e78b5-191">Attributes</span></span>
| <span data-ttu-id="e78b5-192">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-192">Name</span></span> | <span data-ttu-id="e78b5-193">Type</span><span class="sxs-lookup"><span data-stu-id="e78b5-193">Type</span></span> | <span data-ttu-id="e78b5-194">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e78b5-195">**Id**</span><span class="sxs-lookup"><span data-stu-id="e78b5-195">**Id**</span></span><br/><br/> <span data-ttu-id="e78b5-196">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-196">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-197">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-197">Required</span></span> |<span data-ttu-id="e78b5-198">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-198">**xs:int**</span></span> |<span data-ttu-id="e78b5-199">Zero-based index of this video track. **Note:**  This **Id** is not necessarily the TrackID as used in an MP4 file.</span><span class="sxs-lookup"><span data-stu-id="e78b5-199">Zero-based index of this video track. **Note:**  This **Id** is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="e78b5-200">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="e78b5-200">**FourCC**</span></span><br/><br/> <span data-ttu-id="e78b5-201">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-201">Required</span></span> |<span data-ttu-id="e78b5-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-202">**xs:string**</span></span> |<span data-ttu-id="e78b5-203">Video codec FourCC code.</span><span class="sxs-lookup"><span data-stu-id="e78b5-203">Video codec FourCC code.</span></span> |
| <span data-ttu-id="e78b5-204">**Profile**</span><span class="sxs-lookup"><span data-stu-id="e78b5-204">**Profile**</span></span> |<span data-ttu-id="e78b5-205">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-205">**xs:string**</span></span> |<span data-ttu-id="e78b5-206">H264 profile (only applicable to H264 codec).</span><span class="sxs-lookup"><span data-stu-id="e78b5-206">H264 profile (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="e78b5-207">**Level**</span><span class="sxs-lookup"><span data-stu-id="e78b5-207">**Level**</span></span> |<span data-ttu-id="e78b5-208">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-208">**xs:string**</span></span> |<span data-ttu-id="e78b5-209">H264 level (only applicable to H264 codec).</span><span class="sxs-lookup"><span data-stu-id="e78b5-209">H264 level (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="e78b5-210">**Width**</span><span class="sxs-lookup"><span data-stu-id="e78b5-210">**Width**</span></span><br/><br/> <span data-ttu-id="e78b5-211">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-211">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-212">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-212">Required</span></span> |<span data-ttu-id="e78b5-213">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-213">**xs:int**</span></span> |<span data-ttu-id="e78b5-214">Encoded video width in pixels.</span><span class="sxs-lookup"><span data-stu-id="e78b5-214">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="e78b5-215">**Height**</span><span class="sxs-lookup"><span data-stu-id="e78b5-215">**Height**</span></span><br/><br/> <span data-ttu-id="e78b5-216">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-216">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-217">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-217">Required</span></span> |<span data-ttu-id="e78b5-218">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-218">**xs:int**</span></span> |<span data-ttu-id="e78b5-219">Encoded video height in pixels.</span><span class="sxs-lookup"><span data-stu-id="e78b5-219">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="e78b5-220">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="e78b5-220">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="e78b5-221">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-221">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-222">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-222">Required</span></span> |<span data-ttu-id="e78b5-223">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="e78b5-223">**xs:double**</span></span> |<span data-ttu-id="e78b5-224">Video display aspect ratio numerator.</span><span class="sxs-lookup"><span data-stu-id="e78b5-224">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="e78b5-225">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="e78b5-225">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="e78b5-226">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-226">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-227">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-227">Required</span></span> |<span data-ttu-id="e78b5-228">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="e78b5-228">**xs:double**</span></span> |<span data-ttu-id="e78b5-229">Video display aspect ratio denominator.</span><span class="sxs-lookup"><span data-stu-id="e78b5-229">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="e78b5-230">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="e78b5-230">**Framerate**</span></span><br/><br/> <span data-ttu-id="e78b5-231">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-231">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-232">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-232">Required</span></span> |<span data-ttu-id="e78b5-233">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="e78b5-233">**xs:decimal**</span></span> |<span data-ttu-id="e78b5-234">Measured video frame rate in .3f format.</span><span class="sxs-lookup"><span data-stu-id="e78b5-234">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="e78b5-235">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="e78b5-235">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="e78b5-236">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-236">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-237">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-237">Required</span></span> |<span data-ttu-id="e78b5-238">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="e78b5-238">**xs:decimal**</span></span> |<span data-ttu-id="e78b5-239">Preset target video frame rate in .3f format.</span><span class="sxs-lookup"><span data-stu-id="e78b5-239">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="e78b5-240">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="e78b5-240">**Bitrate**</span></span><br/><br/> <span data-ttu-id="e78b5-241">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-241">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-242">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-242">Required</span></span> |<span data-ttu-id="e78b5-243">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-243">**xs:int**</span></span> |<span data-ttu-id="e78b5-244">Average video bit rate in kilobits per second, as calculated from the AssetFile.</span><span class="sxs-lookup"><span data-stu-id="e78b5-244">Average video bit rate in kilobits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="e78b5-245">Counts only the elementary stream payload, and does not include the packaging overhead.</span><span class="sxs-lookup"><span data-stu-id="e78b5-245">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="e78b5-246">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="e78b5-246">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="e78b5-247">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-247">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-248">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-248">Required</span></span> |<span data-ttu-id="e78b5-249">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-249">**xs:int**</span></span> |<span data-ttu-id="e78b5-250">Target average bitrate for this video track, as requested via the encoding preset, in kilobits per second.</span><span class="sxs-lookup"><span data-stu-id="e78b5-250">Target average bitrate for this video track, as requested via the encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="e78b5-251">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="e78b5-251">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="e78b5-252">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-252">minInclusive ="0"</span></span> |<span data-ttu-id="e78b5-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-253">**xs:int**</span></span> |<span data-ttu-id="e78b5-254">Max GOP average bitrate for this video track, in kilobits per second.</span><span class="sxs-lookup"><span data-stu-id="e78b5-254">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <a name="AudioTracks "></a> <span data-ttu-id="e78b5-255">AudioTracks element</span><span class="sxs-lookup"><span data-stu-id="e78b5-255">AudioTracks element</span></span>
<span data-ttu-id="e78b5-256">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="e78b5-256">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="e78b5-257">The **AudioTracks** element represents a collection of all those audio tracks.</span><span class="sxs-lookup"><span data-stu-id="e78b5-257">The **AudioTracks** element represents a collection of all those audio tracks.</span></span>  

<span data-ttu-id="e78b5-258">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-258">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="e78b5-259">Child elements</span><span class="sxs-lookup"><span data-stu-id="e78b5-259">Child elements</span></span>
| <span data-ttu-id="e78b5-260">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-260">Name</span></span> | <span data-ttu-id="e78b5-261">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e78b5-262">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="e78b5-262">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="e78b5-263">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="e78b5-263">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="e78b5-264">A specific audio track in the parent AssetFile.</span><span class="sxs-lookup"><span data-stu-id="e78b5-264">A specific audio track in the parent AssetFile.</span></span> <span data-ttu-id="e78b5-265">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e78b5-265">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <a name="AudioTrack "></a> <span data-ttu-id="e78b5-266">AudioTrack element</span><span class="sxs-lookup"><span data-stu-id="e78b5-266">AudioTrack element</span></span>
<span data-ttu-id="e78b5-267">A specific audio track in the parent AssetFile.</span><span class="sxs-lookup"><span data-stu-id="e78b5-267">A specific audio track in the parent AssetFile.</span></span>  

<span data-ttu-id="e78b5-268">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-268">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e78b5-269">Attributes</span><span class="sxs-lookup"><span data-stu-id="e78b5-269">Attributes</span></span>
| <span data-ttu-id="e78b5-270">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-270">Name</span></span> | <span data-ttu-id="e78b5-271">Type</span><span class="sxs-lookup"><span data-stu-id="e78b5-271">Type</span></span> | <span data-ttu-id="e78b5-272">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-272">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e78b5-273">**Id**</span><span class="sxs-lookup"><span data-stu-id="e78b5-273">**Id**</span></span><br/><br/> <span data-ttu-id="e78b5-274">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-274">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-275">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-275">Required</span></span> |<span data-ttu-id="e78b5-276">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-276">**xs:int**</span></span> |<span data-ttu-id="e78b5-277">Zero-based index of this audio track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span><span class="sxs-lookup"><span data-stu-id="e78b5-277">Zero-based index of this audio track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="e78b5-278">**Codec**</span><span class="sxs-lookup"><span data-stu-id="e78b5-278">**Codec**</span></span> |<span data-ttu-id="e78b5-279">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-279">**xs:string**</span></span> |<span data-ttu-id="e78b5-280">Audio track codec string.</span><span class="sxs-lookup"><span data-stu-id="e78b5-280">Audio track codec string.</span></span> |
| <span data-ttu-id="e78b5-281">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="e78b5-281">**EncoderVersion**</span></span> |<span data-ttu-id="e78b5-282">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-282">**xs:string**</span></span> |<span data-ttu-id="e78b5-283">Optional encoder version string, required for EAC3.</span><span class="sxs-lookup"><span data-stu-id="e78b5-283">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="e78b5-284">**Channels**</span><span class="sxs-lookup"><span data-stu-id="e78b5-284">**Channels**</span></span><br/><br/> <span data-ttu-id="e78b5-285">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-285">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-286">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-286">Required</span></span> |<span data-ttu-id="e78b5-287">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-287">**xs:int**</span></span> |<span data-ttu-id="e78b5-288">Number of audio channels.</span><span class="sxs-lookup"><span data-stu-id="e78b5-288">Number of audio channels.</span></span> |
| <span data-ttu-id="e78b5-289">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="e78b5-289">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="e78b5-290">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-290">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-291">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-291">Required</span></span> |<span data-ttu-id="e78b5-292">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-292">**xs:int**</span></span> |<span data-ttu-id="e78b5-293">Audio sampling rate in samples/sec or Hz.</span><span class="sxs-lookup"><span data-stu-id="e78b5-293">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="e78b5-294">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="e78b5-294">**Bitrate**</span></span><br/><br/> <span data-ttu-id="e78b5-295">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-295">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-296">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-296">Required</span></span> |<span data-ttu-id="e78b5-297">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-297">**xs:int**</span></span> |<span data-ttu-id="e78b5-298">Average audio bit rate in bits per second, as calculated from the AssetFile.</span><span class="sxs-lookup"><span data-stu-id="e78b5-298">Average audio bit rate in bits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="e78b5-299">Counts only the elementary stream payload, and does not include the packaging overhead.</span><span class="sxs-lookup"><span data-stu-id="e78b5-299">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="e78b5-300">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="e78b5-300">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="e78b5-301">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e78b5-301">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e78b5-302">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-302">Required</span></span> |<span data-ttu-id="e78b5-303">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-303">**xs:int**</span></span> |<span data-ttu-id="e78b5-304">Bits per sample for the wFormatTag format type.</span><span class="sxs-lookup"><span data-stu-id="e78b5-304">Bits per sample for the wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="e78b5-305">Child elements</span><span class="sxs-lookup"><span data-stu-id="e78b5-305">Child elements</span></span>
| <span data-ttu-id="e78b5-306">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-306">Name</span></span> | <span data-ttu-id="e78b5-307">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-307">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e78b5-308">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="e78b5-308">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="e78b5-309">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="e78b5-309">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="e78b5-310">Loudness metering result parameters.</span><span class="sxs-lookup"><span data-stu-id="e78b5-310">Loudness metering result parameters.</span></span> <span data-ttu-id="e78b5-311">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e78b5-311">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <a name="LoudnessMeteringResultParameters "></a> <span data-ttu-id="e78b5-312">LoudnessMeteringResultParameters element</span><span class="sxs-lookup"><span data-stu-id="e78b5-312">LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="e78b5-313">Loudness metering result parameters.</span><span class="sxs-lookup"><span data-stu-id="e78b5-313">Loudness metering result parameters.</span></span>  

<span data-ttu-id="e78b5-314">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="e78b5-314">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e78b5-315">Attributes</span><span class="sxs-lookup"><span data-stu-id="e78b5-315">Attributes</span></span>
| <span data-ttu-id="e78b5-316">Name</span><span class="sxs-lookup"><span data-stu-id="e78b5-316">Name</span></span> | <span data-ttu-id="e78b5-317">Type</span><span class="sxs-lookup"><span data-stu-id="e78b5-317">Type</span></span> | <span data-ttu-id="e78b5-318">Description</span><span class="sxs-lookup"><span data-stu-id="e78b5-318">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e78b5-319">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="e78b5-319">**DPLMVersionInformation**</span></span> |<span data-ttu-id="e78b5-320">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-320">**xs:string**</span></span> |<span data-ttu-id="e78b5-321">**Dolby** professional loudness metering development kit version.</span><span class="sxs-lookup"><span data-stu-id="e78b5-321">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="e78b5-322">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="e78b5-322">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="e78b5-323">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="e78b5-323">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="e78b5-324">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-324">Required</span></span> |<span data-ttu-id="e78b5-325">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e78b5-325">**xs:int**</span></span> |<span data-ttu-id="e78b5-326">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span><span class="sxs-lookup"><span data-stu-id="e78b5-326">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="e78b5-327">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="e78b5-327">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="e78b5-328">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="e78b5-328">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="e78b5-329">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-329">Required</span></span> |<span data-ttu-id="e78b5-330">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="e78b5-330">**xs:float**</span></span> |<span data-ttu-id="e78b5-331">Integrated loudness</span><span class="sxs-lookup"><span data-stu-id="e78b5-331">Integrated loudness</span></span> |
| <span data-ttu-id="e78b5-332">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="e78b5-332">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="e78b5-333">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-333">Required</span></span> |<span data-ttu-id="e78b5-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-334">**xs:string**</span></span> |<span data-ttu-id="e78b5-335">Integrated loudness unit.</span><span class="sxs-lookup"><span data-stu-id="e78b5-335">Integrated loudness unit.</span></span> |
| <span data-ttu-id="e78b5-336">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="e78b5-336">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="e78b5-337">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-337">Required</span></span> |<span data-ttu-id="e78b5-338">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e78b5-338">**xs:string**</span></span> |<span data-ttu-id="e78b5-339">Gating identifier</span><span class="sxs-lookup"><span data-stu-id="e78b5-339">Gating identifier</span></span> |
| <span data-ttu-id="e78b5-340">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="e78b5-340">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="e78b5-341">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="e78b5-341">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="e78b5-342">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="e78b5-342">**xs:float**</span></span> |<span data-ttu-id="e78b5-343">Speech content over the program, as a percentage.</span><span class="sxs-lookup"><span data-stu-id="e78b5-343">Speech content over the program, as a percentage.</span></span> |
| <span data-ttu-id="e78b5-344">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="e78b5-344">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="e78b5-345">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-345">Required</span></span> |<span data-ttu-id="e78b5-346">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="e78b5-346">**xs:float**</span></span> |<span data-ttu-id="e78b5-347">Peak absolute sample value, since reset or since it was last cleared, per channel.</span><span class="sxs-lookup"><span data-stu-id="e78b5-347">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="e78b5-348">Units are dBFS.</span><span class="sxs-lookup"><span data-stu-id="e78b5-348">Units are dBFS.</span></span> |
| <span data-ttu-id="e78b5-349">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="e78b5-349">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="e78b5-350">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="e78b5-350">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="e78b5-351">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-351">Required</span></span> |<span data-ttu-id="e78b5-352">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="e78b5-352">**xs:anySimpleType**</span></span> |<span data-ttu-id="e78b5-353">Sample peak unit.</span><span class="sxs-lookup"><span data-stu-id="e78b5-353">Sample peak unit.</span></span> |
| <span data-ttu-id="e78b5-354">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="e78b5-354">**TruePeak**</span></span><br/><br/> <span data-ttu-id="e78b5-355">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-355">Required</span></span> |<span data-ttu-id="e78b5-356">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="e78b5-356">**xs:float**</span></span> |<span data-ttu-id="e78b5-357">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span><span class="sxs-lookup"><span data-stu-id="e78b5-357">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="e78b5-358">Units are dBTP.</span><span class="sxs-lookup"><span data-stu-id="e78b5-358">Units are dBTP.</span></span> |
| <span data-ttu-id="e78b5-359">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="e78b5-359">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="e78b5-360">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="e78b5-360">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="e78b5-361">Required</span><span class="sxs-lookup"><span data-stu-id="e78b5-361">Required</span></span> |<span data-ttu-id="e78b5-362">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="e78b5-362">**xs:anySimpleType**</span></span> |<span data-ttu-id="e78b5-363">True peak unit.</span><span class="sxs-lookup"><span data-stu-id="e78b5-363">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="e78b5-364">Schema Code</span><span class="sxs-lookup"><span data-stu-id="e78b5-364">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order to produce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Width" use="required">  
                              <xs:annotation>  
                                <xs:documentation>encoded video width in pixels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Height" use="required">  
                              <xs:annotation>  
                                <xs:documentation>encoded video height in pixels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:double">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:double">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Framerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via the encoding preset, in kilobits per second</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="MaxGOPBitrate">  
                              <xs:annotation>  
                                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over the program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Channels" use="required">  
                              <xs:annotation>  
                                <xs:documentation>number of audio channels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="SamplingRate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>the media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <a name="xml"></a> <span data-ttu-id="e78b5-365">XML example</span><span class="sxs-lookup"><span data-stu-id="e78b5-365">XML example</span></span>

<span data-ttu-id="e78b5-366">The following XML is an example of the Output metadata file.</span><span class="sxs-lookup"><span data-stu-id="e78b5-366">The following XML is an example of the Output metadata file.</span></span>  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="e78b5-367">Next steps</span><span class="sxs-lookup"><span data-stu-id="e78b5-367">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e78b5-368">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="e78b5-368">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
