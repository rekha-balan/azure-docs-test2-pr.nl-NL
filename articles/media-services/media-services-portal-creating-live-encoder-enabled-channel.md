---
title: How to perform live streaming using Azure Media Services to create multi-bitrate streams with the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of creating a Channel that receives a single-bitrate live stream and encodes it to multi-bitrate stream using the Azure portal.
services: media-services
documentationcenter: ''
author: anilmur
manager: erikre
editor: ''
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: bc7cd97716723363bc514961d5a32a05db2874cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556287"
---
# <a name="how-to-perform-live-streaming-using-azure-media-services-to-create-multi-bitrate-streams-with-the-azure-portal"></a><span data-ttu-id="31eed-103">How to perform live streaming using Azure Media Services to create multi-bitrate streams with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="31eed-103">How to perform live streaming using Azure Media Services to create multi-bitrate streams with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [REST API](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="31eed-107">This tutorial walks you through the steps of creating a **Channel** that receives a single-bitrate live stream and encodes it to multi-bitrate stream.</span><span class="sxs-lookup"><span data-stu-id="31eed-107">This tutorial walks you through the steps of creating a **Channel** that receives a single-bitrate live stream and encodes it to multi-bitrate stream.</span></span>

> [!NOTE]
> For more conceptual information related to Channels that are enabled for live encoding, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="31eed-109">Common Live Streaming Scenario</span><span class="sxs-lookup"><span data-stu-id="31eed-109">Common Live Streaming Scenario</span></span>
<span data-ttu-id="31eed-110">The following are general steps involved in creating common live streaming applications.</span><span class="sxs-lookup"><span data-stu-id="31eed-110">The following are general steps involved in creating common live streaming applications.</span></span>

> [!NOTE]
> Currently, the max recommended duration of a live event is 8 hours. Please contact  amslived at Microsoft.com if you need to run a Channel for longer periods of time.
> 
> 

1. <span data-ttu-id="31eed-113">Connect a video camera to a computer.</span><span class="sxs-lookup"><span data-stu-id="31eed-113">Connect a video camera to a computer.</span></span> <span data-ttu-id="31eed-114">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of the following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="31eed-114">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of the following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="31eed-115">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="31eed-115">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="31eed-116">This step could also be performed after you create your Channel.</span><span class="sxs-lookup"><span data-stu-id="31eed-116">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="31eed-117">Create and start a Channel.</span><span class="sxs-lookup"><span data-stu-id="31eed-117">Create and start a Channel.</span></span> 
3. <span data-ttu-id="31eed-118">Retrieve the Channel ingest URL.</span><span class="sxs-lookup"><span data-stu-id="31eed-118">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="31eed-119">The ingest URL is used by the live encoder to send the stream to the Channel.</span><span class="sxs-lookup"><span data-stu-id="31eed-119">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="31eed-120">Retrieve the Channel preview URL.</span><span class="sxs-lookup"><span data-stu-id="31eed-120">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="31eed-121">Use this URL to verify that your channel is properly receiving the live stream.</span><span class="sxs-lookup"><span data-stu-id="31eed-121">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="31eed-122">Create an event/program (that will also create an asset).</span><span class="sxs-lookup"><span data-stu-id="31eed-122">Create an event/program (that will also create an asset).</span></span> 
6. <span data-ttu-id="31eed-123">Publish the event (that will create an  OnDemand locator for the associated asset).</span><span class="sxs-lookup"><span data-stu-id="31eed-123">Publish the event (that will create an  OnDemand locator for the associated asset).</span></span>    
7. <span data-ttu-id="31eed-124">Start the event when you are ready to start streaming and archiving.</span><span class="sxs-lookup"><span data-stu-id="31eed-124">Start the event when you are ready to start streaming and archiving.</span></span>
8. <span data-ttu-id="31eed-125">Optionally, the live encoder can be signaled to start an advertisement.</span><span class="sxs-lookup"><span data-stu-id="31eed-125">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="31eed-126">The advertisement is inserted in the output stream.</span><span class="sxs-lookup"><span data-stu-id="31eed-126">The advertisement is inserted in the output stream.</span></span>
9. <span data-ttu-id="31eed-127">Stop the event whenever you want to stop streaming and archiving the event.</span><span class="sxs-lookup"><span data-stu-id="31eed-127">Stop the event whenever you want to stop streaming and archiving the event.</span></span>
10. <span data-ttu-id="31eed-128">Delete the event (and optionally delete the asset).</span><span class="sxs-lookup"><span data-stu-id="31eed-128">Delete the event (and optionally delete the asset).</span></span>   

