---
title: Routing and Tag Expressions
description: This topic explains routing and tag expressions for Azure notification hubs.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: ''
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 376d3ed2cdc7fd3eb586b78ab09941ffe7ece5f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552027"
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="50da2-103">Routing and tag expressions</span><span class="sxs-lookup"><span data-stu-id="50da2-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="50da2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="50da2-104">Overview</span></span>
<span data-ttu-id="50da2-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="50da2-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="50da2-106">Targeting specific registrations</span><span class="sxs-lookup"><span data-stu-id="50da2-106">Targeting specific registrations</span></span>
<span data-ttu-id="50da2-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span><span class="sxs-lookup"><span data-stu-id="50da2-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="50da2-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span><span class="sxs-lookup"><span data-stu-id="50da2-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="50da2-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span><span class="sxs-lookup"><span data-stu-id="50da2-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="50da2-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span><span class="sxs-lookup"><span data-stu-id="50da2-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="50da2-111">**Broadcast**: all registrations in the notification hub receive the notification.</span><span class="sxs-lookup"><span data-stu-id="50da2-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="50da2-112">**Tag**: all registrations that contain the specified tag receive the notification.</span><span class="sxs-lookup"><span data-stu-id="50da2-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="50da2-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span><span class="sxs-lookup"><span data-stu-id="50da2-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="50da2-114">Tags</span><span class="sxs-lookup"><span data-stu-id="50da2-114">Tags</span></span>
<span data-ttu-id="50da2-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span><span class="sxs-lookup"><span data-stu-id="50da2-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="50da2-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span><span class="sxs-lookup"><span data-stu-id="50da2-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="50da2-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span><span class="sxs-lookup"><span data-stu-id="50da2-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="50da2-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="50da2-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="50da2-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="50da2-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="50da2-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span><span class="sxs-lookup"><span data-stu-id="50da2-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="50da2-121">You can also use Node.js, or the Push Notifications REST APIs.</span><span class="sxs-lookup"><span data-stu-id="50da2-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="50da2-122">Here's an example using the SDK.</span><span class="sxs-lookup"><span data-stu-id="50da2-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="50da2-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span><span class="sxs-lookup"><span data-stu-id="50da2-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="50da2-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span><span class="sxs-lookup"><span data-stu-id="50da2-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="50da2-125">The following picture shows an example of this scenario:</span><span class="sxs-lookup"><span data-stu-id="50da2-125">The following picture shows an example of this scenario:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="50da2-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span><span class="sxs-lookup"><span data-stu-id="50da2-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="50da2-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span><span class="sxs-lookup"><span data-stu-id="50da2-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="50da2-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span><span class="sxs-lookup"><span data-stu-id="50da2-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="50da2-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span><span class="sxs-lookup"><span data-stu-id="50da2-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="50da2-130">A registration is matched only on the presence or absence of a specific tag.</span><span class="sxs-lookup"><span data-stu-id="50da2-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="50da2-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="50da2-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="50da2-132">Using tags to target users</span><span class="sxs-lookup"><span data-stu-id="50da2-132">Using tags to target users</span></span>
<span data-ttu-id="50da2-133">Another way to use tags is to identify all the devices of a particular user.</span><span class="sxs-lookup"><span data-stu-id="50da2-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="50da2-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span><span class="sxs-lookup"><span data-stu-id="50da2-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="50da2-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span><span class="sxs-lookup"><span data-stu-id="50da2-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="50da2-136">Tag expressions</span><span class="sxs-lookup"><span data-stu-id="50da2-136">Tag expressions</span></span>
<span data-ttu-id="50da2-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span><span class="sxs-lookup"><span data-stu-id="50da2-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="50da2-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span><span class="sxs-lookup"><span data-stu-id="50da2-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="50da2-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span><span class="sxs-lookup"><span data-stu-id="50da2-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="50da2-140">This condition can be expressed with the following Boolean expression:</span><span class="sxs-lookup"><span data-stu-id="50da2-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="50da2-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span><span class="sxs-lookup"><span data-stu-id="50da2-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="50da2-142">They can also contain parentheses.</span><span class="sxs-lookup"><span data-stu-id="50da2-142">They can also contain parentheses.</span></span> <span data-ttu-id="50da2-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span><span class="sxs-lookup"><span data-stu-id="50da2-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="50da2-144">Here's an example for sending notifications with tag expressions using the SDK.</span><span class="sxs-lookup"><span data-stu-id="50da2-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);




