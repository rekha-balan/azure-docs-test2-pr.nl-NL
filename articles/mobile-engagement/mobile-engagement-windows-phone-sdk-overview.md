---
title: Azure Mobile Engagement Windows Phone Silverlight SDK Overview | Microsoft Docs
description: Overview of the Windows Phone Silverlight SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: c4e8ceee4104c3d3a6c3e6b79322ba1cf8463b22
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549736"
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Windows Phone Silverlight SDK Overview for Azure Mobile Engagement
Start here to get the details on how to integrate Azure Mobile Engagement in a Windows Phone Silverlight App. If you'd like to give it a try first, make sure you complete our [15 minutes tutorial](mobile-engagement-windows-phone-get-started.md).

Click to see the [SDK Content](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Integration procedures
1. Start here: [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md)
2. For Notifications: [How to integrate Reach (Notifications) in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Release notes
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Part of the *MicrosoftAzure.MobileEngagement* Nuget package **v3.4.1**

* Stability improvements.

For earlier version please see the [complete release notes](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Upgrade procedures
If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.

You may have to follow several procedures if you missed several versions of the SDK. See the complete [Upgrade Procedures](mobile-engagement-windows-phone-upgrade-procedure.md). For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.

### <a name="from-200-to-330"></a>From 2.0.0 to 3.3.0
#### <a name="test-logs"></a>Test logs
Console logs produced by the SDK can now be enabled/disabled/filtered. To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Upgrade from older versions
See [Upgrade Procedures](mobile-engagement-windows-phone-upgrade-procedure.md)

