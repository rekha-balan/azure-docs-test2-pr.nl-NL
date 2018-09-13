---
title: Media Analytics on the Media Services platform | Microsoft Docs
description: Overview of public preview of Media Analytics, a collection of speech and computer vision services at enterprise scale, compliance, security, and global reach
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 0ac8b9fad35267ceaec5b5acec4722b6005f68a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966810"
---
# <a name="media-analytics-on-the-media-services-platform"></a><span data-ttu-id="c24d1-103">Media Analytics on the Media Services platform</span><span class="sxs-lookup"><span data-stu-id="c24d1-103">Media Analytics on the Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="c24d1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c24d1-104">Overview</span></span>
<span data-ttu-id="c24d1-105">More organizations are using video as the preferred medium to train their employees, engage their customers, and document business functions.</span><span class="sxs-lookup"><span data-stu-id="c24d1-105">More organizations are using video as the preferred medium to train their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="c24d1-106">Cloud computing provides a way to store, stream, and access these large media files.</span><span class="sxs-lookup"><span data-stu-id="c24d1-106">Cloud computing provides a way to store, stream, and access these large media files.</span></span> <span data-ttu-id="c24d1-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from the content.</span><span class="sxs-lookup"><span data-stu-id="c24d1-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from the content.</span></span> 

<span data-ttu-id="c24d1-108">To address this growing need, Azure Media Services offers Azure Media Analytics.</span><span class="sxs-lookup"><span data-stu-id="c24d1-108">To address this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="c24d1-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span><span class="sxs-lookup"><span data-stu-id="c24d1-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="c24d1-110">Built by using the core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span><span class="sxs-lookup"><span data-stu-id="c24d1-110">Built by using the core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="c24d1-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span><span class="sxs-lookup"><span data-stu-id="c24d1-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="c24d1-112">It provides enterprise environments with the full scale, compliance, security, and global reach required by large organizations.</span><span class="sxs-lookup"><span data-stu-id="c24d1-112">It provides enterprise environments with the full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="c24d1-113">The following diagram shows Media Analytics and other major parts of the Media Services platform.</span><span class="sxs-lookup"><span data-stu-id="c24d1-113">The following diagram shows Media Analytics and other major parts of the Media Services platform.</span></span> 

