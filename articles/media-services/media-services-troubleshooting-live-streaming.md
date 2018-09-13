---
title: Troubleshooting guide for live streaming | Microsoft Docs
description: This topic gives suggestions on how to troubleshoot live streaming problems.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/12/2016
ms.author: juliako
ms.openlocfilehash: fe66d144006073fe9241f5e1360a0587dfb25204
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548787"
---
# <a name="troubleshooting-guide-for-live-streaming"></a>Troubleshooting guide for live streaming
This topic gives suggestions on how to troubleshoot some live streaming problems.

## <a name="issues-related-to-on-premises-encoders"></a>Issues related to on-premises encoders
This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.

### <a name="problem-would-like-to-see-logs"></a>Problem: Would like to see logs
* **Potential issue**: Can't find encoder logs that might help in debugging issues.
  
  * **Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\ 
  * **Elemental Live**: You can find has links to logs on the management portal. Click on **Stats**, then **Logs**. On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session. 
  * **Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Problem: There is no option for outputting a progressive stream
* **Potential issue**: The encoder being used doesn't automatically deinterlace. 
  
    **Troubleshooting steps**: Look for a de-interlacing option within the encoder interface. Once de-interlacing is enabled, check again for progressive output settings. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a>Problem: Tried several encoder output settings and still unable to connect.
* **Potential issue**: Azure encoding channel was not properly reset. 
  
    **Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel. Once running again, try connecting your encoder with the new settings. If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.  
* **Potential issue**: The GOP size or key frame settings are not optimal. 
  
    **Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds. Some encoders calculate this setting in number of frames, while others use seconds. For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.  
* **Potential issue**: Closed ports are blocking the stream. 
  
    **Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open. When using RTP streaming, confirm that outbound port 2010 is open. 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a>Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.
* **Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.  
  
    **Troubleshooting steps**: To find the IP address, open a command prompt on any computer. To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.  
  
    Once the command prompt is open, type "Ping [AMS Host Name]". 
  
    The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example: 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.
> 
> 

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


