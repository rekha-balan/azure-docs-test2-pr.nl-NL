---
title: Azure Mobile Engagement iOS SDK Release Notes | Microsoft Docs
description: Latest updates and procedures for iOS SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 6b32e81bb6a714bd0c479c48d6982af4bcc0683d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553073"
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a>Azure Mobile Engagement iOS SDK release notes
## <a name="401-12132016"></a>4.0.1 (12/13/2016)
* Improved log delivery in background.

## <a name="400-09122016"></a>4.0.0 (09/12/2016)
* Fixed notification not actioned on iOS 10 devices.
* Deprecate XCode 7.

## <a name="324-06302016"></a>3.2.4 (06/30/2016)
* Fixed aggregation between technical logs and other logs.

## <a name="323-06072016"></a>3.2.3 (06/07/2016)
* Fixed the bug where delivery feedback is not reported when app is in the background.
* Optimized the sending of technical logs.

## <a name="322-04072016"></a>3.2.2 (04/07/2016)
* Fixed bug on HTTP request cancellation which sometimes leads to crash.

## <a name="321-12112015"></a>3.2.1 (12/11/2015)
* Fixed the delay when a new app instance is triggered by a notification with deep links

## <a name="320-10082015"></a>3.2.0 (10/08/2015)
* Enabled Bitcode in the SDK to make it work with **Xcode 7**.
* Fixed bugs related to in-app notifications.
* Made the in-app notifications more reliable in case of low battery and other such scenarios.
* Removed extra console logs generated by 3rd party library.

## <a name="310-08262015"></a>3.1.0 (08/26/2015)
* Fix iOS 9 compatibility bug with a third party library. It was causing crashes while sending polls results, application information or extra data.

## <a name="300-06192015"></a>3.0.0 (06/19/2015)
* Mobile Engagement uses Silent Push Notifications.
* Dropped support for iOS 4.X. Starting from this version the deployment target of your application must be at least iOS 6.

## <a name="220-05212015"></a>2.2.0 (05/21/2015)
* The Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.

## <a name="210-04242015"></a>2.1.0 (04/24/2015)
* Added Swift compatibility.
* When clicking on a notification, the action URL is now executed right after the application is opened.
* Added missing header file in SDK package.
* Fixed an issue when the Mobile Engagement crash reporter was disabled.

## <a name="200-02172015"></a>2.0.0 (02/17/2015)
* Initial Release of Azure Mobile Engagement
* appId/sdkKey configuration is replaced by a connection string configuration.
* Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.
* Removed API to send and receive messages between devices.
* Security improvements.
* SmartAd tracking removed.
