---
title: Learn about encoders recommended by Azure Media Services | Microsoft Docs
description: Learn about encoders recommended by media services
services: media-services
keywords: encoding;encoders;media
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: d0c5536d2339470eac058250cc14e1f250b86d90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968739"
---
# <a name="recommended-on-premises-encoders"></a>Recommended on-premises encoders
When live streaming with Azure Media Services, you can specify how you want your channel to receive the input stream. If you choose to use an on-prem encoder with a live encoding channel, your encoder should push a high-quality single-bitrate stream as output. If you choose to use an on-prem encoder with a pass through channel, your encoder should push a multi-bitrate stream as output with all desired output qualities. For more information, see [Live streaming with on-prem encoders](media-services-live-streaming-with-onprem-encoders.md).

Azure Media Services recommends using one of following live encoders that have RTMP as output:
- Adobe Flash Media Live Encoder 3.2
- Haivision Makito X HEVC
- Telestream Wirecast 8.1
- Teradek Slice 756
- TriCaster 8000
- Tricaster Mini HD-4

Azure Media Services recommends using one of the following live encoders that have multi-bitrate Smooth Streaming as output:
- Ateme TITAN Live
- Cisco Digital Media Encoder 2200
- Elemental Live
- Envivio 4Caster C4 Gen III
- Imagine Communications Selenio MCP3
- Media Excel Hero Live

> [!NOTE]
> A live encoder can send a single-bitrate stream to a pass through channel, but this configuration is not recommended because it does not allow for adaptive bitrate streaming to the client.

## <a name="how-to-become-an-on-prem-encoder-partner"></a>How to become an on-prem encoder partner
As an Azure Media Services on-prem encoder partner, Media Services promotes your product by recommending your encoder to enterprise customers. To become an on-prem encoder partner, you must verify compatibility of your on-prem encoder with Media Services. To do so, complete the following verifications:

Pass through channel verification
1. Create or visit your Azure Media Services account
2. Create and start a **pass-through** channel
3. Configure your encoder to push a multi-bitrate live stream.
4. Create a published live event
5. Run your live encoder for approximately 10 minutes
6. Stop the live event
7. Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder
8. Reset the channel state after creating each sample
9. Repeat steps 3 through 8 for all configurations supported by your encoder (with and without ad signaling/captions/different encoding speeds)

Live encoding channel verification
1. Create or visit your Azure Media Services account
2. Create and start a **live encoding** channel
3. Configure your encoder to push a single-bitrate live stream.
4. Create a published live event
5. Run your live encoder for approximately 10 minutes
6. Stop the live event
7. Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder
8. Reset the channel state after creating each sample
9. Repeat steps 3 through 8 for all configurations supported by your encoder (with and without ad signaling/captions/various encoding speeds)

Longevity verification
1. Create or visit your Azure Media Services account
2. Create and start a **pass-through** channel
3. Configure your encoder to push a multi-bitrate live stream.
4. Create a published live event
5. Run your live encoder for one week or longer
6. Stop the live event
7. Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder

Lastly, send your recorded settings and live archive parameters to Media Services by emailing amsstreaming@microsoft.com. Upon receipt, Media Services performs verification tests on the samples from your live encoder. You can contact the Media Services with any questions regarding this process.