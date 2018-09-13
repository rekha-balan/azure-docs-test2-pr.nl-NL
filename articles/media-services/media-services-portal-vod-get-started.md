---
title: Get started with delivering VoD using the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 988c441440739194a7a1f903b1d4ee8cdd29205b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564219"
---
# <a name="get-started-with-delivering-content-on-demand-using-the-azure-portal"></a><span data-ttu-id="c5bb0-103">Get started with delivering content on demand using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c5bb0-103">Get started with delivering content on demand using the Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="c5bb0-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5bb0-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c5bb0-105">Prerequisites</span></span>
<span data-ttu-id="c5bb0-106">The following are required to complete the tutorial:</span><span class="sxs-lookup"><span data-stu-id="c5bb0-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="c5bb0-107">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-107">An Azure account.</span></span> <span data-ttu-id="c5bb0-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5bb0-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="c5bb0-109">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-109">A Media Services account.</span></span> <span data-ttu-id="c5bb0-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="c5bb0-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="c5bb0-111">This tutorial includes the following tasks:</span><span class="sxs-lookup"><span data-stu-id="c5bb0-111">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="c5bb0-112">Start streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="c5bb0-113">Upload a video file.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-113">Upload a video file.</span></span>
3. <span data-ttu-id="c5bb0-114">Encode the source file into a set of adaptive bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-114">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="c5bb0-115">Publish the asset and get streaming and progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-115">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="c5bb0-116">Play your content.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="c5bb0-117">Start streaming endpoints</span><span class="sxs-lookup"><span data-stu-id="c5bb0-117">Start streaming endpoints</span></span> 

<span data-ttu-id="c5bb0-118">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-118">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="c5bb0-119">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-119">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="c5bb0-120">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-120">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="c5bb0-121">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-121">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="c5bb0-122">To start the streaming endpoint, do the following:</span><span class="sxs-lookup"><span data-stu-id="c5bb0-122">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="c5bb0-123">Log in at the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c5bb0-123">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c5bb0-124">In the Settings window, click Streaming endpoints.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-124">In the Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="c5bb0-125">Click the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-125">Click the default streaming endpoint.</span></span> 

    <span data-ttu-id="c5bb0-126">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-126">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="c5bb0-127">Click the Start icon.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-127">Click the Start icon.</span></span>
5. <span data-ttu-id="c5bb0-128">Click the Save button to save your changes.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-128">Click the Save button to save your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="c5bb0-129">Upload files</span><span class="sxs-lookup"><span data-stu-id="c5bb0-129">Upload files</span></span>
<span data-ttu-id="c5bb0-130">To stream videos using Azure Media Services, you need to upload the source videos, encode them into multiple bitrates, and publish the result.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-130">To stream videos using Azure Media Services, you need to upload the source videos, encode them into multiple bitrates, and publish the result.</span></span> <span data-ttu-id="c5bb0-131">The first step is covered in this section.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-131">The first step is covered in this section.</span></span> 

