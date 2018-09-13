---
title: Configure the Telestream Wirecast encoder to send a single bitrate live stream | Microsoft Docs
description: 'This topic shows how to configure the Wirecast live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding. '
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: cef839645dcbc02ef35aaa558de65e97e65cbdfc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555799"
---
# <a name="use-the-wirecast-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="9acc4-103">Use the Wirecast encoder to send a single bitrate live stream</span><span class="sxs-lookup"><span data-stu-id="9acc4-103">Use the Wirecast encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="9acc4-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="9acc4-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="9acc4-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="9acc4-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="9acc4-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span><span class="sxs-lookup"><span data-stu-id="9acc4-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="9acc4-111">This tool only runs on Windows PC.</span><span class="sxs-lookup"><span data-stu-id="9acc4-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="9acc4-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="9acc4-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9acc4-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9acc4-113">Prerequisites</span></span>
* [<span data-ttu-id="9acc4-114">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="9acc4-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="9acc4-115">Ensure there is a Streaming Endpoint running.</span><span class="sxs-lookup"><span data-stu-id="9acc4-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="9acc4-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="9acc4-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="9acc4-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span><span class="sxs-lookup"><span data-stu-id="9acc4-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="9acc4-118">Launch the tool and connect to your AMS account.</span><span class="sxs-lookup"><span data-stu-id="9acc4-118">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="9acc4-119">Tips</span><span class="sxs-lookup"><span data-stu-id="9acc4-119">Tips</span></span>
* <span data-ttu-id="9acc4-120">Whenever possible, use a hardwired internet connection.</span><span class="sxs-lookup"><span data-stu-id="9acc4-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="9acc4-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span><span class="sxs-lookup"><span data-stu-id="9acc4-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="9acc4-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span><span class="sxs-lookup"><span data-stu-id="9acc4-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="9acc4-123">When using software based encoders, close out any unnecessary programs.</span><span class="sxs-lookup"><span data-stu-id="9acc4-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="9acc4-124">Create a channel</span><span class="sxs-lookup"><span data-stu-id="9acc4-124">Create a channel</span></span>
1. <span data-ttu-id="9acc4-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span><span class="sxs-lookup"><span data-stu-id="9acc4-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="9acc4-126">Select **Create channel…**</span><span class="sxs-lookup"><span data-stu-id="9acc4-126">Select **Create channel…**</span></span> <span data-ttu-id="9acc4-127">from the menu.</span><span class="sxs-lookup"><span data-stu-id="9acc4-127">from the menu.</span></span>

    ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="9acc4-129">Specify a channel name, the description field is optional.</span><span class="sxs-lookup"><span data-stu-id="9acc4-129">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="9acc4-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="9acc4-131">You can leave all other settings as is.</span><span class="sxs-lookup"><span data-stu-id="9acc4-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="9acc4-132">Make sure the **Start the new channel now** is selected.</span><span class="sxs-lookup"><span data-stu-id="9acc4-132">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="9acc4-133">Click **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-133">Click **Create Channel**.</span></span>

   ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> The channel can take as long as 20 minutes to start.
>
>

<span data-ttu-id="9acc4-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="9acc4-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> Note that billing starts as soon as Channel goes into a ready state. For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a><span data-ttu-id="9acc4-139">Configure the Telestream Wirecast encoder</span><span class="sxs-lookup"><span data-stu-id="9acc4-139">Configure the Telestream Wirecast encoder</span></span>
<span data-ttu-id="9acc4-140">In this tutorial the following output settings are used.</span><span class="sxs-lookup"><span data-stu-id="9acc4-140">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="9acc4-141">The rest of this section describes configuration steps in more detail.</span><span class="sxs-lookup"><span data-stu-id="9acc4-141">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="9acc4-142">**Video**:</span><span class="sxs-lookup"><span data-stu-id="9acc4-142">**Video**:</span></span>

* <span data-ttu-id="9acc4-143">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="9acc4-143">Codec: H.264</span></span>
* <span data-ttu-id="9acc4-144">Profile: High (Level 4.0)</span><span class="sxs-lookup"><span data-stu-id="9acc4-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="9acc4-145">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="9acc4-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="9acc4-146">Keyframe: 2 seconds (60 seconds)</span><span class="sxs-lookup"><span data-stu-id="9acc4-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="9acc4-147">Frame Rate: 30</span><span class="sxs-lookup"><span data-stu-id="9acc4-147">Frame Rate: 30</span></span>

<span data-ttu-id="9acc4-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="9acc4-148">**Audio**:</span></span>

* <span data-ttu-id="9acc4-149">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="9acc4-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="9acc4-150">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="9acc4-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="9acc4-151">Sample Rate: 44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="9acc4-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="9acc4-152">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="9acc4-152">Configuration steps</span></span>
1. <span data-ttu-id="9acc4-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span><span class="sxs-lookup"><span data-stu-id="9acc4-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="9acc4-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="9acc4-155">Make sure the **Output Destination** is set to **RTMP Server**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-155">Make sure the **Output Destination** is set to **RTMP Server**.</span></span>
3. <span data-ttu-id="9acc4-156">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-156">Click **OK**.</span></span>
4. <span data-ttu-id="9acc4-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span></span>

    <span data-ttu-id="9acc4-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="9acc4-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span></span>

    ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="9acc4-161">Configure encoder presets.</span><span class="sxs-lookup"><span data-stu-id="9acc4-161">Configure encoder presets.</span></span>

    <span data-ttu-id="9acc4-162">Name the preset, and check for the following recommended settings:</span><span class="sxs-lookup"><span data-stu-id="9acc4-162">Name the preset, and check for the following recommended settings:</span></span>

    <span data-ttu-id="9acc4-163">**Video**</span><span class="sxs-lookup"><span data-stu-id="9acc4-163">**Video**</span></span>

   * <span data-ttu-id="9acc4-164">Encoder: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="9acc4-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="9acc4-165">Frames per Second: 30</span><span class="sxs-lookup"><span data-stu-id="9acc4-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="9acc4-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span><span class="sxs-lookup"><span data-stu-id="9acc4-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="9acc4-167">Profile: Main</span><span class="sxs-lookup"><span data-stu-id="9acc4-167">Profile: Main</span></span>
   * <span data-ttu-id="9acc4-168">Key frame every: 60 frames</span><span class="sxs-lookup"><span data-stu-id="9acc4-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="9acc4-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="9acc4-169">**Audio**</span></span>

   * <span data-ttu-id="9acc4-170">Target bit rate: 192 kbits/sec</span><span class="sxs-lookup"><span data-stu-id="9acc4-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="9acc4-171">Sample Rate: 44.100 kHz</span><span class="sxs-lookup"><span data-stu-id="9acc4-171">Sample Rate: 44.100 kHz</span></span>

     ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="9acc4-173">Press **Save**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-173">Press **Save**.</span></span>

    <span data-ttu-id="9acc4-174">The Encoding field now has the newly created profile available for selection.</span><span class="sxs-lookup"><span data-stu-id="9acc4-174">The Encoding field now has the newly created profile available for selection.</span></span>

    <span data-ttu-id="9acc4-175">Make sure the new profile is selected.</span><span class="sxs-lookup"><span data-stu-id="9acc4-175">Make sure the new profile is selected.</span></span>
7. <span data-ttu-id="9acc4-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="9acc4-177">Navigate back to the AMSE tool, and check on the channel completion status.</span><span class="sxs-lookup"><span data-stu-id="9acc4-177">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="9acc4-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span><span class="sxs-lookup"><span data-stu-id="9acc4-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="9acc4-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="9acc4-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span><span class="sxs-lookup"><span data-stu-id="9acc4-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span></span>

    ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="9acc4-183">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-183">Select **OK**.</span></span>
2. <span data-ttu-id="9acc4-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span><span class="sxs-lookup"><span data-stu-id="9acc4-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span></span>

   ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Before you click **Stream**, you **must** ensure that the Channel is ready.
> Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.
>
>

## <a name="test-playback"></a><span data-ttu-id="9acc4-188">Test playback</span><span class="sxs-lookup"><span data-stu-id="9acc4-188">Test playback</span></span>

<span data-ttu-id="9acc4-189">Navigate to the AMSE tool, and right click the channel to be tested.</span><span class="sxs-lookup"><span data-stu-id="9acc4-189">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="9acc4-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="9acc4-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span><span class="sxs-lookup"><span data-stu-id="9acc4-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="9acc4-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span><span class="sxs-lookup"><span data-stu-id="9acc4-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="9acc4-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span><span class="sxs-lookup"><span data-stu-id="9acc4-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="9acc4-194">Create a program</span><span class="sxs-lookup"><span data-stu-id="9acc4-194">Create a program</span></span>
1. <span data-ttu-id="9acc4-195">Once channel playback is confirmed, create a program.</span><span class="sxs-lookup"><span data-stu-id="9acc4-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="9acc4-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![wirecast](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="9acc4-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span><span class="sxs-lookup"><span data-stu-id="9acc4-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="9acc4-199">You can also specify a storage location or leave as the default.</span><span class="sxs-lookup"><span data-stu-id="9acc4-199">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="9acc4-200">Check the **Start the Program now** box.</span><span class="sxs-lookup"><span data-stu-id="9acc4-200">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="9acc4-201">Click **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   >Program creation takes less time than channel creation.
       
5. <span data-ttu-id="9acc4-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="9acc4-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="9acc4-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span><span class="sxs-lookup"><span data-stu-id="9acc4-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="9acc4-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span><span class="sxs-lookup"><span data-stu-id="9acc4-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="9acc4-206">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="9acc4-206">Troubleshooting</span></span>
<span data-ttu-id="9acc4-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span><span class="sxs-lookup"><span data-stu-id="9acc4-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9acc4-208">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="9acc4-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9acc4-209">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="9acc4-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]









