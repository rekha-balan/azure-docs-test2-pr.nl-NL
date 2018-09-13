---
title: Mobile Engagement concepts | Microsoft Docs
description: Azure Mobile Engagement concepts
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 8450651528007b4527366b89a6ad7615169f93c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556518"
---
# <a name="azure-mobile-engagement-concepts"></a><span data-ttu-id="9e41b-103">Azure Mobile Engagement concepts</span><span class="sxs-lookup"><span data-stu-id="9e41b-103">Azure Mobile Engagement concepts</span></span>
<span data-ttu-id="9e41b-104">Mobile Engagement defines a few concepts common to all supported platforms.</span><span class="sxs-lookup"><span data-stu-id="9e41b-104">Mobile Engagement defines a few concepts common to all supported platforms.</span></span> <span data-ttu-id="9e41b-105">This article briefly describes those concepts.</span><span class="sxs-lookup"><span data-stu-id="9e41b-105">This article briefly describes those concepts.</span></span>

<span data-ttu-id="9e41b-106">This article is a good start if you are new to Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9e41b-106">This article is a good start if you are new to Mobile Engagement.</span></span> <span data-ttu-id="9e41b-107">Also make sure to read the documentation specific to the platform you are using, as it will refine the concepts described in this article with more details and examples as well as possible limitations.</span><span class="sxs-lookup"><span data-stu-id="9e41b-107">Also make sure to read the documentation specific to the platform you are using, as it will refine the concepts described in this article with more details and examples as well as possible limitations.</span></span>

## <a name="devices-and-users"></a><span data-ttu-id="9e41b-108">Devices and users</span><span class="sxs-lookup"><span data-stu-id="9e41b-108">Devices and users</span></span>
<span data-ttu-id="9e41b-109">Mobile Engagement identifies users by generating a unique identifier for each device.</span><span class="sxs-lookup"><span data-stu-id="9e41b-109">Mobile Engagement identifies users by generating a unique identifier for each device.</span></span> <span data-ttu-id="9e41b-110">This identifier is called the device identifier (or `deviceid`).</span><span class="sxs-lookup"><span data-stu-id="9e41b-110">This identifier is called the device identifier (or `deviceid`).</span></span> <span data-ttu-id="9e41b-111">It is generated in such a way that all applications running of the same device share the same device identifier.</span><span class="sxs-lookup"><span data-stu-id="9e41b-111">It is generated in such a way that all applications running of the same device share the same device identifier.</span></span>

<span data-ttu-id="9e41b-112">Implicitly, it means that Mobile Engagement considers one device to belong to exactly one user, and thus, users and devices are equivalent concepts.</span><span class="sxs-lookup"><span data-stu-id="9e41b-112">Implicitly, it means that Mobile Engagement considers one device to belong to exactly one user, and thus, users and devices are equivalent concepts.</span></span>

## <a name="sessions-and-activities"></a><span data-ttu-id="9e41b-113">Sessions and activities</span><span class="sxs-lookup"><span data-stu-id="9e41b-113">Sessions and activities</span></span>
<span data-ttu-id="9e41b-114">A session is one use of the application performed by a user, from the time the user starts using it, until the user stops.</span><span class="sxs-lookup"><span data-stu-id="9e41b-114">A session is one use of the application performed by a user, from the time the user starts using it, until the user stops.</span></span>

<span data-ttu-id="9e41b-115">An activity is one use of a given sub-part of the application performed by one user (it is usually a screen, but it can be anything suitable to the application).</span><span class="sxs-lookup"><span data-stu-id="9e41b-115">An activity is one use of a given sub-part of the application performed by one user (it is usually a screen, but it can be anything suitable to the application).</span></span>

<span data-ttu-id="9e41b-116">A user can only perform one activity at a time.</span><span class="sxs-lookup"><span data-stu-id="9e41b-116">A user can only perform one activity at a time.</span></span>

<span data-ttu-id="9e41b-117">An activity is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span><span class="sxs-lookup"><span data-stu-id="9e41b-117">An activity is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

<span data-ttu-id="9e41b-118">Sessions are automatically computed from the sequence of activities performed by users.</span><span class="sxs-lookup"><span data-stu-id="9e41b-118">Sessions are automatically computed from the sequence of activities performed by users.</span></span> <span data-ttu-id="9e41b-119">A session starts when the user starts his first activity and stops when he finishes his last activity.</span><span class="sxs-lookup"><span data-stu-id="9e41b-119">A session starts when the user starts his first activity and stops when he finishes his last activity.</span></span> <span data-ttu-id="9e41b-120">This means that a session does not need to be explicitly started or stopped.</span><span class="sxs-lookup"><span data-stu-id="9e41b-120">This means that a session does not need to be explicitly started or stopped.</span></span> <span data-ttu-id="9e41b-121">Instead, activities are explicitly started or stopped.</span><span class="sxs-lookup"><span data-stu-id="9e41b-121">Instead, activities are explicitly started or stopped.</span></span> <span data-ttu-id="9e41b-122">If no activity is reported, no session is reported.</span><span class="sxs-lookup"><span data-stu-id="9e41b-122">If no activity is reported, no session is reported.</span></span>

