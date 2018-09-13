---
title: Azure Mobile Engagement Web SDK Overview | Microsoft Docs
description: The latest updates and procedures for the Web SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562738"
---
# <a name="azure-mobile-engagement-web-sdk"></a>Azure Mobile Engagement Web SDK
Start here for all the details about how to integrate Azure Mobile Engagement in a web app. If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).

## <a name="integration-procedures"></a>Integration procedures
1. Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).
2. For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).

## <a name="release-notes"></a>Release notes
### <a name="202-10182016"></a>2.0.2 (10/18/2016)
* Fixed crash on private browsing (Safari).
* Fixed crash on browsers with cookies disabled.

For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).

## <a name="upgrade-procedures"></a>Upgrade procedures
### <a name="upgrade-from-121-to-200"></a>Upgrade from 1.2.1 to 2.0.0
The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app. If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.

This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.

> [!IMPORTANT]
> Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app. Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.
> 
> 

#### <a name="javascript-files"></a>JavaScript files
Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.

#### <a name="remove-capptain-reach"></a>Remove Capptain Reach
This version of the Mobile Engagement Web SDK doesn't support the Reach feature. If you have integrated Capptain Reach into your application, you need to remove it.

Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).

Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).

Remove the Reach UI for in-app notifications. The default layout looks like this:

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

Remove the Reach UI for text and web announcements and polls. The default layout looks like this:

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

Remove the `reach` object from your configuration, if it exists. It looks like this:

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Remove any other Reach customization, such as categories.

#### <a name="remove-deprecated-apis"></a>Remove deprecated APIs
Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.

Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.

Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.

#### <a name="configuration"></a>Configuration
Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.

Replace the application ID with your connection string. Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.

Before migration:

    window.capptain = {
      appId: ...,
      [...]
    };

After migration:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

The connection string for your application is displayed in the Azure portal.

#### <a name="javascript-apis"></a>JavaScript APIs
The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls. You can't use this alias to define the SDK configuration.

For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.

If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).

