---
title: Live stream with on-premise encoders using the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of creating a Channel that is configured for a pass-through delivery.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 6336dd7171d229be730b8f2a0fad2768f2472796
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549823"
---
# <a name="how-to-perform-live-streaming-with-on-premise-encoders-using-the-azure-portal"></a><span data-ttu-id="6e28b-103">How to perform live streaming with on-premise encoders using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e28b-103">How to perform live streaming with on-premise encoders using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="6e28b-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span><span class="sxs-lookup"><span data-stu-id="6e28b-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6e28b-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6e28b-108">Prerequisites</span></span>
<span data-ttu-id="6e28b-109">The following are required to complete the tutorial:</span><span class="sxs-lookup"><span data-stu-id="6e28b-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="6e28b-110">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="6e28b-110">An Azure account.</span></span> <span data-ttu-id="6e28b-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e28b-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="6e28b-112">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="6e28b-112">A Media Services account.</span></span> <span data-ttu-id="6e28b-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="6e28b-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="6e28b-114">A webcam.</span><span class="sxs-lookup"><span data-stu-id="6e28b-114">A webcam.</span></span> <span data-ttu-id="6e28b-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="6e28b-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="6e28b-116">It is highly recommended to review the following articles:</span><span class="sxs-lookup"><span data-stu-id="6e28b-116">It is highly recommended to review the following articles:</span></span>

