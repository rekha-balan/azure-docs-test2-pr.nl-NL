---
title: Use existing players to playback your content - Azure | Microsoft Docs
description: This topic lists existing players that you can use to playback your content.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2018
ms.author: juliako
ms.openlocfilehash: 3fe82b98163182c73a144b72da371e8aa195e8cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867263"
---
# <a name="playing-your-content-with-existing-players"></a>Playing your content with existing players
Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash. This topic points you to existing players that you can use to test your streams.

### <a name="the-azure-portal-media-services-content-player"></a>The Azure portal Media Services content player
The **Azure** portal provides a content player that you can use to test your video.

Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.

Some considerations apply:

* The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint. If you want to play from a non-default streaming endpoint, use another player. For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure Media Player
Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:

* Smooth Streaming
* MPEG DASH
* HLS
* Progressive MP4

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>AES-encrypted with Token
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Silverlight Players

#### <a name="playready-with-token"></a>PlayReady with Token
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>DASH Players
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>Other
To test HLS URLs you can also use:

* **Safari** on an iOS device or
* **3ivx HLS Player** on Windows.

## <a name="developing-video-players"></a>Developing video players
For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
