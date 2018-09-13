---
title: Configure the FMLE encoder to send a single bitrate live stream | Microsoft Docs
description: This topic shows how to configure the Flash Media Live Encoder (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 1a7cbd19b89663ab874fc5a7a86587e292b86f81
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968914"
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="49171-103">Use the FMLE encoder to send a single bitrate live stream</span><span class="sxs-lookup"><span data-stu-id="49171-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="49171-107">This article shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="49171-107">This article shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="49171-108">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="49171-108">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="49171-109">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span><span class="sxs-lookup"><span data-stu-id="49171-109">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="49171-110">This tool only runs on Windows PC.</span><span class="sxs-lookup"><span data-stu-id="49171-110">This tool only runs on Windows PC.</span></span> <span data-ttu-id="49171-111">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="49171-111">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="49171-112">This tutorial describes using AAC.</span><span class="sxs-lookup"><span data-stu-id="49171-112">This tutorial describes using AAC.</span></span> <span data-ttu-id="49171-113">However, FMLE doesn’t supports AAC by default.</span><span class="sxs-lookup"><span data-stu-id="49171-113">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="49171-114">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="49171-114">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49171-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="49171-115">Prerequisites</span></span>
* [<span data-ttu-id="49171-116">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="49171-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="49171-117">Ensure there is a Streaming Endpoint running.</span><span class="sxs-lookup"><span data-stu-id="49171-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="49171-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="49171-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="49171-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span><span class="sxs-lookup"><span data-stu-id="49171-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="49171-120">Launch the tool and connect to your AMS account.</span><span class="sxs-lookup"><span data-stu-id="49171-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="49171-121">Tips</span><span class="sxs-lookup"><span data-stu-id="49171-121">Tips</span></span>
* <span data-ttu-id="49171-122">Whenever possible, use a hardwired internet connection.</span><span class="sxs-lookup"><span data-stu-id="49171-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="49171-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span><span class="sxs-lookup"><span data-stu-id="49171-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="49171-124">While this is not a mandatory requirement, it helps mitigate the impact of network congestion.</span><span class="sxs-lookup"><span data-stu-id="49171-124">While this is not a mandatory requirement, it helps mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="49171-125">When using software-based encoders, close out any unnecessary programs.</span><span class="sxs-lookup"><span data-stu-id="49171-125">When using software-based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="49171-126">Create a channel</span><span class="sxs-lookup"><span data-stu-id="49171-126">Create a channel</span></span>
1. <span data-ttu-id="49171-127">In the AMSE tool, navigate to the **Live** tab, and right-click within the channel area.</span><span class="sxs-lookup"><span data-stu-id="49171-127">In the AMSE tool, navigate to the **Live** tab, and right-click within the channel area.</span></span> <span data-ttu-id="49171-128">Select **Create channel…**</span><span class="sxs-lookup"><span data-stu-id="49171-128">Select **Create channel…**</span></span> <span data-ttu-id="49171-129">from the menu.</span><span class="sxs-lookup"><span data-stu-id="49171-129">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="49171-131">Specify a channel name, the description field is optional.</span><span class="sxs-lookup"><span data-stu-id="49171-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="49171-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="49171-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="49171-133">You can leave all other settings as is.</span><span class="sxs-lookup"><span data-stu-id="49171-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="49171-134">Make sure the **Start the new channel now** is selected.</span><span class="sxs-lookup"><span data-stu-id="49171-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="49171-135">Click **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="49171-135">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> The channel can take as long as 20 minutes to start.
>
>

<span data-ttu-id="49171-138">While the channel is starting, you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="49171-138">While the channel is starting, you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> Note that billing starts as soon as Channel goes into a ready state. For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a><span data-ttu-id="49171-141">Configure the FMLE encoder</span><span class="sxs-lookup"><span data-stu-id="49171-141">Configure the FMLE encoder</span></span>
<span data-ttu-id="49171-142">In this tutorial, the following output settings are used.</span><span class="sxs-lookup"><span data-stu-id="49171-142">In this tutorial, the following output settings are used.</span></span> <span data-ttu-id="49171-143">The rest of this section describes configuration steps in more detail.</span><span class="sxs-lookup"><span data-stu-id="49171-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="49171-144">**Video**:</span><span class="sxs-lookup"><span data-stu-id="49171-144">**Video**:</span></span>

* <span data-ttu-id="49171-145">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="49171-145">Codec: H.264</span></span>
* <span data-ttu-id="49171-146">Profile: High (Level 4.0)</span><span class="sxs-lookup"><span data-stu-id="49171-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="49171-147">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="49171-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="49171-148">Keyframe: 2 seconds (60 seconds)</span><span class="sxs-lookup"><span data-stu-id="49171-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="49171-149">Frame Rate: 30</span><span class="sxs-lookup"><span data-stu-id="49171-149">Frame Rate: 30</span></span>

<span data-ttu-id="49171-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="49171-150">**Audio**:</span></span>

* <span data-ttu-id="49171-151">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="49171-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="49171-152">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="49171-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="49171-153">Sample Rate: 44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="49171-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="49171-154">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="49171-154">Configuration steps</span></span>
1. <span data-ttu-id="49171-155">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span><span class="sxs-lookup"><span data-stu-id="49171-155">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="49171-156">The interface is one main page of settings.</span><span class="sxs-lookup"><span data-stu-id="49171-156">The interface is one main page of settings.</span></span> <span data-ttu-id="49171-157">Take note of the following recommended settings to get started with streaming using FMLE.</span><span class="sxs-lookup"><span data-stu-id="49171-157">Take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="49171-158">Format: H.264 Frame Rate: 30.00</span><span class="sxs-lookup"><span data-stu-id="49171-158">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="49171-159">Input Size: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="49171-159">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="49171-160">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span><span class="sxs-lookup"><span data-stu-id="49171-160">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="49171-162">When using interlaced sources, please checkmark the “Deinterlace” option</span><span class="sxs-lookup"><span data-stu-id="49171-162">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="49171-163">Select the wrench icon next to Format, these additional settings should be:</span><span class="sxs-lookup"><span data-stu-id="49171-163">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="49171-164">Profile: Main</span><span class="sxs-lookup"><span data-stu-id="49171-164">Profile: Main</span></span>
   * <span data-ttu-id="49171-165">Level: 4.0</span><span class="sxs-lookup"><span data-stu-id="49171-165">Level: 4.0</span></span>
   * <span data-ttu-id="49171-166">Keyframe Frequency: 2 seconds</span><span class="sxs-lookup"><span data-stu-id="49171-166">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="49171-168">Set the following important audio setting:</span><span class="sxs-lookup"><span data-stu-id="49171-168">Set the following important audio setting:</span></span>

   * <span data-ttu-id="49171-169">Format: AAC</span><span class="sxs-lookup"><span data-stu-id="49171-169">Format: AAC</span></span>
   * <span data-ttu-id="49171-170">Sample Rate: 44100 Hz</span><span class="sxs-lookup"><span data-stu-id="49171-170">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="49171-171">Bitrate: 192 Kbps</span><span class="sxs-lookup"><span data-stu-id="49171-171">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="49171-173">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="49171-173">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="49171-174">Navigate back to the AMSE tool, and check on the channel completion status.</span><span class="sxs-lookup"><span data-stu-id="49171-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="49171-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span><span class="sxs-lookup"><span data-stu-id="49171-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="49171-176">When the channel is running, right-click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span><span class="sxs-lookup"><span data-stu-id="49171-176">When the channel is running, right-click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="49171-178">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span><span class="sxs-lookup"><span data-stu-id="49171-178">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="49171-180">For extra redundancy, repeat these steps with the Secondary Input URL.</span><span class="sxs-lookup"><span data-stu-id="49171-180">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="49171-181">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="49171-181">Select **Connect**.</span></span>

> [!IMPORTANT]
> Before you click **Connect**, you **must** ensure that the Channel is ready.
> Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.
>
>

## <a name="test-playback"></a><span data-ttu-id="49171-184">Test playback</span><span class="sxs-lookup"><span data-stu-id="49171-184">Test playback</span></span>

<span data-ttu-id="49171-185">Navigate to the AMSE tool, and right-click the channel to be tested.</span><span class="sxs-lookup"><span data-stu-id="49171-185">Navigate to the AMSE tool, and right-click the channel to be tested.</span></span> <span data-ttu-id="49171-186">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="49171-186">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="49171-187">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span><span class="sxs-lookup"><span data-stu-id="49171-187">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="49171-188">If an error is received, the channel needs to be reset and encoder settings adjusted.</span><span class="sxs-lookup"><span data-stu-id="49171-188">If an error is received, the channel needs to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="49171-189">See the [troubleshooting](media-services-troubleshooting-live-streaming.md) article for guidance.</span><span class="sxs-lookup"><span data-stu-id="49171-189">See the [troubleshooting](media-services-troubleshooting-live-streaming.md) article for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="49171-190">Create a program</span><span class="sxs-lookup"><span data-stu-id="49171-190">Create a program</span></span>
1. <span data-ttu-id="49171-191">Once channel playback is confirmed, create a program.</span><span class="sxs-lookup"><span data-stu-id="49171-191">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="49171-192">Under the **Live** tab in the AMSE tool, right-click within the program area and select **Create New Program**.</span><span class="sxs-lookup"><span data-stu-id="49171-192">Under the **Live** tab in the AMSE tool, right-click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="49171-194">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span><span class="sxs-lookup"><span data-stu-id="49171-194">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="49171-195">You can also specify a storage location or leave as the default.</span><span class="sxs-lookup"><span data-stu-id="49171-195">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="49171-196">Check the **Start the Program now** box.</span><span class="sxs-lookup"><span data-stu-id="49171-196">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="49171-197">Click **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="49171-197">Click **Create Program**.</span></span>  

    >[!NOTE]
    >Program creation takes less time than channel creation.
        
5. <span data-ttu-id="49171-199">Once the program is running, confirm playback by right-clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="49171-199">Once the program is running, confirm playback by right-clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="49171-200">Once confirmed, right-click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span><span class="sxs-lookup"><span data-stu-id="49171-200">Once confirmed, right-click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="49171-201">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span><span class="sxs-lookup"><span data-stu-id="49171-201">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="49171-202">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="49171-202">Troubleshooting</span></span>
<span data-ttu-id="49171-203">See the [troubleshooting](media-services-troubleshooting-live-streaming.md) article for guidance.</span><span class="sxs-lookup"><span data-stu-id="49171-203">See the [troubleshooting](media-services-troubleshooting-live-streaming.md) article for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="49171-204">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="49171-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="49171-205">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="49171-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
