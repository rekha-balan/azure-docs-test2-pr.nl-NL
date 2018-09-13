---
title: Azure Mobile Engagement Windows Universal SDK Integration | Microsoft Docs
description: Windows Universal Integration for SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: d616ad58156a19e89b3e106639a38df67cbd0abb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671644"
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Windows Universal SDK Integration for Azure Mobile Engagement
This document describes all the integration and configuration options available for the Azure Mobile Engagement Windows Universal SDK.

## <a name="prerequisites"></a>Prerequisites
Before starting this tutorial, you must first complete our [15-minute tutorial](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="advanced-features"></a>Advanced features
### <a name="reporting-features"></a>Reporting features
You can add these features:

1. [Advanced reporting options](mobile-engagement-windows-store-advanced-reporting.md)
2. [Advanced configuration options](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Notifications
[How to integrate Reach (Notifications) in your Windows Universal app](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Tag plan implementation:
[How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Release notes
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* Stability improvements.

For earlier versions, see the [complete release notes](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Upgrade procedures
If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.

If you missed several versions of the SDK, you may have to follow several procedures. See the complete [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md). For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.

### <a name="from-330-to-340"></a>From 3.3.0 to 3.4.0
#### <a name="test-logs"></a>Test logs
Console logs produced by the SDK can now be enabled/disabled/filtered. To customize, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the values available from the `EngagementTestLogLevel` enumeration, for instance:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Resources
The Reach overlay has been improved. It is part of the SDK NuGet package resources.

While upgrading to the new version of the SDK, you can choose whether you want to keep your existing files from the overlay folder of your resources or not:

* If the previous overlay is working for you, or you are integrating the `WebView` elements manually, then you can decide to keep your exiting files, it will still work.
* To update to the new overlay, replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Using the new overlay overwrites any customizations made on the previous version.
> 
> 

### <a name="upgrade-from-older-versions"></a>Upgrade from older versions
See [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)