1. <span data-ttu-id="c5bb0-132">In the **Setting** window, click **Assets**.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-132">In the **Setting** window, click **Assets**.</span></span>
   
    ![Upload files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="c5bb0-134">Click the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-134">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="c5bb0-135">The **Upload a video asset** window appears.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-135">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c5bb0-136">There is no file size limitation.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="c5bb0-137">Browse to the desired video on your computer, select it, and hit OK.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-137">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="c5bb0-138">The upload starts and you can see the progress under the file name.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-138">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="c5bb0-139">Once the upload completes, you see the new asset listed in the **Assets** window.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-139">Once the upload completes, you see the new asset listed in the **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="c5bb0-140">Encode assets</span><span class="sxs-lookup"><span data-stu-id="c5bb0-140">Encode assets</span></span>
<span data-ttu-id="c5bb0-141">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-141">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="c5bb0-142">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-142">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="c5bb0-143">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-143">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="c5bb0-144">You should use the **Media Encoder Standard** encoder to encode your videos.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-144">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="c5bb0-145">Media Services also provides dynamic packaging, which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to repackage into these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-145">Media Services also provides dynamic packaging, which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to repackage into these streaming formats.</span></span> <span data-ttu-id="c5bb0-146">With dynamic packaging, you only need to store and pay for the files in single storage format and Media Services builds and serves the appropriate response based on requests from a client.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-146">With dynamic packaging, you only need to store and pay for the files in single storage format and Media Services builds and serves the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="c5bb0-147">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span><span class="sxs-lookup"><span data-stu-id="c5bb0-147">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

### <a name="to-use-the-portal-to-encode"></a><span data-ttu-id="c5bb0-148">To use the portal to encode</span><span class="sxs-lookup"><span data-stu-id="c5bb0-148">To use the portal to encode</span></span>
<span data-ttu-id="c5bb0-149">This section describes the steps you can take to encode your content with Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-149">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="c5bb0-150">In the **Settings** window, select **Assets**.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-150">In the **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="c5bb0-151">In the **Assets** window, select the asset that you would like to encode.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-151">In the **Assets** window, select the asset that you would like to encode.</span></span>
3. <span data-ttu-id="c5bb0-152">Press the **Encode** button.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-152">Press the **Encode** button.</span></span>
4. <span data-ttu-id="c5bb0-153">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-153">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="c5bb0-154">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-154">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="c5bb0-155">For more information about presets, see [this](media-services-mes-presets-overview.md) article – it is important to select the preset that is most appropriate for your input video.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-155">For more information about presets, see [this](media-services-mes-presets-overview.md) article – it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="c5bb0-156">If you have a low resolution (640x360) video, then you should not be using the default "H264 Multiple Bitrate 1080p" preset.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-156">If you have a low resolution (640x360) video, then you should not be using the default "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="c5bb0-157">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-157">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Encode assets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="c5bb0-159">Press **Create**.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-159">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="c5bb0-160">Monitor encoding job progress</span><span class="sxs-lookup"><span data-stu-id="c5bb0-160">Monitor encoding job progress</span></span>
<span data-ttu-id="c5bb0-161">To monitor the progress of the encoding job, click **Settings** (at the top of the page) and then select **Jobs**.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-161">To monitor the progress of the encoding job, click **Settings** (at the top of the page) and then select **Jobs**.</span></span>

![Jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="c5bb0-163">Publish content</span><span class="sxs-lookup"><span data-stu-id="c5bb0-163">Publish content</span></span>
<span data-ttu-id="c5bb0-164">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-164">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="c5bb0-165">Locators provide access to files contained in the asset.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-165">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="c5bb0-166">Media Services supports two types of locators:</span><span class="sxs-lookup"><span data-stu-id="c5bb0-166">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="c5bb0-167">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="c5bb0-167">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="c5bb0-168">To create a streaming locator your asset must contain an .ism file.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-168">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="c5bb0-169">Progressive (SAS) locators, used for delivery of video via progressive download.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-169">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="c5bb0-170">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-170">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="c5bb0-171">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-171">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="c5bb0-172">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-172">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="c5bb0-173">A SAS URL has the following format.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-173">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="c5bb0-174">If you used the portal to create locators before March 2015, locators with a two-year expiration date were created.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-174">If you used the portal to create locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="c5bb0-175">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-175">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="c5bb0-176">When you update the expiration date of a SAS locator, the URL changes.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-176">When you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="c5bb0-177">To use the portal to publish an asset</span><span class="sxs-lookup"><span data-stu-id="c5bb0-177">To use the portal to publish an asset</span></span>
<span data-ttu-id="c5bb0-178">To use the portal to publish an asset, do the following:</span><span class="sxs-lookup"><span data-stu-id="c5bb0-178">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="c5bb0-179">Select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-179">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="c5bb0-180">Select the asset that you want to publish.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-180">Select the asset that you want to publish.</span></span>
3. <span data-ttu-id="c5bb0-181">Click the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-181">Click the **Publish** button.</span></span>
4. <span data-ttu-id="c5bb0-182">Select the locator type.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-182">Select the locator type.</span></span>
5. <span data-ttu-id="c5bb0-183">Press **Add**.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-183">Press **Add**.</span></span>
   
    ![Publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="c5bb0-185">The URL is added to the list of **Published URLs**.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-185">The URL is added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="c5bb0-186">Play content from the portal</span><span class="sxs-lookup"><span data-stu-id="c5bb0-186">Play content from the portal</span></span>
<span data-ttu-id="c5bb0-187">The Azure portal provides a content player that you can use to test your video.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-187">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="c5bb0-188">Click the desired video and then click the **Play** button.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-188">Click the desired video and then click the **Play** button.</span></span>

![Publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="c5bb0-190">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="c5bb0-190">Some considerations apply:</span></span>

* <span data-ttu-id="c5bb0-191">Make sure the video has been published.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-191">Make sure the video has been published.</span></span>
* <span data-ttu-id="c5bb0-192">This **Media player** plays from the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-192">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="c5bb0-193">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-193">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="c5bb0-194">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="c5bb0-194">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5bb0-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5bb0-195">Next steps</span></span>
<span data-ttu-id="c5bb0-196">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="c5bb0-196">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c5bb0-197">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c5bb0-197">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]






