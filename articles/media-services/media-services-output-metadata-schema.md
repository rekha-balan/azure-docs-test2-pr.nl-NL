---
title: Azure Media Services output metadata schema | Microsoft Docs
description: The topic gives an overview of Azure Media Services output metadata schema.
author: Juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: juliako
ms.openlocfilehash: 19966a6e3815c2dd9d37c4701c9188ce63ebbcac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552242"
---
# <a name="output-metadata"></a><span data-ttu-id="a9c85-103">Output Metadata</span><span class="sxs-lookup"><span data-stu-id="a9c85-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="a9c85-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a9c85-104">Overview</span></span>
<span data-ttu-id="a9c85-105">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span><span class="sxs-lookup"><span data-stu-id="a9c85-105">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span> <span data-ttu-id="a9c85-106">For example, encode an MP4 file to H.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span><span class="sxs-lookup"><span data-stu-id="a9c85-106">For example, encode an MP4 file to H.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="a9c85-107">Upon completion of a task, an output asset is produced.</span><span class="sxs-lookup"><span data-stu-id="a9c85-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="a9c85-108">The output asset contains video, audio, thumbnails, etc. The output asset also contains a file with metadata about the output asset.</span><span class="sxs-lookup"><span data-stu-id="a9c85-108">The output asset contains video, audio, thumbnails, etc. The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="a9c85-109">The name of the metadata XML file has the following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-109">The name of the metadata XML file has the following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="a9c85-110">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span><span class="sxs-lookup"><span data-stu-id="a9c85-110">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span>  

<span data-ttu-id="a9c85-111">This topic discusses the elements and types of the XML schema on which the output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span><span class="sxs-lookup"><span data-stu-id="a9c85-111">This topic discusses the elements and types of the XML schema on which the output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="a9c85-112">For information about the file that contains metadata about the input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9c85-112">For information about the file that contains metadata about the input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="a9c85-113">You can find the complete schema code and XML example at the end of this topic.</span><span class="sxs-lookup"><span data-stu-id="a9c85-113">You can find the complete schema code and XML example at the end of this topic.</span></span>  
>
>

## <a name="AssetFiles "></a> <span data-ttu-id="a9c85-114">AssetFiles root element</span><span class="sxs-lookup"><span data-stu-id="a9c85-114">AssetFiles root element</span></span>
<span data-ttu-id="a9c85-115">Collection of AssetFile entries for the encoding job.</span><span class="sxs-lookup"><span data-stu-id="a9c85-115">Collection of AssetFile entries for the encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="a9c85-116">Child elements</span><span class="sxs-lookup"><span data-stu-id="a9c85-116">Child elements</span></span>
| <span data-ttu-id="a9c85-117">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-117">Name</span></span> | <span data-ttu-id="a9c85-118">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9c85-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="a9c85-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="a9c85-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="a9c85-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="a9c85-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of the AssetFiles collection.</span><span class="sxs-lookup"><span data-stu-id="a9c85-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of the AssetFiles collection.</span></span> |