## <a name="events"></a><span data-ttu-id="9e41b-123">Events</span><span class="sxs-lookup"><span data-stu-id="9e41b-123">Events</span></span>
<span data-ttu-id="9e41b-124">Events are used to report instant actions (like button pressed or articles read by users).</span><span class="sxs-lookup"><span data-stu-id="9e41b-124">Events are used to report instant actions (like button pressed or articles read by users).</span></span>

<span data-ttu-id="9e41b-125">An event can be related to the current session, to a running job, or it can be a standalone event.</span><span class="sxs-lookup"><span data-stu-id="9e41b-125">An event can be related to the current session, to a running job, or it can be a standalone event.</span></span>

<span data-ttu-id="9e41b-126">An event is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span><span class="sxs-lookup"><span data-stu-id="9e41b-126">An event is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="error"></a><span data-ttu-id="9e41b-127">Error</span><span class="sxs-lookup"><span data-stu-id="9e41b-127">Error</span></span>
<span data-ttu-id="9e41b-128">Errors are used to report issues correctly detected by the application (like incorrect user actions, or API call failures).</span><span class="sxs-lookup"><span data-stu-id="9e41b-128">Errors are used to report issues correctly detected by the application (like incorrect user actions, or API call failures).</span></span>

<span data-ttu-id="9e41b-129">An error can be related to the current session, to a running job, or it can be a standalone error.</span><span class="sxs-lookup"><span data-stu-id="9e41b-129">An error can be related to the current session, to a running job, or it can be a standalone error.</span></span>

<span data-ttu-id="9e41b-130">An error is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span><span class="sxs-lookup"><span data-stu-id="9e41b-130">An error is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="job"></a><span data-ttu-id="9e41b-131">Job</span><span class="sxs-lookup"><span data-stu-id="9e41b-131">Job</span></span>
<span data-ttu-id="9e41b-132">Jobs are used to report actions having a duration (like duration of API calls, display time of ads, duration of background tasks or duration of user actions).</span><span class="sxs-lookup"><span data-stu-id="9e41b-132">Jobs are used to report actions having a duration (like duration of API calls, display time of ads, duration of background tasks or duration of user actions).</span></span>

<span data-ttu-id="9e41b-133">A job is not related to a session, because a task can be performed in the background, without any user interaction.</span><span class="sxs-lookup"><span data-stu-id="9e41b-133">A job is not related to a session, because a task can be performed in the background, without any user interaction.</span></span>

<span data-ttu-id="9e41b-134">A job is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span><span class="sxs-lookup"><span data-stu-id="9e41b-134">A job is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="crash"></a><span data-ttu-id="9e41b-135">Crash</span><span class="sxs-lookup"><span data-stu-id="9e41b-135">Crash</span></span>
<span data-ttu-id="9e41b-136">Crashes are issued automatically by the Mobile Engagement SDK to report application failures where issues not detected by the application make it crash.</span><span class="sxs-lookup"><span data-stu-id="9e41b-136">Crashes are issued automatically by the Mobile Engagement SDK to report application failures where issues not detected by the application make it crash.</span></span>

## <a name="application-information"></a><span data-ttu-id="9e41b-137">Application information</span><span class="sxs-lookup"><span data-stu-id="9e41b-137">Application information</span></span>
<span data-ttu-id="9e41b-138">Application information (or app info) is used to tag users, that is, to associate some data to the users of an application (this is similar to web cookies, except that app info is stored on the server side on the Azure Mobile Engagement platform).</span><span class="sxs-lookup"><span data-stu-id="9e41b-138">Application information (or app info) is used to tag users, that is, to associate some data to the users of an application (this is similar to web cookies, except that app info is stored on the server side on the Azure Mobile Engagement platform).</span></span>

<span data-ttu-id="9e41b-139">App info can be registered by using the Mobile Engagement SDK API or by using the Mobile Engagement platform Device API.</span><span class="sxs-lookup"><span data-stu-id="9e41b-139">App info can be registered by using the Mobile Engagement SDK API or by using the Mobile Engagement platform Device API.</span></span>

