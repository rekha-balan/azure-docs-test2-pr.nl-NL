---
title: Using partners to deliver Widevine licenses to Azure Media Services | Microsoft Docs
description: This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs. The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by castLabs license server.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 688356323f5c8cc8c59078c9fb060aaa1dcac91f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554756"
---
# <a name="using-partners-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="d9d0b-104">Using partners to deliver Widevine licenses to Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="d9d0b-104">Using partners to deliver Widevine licenses to Azure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="d9d0b-105">Overview</span><span class="sxs-lookup"><span data-stu-id="d9d0b-105">Overview</span></span>
<span data-ttu-id="d9d0b-106">Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.</span><span class="sxs-lookup"><span data-stu-id="d9d0b-106">Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="d9d0b-107">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="d9d0b-107">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="d9d0b-108">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="d9d0b-108">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="d9d0b-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="d9d0b-109">castLabs</span></span>
<span data-ttu-id="d9d0b-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="d9d0b-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses.</span></span> <span data-ttu-id="d9d0b-111">For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="d9d0b-111">For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="d9d0b-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="d9d0b-112">Axinom</span></span>
<span data-ttu-id="d9d0b-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) to deliver Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="d9d0b-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) to deliver Widevine licenses.</span></span> <span data-ttu-id="d9d0b-114">For more information, see [Using Axinom to deliver DRM licenses to Azure Media Services](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="d9d0b-114">For more information, see [Using Axinom to deliver DRM licenses to Azure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d9d0b-115">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d9d0b-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d9d0b-116">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d9d0b-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d9d0b-117">See also</span><span class="sxs-lookup"><span data-stu-id="d9d0b-117">See also</span></span>
[<span data-ttu-id="d9d0b-118">Using PlayReady and/or Widevine dynamic common encryption</span><span class="sxs-lookup"><span data-stu-id="d9d0b-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="d9d0b-119">Mingfei’s blog</span><span class="sxs-lookup"><span data-stu-id="d9d0b-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

