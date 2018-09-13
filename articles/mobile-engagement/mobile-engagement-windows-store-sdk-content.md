---
title: Windows Universal Apps SDK content
description: Learn about the contents of the Windows Universal Apps SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555261"
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="066df-103">Windows Universal Apps SDK content</span><span class="sxs-lookup"><span data-stu-id="066df-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="066df-104">This document lists and describes the content deployed by the SDK in your application.</span><span class="sxs-lookup"><span data-stu-id="066df-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="066df-105">The `/Resources` folder</span><span class="sxs-lookup"><span data-stu-id="066df-105">The `/Resources` folder</span></span>
<span data-ttu-id="066df-106">This folder contains all the resources that Mobile Engagement needs.</span><span class="sxs-lookup"><span data-stu-id="066df-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="066df-107">You can also customize them to fit your app.</span><span class="sxs-lookup"><span data-stu-id="066df-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="066df-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span><span class="sxs-lookup"><span data-stu-id="066df-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="066df-109">/html folder</span><span class="sxs-lookup"><span data-stu-id="066df-109">/html folder</span></span>
* <span data-ttu-id="066df-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span><span class="sxs-lookup"><span data-stu-id="066df-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="066df-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span><span class="sxs-lookup"><span data-stu-id="066df-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="066df-112">/images folder</span><span class="sxs-lookup"><span data-stu-id="066df-112">/images folder</span></span>
* <span data-ttu-id="066df-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span><span class="sxs-lookup"><span data-stu-id="066df-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="066df-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span><span class="sxs-lookup"><span data-stu-id="066df-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="066df-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span><span class="sxs-lookup"><span data-stu-id="066df-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="066df-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span><span class="sxs-lookup"><span data-stu-id="066df-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="066df-117">/overlay folder</span><span class="sxs-lookup"><span data-stu-id="066df-117">/overlay folder</span></span>
* <span data-ttu-id="066df-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span><span class="sxs-lookup"><span data-stu-id="066df-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>