## <a name="AssetFile "></a> <span data-ttu-id="a9c85-122">AssetFile element</span><span class="sxs-lookup"><span data-stu-id="a9c85-122">AssetFile element</span></span>
<span data-ttu-id="a9c85-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a9c85-124">Attributes</span><span class="sxs-lookup"><span data-stu-id="a9c85-124">Attributes</span></span>
| <span data-ttu-id="a9c85-125">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-125">Name</span></span> | <span data-ttu-id="a9c85-126">Type</span><span class="sxs-lookup"><span data-stu-id="a9c85-126">Type</span></span> | <span data-ttu-id="a9c85-127">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9c85-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="a9c85-128">**Name**</span></span><br/><br/> <span data-ttu-id="a9c85-129">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-129">Required</span></span> |<span data-ttu-id="a9c85-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-130">**xs:string**</span></span> |<span data-ttu-id="a9c85-131">The media asset file name.</span><span class="sxs-lookup"><span data-stu-id="a9c85-131">The media asset file name.</span></span> |
| <span data-ttu-id="a9c85-132">**Size**</span><span class="sxs-lookup"><span data-stu-id="a9c85-132">**Size**</span></span><br/><br/> <span data-ttu-id="a9c85-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-134">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-134">Required</span></span> |<span data-ttu-id="a9c85-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="a9c85-135">**xs:long**</span></span> |<span data-ttu-id="a9c85-136">Size of the asset file in bytes.</span><span class="sxs-lookup"><span data-stu-id="a9c85-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="a9c85-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="a9c85-137">**Duration**</span></span><br/><br/> <span data-ttu-id="a9c85-138">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-138">Required</span></span> |<span data-ttu-id="a9c85-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="a9c85-139">**xs:duration**</span></span> |<span data-ttu-id="a9c85-140">Content play back duration.</span><span class="sxs-lookup"><span data-stu-id="a9c85-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="a9c85-141">Child elements</span><span class="sxs-lookup"><span data-stu-id="a9c85-141">Child elements</span></span>
| <span data-ttu-id="a9c85-142">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-142">Name</span></span> | <span data-ttu-id="a9c85-143">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9c85-144">**Sources**</span><span class="sxs-lookup"><span data-stu-id="a9c85-144">**Sources**</span></span> |<span data-ttu-id="a9c85-145">Collection of input/source media files, that was processed in order to produce this AssetFile.</span><span class="sxs-lookup"><span data-stu-id="a9c85-145">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span> <span data-ttu-id="a9c85-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9c85-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="a9c85-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="a9c85-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="a9c85-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="a9c85-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="a9c85-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="a9c85-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="a9c85-150">This is the collection of all those video tracks.</span><span class="sxs-lookup"><span data-stu-id="a9c85-150">This is the collection of all those video tracks.</span></span> <span data-ttu-id="a9c85-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9c85-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="a9c85-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="a9c85-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="a9c85-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="a9c85-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="a9c85-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="a9c85-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="a9c85-155">This is the collection of all those audio tracks.</span><span class="sxs-lookup"><span data-stu-id="a9c85-155">This is the collection of all those audio tracks.</span></span> <span data-ttu-id="a9c85-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9c85-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <a name="Sources "></a> <span data-ttu-id="a9c85-157">Sources element</span><span class="sxs-lookup"><span data-stu-id="a9c85-157">Sources element</span></span>
<span data-ttu-id="a9c85-158">Collection of input/source media files, that was processed in order to produce this AssetFile.</span><span class="sxs-lookup"><span data-stu-id="a9c85-158">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span>  

<span data-ttu-id="a9c85-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="a9c85-160">Child elements</span><span class="sxs-lookup"><span data-stu-id="a9c85-160">Child elements</span></span>
| <span data-ttu-id="a9c85-161">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-161">Name</span></span> | <span data-ttu-id="a9c85-162">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9c85-163">**Source**</span><span class="sxs-lookup"><span data-stu-id="a9c85-163">**Source**</span></span><br/><br/> <span data-ttu-id="a9c85-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="a9c85-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="a9c85-165">An input/source file used when generating this asset.</span><span class="sxs-lookup"><span data-stu-id="a9c85-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="a9c85-166">For more information see [Source element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9c85-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <a name="Source "></a> <span data-ttu-id="a9c85-167">Source element</span><span class="sxs-lookup"><span data-stu-id="a9c85-167">Source element</span></span>
<span data-ttu-id="a9c85-168">An input/source file used when generating this asset.</span><span class="sxs-lookup"><span data-stu-id="a9c85-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="a9c85-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a9c85-170">Attributes</span><span class="sxs-lookup"><span data-stu-id="a9c85-170">Attributes</span></span>
| <span data-ttu-id="a9c85-171">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-171">Name</span></span> | <span data-ttu-id="a9c85-172">Type</span><span class="sxs-lookup"><span data-stu-id="a9c85-172">Type</span></span> | <span data-ttu-id="a9c85-173">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9c85-174">**Name**</span><span class="sxs-lookup"><span data-stu-id="a9c85-174">**Name**</span></span><br/><br/> <span data-ttu-id="a9c85-175">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-175">Required</span></span> |<span data-ttu-id="a9c85-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-176">**xs:string**</span></span> |<span data-ttu-id="a9c85-177">Input source file name.</span><span class="sxs-lookup"><span data-stu-id="a9c85-177">Input source file name.</span></span> |

