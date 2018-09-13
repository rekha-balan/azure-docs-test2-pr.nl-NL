---
title: Configure the Haivision KB encoder to send a single bitrate live stream to Azure | Microsoft Docs
description: This topic shows how to configure the Haivision KB live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.
services: media-services
documentationcenter: ''
author: dbgeorge
manager: vsood
editor: ''
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 02/02/2018
ms.author: juliako;dbgeorge
ms.openlocfilehash: a36e12080cbbcb1a98bf786a6634959362cb52a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871525"
---
# <a name="use-the-haivision-kb-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="cf45f-103">Use the Haivision KB live encoder to send a single bitrate live stream</span><span class="sxs-lookup"><span data-stu-id="cf45f-103">Use the Haivision KB live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Haivision](media-services-configure-kb-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)

<span data-ttu-id="cf45f-108">This topic shows how to configure the [Havision KB live encoder](https://www.haivision.com/products/kb-series/) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="cf45f-108">This topic shows how to configure the [Havision KB live encoder](https://www.haivision.com/products/kb-series/) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="cf45f-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="cf45f-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="cf45f-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span><span class="sxs-lookup"><span data-stu-id="cf45f-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="cf45f-111">This tool only runs on Windows PC.</span><span class="sxs-lookup"><span data-stu-id="cf45f-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="cf45f-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="cf45f-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf45f-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cf45f-113">Prerequisites</span></span>
*   <span data-ttu-id="cf45f-114">Access to a Haivision KB encoder, running SW v5.01, or greater.</span><span class="sxs-lookup"><span data-stu-id="cf45f-114">Access to a Haivision KB encoder, running SW v5.01, or greater.</span></span>
* [<span data-ttu-id="cf45f-115">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="cf45f-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="cf45f-116">Ensure there is a Streaming Endpoint running.</span><span class="sxs-lookup"><span data-stu-id="cf45f-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="cf45f-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="cf45f-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="cf45f-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span><span class="sxs-lookup"><span data-stu-id="cf45f-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="cf45f-119">Launch the tool and connect to your AMS account.</span><span class="sxs-lookup"><span data-stu-id="cf45f-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="cf45f-120">Tips</span><span class="sxs-lookup"><span data-stu-id="cf45f-120">Tips</span></span>
* <span data-ttu-id="cf45f-121">Whenever possible, use a hardwired internet connection.</span><span class="sxs-lookup"><span data-stu-id="cf45f-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="cf45f-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span><span class="sxs-lookup"><span data-stu-id="cf45f-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="cf45f-123">While this is not a mandatory requirement, it helps mitigate the impact of network congestion.</span><span class="sxs-lookup"><span data-stu-id="cf45f-123">While this is not a mandatory requirement, it helps mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="cf45f-124">When using software-based encoders, close out any unnecessary programs.</span><span class="sxs-lookup"><span data-stu-id="cf45f-124">When using software-based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="cf45f-125">Create a channel</span><span class="sxs-lookup"><span data-stu-id="cf45f-125">Create a channel</span></span>
1. <span data-ttu-id="cf45f-126">In the AMSE tool, navigate to the **Live** tab, and right-click within the channel area.</span><span class="sxs-lookup"><span data-stu-id="cf45f-126">In the AMSE tool, navigate to the **Live** tab, and right-click within the channel area.</span></span> <span data-ttu-id="cf45f-127">Select **Create channel…**</span><span class="sxs-lookup"><span data-stu-id="cf45f-127">Select **Create channel…**</span></span> <span data-ttu-id="cf45f-128">from the menu.</span><span class="sxs-lookup"><span data-stu-id="cf45f-128">from the menu.</span></span>
[<span data-ttu-id="cf45f-129">Haivision</span><span class="sxs-lookup"><span data-stu-id="cf45f-129">Haivision</span></span>](./media/media-services-configure-kb-live-encoder/channel.png)
2. <span data-ttu-id="cf45f-130">Specify a channel name, the description field is optional.</span><span class="sxs-lookup"><span data-stu-id="cf45f-130">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="cf45f-131">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="cf45f-131">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="cf45f-132">You can leave all other settings as is.</span><span class="sxs-lookup"><span data-stu-id="cf45f-132">You can leave all other settings as is.</span></span> <span data-ttu-id="cf45f-133">Make sure the **Start the new channel now** is selected.</span><span class="sxs-lookup"><span data-stu-id="cf45f-133">Make sure the **Start the new channel now** is selected.</span></span>
3. <span data-ttu-id="cf45f-134">Click **Create Channel**.</span><span class="sxs-lookup"><span data-stu-id="cf45f-134">Click **Create Channel**.</span></span>
[<span data-ttu-id="cf45f-135">Haivision</span><span class="sxs-lookup"><span data-stu-id="cf45f-135">Haivision</span></span>](./media/media-services-configure-kb-live-encoder/livechannel.png)

> [!NOTE]
> The channel can take as long as 20 minutes to start.

## <a name="configure-the-haivision-kb-encoder"></a><span data-ttu-id="cf45f-137">Configure the Haivision KB encoder</span><span class="sxs-lookup"><span data-stu-id="cf45f-137">Configure the Haivision KB encoder</span></span>
<span data-ttu-id="cf45f-138">In this tutorial, the following output settings are used.</span><span class="sxs-lookup"><span data-stu-id="cf45f-138">In this tutorial, the following output settings are used.</span></span> <span data-ttu-id="cf45f-139">The rest of this section describes configuration steps in more detail.</span><span class="sxs-lookup"><span data-stu-id="cf45f-139">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="cf45f-140">Video:</span><span class="sxs-lookup"><span data-stu-id="cf45f-140">Video:</span></span>
-   <span data-ttu-id="cf45f-141">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="cf45f-141">Codec: H.264</span></span>
-   <span data-ttu-id="cf45f-142">Profile: High (Level 4.0)</span><span class="sxs-lookup"><span data-stu-id="cf45f-142">Profile: High (Level 4.0)</span></span>
-   <span data-ttu-id="cf45f-143">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="cf45f-143">Bitrate: 5000 kbps</span></span>
-   <span data-ttu-id="cf45f-144">Keyframe: 2 seconds (60 seconds)</span><span class="sxs-lookup"><span data-stu-id="cf45f-144">Keyframe: 2 seconds (60 seconds)</span></span>
-   <span data-ttu-id="cf45f-145">Frame Rate: 30</span><span class="sxs-lookup"><span data-stu-id="cf45f-145">Frame Rate: 30</span></span>

<span data-ttu-id="cf45f-146">Audio:</span><span class="sxs-lookup"><span data-stu-id="cf45f-146">Audio:</span></span>
-   <span data-ttu-id="cf45f-147">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="cf45f-147">Codec: AAC (LC)</span></span>
-   <span data-ttu-id="cf45f-148">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="cf45f-148">Bitrate: 192 kbps</span></span>
-   <span data-ttu-id="cf45f-149">Sample Rate: 44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="cf45f-149">Sample Rate: 44.1 kHz</span></span>

## <a name="configuration-steps"></a><span data-ttu-id="cf45f-150">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="cf45f-150">Configuration steps</span></span>
1.  <span data-ttu-id="cf45f-151">Log in to the Haivision KB user interface.</span><span class="sxs-lookup"><span data-stu-id="cf45f-151">Log in to the Haivision KB user interface.</span></span>
2.  <span data-ttu-id="cf45f-152">Click on the **Menu Button** in the channel control center and select **Add Channel**</span><span class="sxs-lookup"><span data-stu-id="cf45f-152">Click on the **Menu Button** in the channel control center and select **Add Channel**</span></span>  
    <span data-ttu-id="cf45f-153">![Screen Shot 2017-08-14 at 9.15.09 AM.png](./media/media-services-configure-kb-live-encoder/step2.png)</span><span class="sxs-lookup"><span data-stu-id="cf45f-153">![Screen Shot 2017-08-14 at 9.15.09 AM.png](./media/media-services-configure-kb-live-encoder/step2.png)</span></span>
3.  <span data-ttu-id="cf45f-154">Type the **Channel Name** in the Name field and click next.</span><span class="sxs-lookup"><span data-stu-id="cf45f-154">Type the **Channel Name** in the Name field and click next.</span></span>  
    <span data-ttu-id="cf45f-155">![Screen Shot 2017-08-14 at 9.19.07 AM.png](./media/media-services-configure-kb-live-encoder/step3.png)</span><span class="sxs-lookup"><span data-stu-id="cf45f-155">![Screen Shot 2017-08-14 at 9.19.07 AM.png](./media/media-services-configure-kb-live-encoder/step3.png)</span></span>
4.  <span data-ttu-id="cf45f-156">Select the **Channel Input Source** from the **Input Source** drop-down and click next.</span><span class="sxs-lookup"><span data-stu-id="cf45f-156">Select the **Channel Input Source** from the **Input Source** drop-down and click next.</span></span>
    <span data-ttu-id="cf45f-157">![Screen Shot 2017-08-14 at 9.20.44 AM.png](./media/media-services-configure-kb-live-encoder/step4.png)</span><span class="sxs-lookup"><span data-stu-id="cf45f-157">![Screen Shot 2017-08-14 at 9.20.44 AM.png](./media/media-services-configure-kb-live-encoder/step4.png)</span></span>
5.  <span data-ttu-id="cf45f-158">From the **Encoder Template** drop-down choose **H264-720-AAC-192** and click next.</span><span class="sxs-lookup"><span data-stu-id="cf45f-158">From the **Encoder Template** drop-down choose **H264-720-AAC-192** and click next.</span></span>
    <span data-ttu-id="cf45f-159">![Screen Shot 2017-08-14 at 9.23.15 AM.png](./media/media-services-configure-kb-live-encoder/step5.png)</span><span class="sxs-lookup"><span data-stu-id="cf45f-159">![Screen Shot 2017-08-14 at 9.23.15 AM.png](./media/media-services-configure-kb-live-encoder/step5.png)</span></span>
6.  <span data-ttu-id="cf45f-160">From the **Select New Output** drop-down choose **RTMP** and click next.</span><span class="sxs-lookup"><span data-stu-id="cf45f-160">From the **Select New Output** drop-down choose **RTMP** and click next.</span></span>  
    <span data-ttu-id="cf45f-161">![Screen Shot 2017-08-14 at 9.27.51 AM.png](./media/media-services-configure-kb-live-encoder/step6.png)</span><span class="sxs-lookup"><span data-stu-id="cf45f-161">![Screen Shot 2017-08-14 at 9.27.51 AM.png](./media/media-services-configure-kb-live-encoder/step6.png)</span></span>
7.  <span data-ttu-id="cf45f-162">From the **Channel Output** window, populate the Azure stream information.</span><span class="sxs-lookup"><span data-stu-id="cf45f-162">From the **Channel Output** window, populate the Azure stream information.</span></span> <span data-ttu-id="cf45f-163">Paste the **RTMP** link from the initial channel setup in the **Server** area.</span><span class="sxs-lookup"><span data-stu-id="cf45f-163">Paste the **RTMP** link from the initial channel setup in the **Server** area.</span></span> <span data-ttu-id="cf45f-164">In the **Output Name** area type in the name of the channel.</span><span class="sxs-lookup"><span data-stu-id="cf45f-164">In the **Output Name** area type in the name of the channel.</span></span> <span data-ttu-id="cf45f-165">In the Stream Name Template area, use the template RTMPStreamName_%video_bitrate% to name the stream.</span><span class="sxs-lookup"><span data-stu-id="cf45f-165">In the Stream Name Template area, use the template RTMPStreamName_%video_bitrate% to name the stream.</span></span>
    <span data-ttu-id="cf45f-166">![Screen Shot 2017-08-14 at 9.33.17 AM.png](./media/media-services-configure-kb-live-encoder/step7.png)</span><span class="sxs-lookup"><span data-stu-id="cf45f-166">![Screen Shot 2017-08-14 at 9.33.17 AM.png](./media/media-services-configure-kb-live-encoder/step7.png)</span></span>
8.  <span data-ttu-id="cf45f-167">Click next and then click Done.</span><span class="sxs-lookup"><span data-stu-id="cf45f-167">Click next and then click Done.</span></span>
9.  <span data-ttu-id="cf45f-168">Click the **Play Button** to start the encoder channel.</span><span class="sxs-lookup"><span data-stu-id="cf45f-168">Click the **Play Button** to start the encoder channel.</span></span>  
    <span data-ttu-id="cf45f-169">![Haivision KB.png](./media/media-services-configure-kb-live-encoder/step9.png)</span><span class="sxs-lookup"><span data-stu-id="cf45f-169">![Haivision KB.png](./media/media-services-configure-kb-live-encoder/step9.png)</span></span>

## <a name="test-playback"></a><span data-ttu-id="cf45f-170">Test playback</span><span class="sxs-lookup"><span data-stu-id="cf45f-170">Test playback</span></span>
<span data-ttu-id="cf45f-171">Navigate to the AMSE tool, and right-click the channel to be tested.</span><span class="sxs-lookup"><span data-stu-id="cf45f-171">Navigate to the AMSE tool, and right-click the channel to be tested.</span></span> <span data-ttu-id="cf45f-172">From the menu, hover over Playback the Preview and select with Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="cf45f-172">From the menu, hover over Playback the Preview and select with Azure Media Player.</span></span>

<span data-ttu-id="cf45f-173">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span><span class="sxs-lookup"><span data-stu-id="cf45f-173">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="cf45f-174">If an error is received, the channel needs to be reset and encoder settings adjusted.</span><span class="sxs-lookup"><span data-stu-id="cf45f-174">If an error is received, the channel needs to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="cf45f-175">See the troubleshooting article for guidance.</span><span class="sxs-lookup"><span data-stu-id="cf45f-175">See the troubleshooting article for guidance.</span></span>

## <a name="create-a-program"></a><span data-ttu-id="cf45f-176">Create a program</span><span class="sxs-lookup"><span data-stu-id="cf45f-176">Create a program</span></span>
1.  <span data-ttu-id="cf45f-177">Once channel playback is confirmed, create a program.</span><span class="sxs-lookup"><span data-stu-id="cf45f-177">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="cf45f-178">Under the Live tab in the AMSE tool, right-click within the program area and select Create New Program.</span><span class="sxs-lookup"><span data-stu-id="cf45f-178">Under the Live tab in the AMSE tool, right-click within the program area and select Create New Program.</span></span>
[<span data-ttu-id="cf45f-179">Haivision</span><span class="sxs-lookup"><span data-stu-id="cf45f-179">Haivision</span></span>](./media/media-services-configure-kb-live-encoder/program.png)
1.  <span data-ttu-id="cf45f-180">Name the program and, if needed, adjust the Archive Window Length (which defaults to four hours).</span><span class="sxs-lookup"><span data-stu-id="cf45f-180">Name the program and, if needed, adjust the Archive Window Length (which defaults to four hours).</span></span> <span data-ttu-id="cf45f-181">You can also specify a storage location or leave as the default.</span><span class="sxs-lookup"><span data-stu-id="cf45f-181">You can also specify a storage location or leave as the default.</span></span>
2.  <span data-ttu-id="cf45f-182">Check the Start the Program now box.</span><span class="sxs-lookup"><span data-stu-id="cf45f-182">Check the Start the Program now box.</span></span>
3.  <span data-ttu-id="cf45f-183">Click Create Program.</span><span class="sxs-lookup"><span data-stu-id="cf45f-183">Click Create Program.</span></span>
4.  <span data-ttu-id="cf45f-184">Once the program is running, confirm playback by right-clicking the program and navigating to Play back the program(s) and then selecting with Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="cf45f-184">Once the program is running, confirm playback by right-clicking the program and navigating to Play back the program(s) and then selecting with Azure Media Player.</span></span>
5.  <span data-ttu-id="cf45f-185">Once confirmed, right-click the program again and select Copy the Output URL to Clipboard (or retrieve this information from the Program information and settings option from the menu).</span><span class="sxs-lookup"><span data-stu-id="cf45f-185">Once confirmed, right-click the program again and select Copy the Output URL to Clipboard (or retrieve this information from the Program information and settings option from the menu).</span></span>

<span data-ttu-id="cf45f-186">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span><span class="sxs-lookup"><span data-stu-id="cf45f-186">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>

> [!NOTE]
> Program creation takes less time than channel creation.