---
title: Azure Media Services input metadata schema | Microsoft Docs
description: The topic gives an overview of Azure Media Services input metadata schema.
author: Juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: juliako
ms.openlocfilehash: 21cbbb10065df9ae9c63b775a6526ea9c4f92136
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552755"
---
# <a name="input-metadata"></a><span data-ttu-id="6d952-103">Input Metadata</span><span class="sxs-lookup"><span data-stu-id="6d952-103">Input Metadata</span></span>
<span data-ttu-id="6d952-104">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span><span class="sxs-lookup"><span data-stu-id="6d952-104">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span>  <span data-ttu-id="6d952-105">Upon completion of a task, an output asset is produced.</span><span class="sxs-lookup"><span data-stu-id="6d952-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="6d952-106">The output asset contains video, audio, thumbnails, manifest, etc. The output asset also contains a file with metadata about the input asset.</span><span class="sxs-lookup"><span data-stu-id="6d952-106">The output asset contains video, audio, thumbnails, manifest, etc. The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="6d952-107">The name of the metadata XML file has the following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is the AssetId value of the input asset.</span><span class="sxs-lookup"><span data-stu-id="6d952-107">The name of the metadata XML file has the following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is the AssetId value of the input asset.</span></span>  

<span data-ttu-id="6d952-108">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span><span class="sxs-lookup"><span data-stu-id="6d952-108">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span> <span data-ttu-id="6d952-109">You can find an example on how to create a SAS locator and download a file  [Using the Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6d952-109">You can find an example on how to create a SAS locator and download a file  [Using the Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="6d952-110">This topic discusses the elements and types of the XML schema on which the input metada (&lt;asset_id&gt;_metadata.xml) is based.</span><span class="sxs-lookup"><span data-stu-id="6d952-110">This topic discusses the elements and types of the XML schema on which the input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="6d952-111">For information about the file that contains metadata about the output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="6d952-111">For information about the file that contains metadata about the output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="6d952-112">You can find the [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at the end of this topic.</span><span class="sxs-lookup"><span data-stu-id="6d952-112">You can find the [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at the end of this topic.</span></span>  
> 
> 

## <a name="AssetFiles"></a> <span data-ttu-id="6d952-113">AssetFiles element (root element)</span><span class="sxs-lookup"><span data-stu-id="6d952-113">AssetFiles element (root element)</span></span>
<span data-ttu-id="6d952-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for the encoding job.</span><span class="sxs-lookup"><span data-stu-id="6d952-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for the encoding job.</span></span>  

<span data-ttu-id="6d952-115">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-115">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="6d952-116">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-116">Name</span></span> | <span data-ttu-id="6d952-117">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d952-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="6d952-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="6d952-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d952-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="6d952-120">A single child element.</span><span class="sxs-lookup"><span data-stu-id="6d952-120">A single child element.</span></span> <span data-ttu-id="6d952-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="6d952-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <a name="AssetFile"></a> <span data-ttu-id="6d952-122">AssetFile element</span><span class="sxs-lookup"><span data-stu-id="6d952-122">AssetFile element</span></span>
 <span data-ttu-id="6d952-123">Contains attributes and elements that describe an asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="6d952-124">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-124">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d952-125">Attributes</span><span class="sxs-lookup"><span data-stu-id="6d952-125">Attributes</span></span>
| <span data-ttu-id="6d952-126">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-126">Name</span></span> | <span data-ttu-id="6d952-127">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-127">Type</span></span> | <span data-ttu-id="6d952-128">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-129">**Name**</span><span class="sxs-lookup"><span data-stu-id="6d952-129">**Name**</span></span><br /><br /> <span data-ttu-id="6d952-130">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-130">Required</span></span> |<span data-ttu-id="6d952-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-131">**xs:string**</span></span> |<span data-ttu-id="6d952-132">Asset file name.</span><span class="sxs-lookup"><span data-stu-id="6d952-132">Asset file name.</span></span> |
| <span data-ttu-id="6d952-133">**Size**</span><span class="sxs-lookup"><span data-stu-id="6d952-133">**Size**</span></span><br /><br /> <span data-ttu-id="6d952-134">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-134">Required</span></span> |<span data-ttu-id="6d952-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="6d952-135">**xs:long**</span></span> |<span data-ttu-id="6d952-136">Size of the asset file in bytes.</span><span class="sxs-lookup"><span data-stu-id="6d952-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="6d952-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="6d952-137">**Duration**</span></span><br /><br /> <span data-ttu-id="6d952-138">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-138">Required</span></span> |<span data-ttu-id="6d952-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6d952-139">**xs:duration**</span></span> |<span data-ttu-id="6d952-140">Content play back duration.</span><span class="sxs-lookup"><span data-stu-id="6d952-140">Content play back duration.</span></span> <span data-ttu-id="6d952-141">Example: Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="6d952-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="6d952-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="6d952-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="6d952-143">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-143">Required</span></span> |<span data-ttu-id="6d952-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-144">**xs:int**</span></span> |<span data-ttu-id="6d952-145">Number of streams in the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-145">Number of streams in the asset file.</span></span> |
| <span data-ttu-id="6d952-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="6d952-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="6d952-147">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-147">Required</span></span> |<span data-ttu-id="6d952-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-148">**xs:string**</span></span> |<span data-ttu-id="6d952-149">Format names.</span><span class="sxs-lookup"><span data-stu-id="6d952-149">Format names.</span></span> |
| <span data-ttu-id="6d952-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="6d952-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="6d952-151">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-151">Required</span></span> |<span data-ttu-id="6d952-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-152">**xs:string**</span></span> |<span data-ttu-id="6d952-153">Format verbose names.</span><span class="sxs-lookup"><span data-stu-id="6d952-153">Format verbose names.</span></span> |
| <span data-ttu-id="6d952-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="6d952-154">**StartTime**</span></span> |<span data-ttu-id="6d952-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6d952-155">**xs:duration**</span></span> |<span data-ttu-id="6d952-156">Content start time.</span><span class="sxs-lookup"><span data-stu-id="6d952-156">Content start time.</span></span> <span data-ttu-id="6d952-157">Example: StartTime="PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="6d952-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="6d952-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="6d952-158">**OverallBitRate**</span></span> |<span data-ttu-id="6d952-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-159">**xs:int**</span></span> |<span data-ttu-id="6d952-160">Average bitrate of the asset file in kbps.</span><span class="sxs-lookup"><span data-stu-id="6d952-160">Average bitrate of the asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="6d952-161">The following 4 child elements must appear in a sequence.</span><span class="sxs-lookup"><span data-stu-id="6d952-161">The following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="6d952-162">Child elements</span><span class="sxs-lookup"><span data-stu-id="6d952-162">Child elements</span></span>
| <span data-ttu-id="6d952-163">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-163">Name</span></span> | <span data-ttu-id="6d952-164">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-164">Type</span></span> | <span data-ttu-id="6d952-165">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-166">**Programs**</span><span class="sxs-lookup"><span data-stu-id="6d952-166">**Programs**</span></span><br /><br /> <span data-ttu-id="6d952-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6d952-167">minOccurs="0"</span></span> | |<span data-ttu-id="6d952-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when the asset file is in MPEG-TS format.</span><span class="sxs-lookup"><span data-stu-id="6d952-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when the asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="6d952-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="6d952-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="6d952-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6d952-170">minOccurs="0"</span></span> | |<span data-ttu-id="6d952-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="6d952-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="6d952-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="6d952-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="6d952-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="6d952-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6d952-174">minOccurs="0"</span></span> | |<span data-ttu-id="6d952-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span><span class="sxs-lookup"><span data-stu-id="6d952-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="6d952-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="6d952-177">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="6d952-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="6d952-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d952-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d952-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="6d952-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="6d952-180">Asset file’s metadata represented as key\value strings.</span><span class="sxs-lookup"><span data-stu-id="6d952-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="6d952-181">For example:</span><span class="sxs-lookup"><span data-stu-id="6d952-181">For example:</span></span><br /><br /> <span data-ttu-id="6d952-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="6d952-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <a name="TrackType"></a> <span data-ttu-id="6d952-183">TrackType</span><span class="sxs-lookup"><span data-stu-id="6d952-183">TrackType</span></span>
<span data-ttu-id="6d952-184">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-184">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d952-185">Attributes</span><span class="sxs-lookup"><span data-stu-id="6d952-185">Attributes</span></span>
| <span data-ttu-id="6d952-186">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-186">Name</span></span> | <span data-ttu-id="6d952-187">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-187">Type</span></span> | <span data-ttu-id="6d952-188">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="6d952-189">**Id**</span></span><br /><br /> <span data-ttu-id="6d952-190">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-190">Required</span></span> |<span data-ttu-id="6d952-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-191">**xs:int**</span></span> |<span data-ttu-id="6d952-192">Zero-based index of this audio or video track.</span><span class="sxs-lookup"><span data-stu-id="6d952-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="6d952-193">This is not necessarily that the TrackID as used in an MP4 file.</span><span class="sxs-lookup"><span data-stu-id="6d952-193">This is not necessarily that the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="6d952-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="6d952-194">**Codec**</span></span> |<span data-ttu-id="6d952-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-195">**xs:string**</span></span> |<span data-ttu-id="6d952-196">Video track codec string.</span><span class="sxs-lookup"><span data-stu-id="6d952-196">Video track codec string.</span></span> |
| <span data-ttu-id="6d952-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="6d952-197">**CodecLongName**</span></span> |<span data-ttu-id="6d952-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-198">**xs:string**</span></span> |<span data-ttu-id="6d952-199">Audio or video track codec long name.</span><span class="sxs-lookup"><span data-stu-id="6d952-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="6d952-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="6d952-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="6d952-201">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-201">Required</span></span> |<span data-ttu-id="6d952-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-202">**xs:string**</span></span> |<span data-ttu-id="6d952-203">Time base.</span><span class="sxs-lookup"><span data-stu-id="6d952-203">Time base.</span></span> <span data-ttu-id="6d952-204">Example: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="6d952-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="6d952-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="6d952-205">**NumberOfFrames**</span></span> |<span data-ttu-id="6d952-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-206">**xs:int**</span></span> |<span data-ttu-id="6d952-207">Number of frames (present for video tracks).</span><span class="sxs-lookup"><span data-stu-id="6d952-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="6d952-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="6d952-208">**StartTime**</span></span> |<span data-ttu-id="6d952-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6d952-209">**xs:duration**</span></span> |<span data-ttu-id="6d952-210">Track start time.</span><span class="sxs-lookup"><span data-stu-id="6d952-210">Track start time.</span></span> <span data-ttu-id="6d952-211">Example: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="6d952-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="6d952-212">**Duration**</span><span class="sxs-lookup"><span data-stu-id="6d952-212">**Duration**</span></span> |<span data-ttu-id="6d952-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6d952-213">**xs:duration**</span></span> |<span data-ttu-id="6d952-214">Track duration.</span><span class="sxs-lookup"><span data-stu-id="6d952-214">Track duration.</span></span> <span data-ttu-id="6d952-215">Example: Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="6d952-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="6d952-216">The following 2 child elements must appear in a sequence.</span><span class="sxs-lookup"><span data-stu-id="6d952-216">The following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="6d952-217">Child elements</span><span class="sxs-lookup"><span data-stu-id="6d952-217">Child elements</span></span>
| <span data-ttu-id="6d952-218">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-218">Name</span></span> | <span data-ttu-id="6d952-219">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-219">Type</span></span> | <span data-ttu-id="6d952-220">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="6d952-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="6d952-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="6d952-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="6d952-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="6d952-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="6d952-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span><span class="sxs-lookup"><span data-stu-id="6d952-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="6d952-225">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="6d952-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="6d952-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d952-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d952-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="6d952-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="6d952-228">Generic key/value strings that can be used to hold a variety of information.</span><span class="sxs-lookup"><span data-stu-id="6d952-228">Generic key/value strings that can be used to hold a variety of information.</span></span> <span data-ttu-id="6d952-229">For example, key=”language”, and value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="6d952-229">For example, key=”language”, and value=”eng”.</span></span> |

## <a name="AudioTrackType"></a> <span data-ttu-id="6d952-230">AudioTrackType (inherits from TrackType)</span><span class="sxs-lookup"><span data-stu-id="6d952-230">AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="6d952-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="6d952-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="6d952-232">The type represents a specific audio track in the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-232">The type represents a specific audio track in the asset file.</span></span>  

 <span data-ttu-id="6d952-233">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-233">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d952-234">Attributes</span><span class="sxs-lookup"><span data-stu-id="6d952-234">Attributes</span></span>
| <span data-ttu-id="6d952-235">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-235">Name</span></span> | <span data-ttu-id="6d952-236">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-236">Type</span></span> | <span data-ttu-id="6d952-237">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="6d952-238">**SampleFormat**</span></span> |<span data-ttu-id="6d952-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-239">**xs:string**</span></span> |<span data-ttu-id="6d952-240">Sample format.</span><span class="sxs-lookup"><span data-stu-id="6d952-240">Sample format.</span></span> |
| <span data-ttu-id="6d952-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="6d952-241">**ChannelLayout**</span></span> |<span data-ttu-id="6d952-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-242">**xs:string**</span></span> |<span data-ttu-id="6d952-243">Channel layout.</span><span class="sxs-lookup"><span data-stu-id="6d952-243">Channel layout.</span></span> |
| <span data-ttu-id="6d952-244">**Channels**</span><span class="sxs-lookup"><span data-stu-id="6d952-244">**Channels**</span></span><br /><br /> <span data-ttu-id="6d952-245">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-245">Required</span></span> |<span data-ttu-id="6d952-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-246">**xs:int**</span></span> |<span data-ttu-id="6d952-247">Number (0 or more) of audio channels.</span><span class="sxs-lookup"><span data-stu-id="6d952-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="6d952-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="6d952-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="6d952-249">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-249">Required</span></span> |<span data-ttu-id="6d952-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-250">**xs:int**</span></span> |<span data-ttu-id="6d952-251">Audio sampling rate in samples/sec or Hz.</span><span class="sxs-lookup"><span data-stu-id="6d952-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="6d952-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="6d952-252">**Bitrate**</span></span> |<span data-ttu-id="6d952-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-253">**xs:int**</span></span> |<span data-ttu-id="6d952-254">Average audio bit rate in bits per second, as calculated from the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-254">Average audio bit rate in bits per second, as calculated from the asset file.</span></span> <span data-ttu-id="6d952-255">Only the elementary stream payload is counted, and the packaging overhead is not included in this count.</span><span class="sxs-lookup"><span data-stu-id="6d952-255">Only the elementary stream payload is counted, and the packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="6d952-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="6d952-256">**BitsPerSample**</span></span> |<span data-ttu-id="6d952-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-257">**xs:int**</span></span> |<span data-ttu-id="6d952-258">Bits per sample for the wFormatTag format type.</span><span class="sxs-lookup"><span data-stu-id="6d952-258">Bits per sample for the wFormatTag format type.</span></span> |

## <a name="VideoTrackType"></a> <span data-ttu-id="6d952-259">VideoTrackType (inherits from TrackType)</span><span class="sxs-lookup"><span data-stu-id="6d952-259">VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="6d952-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="6d952-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="6d952-261">The type represents a specific video track in the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-261">The type represents a specific video track in the asset file.</span></span>  

<span data-ttu-id="6d952-262">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-262">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d952-263">Attributes</span><span class="sxs-lookup"><span data-stu-id="6d952-263">Attributes</span></span>
| <span data-ttu-id="6d952-264">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-264">Name</span></span> | <span data-ttu-id="6d952-265">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-265">Type</span></span> | <span data-ttu-id="6d952-266">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="6d952-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="6d952-268">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-268">Required</span></span> |<span data-ttu-id="6d952-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-269">**xs:string**</span></span> |<span data-ttu-id="6d952-270">Video codec FourCC code.</span><span class="sxs-lookup"><span data-stu-id="6d952-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="6d952-271">**Profile**</span><span class="sxs-lookup"><span data-stu-id="6d952-271">**Profile**</span></span> |<span data-ttu-id="6d952-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-272">**xs:string**</span></span> |<span data-ttu-id="6d952-273">Video track's profile.</span><span class="sxs-lookup"><span data-stu-id="6d952-273">Video track's profile.</span></span> |
| <span data-ttu-id="6d952-274">**Level**</span><span class="sxs-lookup"><span data-stu-id="6d952-274">**Level**</span></span> |<span data-ttu-id="6d952-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-275">**xs:string**</span></span> |<span data-ttu-id="6d952-276">Video track's level.</span><span class="sxs-lookup"><span data-stu-id="6d952-276">Video track's level.</span></span> |
| <span data-ttu-id="6d952-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="6d952-277">**PixelFormat**</span></span> |<span data-ttu-id="6d952-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-278">**xs:string**</span></span> |<span data-ttu-id="6d952-279">Video track's pixel format.</span><span class="sxs-lookup"><span data-stu-id="6d952-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="6d952-280">**Width**</span><span class="sxs-lookup"><span data-stu-id="6d952-280">**Width**</span></span><br /><br /> <span data-ttu-id="6d952-281">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-281">Required</span></span> |<span data-ttu-id="6d952-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-282">**xs:int**</span></span> |<span data-ttu-id="6d952-283">Encoded video width in pixels.</span><span class="sxs-lookup"><span data-stu-id="6d952-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="6d952-284">**Height**</span><span class="sxs-lookup"><span data-stu-id="6d952-284">**Height**</span></span><br /><br /> <span data-ttu-id="6d952-285">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-285">Required</span></span> |<span data-ttu-id="6d952-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-286">**xs:int**</span></span> |<span data-ttu-id="6d952-287">Encoded video height in pixels.</span><span class="sxs-lookup"><span data-stu-id="6d952-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="6d952-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6d952-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="6d952-289">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-289">Required</span></span> |<span data-ttu-id="6d952-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d952-290">**xs:double**</span></span> |<span data-ttu-id="6d952-291">Video display aspect ratio numerator.</span><span class="sxs-lookup"><span data-stu-id="6d952-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="6d952-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="6d952-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="6d952-293">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-293">Required</span></span> |<span data-ttu-id="6d952-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d952-294">**xs:double**</span></span> |<span data-ttu-id="6d952-295">Video display aspect ratio denominator.</span><span class="sxs-lookup"><span data-stu-id="6d952-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="6d952-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="6d952-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="6d952-297">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-297">Required</span></span> |<span data-ttu-id="6d952-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d952-298">**xs:double**</span></span> |<span data-ttu-id="6d952-299">Video sample aspect ratio numerator.</span><span class="sxs-lookup"><span data-stu-id="6d952-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="6d952-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6d952-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="6d952-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d952-301">**xs:double**</span></span> |<span data-ttu-id="6d952-302">Video sample aspect ratio numerator.</span><span class="sxs-lookup"><span data-stu-id="6d952-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="6d952-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6d952-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="6d952-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d952-304">**xs:double**</span></span> |<span data-ttu-id="6d952-305">Video sample aspect ratio denominator.</span><span class="sxs-lookup"><span data-stu-id="6d952-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="6d952-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="6d952-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="6d952-307">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-307">Required</span></span> |<span data-ttu-id="6d952-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="6d952-308">**xs:decimal**</span></span> |<span data-ttu-id="6d952-309">Measured video frame rate in .3f format.</span><span class="sxs-lookup"><span data-stu-id="6d952-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="6d952-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="6d952-310">**Bitrate**</span></span> |<span data-ttu-id="6d952-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-311">**xs:int**</span></span> |<span data-ttu-id="6d952-312">Average video bit rate in kilobits per second, as calculated from the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-312">Average video bit rate in kilobits per second, as calculated from the asset file.</span></span> <span data-ttu-id="6d952-313">Only the elementary stream payload is counted, and the packaging overhead is not included.</span><span class="sxs-lookup"><span data-stu-id="6d952-313">Only the elementary stream payload is counted, and the packaging overhead is not included.</span></span> |
| <span data-ttu-id="6d952-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="6d952-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="6d952-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-315">**xs:int**</span></span> |<span data-ttu-id="6d952-316">Max GOP average bitrate for this video track, in kilobits per second.</span><span class="sxs-lookup"><span data-stu-id="6d952-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="6d952-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="6d952-317">**HasBFrames**</span></span> |<span data-ttu-id="6d952-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-318">**xs:int**</span></span> |<span data-ttu-id="6d952-319">Video track number of B frames.</span><span class="sxs-lookup"><span data-stu-id="6d952-319">Video track number of B frames.</span></span> |

## <a name="MetadataType"></a> <span data-ttu-id="6d952-320">MetadataType</span><span class="sxs-lookup"><span data-stu-id="6d952-320">MetadataType</span></span>
<span data-ttu-id="6d952-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span><span class="sxs-lookup"><span data-stu-id="6d952-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="6d952-322">For example, key=”language”, and value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="6d952-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="6d952-323">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-323">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d952-324">Attributes</span><span class="sxs-lookup"><span data-stu-id="6d952-324">Attributes</span></span>
| <span data-ttu-id="6d952-325">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-325">Name</span></span> | <span data-ttu-id="6d952-326">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-326">Type</span></span> | <span data-ttu-id="6d952-327">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-328">**key**</span><span class="sxs-lookup"><span data-stu-id="6d952-328">**key**</span></span><br /><br /> <span data-ttu-id="6d952-329">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-329">Required</span></span> |<span data-ttu-id="6d952-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-330">**xs:string**</span></span> |<span data-ttu-id="6d952-331">The key in the key/value pair.</span><span class="sxs-lookup"><span data-stu-id="6d952-331">The key in the key/value pair.</span></span> |
| <span data-ttu-id="6d952-332">**value**</span><span class="sxs-lookup"><span data-stu-id="6d952-332">**value**</span></span><br /><br /> <span data-ttu-id="6d952-333">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-333">Required</span></span> |<span data-ttu-id="6d952-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d952-334">**xs:string**</span></span> |<span data-ttu-id="6d952-335">The value in the key/value pair.</span><span class="sxs-lookup"><span data-stu-id="6d952-335">The value in the key/value pair.</span></span> |

## <a name="ProgramType"></a> <span data-ttu-id="6d952-336">ProgramType</span><span class="sxs-lookup"><span data-stu-id="6d952-336">ProgramType</span></span>
<span data-ttu-id="6d952-337">**ProgramType** is a global complex type that describes a program.</span><span class="sxs-lookup"><span data-stu-id="6d952-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d952-338">Attributes</span><span class="sxs-lookup"><span data-stu-id="6d952-338">Attributes</span></span>
| <span data-ttu-id="6d952-339">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-339">Name</span></span> | <span data-ttu-id="6d952-340">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-340">Type</span></span> | <span data-ttu-id="6d952-341">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="6d952-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="6d952-343">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-343">Required</span></span> |<span data-ttu-id="6d952-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-344">**xs:int**</span></span> |<span data-ttu-id="6d952-345">Program Id</span><span class="sxs-lookup"><span data-stu-id="6d952-345">Program Id</span></span> |
| <span data-ttu-id="6d952-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="6d952-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="6d952-347">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-347">Required</span></span> |<span data-ttu-id="6d952-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-348">**xs:int**</span></span> |<span data-ttu-id="6d952-349">Number of programs.</span><span class="sxs-lookup"><span data-stu-id="6d952-349">Number of programs.</span></span> |
| <span data-ttu-id="6d952-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="6d952-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="6d952-351">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-351">Required</span></span> |<span data-ttu-id="6d952-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-352">**xs:int**</span></span> |<span data-ttu-id="6d952-353">Program Map Tables (PMTs) contain information about programs.</span><span class="sxs-lookup"><span data-stu-id="6d952-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="6d952-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="6d952-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="6d952-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="6d952-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="6d952-356">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-356">Required</span></span> |<span data-ttu-id="6d952-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-357">**xs:int**</span></span> |<span data-ttu-id="6d952-358">Used by decoder.</span><span class="sxs-lookup"><span data-stu-id="6d952-358">Used by decoder.</span></span> <span data-ttu-id="6d952-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="6d952-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="6d952-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="6d952-360">**StartPTS**</span></span> |<span data-ttu-id="6d952-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="6d952-361">**xs: long**</span></span> |<span data-ttu-id="6d952-362">Starting presentation time stamp.</span><span class="sxs-lookup"><span data-stu-id="6d952-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="6d952-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="6d952-363">**EndPTS**</span></span> |<span data-ttu-id="6d952-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="6d952-364">**xs: long**</span></span> |<span data-ttu-id="6d952-365">Ending presentation time stamp.</span><span class="sxs-lookup"><span data-stu-id="6d952-365">Ending presentation time stamp.</span></span> |

## <a name="StreamDispositionType"></a> <span data-ttu-id="6d952-366">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="6d952-366">StreamDispositionType</span></span>
<span data-ttu-id="6d952-367">**StreamDispositionType** is a global complex type that describes the stream.</span><span class="sxs-lookup"><span data-stu-id="6d952-367">**StreamDispositionType** is a global complex type that describes the stream.</span></span>  

<span data-ttu-id="6d952-368">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-368">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d952-369">Attributes</span><span class="sxs-lookup"><span data-stu-id="6d952-369">Attributes</span></span>
| <span data-ttu-id="6d952-370">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-370">Name</span></span> | <span data-ttu-id="6d952-371">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-371">Type</span></span> | <span data-ttu-id="6d952-372">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-373">**Default**</span><span class="sxs-lookup"><span data-stu-id="6d952-373">**Default**</span></span><br /><br /> <span data-ttu-id="6d952-374">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-374">Required</span></span> |<span data-ttu-id="6d952-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-375">**xs:int**</span></span> |<span data-ttu-id="6d952-376">Set this attribute to 1 to indicate this is the default presentation.</span><span class="sxs-lookup"><span data-stu-id="6d952-376">Set this attribute to 1 to indicate this is the default presentation.</span></span> |
| <span data-ttu-id="6d952-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="6d952-377">**Dub**</span></span><br /><br /> <span data-ttu-id="6d952-378">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-378">Required</span></span> |<span data-ttu-id="6d952-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-379">**xs:int**</span></span> |<span data-ttu-id="6d952-380">Set this attribute to 1 to indicate this is the dubbed presentation.</span><span class="sxs-lookup"><span data-stu-id="6d952-380">Set this attribute to 1 to indicate this is the dubbed presentation.</span></span> |
| <span data-ttu-id="6d952-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="6d952-381">**Original**</span></span><br /><br /> <span data-ttu-id="6d952-382">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-382">Required</span></span> |<span data-ttu-id="6d952-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-383">**xs:int**</span></span> |<span data-ttu-id="6d952-384">Set this attribute to 1 to indicate this is the original presentation.</span><span class="sxs-lookup"><span data-stu-id="6d952-384">Set this attribute to 1 to indicate this is the original presentation.</span></span> |
| <span data-ttu-id="6d952-385">**Comment**</span><span class="sxs-lookup"><span data-stu-id="6d952-385">**Comment**</span></span><br /><br /> <span data-ttu-id="6d952-386">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-386">Required</span></span> |<span data-ttu-id="6d952-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-387">**xs:int**</span></span> |<span data-ttu-id="6d952-388">Set this attribute to 1 to indicate this track contains commentary.</span><span class="sxs-lookup"><span data-stu-id="6d952-388">Set this attribute to 1 to indicate this track contains commentary.</span></span> |
| <span data-ttu-id="6d952-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="6d952-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="6d952-390">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-390">Required</span></span> |<span data-ttu-id="6d952-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-391">**xs:int**</span></span> |<span data-ttu-id="6d952-392">Set this attribute to 1 to indicate this track contains lyrics.</span><span class="sxs-lookup"><span data-stu-id="6d952-392">Set this attribute to 1 to indicate this track contains lyrics.</span></span> |
| <span data-ttu-id="6d952-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="6d952-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="6d952-394">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-394">Required</span></span> |<span data-ttu-id="6d952-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-395">**xs:int**</span></span> |<span data-ttu-id="6d952-396">Set this attribute to 1 to indicate this represents the karaoke track (background music, no vocals).</span><span class="sxs-lookup"><span data-stu-id="6d952-396">Set this attribute to 1 to indicate this represents the karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="6d952-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="6d952-397">**Forced**</span></span><br /><br /> <span data-ttu-id="6d952-398">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-398">Required</span></span> |<span data-ttu-id="6d952-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-399">**xs:int**</span></span> |<span data-ttu-id="6d952-400">Set this attribute to 1 to indicate this is the forced presentation.</span><span class="sxs-lookup"><span data-stu-id="6d952-400">Set this attribute to 1 to indicate this is the forced presentation.</span></span> |
| <span data-ttu-id="6d952-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="6d952-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="6d952-402">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-402">Required</span></span> |<span data-ttu-id="6d952-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-403">**xs:int**</span></span> |<span data-ttu-id="6d952-404">Set this attribute to 1 to indicate this track is for the hearing impaired.</span><span class="sxs-lookup"><span data-stu-id="6d952-404">Set this attribute to 1 to indicate this track is for the hearing impaired.</span></span> |
| <span data-ttu-id="6d952-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="6d952-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="6d952-406">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-406">Required</span></span> |<span data-ttu-id="6d952-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-407">**xs:int**</span></span> |<span data-ttu-id="6d952-408">Set this attribute to 1 to indicate this track is for the visually impaired.</span><span class="sxs-lookup"><span data-stu-id="6d952-408">Set this attribute to 1 to indicate this track is for the visually impaired.</span></span> |
| <span data-ttu-id="6d952-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="6d952-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="6d952-410">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-410">Required</span></span> |<span data-ttu-id="6d952-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-411">**xs:int**</span></span> |<span data-ttu-id="6d952-412">Set this attribute to 1 to indicate this track has clean effects.</span><span class="sxs-lookup"><span data-stu-id="6d952-412">Set this attribute to 1 to indicate this track has clean effects.</span></span> |
| <span data-ttu-id="6d952-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="6d952-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="6d952-414">Required</span><span class="sxs-lookup"><span data-stu-id="6d952-414">Required</span></span> |<span data-ttu-id="6d952-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d952-415">**xs:int**</span></span> |<span data-ttu-id="6d952-416">Set this attribute to 1 to indicate this track has pictures.</span><span class="sxs-lookup"><span data-stu-id="6d952-416">Set this attribute to 1 to indicate this track has pictures.</span></span> |

## <a name="Programs"></a> <span data-ttu-id="6d952-417">Programs element</span><span class="sxs-lookup"><span data-stu-id="6d952-417">Programs element</span></span>
<span data-ttu-id="6d952-418">Wrapper element holding multiple **Program** elements.</span><span class="sxs-lookup"><span data-stu-id="6d952-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="6d952-419">Child elements</span><span class="sxs-lookup"><span data-stu-id="6d952-419">Child elements</span></span>
| <span data-ttu-id="6d952-420">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-420">Name</span></span> | <span data-ttu-id="6d952-421">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-421">Type</span></span> | <span data-ttu-id="6d952-422">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="6d952-423">**Program**</span></span><br /><br /> <span data-ttu-id="6d952-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d952-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d952-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="6d952-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="6d952-426">For asset files that are in MPEG-TS format, contains information about programs in the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-426">For asset files that are in MPEG-TS format, contains information about programs in the asset file.</span></span> |

## <a name="VideoTracks"></a> <span data-ttu-id="6d952-427">VideoTracks element</span><span class="sxs-lookup"><span data-stu-id="6d952-427">VideoTracks element</span></span>
 <span data-ttu-id="6d952-428">Wrapper element holding multiple **VideoTrack** elements.</span><span class="sxs-lookup"><span data-stu-id="6d952-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="6d952-429">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-429">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="6d952-430">Child elements</span><span class="sxs-lookup"><span data-stu-id="6d952-430">Child elements</span></span>
| <span data-ttu-id="6d952-431">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-431">Name</span></span> | <span data-ttu-id="6d952-432">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-432">Type</span></span> | <span data-ttu-id="6d952-433">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="6d952-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="6d952-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d952-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d952-436">VideoTrackType (inherits from TrackType)</span><span class="sxs-lookup"><span data-stu-id="6d952-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="6d952-437">Contains information about video tracks in the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-437">Contains information about video tracks in the asset file.</span></span> |

## <a name="AudioTracks"></a> <span data-ttu-id="6d952-438">AudioTracks element</span><span class="sxs-lookup"><span data-stu-id="6d952-438">AudioTracks element</span></span>
 <span data-ttu-id="6d952-439">Wrapper element holding multiple **AudioTrack** elements.</span><span class="sxs-lookup"><span data-stu-id="6d952-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="6d952-440">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="6d952-440">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="6d952-441">elements</span><span class="sxs-lookup"><span data-stu-id="6d952-441">elements</span></span>
| <span data-ttu-id="6d952-442">Name</span><span class="sxs-lookup"><span data-stu-id="6d952-442">Name</span></span> | <span data-ttu-id="6d952-443">Type</span><span class="sxs-lookup"><span data-stu-id="6d952-443">Type</span></span> | <span data-ttu-id="6d952-444">Description</span><span class="sxs-lookup"><span data-stu-id="6d952-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d952-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="6d952-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="6d952-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d952-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d952-447">AudioTrackType (inherits from TrackType)</span><span class="sxs-lookup"><span data-stu-id="6d952-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="6d952-448">Contains information about audio tracks in the asset file.</span><span class="sxs-lookup"><span data-stu-id="6d952-448">Contains information about audio tracks in the asset file.</span></span> |

## <a name="code"></a> <span data-ttu-id="6d952-449">Schema Code</span><span class="sxs-lookup"><span data-stu-id="6d952-449">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
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
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
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
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
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
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
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
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
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
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

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
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is the collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
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
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of the asset file in kbps</xs:documentation>  
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
    </xs:schema>  


## <a name="xml"></a> <span data-ttu-id="6d952-450">XML example</span><span class="sxs-lookup"><span data-stu-id="6d952-450">XML example</span></span>
<span data-ttu-id="6d952-451">The following is an example of the Input metadata file.</span><span class="sxs-lookup"><span data-stu-id="6d952-451">The following is an example of the Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="6d952-452">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d952-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6d952-453">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="6d952-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

