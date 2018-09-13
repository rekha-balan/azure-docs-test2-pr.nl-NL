---
title: Configure the FMLE encoder to send a single bitrate live stream | Microsoft Docs
description: This topic shows how to configure the Flash Media Live Encoder (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 43420e28fa3423939bb0050b5c2c03d361125268
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540807"
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="834d8-103">Use the FMLE encoder to send a single bitrate live stream</span><span class="sxs-lookup"><span data-stu-id="834d8-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="834d8-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="834d8-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="834d8-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="834d8-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="834d8-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span><span class="sxs-lookup"><span data-stu-id="834d8-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="834d8-111">This tool only runs on Windows PC.</span><span class="sxs-lookup"><span data-stu-id="834d8-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="834d8-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="834d8-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="834d8-113">Note that this tutorial describes using AAC.</span><span class="sxs-lookup"><span data-stu-id="834d8-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="834d8-114">However, FMLE doesn’t supports AAC by default.</span><span class="sxs-lookup"><span data-stu-id="834d8-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="834d8-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="834d8-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="834d8-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="834d8-116">Prerequisites</span></span>
* [<span data-ttu-id="834d8-117">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="834d8-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="834d8-118">Ensure there is a Streaming Endpoint running.</span><span class="sxs-lookup"><span data-stu-id="834d8-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="834d8-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="834d8-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="834d8-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span><span class="sxs-lookup"><span data-stu-id="834d8-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="834d8-121">Launch the tool and connect to your AMS account.</span><span class="sxs-lookup"><span data-stu-id="834d8-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="834d8-122">Tips</span><span class="sxs-lookup"><span data-stu-id="834d8-122">Tips</span></span>
* <span data-ttu-id="834d8-123">Whenever possible, use a hardwired internet connection.</span><span class="sxs-lookup"><span data-stu-id="834d8-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="834d8-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span><span class="sxs-lookup"><span data-stu-id="834d8-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="834d8-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span><span class="sxs-lookup"><span data-stu-id="834d8-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="834d8-126">When using software based encoders, close out any unnecessary programs.</span><span class="sxs-lookup"><span data-stu-id="834d8-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="834d8-127">Create a channel</span><span class="sxs-lookup"><span data-stu-id="834d8-127">Create a channel</span></span>
1. <span data-ttu-id="834d8-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span><span class="sxs-lookup"><span data-stu-id="834d8-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="834d8-129">Select **Create channel…**</span><span class="sxs-lookup"><span data-stu-id="834d8-129">Select **Create channel…**</span></span> <span data-ttu-id="834d8-130">from the menu.</span><span class="sxs-lookup"><span data-stu-id="834d8-130">from the menu.</span></span>

    ![FMLE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="834d8-132">Specify a channel name, the description field is optional.</span><span class="sxs-lookup"><span data-stu-id="834d8-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="834d8-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="834d8-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="834d8-134">You can leave all other settings as is.</span><span class="sxs-lookup"><span data-stu-id="834d8-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="834d8-135">Make sure the **Start the new channel now** is selected.</span><span class="sxs-lookup"><span data-stu-id="834d8-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="834d8-136">Click **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="834d8-136">Click **Create Channel**.</span></span>

   ![FMLE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> The channel can take as long as 20 minutes to start.
>
>

<span data-ttu-id="834d8-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="834d8-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> Note that billing starts as soon as Channel goes into a ready state. For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a><span data-ttu-id="834d8-142">Configure the FMLE encoder</span><span class="sxs-lookup"><span data-stu-id="834d8-142">Configure the FMLE encoder</span></span>
<span data-ttu-id="834d8-143">In this tutorial the following output settings are used.</span><span class="sxs-lookup"><span data-stu-id="834d8-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="834d8-144">The rest of this section describes configuration steps in more detail.</span><span class="sxs-lookup"><span data-stu-id="834d8-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="834d8-145">**Video**:</span><span class="sxs-lookup"><span data-stu-id="834d8-145">**Video**:</span></span>

* <span data-ttu-id="834d8-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="834d8-146">Codec: H.264</span></span>
* <span data-ttu-id="834d8-147">Profile: High (Level 4.0)</span><span class="sxs-lookup"><span data-stu-id="834d8-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="834d8-148">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="834d8-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="834d8-149">Keyframe: 2 seconds (60 seconds)</span><span class="sxs-lookup"><span data-stu-id="834d8-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="834d8-150">Frame Rate: 30</span><span class="sxs-lookup"><span data-stu-id="834d8-150">Frame Rate: 30</span></span>

<span data-ttu-id="834d8-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="834d8-151">**Audio**:</span></span>

* <span data-ttu-id="834d8-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="834d8-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="834d8-153">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="834d8-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="834d8-154">Sample Rate: 44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="834d8-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="834d8-155">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="834d8-155">Configuration steps</span></span>
1. <span data-ttu-id="834d8-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span><span class="sxs-lookup"><span data-stu-id="834d8-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="834d8-157">The interface is one main page of settings.</span><span class="sxs-lookup"><span data-stu-id="834d8-157">The interface is one main page of settings.</span></span> <span data-ttu-id="834d8-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span><span class="sxs-lookup"><span data-stu-id="834d8-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="834d8-159">Format: H.264 Frame Rate: 30.00</span><span class="sxs-lookup"><span data-stu-id="834d8-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="834d8-160">Input Size: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="834d8-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="834d8-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span><span class="sxs-lookup"><span data-stu-id="834d8-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="834d8-163">When using interlaced sources, please checkmark the “Deinterlace” option</span><span class="sxs-lookup"><span data-stu-id="834d8-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="834d8-164">Select the wrench icon next to Format, these additional settings should be:</span><span class="sxs-lookup"><span data-stu-id="834d8-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="834d8-165">Profile: Main</span><span class="sxs-lookup"><span data-stu-id="834d8-165">Profile: Main</span></span>
   * <span data-ttu-id="834d8-166">Level: 4.0</span><span class="sxs-lookup"><span data-stu-id="834d8-166">Level: 4.0</span></span>
   * <span data-ttu-id="834d8-167">Keyframe Frequency: 2 seconds</span><span class="sxs-lookup"><span data-stu-id="834d8-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="834d8-169">Set the following important audio setting:</span><span class="sxs-lookup"><span data-stu-id="834d8-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="834d8-170">Format: AAC</span><span class="sxs-lookup"><span data-stu-id="834d8-170">Format: AAC</span></span>
   * <span data-ttu-id="834d8-171">Sample Rate: 44100 Hz</span><span class="sxs-lookup"><span data-stu-id="834d8-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="834d8-172">Bitrate: 192 Kbps</span><span class="sxs-lookup"><span data-stu-id="834d8-172">Bitrate: 192 Kbps</span></span>

     ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="834d8-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="834d8-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="834d8-175">Navigate back to the AMSE tool, and check on the channel completion status.</span><span class="sxs-lookup"><span data-stu-id="834d8-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="834d8-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span><span class="sxs-lookup"><span data-stu-id="834d8-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="834d8-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span><span class="sxs-lookup"><span data-stu-id="834d8-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="834d8-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span><span class="sxs-lookup"><span data-stu-id="834d8-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="834d8-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span><span class="sxs-lookup"><span data-stu-id="834d8-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="834d8-182">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="834d8-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> Before you click **Connect**, you **must** ensure that the Channel is ready.
> Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.
>
>

## <a name="test-playback"></a><span data-ttu-id="834d8-185">Test playback</span><span class="sxs-lookup"><span data-stu-id="834d8-185">Test playback</span></span>

<span data-ttu-id="834d8-186">Navigate to the AMSE tool, and right click the channel to be tested.</span><span class="sxs-lookup"><span data-stu-id="834d8-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="834d8-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="834d8-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="834d8-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span><span class="sxs-lookup"><span data-stu-id="834d8-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="834d8-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span><span class="sxs-lookup"><span data-stu-id="834d8-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="834d8-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span><span class="sxs-lookup"><span data-stu-id="834d8-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="834d8-191">Create a program</span><span class="sxs-lookup"><span data-stu-id="834d8-191">Create a program</span></span>
1. <span data-ttu-id="834d8-192">Once channel playback is confirmed, create a program.</span><span class="sxs-lookup"><span data-stu-id="834d8-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="834d8-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span><span class="sxs-lookup"><span data-stu-id="834d8-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="834d8-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span><span class="sxs-lookup"><span data-stu-id="834d8-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="834d8-196">You can also specify a storage location or leave as the default.</span><span class="sxs-lookup"><span data-stu-id="834d8-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="834d8-197">Check the **Start the Program now** box.</span><span class="sxs-lookup"><span data-stu-id="834d8-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="834d8-198">Click **Create Program**.</span><span class="sxs-lookup"><span data-stu-id="834d8-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    >Program creation takes less time than channel creation.
        
5. <span data-ttu-id="834d8-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="834d8-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="834d8-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span><span class="sxs-lookup"><span data-stu-id="834d8-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="834d8-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span><span class="sxs-lookup"><span data-stu-id="834d8-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="834d8-203">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="834d8-203">Troubleshooting</span></span>
<span data-ttu-id="834d8-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span><span class="sxs-lookup"><span data-stu-id="834d8-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="834d8-205">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="834d8-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="834d8-206">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="834d8-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]