## <a name="VideoTracks "></a> <span data-ttu-id="a9c85-178">VideoTracks element</span><span class="sxs-lookup"><span data-stu-id="a9c85-178">VideoTracks element</span></span>
<span data-ttu-id="a9c85-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="a9c85-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="a9c85-180">This is the collection of all those video tracks.</span><span class="sxs-lookup"><span data-stu-id="a9c85-180">This is the collection of all those video tracks.</span></span>  

<span data-ttu-id="a9c85-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="a9c85-182">Child elements</span><span class="sxs-lookup"><span data-stu-id="a9c85-182">Child elements</span></span>
| <span data-ttu-id="a9c85-183">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-183">Name</span></span> | <span data-ttu-id="a9c85-184">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9c85-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="a9c85-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="a9c85-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="a9c85-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="a9c85-187">A specific video track in the parent AssetFile.</span><span class="sxs-lookup"><span data-stu-id="a9c85-187">A specific video track in the parent AssetFile.</span></span> <span data-ttu-id="a9c85-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="a9c85-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <a name="VideoTrack"></a> <span data-ttu-id="a9c85-189">VideoTrack element</span><span class="sxs-lookup"><span data-stu-id="a9c85-189">VideoTrack element</span></span>
<span data-ttu-id="a9c85-190">A specific video track in the parent AssetFile.</span><span class="sxs-lookup"><span data-stu-id="a9c85-190">A specific video track in the parent AssetFile.</span></span>  

