---
title: Analyze your media using the Azure portal | Microsoft Docs
description: This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: juliako
ms.openlocfilehash: bbb538a7adabc2b9cdfa6bf0188ab0aa3ae30b63
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555549"
---
# <a name="analyze-your-media-using-the-azure-portal"></a><span data-ttu-id="8f6a4-103">Analyze your media using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8f6a4-103">Analyze your media using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="8f6a4-104">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="8f6a4-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f6a4-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="8f6a4-106">Overview</span><span class="sxs-lookup"><span data-stu-id="8f6a4-106">Overview</span></span>
<span data-ttu-id="8f6a4-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="8f6a4-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="8f6a4-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span></span> <span data-ttu-id="8f6a4-110">Media Analytics MPs produce MP4 files or JSON files.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="8f6a4-111">If a media processor produced an MP4 file, you can progressively download the file.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-111">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="8f6a4-112">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-112">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-to-analyze"></a><span data-ttu-id="8f6a4-113">Choose an asset that you want to analyze</span><span class="sxs-lookup"><span data-stu-id="8f6a4-113">Choose an asset that you want to analyze</span></span>
1. <span data-ttu-id="8f6a4-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="8f6a4-115">In the **Settings** window, select **Assets**.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-115">In the **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="8f6a4-116">.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-116">.</span></span>
    <span data-ttu-id="8f6a4-117">![Analyze videos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="8f6a4-117">![Analyze videos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="8f6a4-118">Select the asset that you would like to analyze and press the **Analyze** button.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-118">Select the asset that you would like to analyze and press the **Analyze** button.</span></span>
   
    ![Analyze videos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="8f6a4-120">In the **Process media asset with  Media Analytics** window, select the processor.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-120">In the **Process media asset with  Media Analytics** window, select the processor.</span></span> 
   
    <span data-ttu-id="8f6a4-121">The rest of the article explains why and how to use each processor.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-121">The rest of the article explains why and how to use each processor.</span></span> 
5. <span data-ttu-id="8f6a4-122">Press **Create** to the start a job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-122">Press **Create** to the start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="8f6a4-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="8f6a4-123">Azure Media Indexer</span></span>
<span data-ttu-id="8f6a4-124">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-124">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="8f6a4-125">This sections gives some details about options that you can specify for this MP.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analyze videos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="8f6a4-127">Language</span><span class="sxs-lookup"><span data-stu-id="8f6a4-127">Language</span></span>
<span data-ttu-id="8f6a4-128">The natural language to be recognized in the multimedia file.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-128">The natural language to be recognized in the multimedia file.</span></span> <span data-ttu-id="8f6a4-129">For example, English or Spanish.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="8f6a4-130">Captions</span><span class="sxs-lookup"><span data-stu-id="8f6a4-130">Captions</span></span>
<span data-ttu-id="8f6a4-131">You can choose a caption format that will be generated from your content.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="8f6a4-132">An indexing job can generate closed caption files in the following formats:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-132">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="8f6a4-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="8f6a4-133">**SAMI**</span></span>
* <span data-ttu-id="8f6a4-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="8f6a4-134">**TTML**</span></span>
* <span data-ttu-id="8f6a4-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="8f6a4-135">**WebVTT**</span></span>

<span data-ttu-id="8f6a4-136">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-136">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="8f6a4-137">AIB file</span><span class="sxs-lookup"><span data-stu-id="8f6a4-137">AIB file</span></span>
<span data-ttu-id="8f6a4-138">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-138">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span></span> <span data-ttu-id="8f6a4-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="8f6a4-140">Keywords</span><span class="sxs-lookup"><span data-stu-id="8f6a4-140">Keywords</span></span>
<span data-ttu-id="8f6a4-141">Select this option if you would like to generate a keywords XML file.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-141">Select this option if you would like to generate a keywords XML file.</span></span> <span data-ttu-id="8f6a4-142">This file contains keywords extracted from the speech content, with frequency and offset information.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-142">This file contains keywords extracted from the speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="8f6a4-143">Job name</span><span class="sxs-lookup"><span data-stu-id="8f6a4-143">Job name</span></span>
<span data-ttu-id="8f6a4-144">A friendly name that lets you identify the job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-144">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="8f6a4-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="8f6a4-146">Output file</span><span class="sxs-lookup"><span data-stu-id="8f6a4-146">Output file</span></span>
<span data-ttu-id="8f6a4-147">A friendly name that lets you identify the output content.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-147">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="8f6a4-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="8f6a4-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="8f6a4-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="8f6a4-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="8f6a4-151">This sections gives some details about options that you can specify for this MP.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analyze videos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="8f6a4-153">Speed</span><span class="sxs-lookup"><span data-stu-id="8f6a4-153">Speed</span></span>
<span data-ttu-id="8f6a4-154">Specify the speed with which to speed up the input video.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-154">Specify the speed with which to speed up the input video.</span></span> <span data-ttu-id="8f6a4-155">The output is a stabilized and time-lapsed rendition of the input video.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-155">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="8f6a4-156">Job name</span><span class="sxs-lookup"><span data-stu-id="8f6a4-156">Job name</span></span>
<span data-ttu-id="8f6a4-157">A friendly name that lets you identify the job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-157">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="8f6a4-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="8f6a4-159">Output file</span><span class="sxs-lookup"><span data-stu-id="8f6a4-159">Output file</span></span>
<span data-ttu-id="8f6a4-160">A friendly name that lets you identify the output content.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-160">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="8f6a4-161">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="8f6a4-161">Azure Media Face Detector</span></span>
<span data-ttu-id="8f6a4-162">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-162">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="8f6a4-163">This service contains two features:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-163">This service contains two features:</span></span> 

* <span data-ttu-id="8f6a4-164">**Face detection**</span><span class="sxs-lookup"><span data-stu-id="8f6a4-164">**Face detection**</span></span>
  
    <span data-ttu-id="8f6a4-165">Face detection finds and tracks human faces within a video.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="8f6a4-166">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-166">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="8f6a4-167">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-167">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8f6a4-168">This services does not perform facial recognition.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="8f6a4-169">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-169">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="8f6a4-170">**Emotion detection**</span><span class="sxs-lookup"><span data-stu-id="8f6a4-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="8f6a4-171">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-171">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analyze videos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="8f6a4-173">Detection mode</span><span class="sxs-lookup"><span data-stu-id="8f6a4-173">Detection mode</span></span>
<span data-ttu-id="8f6a4-174">One of the following modes can be used by the processor:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-174">One of the following modes can be used by the processor:</span></span>

* <span data-ttu-id="8f6a4-175">face detection</span><span class="sxs-lookup"><span data-stu-id="8f6a4-175">face detection</span></span>
* <span data-ttu-id="8f6a4-176">per face emotion detection</span><span class="sxs-lookup"><span data-stu-id="8f6a4-176">per face emotion detection</span></span>
* <span data-ttu-id="8f6a4-177">aggregate emotion detection</span><span class="sxs-lookup"><span data-stu-id="8f6a4-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="8f6a4-178">Job name</span><span class="sxs-lookup"><span data-stu-id="8f6a4-178">Job name</span></span>
<span data-ttu-id="8f6a4-179">A friendly name that lets you identify the job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-179">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="8f6a4-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="8f6a4-181">Output file</span><span class="sxs-lookup"><span data-stu-id="8f6a4-181">Output file</span></span>
<span data-ttu-id="8f6a4-182">A friendly name that lets you identify the output content.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-182">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="8f6a4-183">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="8f6a4-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="8f6a4-184">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-184">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="8f6a4-185">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-185">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="8f6a4-186">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-186">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="8f6a4-187">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-187">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="8f6a4-188">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-188">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

![Analyze videos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="8f6a4-190">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="8f6a4-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="8f6a4-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="8f6a4-192">This is useful when you want to provide a quick overview of what to expect in a long video.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-192">This is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="8f6a4-193">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="8f6a4-193">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span></span>

![Analyze videos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="8f6a4-195">Job name</span><span class="sxs-lookup"><span data-stu-id="8f6a4-195">Job name</span></span>
<span data-ttu-id="8f6a4-196">A friendly name that lets you identify the job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-196">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="8f6a4-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="8f6a4-198">Output file</span><span class="sxs-lookup"><span data-stu-id="8f6a4-198">Output file</span></span>
<span data-ttu-id="8f6a4-199">A friendly name that lets you identify the output content.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-199">A friendly name that lets you identify the output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8f6a4-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f6a4-200">Next steps</span></span>
<span data-ttu-id="8f6a4-201">View Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8f6a4-202">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="8f6a4-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]








