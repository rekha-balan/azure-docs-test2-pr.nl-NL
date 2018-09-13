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
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.

If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment. (Although, as discussed, this will not guarantee a better than average user experience.)

## <a name="complex-powerpoint-simple-powerpoint"></a>Complex PowerPoint, simple PowerPoint
Azure RemoteApp does best on 100 MB LAN. At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience. At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, mixed PDF, PDF, Text
10 MB/s network profile is close to LAN in most aspects. 1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.

## <a name="flash-video-youtube"></a>Flash video (YouTube)
100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases). At 1 MB/s, jitter is very high and noticeable.

## <a name="word-typing-word-remote-input"></a>Word typing (Word remote input)
This is a low-bandwidth usage scenario. At 256 KB/s we provide as good of an experience as LAN.

## <a name="learn-more"></a>Learn more
* [Estimate Azure RemoteApp network bandwidth usage](remoteapp-bandwidth.md)
* [Azure RemoteApp - how do network bandwidth and quality of experience work together?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp - tseting your network bandwidth usage with some common scenarios](remoteapp-bandwidthtests.md)