<span data-ttu-id="9e41b-140">App info is a key/value pair associated to a device.</span><span class="sxs-lookup"><span data-stu-id="9e41b-140">App info is a key/value pair associated to a device.</span></span> <span data-ttu-id="9e41b-141">The key is the name of the app info (limited to 64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]).</span><span class="sxs-lookup"><span data-stu-id="9e41b-141">The key is the name of the app info (limited to 64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]).</span></span> <span data-ttu-id="9e41b-142">The value (limited to 1024 characters) can be any string, integer, date (yyyy-MM-dd) or Boolean (true or false).</span><span class="sxs-lookup"><span data-stu-id="9e41b-142">The value (limited to 1024 characters) can be any string, integer, date (yyyy-MM-dd) or Boolean (true or false).</span></span>

<span data-ttu-id="9e41b-143">Any number of app info can be associated to a device, within the limits defined by the Mobile Engagement pricing terms.</span><span class="sxs-lookup"><span data-stu-id="9e41b-143">Any number of app info can be associated to a device, within the limits defined by the Mobile Engagement pricing terms.</span></span> <span data-ttu-id="9e41b-144">For one given key, Mobile Engagement only keeps track of the latest value set (no history).</span><span class="sxs-lookup"><span data-stu-id="9e41b-144">For one given key, Mobile Engagement only keeps track of the latest value set (no history).</span></span> <span data-ttu-id="9e41b-145">Setting or changing the value of an app info forces Mobile Engagement to re-evaluate audience criteria set on this app info (if any) meaning that app info can be used to trigger realtime pushes.</span><span class="sxs-lookup"><span data-stu-id="9e41b-145">Setting or changing the value of an app info forces Mobile Engagement to re-evaluate audience criteria set on this app info (if any) meaning that app info can be used to trigger realtime pushes.</span></span>

## <a name="extra-data"></a><span data-ttu-id="9e41b-146">Extra data</span><span class="sxs-lookup"><span data-stu-id="9e41b-146">Extra data</span></span>
<span data-ttu-id="9e41b-147">Extra data (or extras) is some arbitrary data that can be attached to events, errors, activities and jobs.</span><span class="sxs-lookup"><span data-stu-id="9e41b-147">Extra data (or extras) is some arbitrary data that can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="9e41b-148">Extras are structured similarly to JSON objects: they are made of a tree of key/value pairs.</span><span class="sxs-lookup"><span data-stu-id="9e41b-148">Extras are structured similarly to JSON objects: they are made of a tree of key/value pairs.</span></span> <span data-ttu-id="9e41b-149">Keys are limited to 64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]) and the total size of extras is limited to 1024 characters (once encoded in JSON by the Mobile Engagement SDK).</span><span class="sxs-lookup"><span data-stu-id="9e41b-149">Keys are limited to 64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]) and the total size of extras is limited to 1024 characters (once encoded in JSON by the Mobile Engagement SDK).</span></span>

<span data-ttu-id="9e41b-150">The whole tree of key/value pairs is stored as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="9e41b-150">The whole tree of key/value pairs is stored as a JSON object.</span></span> <span data-ttu-id="9e41b-151">Nevertheless, only the first level of keys/values is decomposed to be directly accessible to some advanced functions like Segments (for example, you can easily define a segment called “SciFi fans” that is made of all users having sent at least 10 times the event named “content_viewed” with the extra key “content_type” set to the value “scifi” in the last month).</span><span class="sxs-lookup"><span data-stu-id="9e41b-151">Nevertheless, only the first level of keys/values is decomposed to be directly accessible to some advanced functions like Segments (for example, you can easily define a segment called “SciFi fans” that is made of all users having sent at least 10 times the event named “content_viewed” with the extra key “content_type” set to the value “scifi” in the last month).</span></span> <span data-ttu-id="9e41b-152">It is thus highly recommended to send only extras made of simple lists of key/value pairs using scalar values (for example, strings, dates, integers or Boolean).</span><span class="sxs-lookup"><span data-stu-id="9e41b-152">It is thus highly recommended to send only extras made of simple lists of key/value pairs using scalar values (for example, strings, dates, integers or Boolean).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e41b-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e41b-153">Next steps</span></span>
* [<span data-ttu-id="9e41b-154">Windows Universal SDK overview for Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9e41b-154">Windows Universal SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-store-sdk-overview.md)
* [<span data-ttu-id="9e41b-155">Windows Phone Silverlight SDK overview for Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9e41b-155">Windows Phone Silverlight SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
* [<span data-ttu-id="9e41b-156">iOS SDK for Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9e41b-156">iOS SDK for Azure Mobile Engagement</span></span>](mobile-engagement-ios-sdk-overview.md)
* [<span data-ttu-id="9e41b-157">Android SDK for Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9e41b-157">Android SDK for Azure Mobile Engagement</span></span>](mobile-engagement-android-sdk-overview.md)