* [<span data-ttu-id="6e28b-117">Azure Media Services RTMP Support and Live Encoders</span><span class="sxs-lookup"><span data-stu-id="6e28b-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="6e28b-118">Overview of Live Steaming using Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="6e28b-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="6e28b-119">Live streaming with on-premise encoders that create multi-bitrate streams</span><span class="sxs-lookup"><span data-stu-id="6e28b-119">Live streaming with on-premise encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a><span data-ttu-id="6e28b-120">Common live streaming scenario</span><span class="sxs-lookup"><span data-stu-id="6e28b-120">Common live streaming scenario</span></span>
<span data-ttu-id="6e28b-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span><span class="sxs-lookup"><span data-stu-id="6e28b-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="6e28b-122">This tutorial shows how to create and manage a pass-through channel and live events.</span><span class="sxs-lookup"><span data-stu-id="6e28b-122">This tutorial shows how to create and manage a pass-through channel and live events.</span></span>

>[!NOTE]
>Make sure the streaming endpoint from which you want to stream content is in the **Running** state. 
    
1. <span data-ttu-id="6e28b-124">Connect a video camera to a computer.</span><span class="sxs-lookup"><span data-stu-id="6e28b-124">Connect a video camera to a computer.</span></span> <span data-ttu-id="6e28b-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span><span class="sxs-lookup"><span data-stu-id="6e28b-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="6e28b-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="6e28b-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="6e28b-127">This step could also be performed after you create your Channel.</span><span class="sxs-lookup"><span data-stu-id="6e28b-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="6e28b-128">Create and start a pass-through Channel.</span><span class="sxs-lookup"><span data-stu-id="6e28b-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="6e28b-129">Retrieve the Channel ingest URL.</span><span class="sxs-lookup"><span data-stu-id="6e28b-129">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="6e28b-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span><span class="sxs-lookup"><span data-stu-id="6e28b-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="6e28b-131">Retrieve the Channel preview URL.</span><span class="sxs-lookup"><span data-stu-id="6e28b-131">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="6e28b-132">Use this URL to verify that your channel is properly receiving the live stream.</span><span class="sxs-lookup"><span data-stu-id="6e28b-132">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="6e28b-133">Create a live event/program.</span><span class="sxs-lookup"><span data-stu-id="6e28b-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="6e28b-134">When using the Azure portal, creating a live event also creates an asset.</span><span class="sxs-lookup"><span data-stu-id="6e28b-134">When using the Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="6e28b-135">Start the event/program when you are ready to start streaming and archiving.</span><span class="sxs-lookup"><span data-stu-id="6e28b-135">Start the event/program when you are ready to start streaming and archiving.</span></span>
7. <span data-ttu-id="6e28b-136">Optionally, the live encoder can be signaled to start an advertisement.</span><span class="sxs-lookup"><span data-stu-id="6e28b-136">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="6e28b-137">The advertisement is inserted in the output stream.</span><span class="sxs-lookup"><span data-stu-id="6e28b-137">The advertisement is inserted in the output stream.</span></span>
8. <span data-ttu-id="6e28b-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span><span class="sxs-lookup"><span data-stu-id="6e28b-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span></span>
9. <span data-ttu-id="6e28b-139">Delete the event/program (and optionally delete the asset).</span><span class="sxs-lookup"><span data-stu-id="6e28b-139">Delete the event/program (and optionally delete the asset).</span></span>     

> [!IMPORTANT]
> Please review [Live streaming with on-premise encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) to learn about concepts and considerations related to live streaming with on-premise encoders and pass-through channels.
> 
> 

## <a name="to-view-notifications-and-errors"></a><span data-ttu-id="6e28b-141">To view notifications and errors</span><span class="sxs-lookup"><span data-stu-id="6e28b-141">To view notifications and errors</span></span>
<span data-ttu-id="6e28b-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span><span class="sxs-lookup"><span data-stu-id="6e28b-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span></span>

![Notifications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="6e28b-144">Create and start pass-through channels and events</span><span class="sxs-lookup"><span data-stu-id="6e28b-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="6e28b-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span><span class="sxs-lookup"><span data-stu-id="6e28b-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="6e28b-146">Channels manage events.</span><span class="sxs-lookup"><span data-stu-id="6e28b-146">Channels manage events.</span></span> 

<span data-ttu-id="6e28b-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span><span class="sxs-lookup"><span data-stu-id="6e28b-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span></span> <span data-ttu-id="6e28b-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span><span class="sxs-lookup"><span data-stu-id="6e28b-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="6e28b-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span><span class="sxs-lookup"><span data-stu-id="6e28b-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="6e28b-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span><span class="sxs-lookup"><span data-stu-id="6e28b-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="6e28b-151">This value of this property also determines how long the client manifests can grow.</span><span class="sxs-lookup"><span data-stu-id="6e28b-151">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="6e28b-152">Each event is associated with an asset.</span><span class="sxs-lookup"><span data-stu-id="6e28b-152">Each event is associated with an asset.</span></span> <span data-ttu-id="6e28b-153">To publish the event, you must create an OnDemand locator for the associated asset.</span><span class="sxs-lookup"><span data-stu-id="6e28b-153">To publish the event, you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="6e28b-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span><span class="sxs-lookup"><span data-stu-id="6e28b-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="6e28b-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span><span class="sxs-lookup"><span data-stu-id="6e28b-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="6e28b-156">This allows you to publish and archive different parts of an event as needed.</span><span class="sxs-lookup"><span data-stu-id="6e28b-156">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="6e28b-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="6e28b-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="6e28b-158">To accomplish this, you need to create two concurrently running programs.</span><span class="sxs-lookup"><span data-stu-id="6e28b-158">To accomplish this, you need to create two concurrently running programs.</span></span> <span data-ttu-id="6e28b-159">One program is set to archive 6 hours of the event but the program is not published.</span><span class="sxs-lookup"><span data-stu-id="6e28b-159">One program is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="6e28b-160">The other program is set to archive for 10 minutes and this program is published.</span><span class="sxs-lookup"><span data-stu-id="6e28b-160">The other program is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="6e28b-161">You should not reuse existing live events.</span><span class="sxs-lookup"><span data-stu-id="6e28b-161">You should not reuse existing live events.</span></span> <span data-ttu-id="6e28b-162">Instead, create and start a new event for each event.</span><span class="sxs-lookup"><span data-stu-id="6e28b-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="6e28b-163">Start the event when you are ready to start streaming and archiving.</span><span class="sxs-lookup"><span data-stu-id="6e28b-163">Start the event when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="6e28b-164">Stop the program whenever you want to stop streaming and archiving the event.</span><span class="sxs-lookup"><span data-stu-id="6e28b-164">Stop the program whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="6e28b-165">To delete archived content, stop and delete the event and then delete the associated asset.</span><span class="sxs-lookup"><span data-stu-id="6e28b-165">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="6e28b-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span><span class="sxs-lookup"><span data-stu-id="6e28b-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="6e28b-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span><span class="sxs-lookup"><span data-stu-id="6e28b-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="6e28b-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span><span class="sxs-lookup"><span data-stu-id="6e28b-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="to-use-the-portal-to-create-a-channel"></a><span data-ttu-id="6e28b-169">To use the portal to create a channel</span><span class="sxs-lookup"><span data-stu-id="6e28b-169">To use the portal to create a channel</span></span>
<span data-ttu-id="6e28b-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span><span class="sxs-lookup"><span data-stu-id="6e28b-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span></span>

<span data-ttu-id="6e28b-171">For more details about pass-through channels, see [Live streaming with on-premise encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="6e28b-171">For more details about pass-through channels, see [Live streaming with on-premise encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="6e28b-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="6e28b-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="6e28b-173">In the **Settings** window, click **Live streaming**.</span><span class="sxs-lookup"><span data-stu-id="6e28b-173">In the **Settings** window, click **Live streaming**.</span></span> 
   
    ![Getting started](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="6e28b-175">The **Live streaming** window appears.</span><span class="sxs-lookup"><span data-stu-id="6e28b-175">The **Live streaming** window appears.</span></span>
3. <span data-ttu-id="6e28b-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span><span class="sxs-lookup"><span data-stu-id="6e28b-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="6e28b-177">The **CREATE A NEW CHANNEL** window appears.</span><span class="sxs-lookup"><span data-stu-id="6e28b-177">The **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="6e28b-178">Give the new channel a name and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e28b-178">Give the new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="6e28b-179">This creates a pass-through channel with the RTMP ingest protocol.</span><span class="sxs-lookup"><span data-stu-id="6e28b-179">This creates a pass-through channel with the RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="6e28b-180">Create events</span><span class="sxs-lookup"><span data-stu-id="6e28b-180">Create events</span></span>
1. <span data-ttu-id="6e28b-181">Select a channel to which you want to add an event.</span><span class="sxs-lookup"><span data-stu-id="6e28b-181">Select a channel to which you want to add an event.</span></span>
2. <span data-ttu-id="6e28b-182">Press **Live Event** button.</span><span class="sxs-lookup"><span data-stu-id="6e28b-182">Press **Live Event** button.</span></span>

![Event](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="6e28b-184">Get ingest URLs</span><span class="sxs-lookup"><span data-stu-id="6e28b-184">Get ingest URLs</span></span>
<span data-ttu-id="6e28b-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span><span class="sxs-lookup"><span data-stu-id="6e28b-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="6e28b-186">The encoder uses these URLs to input a live stream.</span><span class="sxs-lookup"><span data-stu-id="6e28b-186">The encoder uses these URLs to input a live stream.</span></span>

![Created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-the-event"></a><span data-ttu-id="6e28b-188">Watch the event</span><span class="sxs-lookup"><span data-stu-id="6e28b-188">Watch the event</span></span>
<span data-ttu-id="6e28b-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span><span class="sxs-lookup"><span data-stu-id="6e28b-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![Created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="6e28b-191">Live event automatically get converted to on-demand content when stopped.</span><span class="sxs-lookup"><span data-stu-id="6e28b-191">Live event automatically get converted to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="6e28b-192">Clean up</span><span class="sxs-lookup"><span data-stu-id="6e28b-192">Clean up</span></span>
<span data-ttu-id="6e28b-193">For more details about pass-through channels, see [Live streaming with on-premise encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="6e28b-193">For more details about pass-through channels, see [Live streaming with on-premise encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="6e28b-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span><span class="sxs-lookup"><span data-stu-id="6e28b-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span></span>  <span data-ttu-id="6e28b-195">Once the Channel is stopped, it does not incur any charges.</span><span class="sxs-lookup"><span data-stu-id="6e28b-195">Once the Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="6e28b-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span><span class="sxs-lookup"><span data-stu-id="6e28b-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="6e28b-197">A channel can be deleted only when all live events on the channel have been deleted.</span><span class="sxs-lookup"><span data-stu-id="6e28b-197">A channel can be deleted only when all live events on the channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="6e28b-198">View archived content</span><span class="sxs-lookup"><span data-stu-id="6e28b-198">View archived content</span></span>
<span data-ttu-id="6e28b-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span><span class="sxs-lookup"><span data-stu-id="6e28b-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="6e28b-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span><span class="sxs-lookup"><span data-stu-id="6e28b-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="6e28b-201">To manage your assets, select **Setting** and click **Assets**.</span><span class="sxs-lookup"><span data-stu-id="6e28b-201">To manage your assets, select **Setting** and click **Assets**.</span></span>

![Assets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="6e28b-203">Next step</span><span class="sxs-lookup"><span data-stu-id="6e28b-203">Next step</span></span>
<span data-ttu-id="6e28b-204">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="6e28b-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6e28b-205">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="6e28b-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]