## <a name="in-this-tutorial"></a><span data-ttu-id="31eed-129">In this tutorial</span><span class="sxs-lookup"><span data-stu-id="31eed-129">In this tutorial</span></span>
<span data-ttu-id="31eed-130">In this tutorial, the Azure portal is used to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="31eed-130">In this tutorial, the Azure portal is used to accomplish the following tasks:</span></span> 

1. <span data-ttu-id="31eed-131">Create a channel that is enabled to perform live encoding.</span><span class="sxs-lookup"><span data-stu-id="31eed-131">Create a channel that is enabled to perform live encoding.</span></span>
2. <span data-ttu-id="31eed-132">Get the Ingest URL in order to supply it to live encoder.</span><span class="sxs-lookup"><span data-stu-id="31eed-132">Get the Ingest URL in order to supply it to live encoder.</span></span> <span data-ttu-id="31eed-133">The live encoder will use this URL to ingest the stream into the Channel.</span><span class="sxs-lookup"><span data-stu-id="31eed-133">The live encoder will use this URL to ingest the stream into the Channel.</span></span>
3. <span data-ttu-id="31eed-134">Create an event/program (and an asset).</span><span class="sxs-lookup"><span data-stu-id="31eed-134">Create an event/program (and an asset).</span></span>
4. <span data-ttu-id="31eed-135">Publish the asset and get streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="31eed-135">Publish the asset and get streaming URLs.</span></span>  
5. <span data-ttu-id="31eed-136">Play your content.</span><span class="sxs-lookup"><span data-stu-id="31eed-136">Play your content.</span></span>
6. <span data-ttu-id="31eed-137">Cleaning up.</span><span class="sxs-lookup"><span data-stu-id="31eed-137">Cleaning up.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31eed-138">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31eed-138">Prerequisites</span></span>
<span data-ttu-id="31eed-139">The following are required to complete the tutorial.</span><span class="sxs-lookup"><span data-stu-id="31eed-139">The following are required to complete the tutorial.</span></span>

* <span data-ttu-id="31eed-140">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="31eed-140">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="31eed-141">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="31eed-141">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> 
  <span data-ttu-id="31eed-142">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31eed-142">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="31eed-143">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="31eed-143">A Media Services account.</span></span> <span data-ttu-id="31eed-144">To create a Media Services account, see [Create Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="31eed-144">To create a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="31eed-145">A webcam and an encoder that can send a single bitrate live stream.</span><span class="sxs-lookup"><span data-stu-id="31eed-145">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="31eed-146">Create a channel</span><span class="sxs-lookup"><span data-stu-id="31eed-146">Create a channel</span></span>
