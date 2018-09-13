---
title: Configure the Elemental Live encoder to send a single bitrate live stream | Microsoft Docs
description: This topic shows how to configure the Elemental Live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.
services: media-services
documentationcenter: ''
author: cenkdin
manager: erikre
editor: ''
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 70548837a20b0222a1f62ef83da1ccb8564d9503
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670655"
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="74d3e-103">Use the Elemental Live encoder to send a single bitrate live stream</span><span class="sxs-lookup"><span data-stu-id="74d3e-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="74d3e-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="74d3e-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="74d3e-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="74d3e-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="74d3e-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span><span class="sxs-lookup"><span data-stu-id="74d3e-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="74d3e-111">This tool only runs on Windows PC.</span><span class="sxs-lookup"><span data-stu-id="74d3e-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="74d3e-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="74d3e-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74d3e-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74d3e-113">Prerequisites</span></span>
* <span data-ttu-id="74d3e-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span><span class="sxs-lookup"><span data-stu-id="74d3e-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* [<span data-ttu-id="74d3e-115">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="74d3e-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="74d3e-116">Ensure there is a Streaming Endpoint running.</span><span class="sxs-lookup"><span data-stu-id="74d3e-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="74d3e-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="74d3e-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="74d3e-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span><span class="sxs-lookup"><span data-stu-id="74d3e-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="74d3e-119">Launch the tool and connect to your AMS account.</span><span class="sxs-lookup"><span data-stu-id="74d3e-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="74d3e-120">Tips</span><span class="sxs-lookup"><span data-stu-id="74d3e-120">Tips</span></span>
* <span data-ttu-id="74d3e-121">Whenever possible, use a hardwired internet connection.</span><span class="sxs-lookup"><span data-stu-id="74d3e-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="74d3e-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span><span class="sxs-lookup"><span data-stu-id="74d3e-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="74d3e-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span><span class="sxs-lookup"><span data-stu-id="74d3e-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="74d3e-124">When using software based encoders, close out any unnecessary programs.</span><span class="sxs-lookup"><span data-stu-id="74d3e-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="74d3e-125">Elemental Live with RTP ingest</span><span class="sxs-lookup"><span data-stu-id="74d3e-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="74d3e-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span><span class="sxs-lookup"><span data-stu-id="74d3e-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="74d3e-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="74d3e-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="74d3e-128">Create a channel</span><span class="sxs-lookup"><span data-stu-id="74d3e-128">Create a channel</span></span>

1. <span data-ttu-id="74d3e-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span><span class="sxs-lookup"><span data-stu-id="74d3e-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="74d3e-130">Select **Create channel…**</span><span class="sxs-lookup"><span data-stu-id="74d3e-130">Select **Create channel…**</span></span> <span data-ttu-id="74d3e-131">from the menu.</span><span class="sxs-lookup"><span data-stu-id="74d3e-131">from the menu.</span></span>

    ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="74d3e-133">Specify a channel name, the description field is optional.</span><span class="sxs-lookup"><span data-stu-id="74d3e-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="74d3e-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="74d3e-135">You can leave all other settings as is.</span><span class="sxs-lookup"><span data-stu-id="74d3e-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="74d3e-136">Make sure the **Start the new channel now** is selected.</span><span class="sxs-lookup"><span data-stu-id="74d3e-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="74d3e-137">Click **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-137">Click **Create Channel**.</span></span>

   ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> The channel can take as long as 20 minutes to start.
>
>

<span data-ttu-id="74d3e-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="74d3e-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> Note that billing starts as soon as Channel goes into a ready state. For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a><span data-ttu-id="74d3e-143">Configure the Elemental Live encoder</span><span class="sxs-lookup"><span data-stu-id="74d3e-143">Configure the Elemental Live encoder</span></span>
<span data-ttu-id="74d3e-144">In this tutorial the following output settings are used.</span><span class="sxs-lookup"><span data-stu-id="74d3e-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="74d3e-145">The rest of this section describes configuration steps in more detail.</span><span class="sxs-lookup"><span data-stu-id="74d3e-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="74d3e-146">**Video**:</span><span class="sxs-lookup"><span data-stu-id="74d3e-146">**Video**:</span></span>

* <span data-ttu-id="74d3e-147">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="74d3e-147">Codec: H.264</span></span>
* <span data-ttu-id="74d3e-148">Profile: High (Level 4.0)</span><span class="sxs-lookup"><span data-stu-id="74d3e-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="74d3e-149">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="74d3e-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="74d3e-150">Keyframe: 2 seconds (60 seconds)</span><span class="sxs-lookup"><span data-stu-id="74d3e-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="74d3e-151">Frame Rate: 30</span><span class="sxs-lookup"><span data-stu-id="74d3e-151">Frame Rate: 30</span></span>

<span data-ttu-id="74d3e-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="74d3e-152">**Audio**:</span></span>

* <span data-ttu-id="74d3e-153">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="74d3e-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="74d3e-154">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="74d3e-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="74d3e-155">Sample Rate: 44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="74d3e-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="74d3e-156">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="74d3e-156">Configuration steps</span></span>
1. <span data-ttu-id="74d3e-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span><span class="sxs-lookup"><span data-stu-id="74d3e-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="74d3e-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span><span class="sxs-lookup"><span data-stu-id="74d3e-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="74d3e-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.
   >
   >
4. <span data-ttu-id="74d3e-162">Now that the Output has been created, click **Add Stream**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="74d3e-163">The output settings can now be configured.</span><span class="sxs-lookup"><span data-stu-id="74d3e-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="74d3e-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span><span class="sxs-lookup"><span data-stu-id="74d3e-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="74d3e-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span><span class="sxs-lookup"><span data-stu-id="74d3e-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="74d3e-167">Resolution: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="74d3e-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="74d3e-168">Framerate: 30</span><span class="sxs-lookup"><span data-stu-id="74d3e-168">Framerate: 30</span></span>
   * <span data-ttu-id="74d3e-169">GOP Size: 60 frames</span><span class="sxs-lookup"><span data-stu-id="74d3e-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="74d3e-170">Interlace Mode: Progressive</span><span class="sxs-lookup"><span data-stu-id="74d3e-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="74d3e-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span><span class="sxs-lookup"><span data-stu-id="74d3e-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="74d3e-173">Get the channel's input URL.</span><span class="sxs-lookup"><span data-stu-id="74d3e-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="74d3e-174">Navigate back to the AMSE tool, and check on the channel completion status.</span><span class="sxs-lookup"><span data-stu-id="74d3e-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="74d3e-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span><span class="sxs-lookup"><span data-stu-id="74d3e-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="74d3e-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="74d3e-178">Paste this information in the **Primary Destination** field of the Elemental.</span><span class="sxs-lookup"><span data-stu-id="74d3e-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="74d3e-179">All other settings can remain the default.</span><span class="sxs-lookup"><span data-stu-id="74d3e-179">All other settings can remain the default.</span></span>

    ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="74d3e-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span><span class="sxs-lookup"><span data-stu-id="74d3e-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="74d3e-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span><span class="sxs-lookup"><span data-stu-id="74d3e-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.
> Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.
>
>

<span data-ttu-id="74d3e-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span><span class="sxs-lookup"><span data-stu-id="74d3e-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="74d3e-186">Test playback</span><span class="sxs-lookup"><span data-stu-id="74d3e-186">Test playback</span></span>

<span data-ttu-id="74d3e-187">Navigate to the AMSE tool, and right click the channel to be tested.</span><span class="sxs-lookup"><span data-stu-id="74d3e-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="74d3e-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="74d3e-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span><span class="sxs-lookup"><span data-stu-id="74d3e-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="74d3e-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span><span class="sxs-lookup"><span data-stu-id="74d3e-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="74d3e-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span><span class="sxs-lookup"><span data-stu-id="74d3e-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="74d3e-192">Create a program</span><span class="sxs-lookup"><span data-stu-id="74d3e-192">Create a program</span></span>
1. <span data-ttu-id="74d3e-193">Once channel playback is confirmed, create a program.</span><span class="sxs-lookup"><span data-stu-id="74d3e-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="74d3e-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Elemental](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="74d3e-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span><span class="sxs-lookup"><span data-stu-id="74d3e-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="74d3e-197">You can also specify a storage location or leave as the default.</span><span class="sxs-lookup"><span data-stu-id="74d3e-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="74d3e-198">Check the **Start the Program now** box.</span><span class="sxs-lookup"><span data-stu-id="74d3e-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="74d3e-199">Click **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > Program creation takes less time than channel creation.   
      
5. <span data-ttu-id="74d3e-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="74d3e-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="74d3e-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span><span class="sxs-lookup"><span data-stu-id="74d3e-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="74d3e-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span><span class="sxs-lookup"><span data-stu-id="74d3e-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="74d3e-204">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="74d3e-204">Troubleshooting</span></span>
<span data-ttu-id="74d3e-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span><span class="sxs-lookup"><span data-stu-id="74d3e-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="74d3e-206">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="74d3e-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="74d3e-207">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="74d3e-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]