<span data-ttu-id="a9c85-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a9c85-192">Attributes</span><span class="sxs-lookup"><span data-stu-id="a9c85-192">Attributes</span></span>
| <span data-ttu-id="a9c85-193">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-193">Name</span></span> | <span data-ttu-id="a9c85-194">Type</span><span class="sxs-lookup"><span data-stu-id="a9c85-194">Type</span></span> | <span data-ttu-id="a9c85-195">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9c85-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="a9c85-196">**Id**</span></span><br/><br/> <span data-ttu-id="a9c85-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-198">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-198">Required</span></span> |<span data-ttu-id="a9c85-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-199">**xs:int**</span></span> |<span data-ttu-id="a9c85-200">Zero-based index of this video track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span><span class="sxs-lookup"><span data-stu-id="a9c85-200">Zero-based index of this video track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="a9c85-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="a9c85-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="a9c85-202">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-202">Required</span></span> |<span data-ttu-id="a9c85-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-203">**xs:string**</span></span> |<span data-ttu-id="a9c85-204">Video codec FourCC code.</span><span class="sxs-lookup"><span data-stu-id="a9c85-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="a9c85-205">**Profile**</span><span class="sxs-lookup"><span data-stu-id="a9c85-205">**Profile**</span></span> |<span data-ttu-id="a9c85-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-206">**xs:string**</span></span> |<span data-ttu-id="a9c85-207">H264 profile (only applicable to H264 codec).</span><span class="sxs-lookup"><span data-stu-id="a9c85-207">H264 profile (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="a9c85-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="a9c85-208">**Level**</span></span> |<span data-ttu-id="a9c85-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-209">**xs:string**</span></span> |<span data-ttu-id="a9c85-210">H264 level (only applicable to H264 codec).</span><span class="sxs-lookup"><span data-stu-id="a9c85-210">H264 level (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="a9c85-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="a9c85-211">**Width**</span></span><br/><br/> <span data-ttu-id="a9c85-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-213">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-213">Required</span></span> |<span data-ttu-id="a9c85-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-214">**xs:int**</span></span> |<span data-ttu-id="a9c85-215">Encoded video width in pixels.</span><span class="sxs-lookup"><span data-stu-id="a9c85-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="a9c85-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="a9c85-216">**Height**</span></span><br/><br/> <span data-ttu-id="a9c85-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-218">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-218">Required</span></span> |<span data-ttu-id="a9c85-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-219">**xs:int**</span></span> |<span data-ttu-id="a9c85-220">Encoded video height in pixels.</span><span class="sxs-lookup"><span data-stu-id="a9c85-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="a9c85-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="a9c85-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="a9c85-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-223">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-223">Required</span></span> |<span data-ttu-id="a9c85-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="a9c85-224">**xs:double**</span></span> |<span data-ttu-id="a9c85-225">Video display aspect ratio numerator.</span><span class="sxs-lookup"><span data-stu-id="a9c85-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="a9c85-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="a9c85-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="a9c85-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-228">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-228">Required</span></span> |<span data-ttu-id="a9c85-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="a9c85-229">**xs:double**</span></span> |<span data-ttu-id="a9c85-230">Video display aspect ratio denominator.</span><span class="sxs-lookup"><span data-stu-id="a9c85-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="a9c85-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="a9c85-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="a9c85-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-233">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-233">Required</span></span> |<span data-ttu-id="a9c85-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="a9c85-234">**xs:decimal**</span></span> |<span data-ttu-id="a9c85-235">Measured video frame rate in .3f format.</span><span class="sxs-lookup"><span data-stu-id="a9c85-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="a9c85-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="a9c85-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="a9c85-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-238">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-238">Required</span></span> |<span data-ttu-id="a9c85-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="a9c85-239">**xs:decimal**</span></span> |<span data-ttu-id="a9c85-240">Preset target video frame rate in .3f format.</span><span class="sxs-lookup"><span data-stu-id="a9c85-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="a9c85-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="a9c85-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="a9c85-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-243">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-243">Required</span></span> |<span data-ttu-id="a9c85-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-244">**xs:int**</span></span> |<span data-ttu-id="a9c85-245">Average video bit rate in kilobits per second, as calculated from the AssetFile.</span><span class="sxs-lookup"><span data-stu-id="a9c85-245">Average video bit rate in kilobits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="a9c85-246">Counts only the elementary stream payload, and does not include the packaging overhead.</span><span class="sxs-lookup"><span data-stu-id="a9c85-246">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="a9c85-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="a9c85-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="a9c85-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-249">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-249">Required</span></span> |<span data-ttu-id="a9c85-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-250">**xs:int**</span></span> |<span data-ttu-id="a9c85-251">Target average bitrate for this video track, as requested via the encoding preset, in kilobits per second.</span><span class="sxs-lookup"><span data-stu-id="a9c85-251">Target average bitrate for this video track, as requested via the encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="a9c85-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="a9c85-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="a9c85-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-253">minInclusive ="0"</span></span> |<span data-ttu-id="a9c85-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-254">**xs:int**</span></span> |<span data-ttu-id="a9c85-255">Max GOP average bitrate for this video track, in kilobits per second.</span><span class="sxs-lookup"><span data-stu-id="a9c85-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <a name="AudioTracks "></a> <span data-ttu-id="a9c85-256">AudioTracks element</span><span class="sxs-lookup"><span data-stu-id="a9c85-256">AudioTracks element</span></span>
<span data-ttu-id="a9c85-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="a9c85-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="a9c85-258">This is the collection of all those audio tracks.</span><span class="sxs-lookup"><span data-stu-id="a9c85-258">This is the collection of all those audio tracks.</span></span>  

<span data-ttu-id="a9c85-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="a9c85-260">Child elements</span><span class="sxs-lookup"><span data-stu-id="a9c85-260">Child elements</span></span>
| <span data-ttu-id="a9c85-261">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-261">Name</span></span> | <span data-ttu-id="a9c85-262">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9c85-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="a9c85-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="a9c85-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="a9c85-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="a9c85-265">A specific audio track in the parent AssetFile.</span><span class="sxs-lookup"><span data-stu-id="a9c85-265">A specific audio track in the parent AssetFile.</span></span> <span data-ttu-id="a9c85-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9c85-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <a name="AudioTrack "></a> <span data-ttu-id="a9c85-267">AudioTrack element</span><span class="sxs-lookup"><span data-stu-id="a9c85-267">AudioTrack element</span></span>
<span data-ttu-id="a9c85-268">A specific audio track in the parent AssetFile.</span><span class="sxs-lookup"><span data-stu-id="a9c85-268">A specific audio track in the parent AssetFile.</span></span>  

<span data-ttu-id="a9c85-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a9c85-270">Attributes</span><span class="sxs-lookup"><span data-stu-id="a9c85-270">Attributes</span></span>
| <span data-ttu-id="a9c85-271">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-271">Name</span></span> | <span data-ttu-id="a9c85-272">Type</span><span class="sxs-lookup"><span data-stu-id="a9c85-272">Type</span></span> | <span data-ttu-id="a9c85-273">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9c85-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="a9c85-274">**Id**</span></span><br/><br/> <span data-ttu-id="a9c85-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-276">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-276">Required</span></span> |<span data-ttu-id="a9c85-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-277">**xs:int**</span></span> |<span data-ttu-id="a9c85-278">Zero-based index of this audio track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span><span class="sxs-lookup"><span data-stu-id="a9c85-278">Zero-based index of this audio track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="a9c85-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="a9c85-279">**Codec**</span></span> |<span data-ttu-id="a9c85-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-280">**xs:string**</span></span> |<span data-ttu-id="a9c85-281">Audio track codec string.</span><span class="sxs-lookup"><span data-stu-id="a9c85-281">Audio track codec string.</span></span> |
| <span data-ttu-id="a9c85-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="a9c85-282">**EncoderVersion**</span></span> |<span data-ttu-id="a9c85-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-283">**xs:string**</span></span> |<span data-ttu-id="a9c85-284">Optional encoder version string, required for EAC3.</span><span class="sxs-lookup"><span data-stu-id="a9c85-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="a9c85-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="a9c85-285">**Channels**</span></span><br/><br/> <span data-ttu-id="a9c85-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-287">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-287">Required</span></span> |<span data-ttu-id="a9c85-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-288">**xs:int**</span></span> |<span data-ttu-id="a9c85-289">Number of audio channels.</span><span class="sxs-lookup"><span data-stu-id="a9c85-289">Number of audio channels.</span></span> |
| <span data-ttu-id="a9c85-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="a9c85-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="a9c85-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-292">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-292">Required</span></span> |<span data-ttu-id="a9c85-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-293">**xs:int**</span></span> |<span data-ttu-id="a9c85-294">Audio sampling rate in samples/sec or Hz.</span><span class="sxs-lookup"><span data-stu-id="a9c85-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="a9c85-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="a9c85-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="a9c85-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-297">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-297">Required</span></span> |<span data-ttu-id="a9c85-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-298">**xs:int**</span></span> |<span data-ttu-id="a9c85-299">Average audio bit rate in bits per second, as calculated from the AssetFile.</span><span class="sxs-lookup"><span data-stu-id="a9c85-299">Average audio bit rate in bits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="a9c85-300">Counts only the elementary stream payload, and does not include the packaging overhead.</span><span class="sxs-lookup"><span data-stu-id="a9c85-300">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="a9c85-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="a9c85-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="a9c85-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="a9c85-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="a9c85-303">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-303">Required</span></span> |<span data-ttu-id="a9c85-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-304">**xs:int**</span></span> |<span data-ttu-id="a9c85-305">Bits per sample for the wFormatTag format type.</span><span class="sxs-lookup"><span data-stu-id="a9c85-305">Bits per sample for the wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="a9c85-306">Child elements</span><span class="sxs-lookup"><span data-stu-id="a9c85-306">Child elements</span></span>
| <span data-ttu-id="a9c85-307">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-307">Name</span></span> | <span data-ttu-id="a9c85-308">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9c85-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="a9c85-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="a9c85-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="a9c85-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="a9c85-311">Loudness metering result parameters.</span><span class="sxs-lookup"><span data-stu-id="a9c85-311">Loudness metering result parameters.</span></span> <span data-ttu-id="a9c85-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9c85-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <a name="LoudnessMeteringResultParameters "></a> <span data-ttu-id="a9c85-313">LoudnessMeteringResultParameters element</span><span class="sxs-lookup"><span data-stu-id="a9c85-313">LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="a9c85-314">Loudness metering result parameters.</span><span class="sxs-lookup"><span data-stu-id="a9c85-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="a9c85-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="a9c85-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="a9c85-316">Attributes</span><span class="sxs-lookup"><span data-stu-id="a9c85-316">Attributes</span></span>
| <span data-ttu-id="a9c85-317">Name</span><span class="sxs-lookup"><span data-stu-id="a9c85-317">Name</span></span> | <span data-ttu-id="a9c85-318">Type</span><span class="sxs-lookup"><span data-stu-id="a9c85-318">Type</span></span> | <span data-ttu-id="a9c85-319">Description</span><span class="sxs-lookup"><span data-stu-id="a9c85-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9c85-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="a9c85-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="a9c85-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-321">**xs:string**</span></span> |<span data-ttu-id="a9c85-322">**Dolby** professional loudness metering development kit version.</span><span class="sxs-lookup"><span data-stu-id="a9c85-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="a9c85-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="a9c85-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="a9c85-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="a9c85-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="a9c85-325">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-325">Required</span></span> |<span data-ttu-id="a9c85-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="a9c85-326">**xs:int**</span></span> |<span data-ttu-id="a9c85-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span><span class="sxs-lookup"><span data-stu-id="a9c85-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="a9c85-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="a9c85-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="a9c85-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="a9c85-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="a9c85-330">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-330">Required</span></span> |<span data-ttu-id="a9c85-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="a9c85-331">**xs:float**</span></span> |<span data-ttu-id="a9c85-332">Integrated loudness</span><span class="sxs-lookup"><span data-stu-id="a9c85-332">Integrated loudness</span></span> |
| <span data-ttu-id="a9c85-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="a9c85-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="a9c85-334">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-334">Required</span></span> |<span data-ttu-id="a9c85-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-335">**xs:string**</span></span> |<span data-ttu-id="a9c85-336">Integrated loudness unit.</span><span class="sxs-lookup"><span data-stu-id="a9c85-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="a9c85-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="a9c85-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="a9c85-338">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-338">Required</span></span> |<span data-ttu-id="a9c85-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="a9c85-339">**xs:string**</span></span> |<span data-ttu-id="a9c85-340">Gating identifier</span><span class="sxs-lookup"><span data-stu-id="a9c85-340">Gating identifier</span></span> |
| <span data-ttu-id="a9c85-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="a9c85-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="a9c85-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="a9c85-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="a9c85-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="a9c85-343">**xs:float**</span></span> |<span data-ttu-id="a9c85-344">Speech content over the program, as a percentage.</span><span class="sxs-lookup"><span data-stu-id="a9c85-344">Speech content over the program, as a percentage.</span></span> |
| <span data-ttu-id="a9c85-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="a9c85-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="a9c85-346">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-346">Required</span></span> |<span data-ttu-id="a9c85-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="a9c85-347">**xs:float**</span></span> |<span data-ttu-id="a9c85-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span><span class="sxs-lookup"><span data-stu-id="a9c85-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="a9c85-349">Units are dBFS.</span><span class="sxs-lookup"><span data-stu-id="a9c85-349">Units are dBFS.</span></span> |
| <span data-ttu-id="a9c85-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="a9c85-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="a9c85-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="a9c85-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="a9c85-352">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-352">Required</span></span> |<span data-ttu-id="a9c85-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="a9c85-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="a9c85-354">Sample peak unit.</span><span class="sxs-lookup"><span data-stu-id="a9c85-354">Sample peak unit.</span></span> |
| <span data-ttu-id="a9c85-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="a9c85-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="a9c85-356">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-356">Required</span></span> |<span data-ttu-id="a9c85-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="a9c85-357">**xs:float**</span></span> |<span data-ttu-id="a9c85-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span><span class="sxs-lookup"><span data-stu-id="a9c85-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="a9c85-359">Units are dBTP.</span><span class="sxs-lookup"><span data-stu-id="a9c85-359">Units are dBTP.</span></span> |
| <span data-ttu-id="a9c85-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="a9c85-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="a9c85-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="a9c85-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="a9c85-362">Required</span><span class="sxs-lookup"><span data-stu-id="a9c85-362">Required</span></span> |<span data-ttu-id="a9c85-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="a9c85-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="a9c85-364">True peak unit.</span><span class="sxs-lookup"><span data-stu-id="a9c85-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="a9c85-365">Schema Code</span><span class="sxs-lookup"><span data-stu-id="a9c85-365">Schema Code</span></span>
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



## <a name="xml"></a> <span data-ttu-id="a9c85-366">XML example</span><span class="sxs-lookup"><span data-stu-id="a9c85-366">XML example</span></span>
 <span data-ttu-id="a9c85-367">The following is an example of the Output metadata file.</span><span class="sxs-lookup"><span data-stu-id="a9c85-367">The following is an example of the Output metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="a9c85-368">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9c85-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a9c85-369">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="a9c85-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