1. <span data-ttu-id="31eed-147">In the [Azure portal](https://portal.azure.com/), select Media Services and then click on your Media Services account name.</span><span class="sxs-lookup"><span data-stu-id="31eed-147">In the [Azure portal](https://portal.azure.com/), select Media Services and then click on your Media Services account name.</span></span>
2. <span data-ttu-id="31eed-148">Select **Live Streaming**.</span><span class="sxs-lookup"><span data-stu-id="31eed-148">Select **Live Streaming**.</span></span>
3. <span data-ttu-id="31eed-149">Select **Custom create**.</span><span class="sxs-lookup"><span data-stu-id="31eed-149">Select **Custom create**.</span></span> <span data-ttu-id="31eed-150">This option will let you create a channel that is enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="31eed-150">This option will let you create a channel that is enabled for live encoding.</span></span>
   
    ![Create a channel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. <span data-ttu-id="31eed-152">Click on **Settings**.</span><span class="sxs-lookup"><span data-stu-id="31eed-152">Click on **Settings**.</span></span>
   
   1. <span data-ttu-id="31eed-153">Choose the **Live Encoding** channel type.</span><span class="sxs-lookup"><span data-stu-id="31eed-153">Choose the **Live Encoding** channel type.</span></span> <span data-ttu-id="31eed-154">This type specifies that you want to create a Channel that is enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="31eed-154">This type specifies that you want to create a Channel that is enabled for live encoding.</span></span> <span data-ttu-id="31eed-155">That means the incoming single bitrate stream is sent to the Channel and encoded into a multi-bitrate stream using specified live encoder settings.</span><span class="sxs-lookup"><span data-stu-id="31eed-155">That means the incoming single bitrate stream is sent to the Channel and encoded into a multi-bitrate stream using specified live encoder settings.</span></span> <span data-ttu-id="31eed-156">For more information, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="31eed-156">For more information, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span> <span data-ttu-id="31eed-157">Click OK.</span><span class="sxs-lookup"><span data-stu-id="31eed-157">Click OK.</span></span>
   2. <span data-ttu-id="31eed-158">Specify a channel's name.</span><span class="sxs-lookup"><span data-stu-id="31eed-158">Specify a channel's name.</span></span>
   3. <span data-ttu-id="31eed-159">Click OK at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="31eed-159">Click OK at the bottom of the screen.</span></span>
5. <span data-ttu-id="31eed-160">Select the **Ingest** tab.</span><span class="sxs-lookup"><span data-stu-id="31eed-160">Select the **Ingest** tab.</span></span>
   
   1. <span data-ttu-id="31eed-161">On this page, you can select a streaming protocol.</span><span class="sxs-lookup"><span data-stu-id="31eed-161">On this page, you can select a streaming protocol.</span></span> <span data-ttu-id="31eed-162">For the **Live Encoding** channel type, valid protocol options are:</span><span class="sxs-lookup"><span data-stu-id="31eed-162">For the **Live Encoding** channel type, valid protocol options are:</span></span>
      
      * <span data-ttu-id="31eed-163">Single bitrate Fragmented MP4 (Smooth Streaming)</span><span class="sxs-lookup"><span data-stu-id="31eed-163">Single bitrate Fragmented MP4 (Smooth Streaming)</span></span>
      * <span data-ttu-id="31eed-164">Single bitrate RTMP</span><span class="sxs-lookup"><span data-stu-id="31eed-164">Single bitrate RTMP</span></span>
      * <span data-ttu-id="31eed-165">RTP (MPEG-TS): MPEG-2 Transport Stream over RTP.</span><span class="sxs-lookup"><span data-stu-id="31eed-165">RTP (MPEG-TS): MPEG-2 Transport Stream over RTP.</span></span>
        
        <span data-ttu-id="31eed-166">For detailed explanation about each protocol, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="31eed-166">For detailed explanation about each protocol, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>
        
        <span data-ttu-id="31eed-167">You cannot change the protocol option while the Channel or its associated events/programs are running.</span><span class="sxs-lookup"><span data-stu-id="31eed-167">You cannot change the protocol option while the Channel or its associated events/programs are running.</span></span> <span data-ttu-id="31eed-168">If you require different protocols, you should create separate channels for each streaming protocol.</span><span class="sxs-lookup"><span data-stu-id="31eed-168">If you require different protocols, you should create separate channels for each streaming protocol.</span></span>  
   2. <span data-ttu-id="31eed-169">You can apply IP restriction on the ingest.</span><span class="sxs-lookup"><span data-stu-id="31eed-169">You can apply IP restriction on the ingest.</span></span> 
      
       <span data-ttu-id="31eed-170">You can define the IP addresses that are allowed to ingest a video to this channel.</span><span class="sxs-lookup"><span data-stu-id="31eed-170">You can define the IP addresses that are allowed to ingest a video to this channel.</span></span> <span data-ttu-id="31eed-171">Allowed IP addresses can be specified as either a single IP address (e.g. '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (e.g. '10.0.0.1/22'), or an IP range using an IP address and a dotted decimal subnet mask (e.g. '10.0.0.1(255.255.252.0)').</span><span class="sxs-lookup"><span data-stu-id="31eed-171">Allowed IP addresses can be specified as either a single IP address (e.g. '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (e.g. '10.0.0.1/22'), or an IP range using an IP address and a dotted decimal subnet mask (e.g. '10.0.0.1(255.255.252.0)').</span></span>
      
       <span data-ttu-id="31eed-172">If no IP addresses are specified and there is no rule definition then no IP address will be allowed.</span><span class="sxs-lookup"><span data-stu-id="31eed-172">If no IP addresses are specified and there is no rule definition then no IP address will be allowed.</span></span> <span data-ttu-id="31eed-173">To allow any IP address, create a rule and set 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="31eed-173">To allow any IP address, create a rule and set 0.0.0.0/0.</span></span>
6. <span data-ttu-id="31eed-174">On the **Preview** tab, apply IP restriction on the preview.</span><span class="sxs-lookup"><span data-stu-id="31eed-174">On the **Preview** tab, apply IP restriction on the preview.</span></span>
7. <span data-ttu-id="31eed-175">On the **Encoding** tab, specify the encoding preset.</span><span class="sxs-lookup"><span data-stu-id="31eed-175">On the **Encoding** tab, specify the encoding preset.</span></span> 
   
    <span data-ttu-id="31eed-176">Currently, the only system preset you can select is **Default 720p**.</span><span class="sxs-lookup"><span data-stu-id="31eed-176">Currently, the only system preset you can select is **Default 720p**.</span></span> <span data-ttu-id="31eed-177">To specify a custom preset, open a Microsoft support ticket.</span><span class="sxs-lookup"><span data-stu-id="31eed-177">To specify a custom preset, open a Microsoft support ticket.</span></span> <span data-ttu-id="31eed-178">Then, enter the name of the preset created for you.</span><span class="sxs-lookup"><span data-stu-id="31eed-178">Then, enter the name of the preset created for you.</span></span> 

> [!NOTE]
> Currently, the Channel start can take up to 30 minutes. Channel reset can take up to 5 minutes.
> 
> 

<span data-ttu-id="31eed-181">Once you created the Channel, you can click on the channel and select **Settings** where you can view your channels configurations.</span><span class="sxs-lookup"><span data-stu-id="31eed-181">Once you created the Channel, you can click on the channel and select **Settings** where you can view your channels configurations.</span></span> 

<span data-ttu-id="31eed-182">For more information, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="31eed-182">For more information, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="get-ingest-urls"></a><span data-ttu-id="31eed-183">Get ingest URLs</span><span class="sxs-lookup"><span data-stu-id="31eed-183">Get ingest URLs</span></span>
<span data-ttu-id="31eed-184">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span><span class="sxs-lookup"><span data-stu-id="31eed-184">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="31eed-185">The encoder uses these URLs to input a live stream.</span><span class="sxs-lookup"><span data-stu-id="31eed-185">The encoder uses these URLs to input a live stream.</span></span>

![ingesturls](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a><span data-ttu-id="31eed-187">Create and manage events</span><span class="sxs-lookup"><span data-stu-id="31eed-187">Create and manage events</span></span>
### <a name="overview"></a><span data-ttu-id="31eed-188">Overview</span><span class="sxs-lookup"><span data-stu-id="31eed-188">Overview</span></span>
<span data-ttu-id="31eed-189">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span><span class="sxs-lookup"><span data-stu-id="31eed-189">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="31eed-190">Channels manage events/programs.</span><span class="sxs-lookup"><span data-stu-id="31eed-190">Channels manage events/programs.</span></span> <span data-ttu-id="31eed-191">The Channel and Program relationship is very similar to traditional media where a channel has a constant stream of content and a program is scoped to some timed event on that channel.</span><span class="sxs-lookup"><span data-stu-id="31eed-191">The Channel and Program relationship is very similar to traditional media where a channel has a constant stream of content and a program is scoped to some timed event on that channel.</span></span>

<span data-ttu-id="31eed-192">You can specify the number of hours you want to retain the recorded content for the event by setting the **Archive Window** length.</span><span class="sxs-lookup"><span data-stu-id="31eed-192">You can specify the number of hours you want to retain the recorded content for the event by setting the **Archive Window** length.</span></span> <span data-ttu-id="31eed-193">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span><span class="sxs-lookup"><span data-stu-id="31eed-193">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="31eed-194">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span><span class="sxs-lookup"><span data-stu-id="31eed-194">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="31eed-195">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span><span class="sxs-lookup"><span data-stu-id="31eed-195">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="31eed-196">This value of this property also determines how long the client manifests can grow.</span><span class="sxs-lookup"><span data-stu-id="31eed-196">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="31eed-197">Each event is associated with an Asset.</span><span class="sxs-lookup"><span data-stu-id="31eed-197">Each event is associated with an Asset.</span></span> <span data-ttu-id="31eed-198">To publish the event you must create an OnDemand locator for the associated asset.</span><span class="sxs-lookup"><span data-stu-id="31eed-198">To publish the event you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="31eed-199">Having this locator will enable you to build a streaming URL that you can provide to your clients.</span><span class="sxs-lookup"><span data-stu-id="31eed-199">Having this locator will enable you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="31eed-200">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span><span class="sxs-lookup"><span data-stu-id="31eed-200">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="31eed-201">This allows you to publish and archive different parts of an event as needed.</span><span class="sxs-lookup"><span data-stu-id="31eed-201">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="31eed-202">For example, your business requirement is to archive 6 hours of an event, but to broadcast only last 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="31eed-202">For example, your business requirement is to archive 6 hours of an event, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="31eed-203">To accomplish this, you need to create two concurrently running event.</span><span class="sxs-lookup"><span data-stu-id="31eed-203">To accomplish this, you need to create two concurrently running event.</span></span> <span data-ttu-id="31eed-204">One event is set to archive 6 hours of the event but the program is not published.</span><span class="sxs-lookup"><span data-stu-id="31eed-204">One event is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="31eed-205">The other event is set to archive for 10 minutes and this program is published.</span><span class="sxs-lookup"><span data-stu-id="31eed-205">The other event is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="31eed-206">You should not reuse existing programs for new events.</span><span class="sxs-lookup"><span data-stu-id="31eed-206">You should not reuse existing programs for new events.</span></span> <span data-ttu-id="31eed-207">Instead, create and start a new program for each event.</span><span class="sxs-lookup"><span data-stu-id="31eed-207">Instead, create and start a new program for each event.</span></span>

<span data-ttu-id="31eed-208">Start an event/program when you are ready to start streaming and archiving.</span><span class="sxs-lookup"><span data-stu-id="31eed-208">Start an event/program when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="31eed-209">Stop the event whenever you want to stop streaming and archiving the event.</span><span class="sxs-lookup"><span data-stu-id="31eed-209">Stop the event whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="31eed-210">To delete archived content, stop and delete the event and then delete the associated asset.</span><span class="sxs-lookup"><span data-stu-id="31eed-210">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="31eed-211">An asset cannot be deleted if it is used by the event; the event must be deleted first.</span><span class="sxs-lookup"><span data-stu-id="31eed-211">An asset cannot be deleted if it is used by the event; the event must be deleted first.</span></span> 

<span data-ttu-id="31eed-212">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span><span class="sxs-lookup"><span data-stu-id="31eed-212">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="31eed-213">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span><span class="sxs-lookup"><span data-stu-id="31eed-213">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="createstartstop-events"></a><span data-ttu-id="31eed-214">Create/start/stop events</span><span class="sxs-lookup"><span data-stu-id="31eed-214">Create/start/stop events</span></span>
<span data-ttu-id="31eed-215">Once you have the stream flowing into the Channel you can begin the streaming event by creating an Asset, Program, and Streaming Locator.</span><span class="sxs-lookup"><span data-stu-id="31eed-215">Once you have the stream flowing into the Channel you can begin the streaming event by creating an Asset, Program, and Streaming Locator.</span></span> <span data-ttu-id="31eed-216">This will archive the stream and make it available to viewers through the Streaming Endpoint.</span><span class="sxs-lookup"><span data-stu-id="31eed-216">This will archive the stream and make it available to viewers through the Streaming Endpoint.</span></span> 

>[!NOTE]
>When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state. To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state. 

<span data-ttu-id="31eed-219">There are two ways to start event:</span><span class="sxs-lookup"><span data-stu-id="31eed-219">There are two ways to start event:</span></span> 

1. <span data-ttu-id="31eed-220">From the **Channel** page, press **Live Event** to add a new event.</span><span class="sxs-lookup"><span data-stu-id="31eed-220">From the **Channel** page, press **Live Event** to add a new event.</span></span>
   
    <span data-ttu-id="31eed-221">Specify: event name, asset name, archive window, and encryption option.</span><span class="sxs-lookup"><span data-stu-id="31eed-221">Specify: event name, asset name, archive window, and encryption option.</span></span>
   
    ![createprogram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    <span data-ttu-id="31eed-223">If you left **Publish this live event now** checked, the event the PUBLISHING URLs will get created.</span><span class="sxs-lookup"><span data-stu-id="31eed-223">If you left **Publish this live event now** checked, the event the PUBLISHING URLs will get created.</span></span>
   
    <span data-ttu-id="31eed-224">You can press **Start**, whenever you are ready to stream the event.</span><span class="sxs-lookup"><span data-stu-id="31eed-224">You can press **Start**, whenever you are ready to stream the event.</span></span>
   
    <span data-ttu-id="31eed-225">Once you start the event, you can press **Watch** to start playing the content.</span><span class="sxs-lookup"><span data-stu-id="31eed-225">Once you start the event, you can press **Watch** to start playing the content.</span></span>
2. <span data-ttu-id="31eed-226">Alternatively, you can use a shortcut and press **Go Live** button on the **Channel** page.</span><span class="sxs-lookup"><span data-stu-id="31eed-226">Alternatively, you can use a shortcut and press **Go Live** button on the **Channel** page.</span></span> <span data-ttu-id="31eed-227">This will create a default Asset, Program, and Streaming Locator.</span><span class="sxs-lookup"><span data-stu-id="31eed-227">This will create a default Asset, Program, and Streaming Locator.</span></span>
   
    <span data-ttu-id="31eed-228">The event is named **default** and the archive window is set to 8 hours.</span><span class="sxs-lookup"><span data-stu-id="31eed-228">The event is named **default** and the archive window is set to 8 hours.</span></span>

<span data-ttu-id="31eed-229">You can watch the published event from the **Live event** page.</span><span class="sxs-lookup"><span data-stu-id="31eed-229">You can watch the published event from the **Live event** page.</span></span> 

<span data-ttu-id="31eed-230">If you click **Off Air**, it will stop all live events.</span><span class="sxs-lookup"><span data-stu-id="31eed-230">If you click **Off Air**, it will stop all live events.</span></span> 

## <a name="watch-the-event"></a><span data-ttu-id="31eed-231">Watch the event</span><span class="sxs-lookup"><span data-stu-id="31eed-231">Watch the event</span></span>
<span data-ttu-id="31eed-232">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span><span class="sxs-lookup"><span data-stu-id="31eed-232">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![Created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

<span data-ttu-id="31eed-234">Live event automatically converts events to on-demand content when stopped.</span><span class="sxs-lookup"><span data-stu-id="31eed-234">Live event automatically converts events to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="31eed-235">Clean up</span><span class="sxs-lookup"><span data-stu-id="31eed-235">Clean up</span></span>
<span data-ttu-id="31eed-236">If you are done streaming events and want to clean up the resources provisioned earlier, follow the following procedure.</span><span class="sxs-lookup"><span data-stu-id="31eed-236">If you are done streaming events and want to clean up the resources provisioned earlier, follow the following procedure.</span></span>

* <span data-ttu-id="31eed-237">Stop pushing the stream from the encoder.</span><span class="sxs-lookup"><span data-stu-id="31eed-237">Stop pushing the stream from the encoder.</span></span>
* <span data-ttu-id="31eed-238">Stop the channel.</span><span class="sxs-lookup"><span data-stu-id="31eed-238">Stop the channel.</span></span> <span data-ttu-id="31eed-239">Once the Channel is stopped, it will not incur any charges.</span><span class="sxs-lookup"><span data-stu-id="31eed-239">Once the Channel is stopped, it will not incur any charges.</span></span> <span data-ttu-id="31eed-240">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span><span class="sxs-lookup"><span data-stu-id="31eed-240">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="31eed-241">You can stop your Streaming Endpoint, unless you want to continue to provide the archive of your live event as an on-demand stream.</span><span class="sxs-lookup"><span data-stu-id="31eed-241">You can stop your Streaming Endpoint, unless you want to continue to provide the archive of your live event as an on-demand stream.</span></span> <span data-ttu-id="31eed-242">If the channel is in stopped state, it will not incur any charges.</span><span class="sxs-lookup"><span data-stu-id="31eed-242">If the channel is in stopped state, it will not incur any charges.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="31eed-243">View archived content</span><span class="sxs-lookup"><span data-stu-id="31eed-243">View archived content</span></span>
<span data-ttu-id="31eed-244">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span><span class="sxs-lookup"><span data-stu-id="31eed-244">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="31eed-245">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span><span class="sxs-lookup"><span data-stu-id="31eed-245">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="31eed-246">To manage your assets, select **Setting** and click **Assets**.</span><span class="sxs-lookup"><span data-stu-id="31eed-246">To manage your assets, select **Setting** and click **Assets**.</span></span>

![Assets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a><span data-ttu-id="31eed-248">Considerations</span><span class="sxs-lookup"><span data-stu-id="31eed-248">Considerations</span></span>
* <span data-ttu-id="31eed-249">Currently, the max recommended duration of a live event is 8 hours.</span><span class="sxs-lookup"><span data-stu-id="31eed-249">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="31eed-250">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span><span class="sxs-lookup"><span data-stu-id="31eed-250">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
* <span data-ttu-id="31eed-251">Make sure the streaming endpoint from which you want to stream  your content is in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="31eed-251">Make sure the streaming endpoint from which you want to stream  your content is in the **Running** state.</span></span>

## <a name="next-step"></a><span data-ttu-id="31eed-252">Next step</span><span class="sxs-lookup"><span data-stu-id="31eed-252">Next step</span></span>
<span data-ttu-id="31eed-253">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="31eed-253">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="31eed-254">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="31eed-254">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]






