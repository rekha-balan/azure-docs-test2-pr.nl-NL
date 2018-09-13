---
title: Use existing players to playback your content - Azure | Microsoft Docs
description: This topic lists existing players that you can use to playback your content.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 0ffb5b634b917459db370ce73692aa79a006e95b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550318"
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="d705d-103">Playing your content with existing players</span><span class="sxs-lookup"><span data-stu-id="d705d-103">Playing your content with existing players</span></span>
<span data-ttu-id="d705d-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span><span class="sxs-lookup"><span data-stu-id="d705d-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="d705d-105">This topic points you to existing players that you can use to test your streams.</span><span class="sxs-lookup"><span data-stu-id="d705d-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="d705d-106">The Azure portal Media Services content player</span><span class="sxs-lookup"><span data-stu-id="d705d-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="d705d-107">The **Azure** portal provides a content player that you can use to test your video.</span><span class="sxs-lookup"><span data-stu-id="d705d-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="d705d-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span><span class="sxs-lookup"><span data-stu-id="d705d-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="d705d-109">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="d705d-109">Some considerations apply:</span></span>

* <span data-ttu-id="d705d-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="d705d-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="d705d-111">If you want to play from a non-default streaming endpoint, use another player.</span><span class="sxs-lookup"><span data-stu-id="d705d-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="d705d-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d705d-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="d705d-114">Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="d705d-114">Azure Media Player</span></span>
<span data-ttu-id="d705d-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span><span class="sxs-lookup"><span data-stu-id="d705d-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="d705d-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="d705d-116">Smooth Streaming</span></span>
* <span data-ttu-id="d705d-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="d705d-117">MPEG DASH</span></span>
* <span data-ttu-id="d705d-118">HLS</span><span class="sxs-lookup"><span data-stu-id="d705d-118">HLS</span></span>
* <span data-ttu-id="d705d-119">Progressive MP4</span><span class="sxs-lookup"><span data-stu-id="d705d-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="d705d-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="d705d-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="d705d-121">AES-encrypted with Token</span><span class="sxs-lookup"><span data-stu-id="d705d-121">AES-encrypted with Token</span></span>
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="d705d-122">Silverlight Players</span><span class="sxs-lookup"><span data-stu-id="d705d-122">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="d705d-123">Monitoring</span><span class="sxs-lookup"><span data-stu-id="d705d-123">Monitoring</span></span>
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="d705d-124">PlayReady with Token</span><span class="sxs-lookup"><span data-stu-id="d705d-124">PlayReady with Token</span></span>
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="d705d-125">DASH Players</span><span class="sxs-lookup"><span data-stu-id="d705d-125">DASH Players</span></span>
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a><span data-ttu-id="d705d-126">Other</span><span class="sxs-lookup"><span data-stu-id="d705d-126">Other</span></span>
<span data-ttu-id="d705d-127">To test HLS URLs you can also use:</span><span class="sxs-lookup"><span data-stu-id="d705d-127">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="d705d-128">**Safari** on an iOS device or</span><span class="sxs-lookup"><span data-stu-id="d705d-128">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="d705d-129">**3ivx HLS Player** on Windows.</span><span class="sxs-lookup"><span data-stu-id="d705d-129">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="d705d-130">Developing video players</span><span class="sxs-lookup"><span data-stu-id="d705d-130">Developing video players</span></span>
<span data-ttu-id="d705d-131">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="d705d-131">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d705d-132">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d705d-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d705d-133">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d705d-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-playback-content-with-existing-players/media-services-portal-player.png

