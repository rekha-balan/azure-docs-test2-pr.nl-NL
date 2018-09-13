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
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="19ef9-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="19ef9-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="19ef9-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span><span class="sxs-lookup"><span data-stu-id="19ef9-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="19ef9-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="19ef9-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="19ef9-106">Integration procedures</span><span class="sxs-lookup"><span data-stu-id="19ef9-106">Integration procedures</span></span>
1. <span data-ttu-id="19ef9-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="19ef9-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="19ef9-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="19ef9-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="19ef9-109">Release notes</span><span class="sxs-lookup"><span data-stu-id="19ef9-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="19ef9-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="19ef9-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="19ef9-111">Fixed crash on private browsing (Safari).</span><span class="sxs-lookup"><span data-stu-id="19ef9-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="19ef9-112">Fixed crash on browsers with cookies disabled.</span><span class="sxs-lookup"><span data-stu-id="19ef9-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="19ef9-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="19ef9-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="19ef9-114">Upgrade procedures</span><span class="sxs-lookup"><span data-stu-id="19ef9-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="19ef9-115">Upgrade from 1.2.1 to 2.0.0</span><span class="sxs-lookup"><span data-stu-id="19ef9-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="19ef9-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span><span class="sxs-lookup"><span data-stu-id="19ef9-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="19ef9-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span><span class="sxs-lookup"><span data-stu-id="19ef9-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="19ef9-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span><span class="sxs-lookup"><span data-stu-id="19ef9-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19ef9-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span><span class="sxs-lookup"><span data-stu-id="19ef9-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="19ef9-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span><span class="sxs-lookup"><span data-stu-id="19ef9-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="19ef9-121">JavaScript files</span><span class="sxs-lookup"><span data-stu-id="19ef9-121">JavaScript files</span></span>
<span data-ttu-id="19ef9-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span><span class="sxs-lookup"><span data-stu-id="19ef9-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="19ef9-123">Remove Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="19ef9-123">Remove Capptain Reach</span></span>
<span data-ttu-id="19ef9-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span><span class="sxs-lookup"><span data-stu-id="19ef9-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="19ef9-125">If you have integrated Capptain Reach into your application, you need to remove it.</span><span class="sxs-lookup"><span data-stu-id="19ef9-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="19ef9-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span><span class="sxs-lookup"><span data-stu-id="19ef9-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="19ef9-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span><span class="sxs-lookup"><span data-stu-id="19ef9-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="19ef9-128">Remove the Reach UI for in-app notifications.</span><span class="sxs-lookup"><span data-stu-id="19ef9-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="19ef9-129">The default layout looks like this:</span><span class="sxs-lookup"><span data-stu-id="19ef9-129">The default layout looks like this:</span></span>

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

<span data-ttu-id="19ef9-130">Remove the Reach UI for text and web announcements and polls.</span><span class="sxs-lookup"><span data-stu-id="19ef9-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="19ef9-131">The default layout looks like this:</span><span class="sxs-lookup"><span data-stu-id="19ef9-131">The default layout looks like this:</span></span>

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

<span data-ttu-id="19ef9-132">Remove the `reach` object from your configuration, if it exists.</span><span class="sxs-lookup"><span data-stu-id="19ef9-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="19ef9-133">It looks like this:</span><span class="sxs-lookup"><span data-stu-id="19ef9-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="19ef9-134">Remove any other Reach customization, such as categories.</span><span class="sxs-lookup"><span data-stu-id="19ef9-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="19ef9-135">Remove deprecated APIs</span><span class="sxs-lookup"><span data-stu-id="19ef9-135">Remove deprecated APIs</span></span>
<span data-ttu-id="19ef9-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="19ef9-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="19ef9-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="19ef9-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="19ef9-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="19ef9-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="19ef9-139">Configuration</span><span class="sxs-lookup"><span data-stu-id="19ef9-139">Configuration</span></span>
<span data-ttu-id="19ef9-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span><span class="sxs-lookup"><span data-stu-id="19ef9-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="19ef9-141">Replace the application ID with your connection string.</span><span class="sxs-lookup"><span data-stu-id="19ef9-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="19ef9-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="19ef9-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="19ef9-143">Before migration:</span><span class="sxs-lookup"><span data-stu-id="19ef9-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="19ef9-144">After migration:</span><span class="sxs-lookup"><span data-stu-id="19ef9-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="19ef9-145">The connection string for your application is displayed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="19ef9-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="19ef9-146">JavaScript APIs</span><span class="sxs-lookup"><span data-stu-id="19ef9-146">JavaScript APIs</span></span>
<span data-ttu-id="19ef9-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span><span class="sxs-lookup"><span data-stu-id="19ef9-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="19ef9-148">You can't use this alias to define the SDK configuration.</span><span class="sxs-lookup"><span data-stu-id="19ef9-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="19ef9-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span><span class="sxs-lookup"><span data-stu-id="19ef9-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="19ef9-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="19ef9-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

