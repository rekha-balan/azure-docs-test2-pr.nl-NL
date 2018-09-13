---
title: Configure the NewTek TriCaster encoder to send a single bitrate live stream | Microsoft Docs
description: This topic shows how to configure the Tricaster live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.
services: media-services
documentationcenter: ''
author: cenkdin
manager: erikre
editor: ''
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 07c56076e28fcecdd9a791f34cfd7330321de7e1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553080"
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="dd3ba-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span><span class="sxs-lookup"><span data-stu-id="dd3ba-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="dd3ba-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="dd3ba-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="dd3ba-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="dd3ba-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="dd3ba-111">This tool only runs on Windows PC.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="dd3ba-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="dd3ba-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates. The AMS team is working on fixing these issues, until then, it is not recommend to use these features.
>
>

## <a name="prerequisites"></a><span data-ttu-id="dd3ba-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dd3ba-115">Prerequisites</span></span>
* [<span data-ttu-id="dd3ba-116">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="dd3ba-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="dd3ba-117">Ensure there is a Streaming Endpoint running.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="dd3ba-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="dd3ba-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="dd3ba-120">Launch the tool and connect to your AMS account.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="dd3ba-121">Tips</span><span class="sxs-lookup"><span data-stu-id="dd3ba-121">Tips</span></span>
* <span data-ttu-id="dd3ba-122">Whenever possible, use a hardwired internet connection.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="dd3ba-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="dd3ba-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="dd3ba-125">When using software based encoders, close out any unnecessary programs.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="dd3ba-126">Create a channel</span><span class="sxs-lookup"><span data-stu-id="dd3ba-126">Create a channel</span></span>
1. <span data-ttu-id="dd3ba-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="dd3ba-128">Select **Create channel…**</span><span class="sxs-lookup"><span data-stu-id="dd3ba-128">Select **Create channel…**</span></span> <span data-ttu-id="dd3ba-129">from the menu.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-129">from the menu.</span></span>

    ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="dd3ba-131">Specify a channel name, the description field is optional.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="dd3ba-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="dd3ba-133">You can leave all other settings as is.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="dd3ba-134">Make sure the **Start the new channel now** is selected.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="dd3ba-135">Click **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-135">Click **Create Channel**.</span></span>

   ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> The channel can take as long as 20 minutes to start.
>
>

<span data-ttu-id="dd3ba-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="dd3ba-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> Note that billing starts as soon as Channel goes into a ready state. For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_tricaster_rtmp></a><span data-ttu-id="dd3ba-141">Configure the NewTek TriCaster encoder</span><span class="sxs-lookup"><span data-stu-id="dd3ba-141">Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="dd3ba-142">In this tutorial the following output settings are used.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="dd3ba-143">The rest of this section describes configuration steps in more detail.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="dd3ba-144">**Video**:</span><span class="sxs-lookup"><span data-stu-id="dd3ba-144">**Video**:</span></span>

* <span data-ttu-id="dd3ba-145">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="dd3ba-145">Codec: H.264</span></span>
* <span data-ttu-id="dd3ba-146">Profile: High (Level 4.0)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="dd3ba-147">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="dd3ba-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="dd3ba-148">Keyframe: 2 seconds (60 seconds)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="dd3ba-149">Frame Rate: 30</span><span class="sxs-lookup"><span data-stu-id="dd3ba-149">Frame Rate: 30</span></span>

<span data-ttu-id="dd3ba-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="dd3ba-150">**Audio**:</span></span>

* <span data-ttu-id="dd3ba-151">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="dd3ba-152">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="dd3ba-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="dd3ba-153">Sample Rate: 44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="dd3ba-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="dd3ba-154">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="dd3ba-154">Configuration steps</span></span>
1. <span data-ttu-id="dd3ba-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="dd3ba-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="dd3ba-158">Once the menu has opened, click **New** under the Connection heading.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="dd3ba-159">When prompted for the connection type, select **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="dd3ba-161">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-161">Click **OK**.</span></span>
5. <span data-ttu-id="dd3ba-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="dd3ba-164">Navigate to where the configured FMLE profile was saved.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="dd3ba-165">Select it, and press **OK**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="dd3ba-166">Once the profile is uploaded, proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="dd3ba-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="dd3ba-168">Navigate back to the AMSE tool, and check on the channel completion status.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="dd3ba-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="dd3ba-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="dd3ba-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="dd3ba-173">Also assign a stream name in the **Stream ID** field.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="dd3ba-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="dd3ba-175">The relevant Flash Server fields should populate with the information from FMLE.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="dd3ba-177">When finished, click **OK** at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="dd3ba-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> Before you click **Stream**, you **must** ensure that the Channel is ready.
> Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.
>
>

## <a name="test-playback"></a><span data-ttu-id="dd3ba-182">Test playback</span><span class="sxs-lookup"><span data-stu-id="dd3ba-182">Test playback</span></span>
<span data-ttu-id="dd3ba-183">Navigate to the AMSE tool, and right click the channel to be tested.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="dd3ba-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="dd3ba-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="dd3ba-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="dd3ba-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="dd3ba-188">Create a program</span><span class="sxs-lookup"><span data-stu-id="dd3ba-188">Create a program</span></span>
1. <span data-ttu-id="dd3ba-189">Once channel playback is confirmed, create a program.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="dd3ba-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![tricaster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="dd3ba-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span><span class="sxs-lookup"><span data-stu-id="dd3ba-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="dd3ba-193">You can also specify a storage location or leave as the default.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="dd3ba-194">Check the **Start the Program now** box.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="dd3ba-195">Click **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    >Program creation takes less time than channel creation.
        
5. <span data-ttu-id="dd3ba-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="dd3ba-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span><span class="sxs-lookup"><span data-stu-id="dd3ba-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="dd3ba-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="dd3ba-200">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="dd3ba-200">Troubleshooting</span></span>
<span data-ttu-id="dd3ba-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="dd3ba-202">Next step</span><span class="sxs-lookup"><span data-stu-id="dd3ba-202">Next step</span></span>
<span data-ttu-id="dd3ba-203">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dd3ba-204">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="dd3ba-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]










