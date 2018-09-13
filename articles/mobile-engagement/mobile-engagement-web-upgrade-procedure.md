---
title: Azure Mobile Engagement Web SDK upgrade procedures | Microsoft Docs
description: The latest updates and procedures for the Web SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: afa8037dcb7a53042fa606e2c4014b442d4be326
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551520"
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="d4044-103">Azure Mobile Engagement Web SDK upgrade procedures</span><span class="sxs-lookup"><span data-stu-id="d4044-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="d4044-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span><span class="sxs-lookup"><span data-stu-id="d4044-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span></span>

<span data-ttu-id="d4044-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span><span class="sxs-lookup"><span data-stu-id="d4044-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span></span> <span data-ttu-id="d4044-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="d4044-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span></span> <span data-ttu-id="d4044-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span><span class="sxs-lookup"><span data-stu-id="d4044-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span></span>

<span data-ttu-id="d4044-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span><span class="sxs-lookup"><span data-stu-id="d4044-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span></span>

## <a name="upgrade-from-121-to-200"></a><span data-ttu-id="d4044-109">Upgrade from 1.2.1 to 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d4044-109">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="d4044-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span><span class="sxs-lookup"><span data-stu-id="d4044-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="d4044-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span><span class="sxs-lookup"><span data-stu-id="d4044-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span></span>

<span data-ttu-id="d4044-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span><span class="sxs-lookup"><span data-stu-id="d4044-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4044-113">Capptain and Azure Mobile Engagement are not the same service.</span><span class="sxs-lookup"><span data-stu-id="d4044-113">Capptain and Azure Mobile Engagement are not the same service.</span></span> <span data-ttu-id="d4044-114">The following procedure highlights only how to migrate the client app.</span><span class="sxs-lookup"><span data-stu-id="d4044-114">The following procedure highlights only how to migrate the client app.</span></span> <span data-ttu-id="d4044-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span><span class="sxs-lookup"><span data-stu-id="d4044-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="d4044-116">JavaScript files</span><span class="sxs-lookup"><span data-stu-id="d4044-116">JavaScript files</span></span>
<span data-ttu-id="d4044-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span><span class="sxs-lookup"><span data-stu-id="d4044-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="d4044-118">Remove Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="d4044-118">Remove Capptain Reach</span></span>
<span data-ttu-id="d4044-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span><span class="sxs-lookup"><span data-stu-id="d4044-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="d4044-120">If you integrated Capptain Reach into your application, you need to remove it.</span><span class="sxs-lookup"><span data-stu-id="d4044-120">If you integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="d4044-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span><span class="sxs-lookup"><span data-stu-id="d4044-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="d4044-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span><span class="sxs-lookup"><span data-stu-id="d4044-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="d4044-123">Remove the Reach UI for in-app notifications.</span><span class="sxs-lookup"><span data-stu-id="d4044-123">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="d4044-124">The default layout looks like this:</span><span class="sxs-lookup"><span data-stu-id="d4044-124">The default layout looks like this:</span></span>

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

<span data-ttu-id="d4044-125">Remove the Reach UI for text and web announcements and polls.</span><span class="sxs-lookup"><span data-stu-id="d4044-125">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="d4044-126">The default layout looks like this:</span><span class="sxs-lookup"><span data-stu-id="d4044-126">The default layout looks like this:</span></span>

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

<span data-ttu-id="d4044-127">Remove the `reach` object from your configuration, if it exists.</span><span class="sxs-lookup"><span data-stu-id="d4044-127">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="d4044-128">It looks like this:</span><span class="sxs-lookup"><span data-stu-id="d4044-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="d4044-129">Remove any other Reach customization, such as categories.</span><span class="sxs-lookup"><span data-stu-id="d4044-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="d4044-130">Remove deprecated APIs</span><span class="sxs-lookup"><span data-stu-id="d4044-130">Remove deprecated APIs</span></span>
<span data-ttu-id="d4044-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="d4044-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="d4044-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="d4044-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="d4044-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="d4044-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="d4044-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="d4044-134">Configuration</span></span>
<span data-ttu-id="d4044-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span><span class="sxs-lookup"><span data-stu-id="d4044-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="d4044-136">Replace the application ID with your connection string.</span><span class="sxs-lookup"><span data-stu-id="d4044-136">Replace the application ID with your connection string.</span></span> <span data-ttu-id="d4044-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="d4044-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="d4044-138">Before migration:</span><span class="sxs-lookup"><span data-stu-id="d4044-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="d4044-139">After migration:</span><span class="sxs-lookup"><span data-stu-id="d4044-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="d4044-140">The connection string for your application is displayed in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4044-140">The connection string for your application is displayed in the Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="d4044-141">JavaScript APIs</span><span class="sxs-lookup"><span data-stu-id="d4044-141">JavaScript APIs</span></span>
<span data-ttu-id="d4044-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span><span class="sxs-lookup"><span data-stu-id="d4044-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="d4044-143">You can't use the alias to define the SDK configuration.</span><span class="sxs-lookup"><span data-stu-id="d4044-143">You can't use the alias to define the SDK configuration.</span></span>

<span data-ttu-id="d4044-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span><span class="sxs-lookup"><span data-stu-id="d4044-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