![VoD workflow](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="c24d1-115">Media Analytics media processors produce MP4 files or JSON files.</span><span class="sxs-lookup"><span data-stu-id="c24d1-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="c24d1-116">If a media processor produces an MP4 file, you can progressively download the file.</span><span class="sxs-lookup"><span data-stu-id="c24d1-116">If a media processor produces an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="c24d1-117">If a media processor produces a JSON file, you can download the file from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="c24d1-117">If a media processor produces a JSON file, you can download the file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="c24d1-118">Media Analytics services</span><span class="sxs-lookup"><span data-stu-id="c24d1-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="c24d1-119">Indexer</span><span class="sxs-lookup"><span data-stu-id="c24d1-119">Indexer</span></span>
<span data-ttu-id="c24d1-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span><span class="sxs-lookup"><span data-stu-id="c24d1-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="c24d1-121">Compared to the previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span><span class="sxs-lookup"><span data-stu-id="c24d1-121">Compared to the previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="c24d1-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span><span class="sxs-lookup"><span data-stu-id="c24d1-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="c24d1-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="c24d1-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="c24d1-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c24d1-124">Hyperlapse</span></span>
<span data-ttu-id="c24d1-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability to create quick, consumable videos from your long-form content.</span><span class="sxs-lookup"><span data-stu-id="c24d1-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability to create quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="c24d1-126">Besides creating time-lapse video, you can use Hyperlapse to create stable videos from shaky videos captured via cell phones and camcorders.</span><span class="sxs-lookup"><span data-stu-id="c24d1-126">Besides creating time-lapse video, you can use Hyperlapse to create stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="c24d1-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="c24d1-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="c24d1-128">Motion Detector</span><span class="sxs-lookup"><span data-stu-id="c24d1-128">Motion Detector</span></span>
<span data-ttu-id="c24d1-129">You can use Motion Detector to detect motion in a video with stationary backgrounds.</span><span class="sxs-lookup"><span data-stu-id="c24d1-129">You can use Motion Detector to detect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="c24d1-130">This makes it possible to check for false positives on motion events detected by surveillance cameras.</span><span class="sxs-lookup"><span data-stu-id="c24d1-130">This makes it possible to check for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="c24d1-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="c24d1-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="c24d1-132">Face Detector</span><span class="sxs-lookup"><span data-stu-id="c24d1-132">Face Detector</span></span>
<span data-ttu-id="c24d1-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span><span class="sxs-lookup"><span data-stu-id="c24d1-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="c24d1-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span><span class="sxs-lookup"><span data-stu-id="c24d1-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="c24d1-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="c24d1-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="c24d1-136">Video summarization</span><span class="sxs-lookup"><span data-stu-id="c24d1-136">Video summarization</span></span>
<span data-ttu-id="c24d1-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span><span class="sxs-lookup"><span data-stu-id="c24d1-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="c24d1-138">This ability is useful when you want to provide a quick overview of what to expect in a long video.</span><span class="sxs-lookup"><span data-stu-id="c24d1-138">This ability is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="c24d1-139">For detailed information and examples, see [Use Azure Media Video Thumbnails to create video summarization](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="c24d1-139">For detailed information and examples, see [Use Azure Media Video Thumbnails to create video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="c24d1-140">Optical character recognition</span><span class="sxs-lookup"><span data-stu-id="c24d1-140">Optical character recognition</span></span>
<span data-ttu-id="c24d1-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span><span class="sxs-lookup"><span data-stu-id="c24d1-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="c24d1-142">You can then automate the extraction of meaningful metadata from the video signal of your media.</span><span class="sxs-lookup"><span data-stu-id="c24d1-142">You can then automate the extraction of meaningful metadata from the video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="c24d1-143">Scalable face redaction</span><span class="sxs-lookup"><span data-stu-id="c24d1-143">Scalable face redaction</span></span>
<span data-ttu-id="c24d1-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c24d1-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="c24d1-145">By using face redaction, you can modify your video to blur faces of selected individuals.</span><span class="sxs-lookup"><span data-stu-id="c24d1-145">By using face redaction, you can modify your video to blur faces of selected individuals.</span></span> <span data-ttu-id="c24d1-146">You might want to use the face redaction service in news media or when public safety is involved.</span><span class="sxs-lookup"><span data-stu-id="c24d1-146">You might want to use the face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="c24d1-147">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service, face redaction takes just a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="c24d1-147">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="c24d1-148">For more information, see the [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span><span class="sxs-lookup"><span data-stu-id="c24d1-148">For more information, see the [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>
### <a name="content-moderation"></a><span data-ttu-id="c24d1-149">Content Moderation</span><span class="sxs-lookup"><span data-stu-id="c24d1-149">Content Moderation</span></span>
<span data-ttu-id="c24d1-150">Azure Content Moderator enables you to use machine-assisted moderation for your videos.</span><span class="sxs-lookup"><span data-stu-id="c24d1-150">Azure Content Moderator enables you to use machine-assisted moderation for your videos.</span></span> <span data-ttu-id="c24d1-151">For example, you might want to detect possible adult and racy content in videos and review the flagged content by your human moderation teams.</span><span class="sxs-lookup"><span data-stu-id="c24d1-151">For example, you might want to detect possible adult and racy content in videos and review the flagged content by your human moderation teams.</span></span> <span data-ttu-id="c24d1-152">Manually moderating videos for undesirable content is a time consuming and expensive task.</span><span class="sxs-lookup"><span data-stu-id="c24d1-152">Manually moderating videos for undesirable content is a time consuming and expensive task.</span></span> <span data-ttu-id="c24d1-153">With this service and associated review tools, you combine machine-assisted moderation with human-in-the-loop capabilities for best results  efficiently and cost-effectively.</span><span class="sxs-lookup"><span data-stu-id="c24d1-153">With this service and associated review tools, you combine machine-assisted moderation with human-in-the-loop capabilities for best results  efficiently and cost-effectively.</span></span> <span data-ttu-id="c24d1-154">To learn more, see the [Process your videos with Azure Content Moderator](media-services-content-moderation.md) article.</span><span class="sxs-lookup"><span data-stu-id="c24d1-154">To learn more, see the [Process your videos with Azure Content Moderator](media-services-content-moderation.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="c24d1-155">Common scenarios</span><span class="sxs-lookup"><span data-stu-id="c24d1-155">Common scenarios</span></span>
<span data-ttu-id="c24d1-156">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span><span class="sxs-lookup"><span data-stu-id="c24d1-156">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="c24d1-157">Here are several scenarios:</span><span class="sxs-lookup"><span data-stu-id="c24d1-157">Here are several scenarios:</span></span>

* <span data-ttu-id="c24d1-158">**Call centers**.</span><span class="sxs-lookup"><span data-stu-id="c24d1-158">**Call centers**.</span></span> <span data-ttu-id="c24d1-159">Even with the advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span><span class="sxs-lookup"><span data-stu-id="c24d1-159">Even with the advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="c24d1-160">Encoded in this audio data is a large amount of customer information that can be analyzed to achieve higher customer satisfaction.</span><span class="sxs-lookup"><span data-stu-id="c24d1-160">Encoded in this audio data is a large amount of customer information that can be analyzed to achieve higher customer satisfaction.</span></span> <span data-ttu-id="c24d1-161">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span><span class="sxs-lookup"><span data-stu-id="c24d1-161">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="c24d1-162">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span><span class="sxs-lookup"><span data-stu-id="c24d1-162">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="c24d1-163">**User-generated content moderation**.</span><span class="sxs-lookup"><span data-stu-id="c24d1-163">**User-generated content moderation**.</span></span> <span data-ttu-id="c24d1-164">From news media outlets to police departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span><span class="sxs-lookup"><span data-stu-id="c24d1-164">From news media outlets to police departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="c24d1-165">The volume of content can spike due to unexpected events.</span><span class="sxs-lookup"><span data-stu-id="c24d1-165">The volume of content can spike due to unexpected events.</span></span> <span data-ttu-id="c24d1-166">In these scenarios, it is difficult to conduct effective manual reviews of content for appropriateness.</span><span class="sxs-lookup"><span data-stu-id="c24d1-166">In these scenarios, it is difficult to conduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="c24d1-167">Customers can rely on the content-moderation service to focus on content that is appropriate.</span><span class="sxs-lookup"><span data-stu-id="c24d1-167">Customers can rely on the content-moderation service to focus on content that is appropriate.</span></span>
* <span data-ttu-id="c24d1-168">**Surveillance**.</span><span class="sxs-lookup"><span data-stu-id="c24d1-168">**Surveillance**.</span></span> <span data-ttu-id="c24d1-169">With the growth in use of IP cameras comes a growing inventory of surveillance video.</span><span class="sxs-lookup"><span data-stu-id="c24d1-169">With the growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="c24d1-170">Manually reviewing surveillance video is time intensive and prone to human error.</span><span class="sxs-lookup"><span data-stu-id="c24d1-170">Manually reviewing surveillance video is time intensive and prone to human error.</span></span> <span data-ttu-id="c24d1-171">Media Analytics provides services such as motion detection, face detection, and Hyperlapse to make the process of reviewing, managing, and creating derivatives easier.</span><span class="sxs-lookup"><span data-stu-id="c24d1-171">Media Analytics provides services such as motion detection, face detection, and Hyperlapse to make the process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="c24d1-172">Media Analytics media processors</span><span class="sxs-lookup"><span data-stu-id="c24d1-172">Media Analytics media processors</span></span>
<span data-ttu-id="c24d1-173">This section lists the Media Analytics media processors and shows how to use .NET or REST to get a media processor (MP) object.</span><span class="sxs-lookup"><span data-stu-id="c24d1-173">This section lists the Media Analytics media processors and shows how to use .NET or REST to get a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="c24d1-174">MP names</span><span class="sxs-lookup"><span data-stu-id="c24d1-174">MP names</span></span>
* <span data-ttu-id="c24d1-175">Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="c24d1-175">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="c24d1-176">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="c24d1-176">Azure Media Indexer</span></span>
* <span data-ttu-id="c24d1-177">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c24d1-177">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="c24d1-178">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="c24d1-178">Azure Media Face Detector</span></span>
* <span data-ttu-id="c24d1-179">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="c24d1-179">Azure Media Motion Detector</span></span>
* <span data-ttu-id="c24d1-180">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="c24d1-180">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="c24d1-181">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="c24d1-181">Azure Media OCR</span></span>
* <span data-ttu-id="c24d1-182">Azure Media Content Moderator</span><span class="sxs-lookup"><span data-stu-id="c24d1-182">Azure Media Content Moderator</span></span>

### <a name="net"></a><span data-ttu-id="c24d1-183">.NET</span><span class="sxs-lookup"><span data-stu-id="c24d1-183">.NET</span></span>
<span data-ttu-id="c24d1-184">The following function takes one of the specified MP names and returns an MP object.</span><span class="sxs-lookup"><span data-stu-id="c24d1-184">The following function takes one of the specified MP names and returns an MP object.</span></span>

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a><span data-ttu-id="c24d1-185">REST</span><span class="sxs-lookup"><span data-stu-id="c24d1-185">REST</span></span>
<span data-ttu-id="c24d1-186">Request:</span><span class="sxs-lookup"><span data-stu-id="c24d1-186">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="c24d1-187">Response:</span><span class="sxs-lookup"><span data-stu-id="c24d1-187">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="c24d1-188">Demos</span><span class="sxs-lookup"><span data-stu-id="c24d1-188">Demos</span></span>
<span data-ttu-id="c24d1-189">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="c24d1-189">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="c24d1-190">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c24d1-190">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="c24d1-191">Related articles</span><span class="sxs-lookup"><span data-stu-id="c24d1-191">Related articles</span></span>
<span data-ttu-id="c24d1-192">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="c24d1-192">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png

## <a name="next-steps"></a><span data-ttu-id="c24d1-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="c24d1-193">Next steps</span></span>
<span data-ttu-id="c24d1-194">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="c24d1-194">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]
