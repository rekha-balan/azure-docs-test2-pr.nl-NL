---
title: Get started with delivering video-on-demand by using the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of implementing a basic video-on-demand content delivery service with an Azure Media Services application in the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 11babf8a66c38354499ce85fad424fed04c07c15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870697"
---
# <a name="get-started-with-delivering-content-on-demand-by-using-the-azure-portal"></a><span data-ttu-id="568a5-103">Get started with delivering content on demand by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="568a5-103">Get started with delivering content on demand by using the Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="568a5-104">This tutorial walks you through the steps of implementing a basic video-on-demand content delivery service with an Azure Media Services application in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="568a5-104">This tutorial walks you through the steps of implementing a basic video-on-demand content delivery service with an Azure Media Services application in the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="568a5-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="568a5-105">Prerequisites</span></span>
<span data-ttu-id="568a5-106">The following items are required to complete the tutorial:</span><span class="sxs-lookup"><span data-stu-id="568a5-106">The following items are required to complete the tutorial:</span></span>

* <span data-ttu-id="568a5-107">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="568a5-107">An Azure account.</span></span> <span data-ttu-id="568a5-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="568a5-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="568a5-109">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="568a5-109">A Media Services account.</span></span> <span data-ttu-id="568a5-110">To create a Media Services account, see [How to create a Media Services account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="568a5-110">To create a Media Services account, see [How to create a Media Services account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="568a5-111">This tutorial includes the following tasks:</span><span class="sxs-lookup"><span data-stu-id="568a5-111">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="568a5-112">Start the streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="568a5-112">Start the streaming endpoint.</span></span>
2. <span data-ttu-id="568a5-113">Upload a video file.</span><span class="sxs-lookup"><span data-stu-id="568a5-113">Upload a video file.</span></span>
3. <span data-ttu-id="568a5-114">Encode the source file into a set of adaptive bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="568a5-114">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="568a5-115">Publish the asset, and get streaming and progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="568a5-115">Publish the asset, and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="568a5-116">Play your content.</span><span class="sxs-lookup"><span data-stu-id="568a5-116">Play your content.</span></span>

## <a name="start-the-streaming-endpoint"></a><span data-ttu-id="568a5-117">Start the streaming endpoint</span><span class="sxs-lookup"><span data-stu-id="568a5-117">Start the streaming endpoint</span></span>

<span data-ttu-id="568a5-118">One of the most common scenarios when working with Azure Media Services is delivering video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="568a5-118">One of the most common scenarios when working with Azure Media Services is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="568a5-119">Media Services gives you dynamic packaging.</span><span class="sxs-lookup"><span data-stu-id="568a5-119">Media Services gives you dynamic packaging.</span></span> <span data-ttu-id="568a5-120">With dynamic packaging, you can deliver your adaptive bitrate MP4 encoded content in just-in-time streaming formats that are supported by Media Services.</span><span class="sxs-lookup"><span data-stu-id="568a5-120">With dynamic packaging, you can deliver your adaptive bitrate MP4 encoded content in just-in-time streaming formats that are supported by Media Services.</span></span> <span data-ttu-id="568a5-121">Examples include Apple HTTP Live Streaming (HLS), Microsoft Smooth Streaming, and Dynamic Adaptive Streaming over HTTP (DASH, also called MPEG-DASH).</span><span class="sxs-lookup"><span data-stu-id="568a5-121">Examples include Apple HTTP Live Streaming (HLS), Microsoft Smooth Streaming, and Dynamic Adaptive Streaming over HTTP (DASH, also called MPEG-DASH).</span></span> <span data-ttu-id="568a5-122">By using Media Services adaptive bitrate streaming, you can deliver your videos without storing prepackaged versions of each of these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="568a5-122">By using Media Services adaptive bitrate streaming, you can deliver your videos without storing prepackaged versions of each of these streaming formats.</span></span>

> [!NOTE]
> <span data-ttu-id="568a5-123">When you create your Media Services account, a default streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="568a5-123">When you create your Media Services account, a default streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="568a5-124">To start streaming your content, and to take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="568a5-124">To start streaming your content, and to take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="568a5-125">To start the streaming endpoint:</span><span class="sxs-lookup"><span data-stu-id="568a5-125">To start the streaming endpoint:</span></span>

1. <span data-ttu-id="568a5-126">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="568a5-126">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="568a5-127">Select **Settings** > **Streaming endpoints**.</span><span class="sxs-lookup"><span data-stu-id="568a5-127">Select **Settings** > **Streaming endpoints**.</span></span> 
3. <span data-ttu-id="568a5-128">Select the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="568a5-128">Select the default streaming endpoint.</span></span> <span data-ttu-id="568a5-129">The **DEFAULT STREAMING ENDPOINT DETAILS** window appears.</span><span class="sxs-lookup"><span data-stu-id="568a5-129">The **DEFAULT STREAMING ENDPOINT DETAILS** window appears.</span></span>
4. <span data-ttu-id="568a5-130">Select the **Start** icon.</span><span class="sxs-lookup"><span data-stu-id="568a5-130">Select the **Start** icon.</span></span>
5. <span data-ttu-id="568a5-131">Select the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="568a5-131">Select the **Save** button.</span></span>

## <a name="upload-files"></a><span data-ttu-id="568a5-132">Upload files</span><span class="sxs-lookup"><span data-stu-id="568a5-132">Upload files</span></span>
<span data-ttu-id="568a5-133">To stream videos by using Media Services, you upload the source videos, encode them into multiple bitrates, and then publish the result.</span><span class="sxs-lookup"><span data-stu-id="568a5-133">To stream videos by using Media Services, you upload the source videos, encode them into multiple bitrates, and then publish the result.</span></span> <span data-ttu-id="568a5-134">The first step is covered in this section.</span><span class="sxs-lookup"><span data-stu-id="568a5-134">The first step is covered in this section.</span></span> 

1. <span data-ttu-id="568a5-135">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="568a5-135">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="568a5-136">Select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="568a5-136">Select **Settings** > **Assets**.</span></span> <span data-ttu-id="568a5-137">Then, select the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="568a5-137">Then, select the **Upload** button.</span></span>
   
    ![Upload files](./media/media-services-portal-vod-get-started/media-services-upload.png)
   
    <span data-ttu-id="568a5-139">The **Upload a video asset** window appears.</span><span class="sxs-lookup"><span data-stu-id="568a5-139">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="568a5-140">Media Services doesn't limit the file size for uploading videos.</span><span class="sxs-lookup"><span data-stu-id="568a5-140">Media Services doesn't limit the file size for uploading videos.</span></span>
   > 
   > 
3. <span data-ttu-id="568a5-141">On your computer, go to the video that you want to upload.</span><span class="sxs-lookup"><span data-stu-id="568a5-141">On your computer, go to the video that you want to upload.</span></span> <span data-ttu-id="568a5-142">Select the video, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="568a5-142">Select the video, and then select **OK**.</span></span>  
   
    <span data-ttu-id="568a5-143">The upload begins.</span><span class="sxs-lookup"><span data-stu-id="568a5-143">The upload begins.</span></span> <span data-ttu-id="568a5-144">You can see the progress under the file name.</span><span class="sxs-lookup"><span data-stu-id="568a5-144">You can see the progress under the file name.</span></span>  

<span data-ttu-id="568a5-145">When the upload is finished, the new asset is listed in the **Assets** pane.</span><span class="sxs-lookup"><span data-stu-id="568a5-145">When the upload is finished, the new asset is listed in the **Assets** pane.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="568a5-146">Encode assets</span><span class="sxs-lookup"><span data-stu-id="568a5-146">Encode assets</span></span>
<span data-ttu-id="568a5-147">To take advantage of dynamic packaging, you must encode your source file into a set of multi-bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="568a5-147">To take advantage of dynamic packaging, you must encode your source file into a set of multi-bitrate MP4 files.</span></span> <span data-ttu-id="568a5-148">The encoding steps are demonstrated in this section.</span><span class="sxs-lookup"><span data-stu-id="568a5-148">The encoding steps are demonstrated in this section.</span></span>

### <a name="encode-assets-in-the-portal"></a><span data-ttu-id="568a5-149">Encode assets in the portal</span><span class="sxs-lookup"><span data-stu-id="568a5-149">Encode assets in the portal</span></span>
<span data-ttu-id="568a5-150">To encode your content by using Media Encoder Standard in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="568a5-150">To encode your content by using Media Encoder Standard in the Azure portal:</span></span>

1. <span data-ttu-id="568a5-151">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="568a5-151">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="568a5-152">Select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="568a5-152">Select **Settings** > **Assets**.</span></span> <span data-ttu-id="568a5-153">Select the asset that you want to encode.</span><span class="sxs-lookup"><span data-stu-id="568a5-153">Select the asset that you want to encode.</span></span>
3. <span data-ttu-id="568a5-154">Select the **Encode** button.</span><span class="sxs-lookup"><span data-stu-id="568a5-154">Select the **Encode** button.</span></span>
4. <span data-ttu-id="568a5-155">In the **Encode an asset** pane, select the **Media Encoder Standard** processor and a preset.</span><span class="sxs-lookup"><span data-stu-id="568a5-155">In the **Encode an asset** pane, select the **Media Encoder Standard** processor and a preset.</span></span> <span data-ttu-id="568a5-156">For information about presets, see [Auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="568a5-156">For information about presets, see [Auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="568a5-157">It's important to choose the preset that will work best for your input video.</span><span class="sxs-lookup"><span data-stu-id="568a5-157">It's important to choose the preset that will work best for your input video.</span></span> <span data-ttu-id="568a5-158">For example, if you know your input video has a resolution of 1920 &#215; 1080 pixels, you might choose the **H264 Multiple Bitrate 1080p** preset.</span><span class="sxs-lookup"><span data-stu-id="568a5-158">For example, if you know your input video has a resolution of 1920 &#215; 1080 pixels, you might choose the **H264 Multiple Bitrate 1080p** preset.</span></span> <span data-ttu-id="568a5-159">If you have a low-resolution (640 &#215; 360) video, you shouldn't use the **H264 Multiple Bitrate 1080p** preset.</span><span class="sxs-lookup"><span data-stu-id="568a5-159">If you have a low-resolution (640 &#215; 360) video, you shouldn't use the **H264 Multiple Bitrate 1080p** preset.</span></span>
   
   <span data-ttu-id="568a5-160">To help you manage your resources, you can edit the name of the output asset and the name of the job.</span><span class="sxs-lookup"><span data-stu-id="568a5-160">To help you manage your resources, you can edit the name of the output asset and the name of the job.</span></span>
   
   ![Encode assets](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="568a5-162">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="568a5-162">Select **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="568a5-163">Monitor encoding job progress</span><span class="sxs-lookup"><span data-stu-id="568a5-163">Monitor encoding job progress</span></span>
<span data-ttu-id="568a5-164">To monitor the progress of the encoding job, at the top of the page, select **Settings**, and then select **Jobs**.</span><span class="sxs-lookup"><span data-stu-id="568a5-164">To monitor the progress of the encoding job, at the top of the page, select **Settings**, and then select **Jobs**.</span></span>

![Jobs](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="568a5-166">Publish content</span><span class="sxs-lookup"><span data-stu-id="568a5-166">Publish content</span></span>
<span data-ttu-id="568a5-167">To provide your user with a URL that they can use to stream or download your content, first you must publish your asset by creating a locator.</span><span class="sxs-lookup"><span data-stu-id="568a5-167">To provide your user with a URL that they can use to stream or download your content, first you must publish your asset by creating a locator.</span></span> <span data-ttu-id="568a5-168">Locators provide access to files that are in the asset.</span><span class="sxs-lookup"><span data-stu-id="568a5-168">Locators provide access to files that are in the asset.</span></span> <span data-ttu-id="568a5-169">Azure Media Services supports two types of locators:</span><span class="sxs-lookup"><span data-stu-id="568a5-169">Azure Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="568a5-170">**Streaming (OnDemandOrigin) locators**.</span><span class="sxs-lookup"><span data-stu-id="568a5-170">**Streaming (OnDemandOrigin) locators**.</span></span> <span data-ttu-id="568a5-171">Streaming locators are used for adaptive streaming.</span><span class="sxs-lookup"><span data-stu-id="568a5-171">Streaming locators are used for adaptive streaming.</span></span> <span data-ttu-id="568a5-172">Examples of adaptive streaming include HLS, Smooth Streaming, and MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="568a5-172">Examples of adaptive streaming include HLS, Smooth Streaming, and MPEG-DASH.</span></span> <span data-ttu-id="568a5-173">To create a streaming locator, your asset must include an .ism file.</span><span class="sxs-lookup"><span data-stu-id="568a5-173">To create a streaming locator, your asset must include an .ism file.</span></span> 
* <span data-ttu-id="568a5-174">**Progressive (shared access signature) locators**.</span><span class="sxs-lookup"><span data-stu-id="568a5-174">**Progressive (shared access signature) locators**.</span></span> <span data-ttu-id="568a5-175">Progressive locators are used to deliver video via progressive download.</span><span class="sxs-lookup"><span data-stu-id="568a5-175">Progressive locators are used to deliver video via progressive download.</span></span>

<span data-ttu-id="568a5-176">To build an HLS streaming URL, append *(format=m3u8-aapl)* to the URL:</span><span class="sxs-lookup"><span data-stu-id="568a5-176">To build an HLS streaming URL, append *(format=m3u8-aapl)* to the URL:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{file name}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="568a5-177">To build a streaming URL to play Smooth Streaming assets, use the following URL format:</span><span class="sxs-lookup"><span data-stu-id="568a5-177">To build a streaming URL to play Smooth Streaming assets, use the following URL format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{file name}.ism/Manifest

<span data-ttu-id="568a5-178">To build an MPEG-DASH streaming URL, append *(format=mpd-time-csf)* to the URL:</span><span class="sxs-lookup"><span data-stu-id="568a5-178">To build an MPEG-DASH streaming URL, append *(format=mpd-time-csf)* to the URL:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{file name}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="568a5-179">A shared access signature URL has the following format:</span><span class="sxs-lookup"><span data-stu-id="568a5-179">A shared access signature URL has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{shared access signature}

> [!NOTE]
> <span data-ttu-id="568a5-180">Locators that were created in the Azure portal before March 2015 have a two-year expiration date.</span><span class="sxs-lookup"><span data-stu-id="568a5-180">Locators that were created in the Azure portal before March 2015 have a two-year expiration date.</span></span>  
> 
> 

<span data-ttu-id="568a5-181">To update an expiration date on a locator, you can use a [REST API](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or a [.NET API](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="568a5-181">To update an expiration date on a locator, you can use a [REST API](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or a [.NET API](http://go.microsoft.com/fwlink/?LinkID=533259).</span></span> 

> [!NOTE]
> <span data-ttu-id="568a5-182">When you update the expiration date of a shared access signature locator, the URL changes.</span><span class="sxs-lookup"><span data-stu-id="568a5-182">When you update the expiration date of a shared access signature locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="568a5-183">To use the portal to publish an asset</span><span class="sxs-lookup"><span data-stu-id="568a5-183">To use the portal to publish an asset</span></span>
1. <span data-ttu-id="568a5-184">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="568a5-184">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="568a5-185">Select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="568a5-185">Select **Settings** > **Assets**.</span></span> <span data-ttu-id="568a5-186">Select the asset that you want to publish.</span><span class="sxs-lookup"><span data-stu-id="568a5-186">Select the asset that you want to publish.</span></span>
3. <span data-ttu-id="568a5-187">Select the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="568a5-187">Select the **Publish** button.</span></span>
4. <span data-ttu-id="568a5-188">Select the locator type.</span><span class="sxs-lookup"><span data-stu-id="568a5-188">Select the locator type.</span></span>
5. <span data-ttu-id="568a5-189">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="568a5-189">Select **Add**.</span></span>
   
    ![Publish the video](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="568a5-191">The URL is added to the list of **Published URLs**.</span><span class="sxs-lookup"><span data-stu-id="568a5-191">The URL is added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="568a5-192">Play content from the portal</span><span class="sxs-lookup"><span data-stu-id="568a5-192">Play content from the portal</span></span>
<span data-ttu-id="568a5-193">You can test your video on a content player in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="568a5-193">You can test your video on a content player in the Azure portal.</span></span>

<span data-ttu-id="568a5-194">Select the video, and then select the **Play** button.</span><span class="sxs-lookup"><span data-stu-id="568a5-194">Select the video, and then select the **Play** button.</span></span>

![Play the video in the Azure portal](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="568a5-196">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="568a5-196">Some considerations apply:</span></span>

* <span data-ttu-id="568a5-197">To begin streaming, start running the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="568a5-197">To begin streaming, start running the default streaming endpoint.</span></span>
* <span data-ttu-id="568a5-198">Make sure that the video has been published.</span><span class="sxs-lookup"><span data-stu-id="568a5-198">Make sure that the video has been published.</span></span>
* <span data-ttu-id="568a5-199">The Azure portal media player plays from the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="568a5-199">The Azure portal media player plays from the default streaming endpoint.</span></span> <span data-ttu-id="568a5-200">If you want to play from a non-default streaming endpoint, select and copy the URL, and then paste it into another player.</span><span class="sxs-lookup"><span data-stu-id="568a5-200">If you want to play from a non-default streaming endpoint, select and copy the URL, and then paste it into another player.</span></span> <span data-ttu-id="568a5-201">For example, you can test your video on the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="568a5-201">For example, you can test your video on the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="568a5-202">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="568a5-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="568a5-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="568a5-203">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]
