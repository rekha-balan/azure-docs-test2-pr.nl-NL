---
title: Analyze your media using the Azure portal | Microsoft Docs
description: This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d8c3bb07c88dc96b7ca779ca0f4dfe09052ab290
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865205"
---
# <a name="analyze-your-media-using-the-azure-portal"></a><span data-ttu-id="cc8e7-103">Analyze your media using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cc8e7-103">Analyze your media using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="cc8e7-104">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="cc8e7-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc8e7-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="cc8e7-106">Overview</span><span class="sxs-lookup"><span data-stu-id="cc8e7-106">Overview</span></span>
<span data-ttu-id="cc8e7-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="cc8e7-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="cc8e7-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span></span> <span data-ttu-id="cc8e7-110">Media Analytics MPs produce MP4 files or JSON files.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="cc8e7-111">If a media processor produced an MP4 file, you progressively download the file.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-111">If a media processor produced an MP4 file, you progressively download the file.</span></span> <span data-ttu-id="cc8e7-112">If a media processor produced a JSON file, you download the file from the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-112">If a media processor produced a JSON file, you download the file from the Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-to-analyze"></a><span data-ttu-id="cc8e7-113">Choose an asset that you want to analyze</span><span class="sxs-lookup"><span data-stu-id="cc8e7-113">Choose an asset that you want to analyze</span></span>
1. <span data-ttu-id="cc8e7-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="cc8e7-115">In the **Settings** window, select **Assets**.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-115">In the **Settings** window, select **Assets**.</span></span>  
   
    ![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. <span data-ttu-id="cc8e7-117">Select the asset that you would like to analyze and press the **Analyze** button.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-117">Select the asset that you would like to analyze and press the **Analyze** button.</span></span>
   
    ![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="cc8e7-119">In the **Process media asset with  Media Analytics** window, select the processor.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-119">In the **Process media asset with  Media Analytics** window, select the processor.</span></span> 
   
    <span data-ttu-id="cc8e7-120">The rest of the article explains why and how to use each processor.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-120">The rest of the article explains why and how to use each processor.</span></span> 
5. <span data-ttu-id="cc8e7-121">Press **Create** to the start a job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-121">Press **Create** to the start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="cc8e7-122">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="cc8e7-122">Azure Media Indexer</span></span>
<span data-ttu-id="cc8e7-123">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-123">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="cc8e7-124">This section gives some details about options that you specify for this MP.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-124">This section gives some details about options that you specify for this MP.</span></span>

![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="cc8e7-126">Language</span><span class="sxs-lookup"><span data-stu-id="cc8e7-126">Language</span></span>
<span data-ttu-id="cc8e7-127">The natural language to be recognized in the multimedia file.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-127">The natural language to be recognized in the multimedia file.</span></span> <span data-ttu-id="cc8e7-128">For example, English or Spanish.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-128">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="cc8e7-129">Captions</span><span class="sxs-lookup"><span data-stu-id="cc8e7-129">Captions</span></span>
<span data-ttu-id="cc8e7-130">You can choose a caption format that will be generated from your content.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-130">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="cc8e7-131">An indexing job can generate closed caption files in the following formats:</span><span class="sxs-lookup"><span data-stu-id="cc8e7-131">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="cc8e7-132">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="cc8e7-132">**SAMI**</span></span>
* <span data-ttu-id="cc8e7-133">**TTML**</span><span class="sxs-lookup"><span data-stu-id="cc8e7-133">**TTML**</span></span>
* <span data-ttu-id="cc8e7-134">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="cc8e7-134">**WebVTT**</span></span>

<span data-ttu-id="cc8e7-135">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-135">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="cc8e7-136">AIB file</span><span class="sxs-lookup"><span data-stu-id="cc8e7-136">AIB file</span></span>
<span data-ttu-id="cc8e7-137">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-137">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span></span> <span data-ttu-id="cc8e7-138">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-138">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="cc8e7-139">Keywords</span><span class="sxs-lookup"><span data-stu-id="cc8e7-139">Keywords</span></span>
<span data-ttu-id="cc8e7-140">Select this option if you would like to generate a keywords XML file.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-140">Select this option if you would like to generate a keywords XML file.</span></span> <span data-ttu-id="cc8e7-141">This file contains keywords extracted from the speech content, with frequency and offset information.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-141">This file contains keywords extracted from the speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="cc8e7-142">Job name</span><span class="sxs-lookup"><span data-stu-id="cc8e7-142">Job name</span></span>
<span data-ttu-id="cc8e7-143">A friendly name that lets you identify the job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-143">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="cc8e7-144">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-144">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="cc8e7-145">Output file</span><span class="sxs-lookup"><span data-stu-id="cc8e7-145">Output file</span></span>
<span data-ttu-id="cc8e7-146">A friendly name that lets you identify the output content.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-146">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="cc8e7-147">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="cc8e7-147">Azure Media Hyperlapse</span></span>
<span data-ttu-id="cc8e7-148">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-148">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="cc8e7-149">For more information, see [this](media-services-hyperlapse-content.md) topic.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-149">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="cc8e7-150">This section gives some details about options that you specify for this MP.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-150">This section gives some details about options that you specify for this MP.</span></span>

![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="cc8e7-152">Speed</span><span class="sxs-lookup"><span data-stu-id="cc8e7-152">Speed</span></span>
<span data-ttu-id="cc8e7-153">Specify the speed with which to speed up the input video.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-153">Specify the speed with which to speed up the input video.</span></span> <span data-ttu-id="cc8e7-154">The output is a stabilized and time-lapsed rendition of the input video.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-154">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="cc8e7-155">Job name</span><span class="sxs-lookup"><span data-stu-id="cc8e7-155">Job name</span></span>
<span data-ttu-id="cc8e7-156">A friendly name that lets you identify the job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-156">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="cc8e7-157">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-157">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="cc8e7-158">Output file</span><span class="sxs-lookup"><span data-stu-id="cc8e7-158">Output file</span></span>
<span data-ttu-id="cc8e7-159">A friendly name that lets you identify the output content.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-159">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="cc8e7-160">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="cc8e7-160">Azure Media Face Detector</span></span>
<span data-ttu-id="cc8e7-161">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-161">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="cc8e7-162">This service contains two features:</span><span class="sxs-lookup"><span data-stu-id="cc8e7-162">This service contains two features:</span></span> 

* <span data-ttu-id="cc8e7-163">**Face detection**</span><span class="sxs-lookup"><span data-stu-id="cc8e7-163">**Face detection**</span></span>
  
    <span data-ttu-id="cc8e7-164">Face detection finds and tracks human faces within a video.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-164">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="cc8e7-165">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-165">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="cc8e7-166">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-166">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cc8e7-167">This services does not perform facial recognition.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-167">This services does not perform facial recognition.</span></span> <span data-ttu-id="cc8e7-168">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-168">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="cc8e7-169">**Emotion detection**</span><span class="sxs-lookup"><span data-stu-id="cc8e7-169">**Emotion detection**</span></span>
  
    <span data-ttu-id="cc8e7-170">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-170">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="cc8e7-172">Detection mode</span><span class="sxs-lookup"><span data-stu-id="cc8e7-172">Detection mode</span></span>
<span data-ttu-id="cc8e7-173">One of the following modes can be used by the processor:</span><span class="sxs-lookup"><span data-stu-id="cc8e7-173">One of the following modes can be used by the processor:</span></span>

* <span data-ttu-id="cc8e7-174">face detection</span><span class="sxs-lookup"><span data-stu-id="cc8e7-174">face detection</span></span>
* <span data-ttu-id="cc8e7-175">per face emotion detection</span><span class="sxs-lookup"><span data-stu-id="cc8e7-175">per face emotion detection</span></span>
* <span data-ttu-id="cc8e7-176">aggregate emotion detection</span><span class="sxs-lookup"><span data-stu-id="cc8e7-176">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="cc8e7-177">Job name</span><span class="sxs-lookup"><span data-stu-id="cc8e7-177">Job name</span></span>
<span data-ttu-id="cc8e7-178">A friendly name that lets you identify the job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-178">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="cc8e7-179">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-179">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="cc8e7-180">Output file</span><span class="sxs-lookup"><span data-stu-id="cc8e7-180">Output file</span></span>
<span data-ttu-id="cc8e7-181">A friendly name that lets you identify the output content.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-181">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="cc8e7-182">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="cc8e7-182">Azure Media Motion Detector</span></span>
<span data-ttu-id="cc8e7-183">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-183">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="cc8e7-184">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-184">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="cc8e7-185">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-185">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="cc8e7-186">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-186">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="cc8e7-187">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-187">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="cc8e7-189">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="cc8e7-189">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="cc8e7-190">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-190">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="cc8e7-191">This is useful when you want to provide a quick overview of what to expect in a long video.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-191">This is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="cc8e7-192">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="cc8e7-192">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span></span>

![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="cc8e7-194">Job name</span><span class="sxs-lookup"><span data-stu-id="cc8e7-194">Job name</span></span>
<span data-ttu-id="cc8e7-195">A friendly name that lets you identify the job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-195">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="cc8e7-196">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-196">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="cc8e7-197">Output file</span><span class="sxs-lookup"><span data-stu-id="cc8e7-197">Output file</span></span>
<span data-ttu-id="cc8e7-198">A friendly name that lets you identify the output content.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-198">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-content-moderator"></a><span data-ttu-id="cc8e7-199">Azure Media Content Moderator</span><span class="sxs-lookup"><span data-stu-id="cc8e7-199">Azure Media Content Moderator</span></span>
<span data-ttu-id="cc8e7-200">This processor helps you detect potential adult and racy content in videos.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-200">This processor helps you detect potential adult and racy content in videos.</span></span> <span data-ttu-id="cc8e7-201">The processor automatically detects shots and keyframes in the video.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-201">The processor automatically detects shots and keyframes in the video.</span></span> <span data-ttu-id="cc8e7-202">It scores the keyframes for possible adult or racy content, and suggests reviews based on default thresholds.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-202">It scores the keyframes for possible adult or racy content, and suggests reviews based on default thresholds.</span></span> <span data-ttu-id="cc8e7-203">For detailed information and examples, see [Use Azure Media Content Moderator to moderate videos](media-services-content-moderation.md)</span><span class="sxs-lookup"><span data-stu-id="cc8e7-203">For detailed information and examples, see [Use Azure Media Content Moderator to moderate videos](media-services-content-moderation.md)</span></span>

![Moderate videos](./media/media-services-portal-analyze/media-services-portal-analyze-content-moderator.PNG)

### <a name="version"></a><span data-ttu-id="cc8e7-205">Version</span><span class="sxs-lookup"><span data-stu-id="cc8e7-205">Version</span></span> 
<span data-ttu-id="cc8e7-206">Use "2.0".</span><span class="sxs-lookup"><span data-stu-id="cc8e7-206">Use "2.0".</span></span>

### <a name="mode"></a><span data-ttu-id="cc8e7-207">Mode</span><span class="sxs-lookup"><span data-stu-id="cc8e7-207">Mode</span></span>
<span data-ttu-id="cc8e7-208">The 2.0 version ignore the `Mode` setting.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-208">The 2.0 version ignore the `Mode` setting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc8e7-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc8e7-209">Next steps</span></span>
<span data-ttu-id="cc8e7-210">View Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="cc8e7-210">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cc8e7-211">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="cc8e7-211">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
