---
title: Azure RemoteApp network bandwidth - general guidelines | Microsoft Docs
description: Understand some basic network bandwidth guidelines for your Azure RemoteApp collections and apps.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: df3586781ca7ebaaf574a877b96887187add0222
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555260"
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="273c6-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span><span class="sxs-lookup"><span data-stu-id="273c6-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="273c6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="273c6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="273c6-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="273c6-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="273c6-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span><span class="sxs-lookup"><span data-stu-id="273c6-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="273c6-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span><span class="sxs-lookup"><span data-stu-id="273c6-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="273c6-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span><span class="sxs-lookup"><span data-stu-id="273c6-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="273c6-109">Complex PowerPoint, simple PowerPoint</span><span class="sxs-lookup"><span data-stu-id="273c6-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="273c6-110">Azure RemoteApp does best on 100 MB LAN.</span><span class="sxs-lookup"><span data-stu-id="273c6-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="273c6-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span><span class="sxs-lookup"><span data-stu-id="273c6-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="273c6-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span><span class="sxs-lookup"><span data-stu-id="273c6-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="273c6-113">Internet Explorer, mixed PDF, PDF, Text</span><span class="sxs-lookup"><span data-stu-id="273c6-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="273c6-114">10 MB/s network profile is close to LAN in most aspects.</span><span class="sxs-lookup"><span data-stu-id="273c6-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="273c6-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span><span class="sxs-lookup"><span data-stu-id="273c6-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="273c6-116">Flash video (YouTube)</span><span class="sxs-lookup"><span data-stu-id="273c6-116">Flash video (YouTube)</span></span>
<span data-ttu-id="273c6-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span><span class="sxs-lookup"><span data-stu-id="273c6-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="273c6-118">At 1 MB/s, jitter is very high and noticeable.</span><span class="sxs-lookup"><span data-stu-id="273c6-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="273c6-119">Word typing (Word remote input)</span><span class="sxs-lookup"><span data-stu-id="273c6-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="273c6-120">This is a low-bandwidth usage scenario.</span><span class="sxs-lookup"><span data-stu-id="273c6-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="273c6-121">At 256 KB/s we provide as good of an experience as LAN.</span><span class="sxs-lookup"><span data-stu-id="273c6-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="273c6-122">Learn more</span><span class="sxs-lookup"><span data-stu-id="273c6-122">Learn more</span></span>
* [<span data-ttu-id="273c6-123">Estimate Azure RemoteApp network bandwidth usage</span><span class="sxs-lookup"><span data-stu-id="273c6-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="273c6-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span><span class="sxs-lookup"><span data-stu-id="273c6-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="273c6-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span><span class="sxs-lookup"><span data-stu-id="273c6-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

