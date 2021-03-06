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
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a>Use the FMLE encoder to send a single bitrate live stream
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding. For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool. This tool only runs on Windows PC. If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).

Note that this tutorial describes using AAC. However, FMLE doesn’t supports AAC by default. You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)

## <a name="prerequisites"></a>Prerequisites
* [Create an Azure Media Services account](media-services-portal-create-account.md)
* Ensure there is a Streaming Endpoint running. For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)
* Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.
* Launch the tool and connect to your AMS account.

## <a name="tips"></a>Tips
* Whenever possible, use a hardwired internet connection.
* A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates. While this is not a mandatory requirement, it will help mitigate the impact of network congestion.
* When using software based encoders, close out any unnecessary programs.

## <a name="create-a-channel"></a>Create a channel
1. In the AMSE tool, navigate to the **Live** tab, and right click within the channel area. Select **Create channel…** from the menu.

    ![FMLE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. Specify a channel name, the description field is optional. Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**. You can leave all other settings as is.

    Make sure the **Start the new channel now** is selected.

3. Click **Create Channel**.

   ![FMLE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> The channel can take as long as 20 minutes to start.
>
>

While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).

> [!IMPORTANT]
> Note that billing starts as soon as Channel goes into a ready state. For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a>Configure the FMLE encoder
In this tutorial the following output settings are used. The rest of this section describes configuration steps in more detail.

**Video**:

* Codec: H.264
* Profile: High (Level 4.0)
* Bitrate: 5000 kbps
* Keyframe: 2 seconds (60 seconds)
* Frame Rate: 30

**Audio**:

* Codec: AAC (LC)
* Bitrate: 192 kbps
* Sample Rate: 44.1 kHz

### <a name="configuration-steps"></a>Configuration steps
1. Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.

    The interface is one main page of settings. Please take note of the following recommended settings to get started with streaming using FMLE.

   * Format: H.264 Frame Rate: 30.00
   * Input Size: 1280 x 720
   * Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)  

     ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle3.png)

     When using interlaced sources, please checkmark the “Deinterlace” option
2. Select the wrench icon next to Format, these additional settings should be:

   * Profile: Main
   * Level: 4.0
   * Keyframe Frequency: 2 seconds

     ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. Set the following important audio setting:

   * Format: AAC
   * Sample Rate: 44100 Hz
   * Bitrate: 192 Kbps

     ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.

    Navigate back to the AMSE tool, and check on the channel completion status. Once the State has changed from **Starting** to **Running**, you can get the input URL.

    When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.  

    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. Paste this information in the **FMS URL** field of the output section, and assign a stream name.

    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle7.png)

    For extra redundancy, repeat these steps with the Secondary Input URL.
6. Select **Connect**.

> [!IMPORTANT]
> Before you click **Connect**, you **must** ensure that the Channel is ready.
> Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.
>
>

## <a name="test-playback"></a>Test playback

Navigate to the AMSE tool, and right click the channel to be tested. From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.  

    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle8.png)

If the stream appears in the player, then the encoder has been properly configured to connect to AMS.

If an error is received, the channel will need to be reset and encoder settings adjusted. Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.  

## <a name="create-a-program"></a>Create a program
1. Once channel playback is confirmed, create a program. Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.  

    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours). You can also specify a storage location or leave as the default.  
3. Check the **Start the Program now** box.
4. Click **Create Program**.  

    >[!NOTE]
    >Program creation takes less time than channel creation.
        
5. Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.  
6. Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).

The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.  

## <a name="troubleshooting"></a>Troubleshooting
Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]









