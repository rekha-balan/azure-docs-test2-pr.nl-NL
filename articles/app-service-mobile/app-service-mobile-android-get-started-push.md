---
title: Add push notifications to your Android app with Mobile Apps | Microsoft Docs
description: Learn how to use Mobile Apps to send push notifications to your Android app.
services: app-service\mobile
documentationcenter: android
manager: crdun
editor: ''
author: conceptdev
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 11/17/2017
ms.author: crdun
ms.openlocfilehash: 557f6f6a6d4925ec167760455dfc67449582c05c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800116"
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="842a0-103">Add push notifications to your Android app</span><span class="sxs-lookup"><span data-stu-id="842a0-103">Add push notifications to your Android app</span></span>

[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="842a0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="842a0-104">Overview</span></span>

<span data-ttu-id="842a0-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="842a0-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="842a0-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span><span class="sxs-lookup"><span data-stu-id="842a0-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="842a0-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="842a0-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="842a0-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="842a0-108">Prerequisites</span></span>

<span data-ttu-id="842a0-109">You need the following:</span><span class="sxs-lookup"><span data-stu-id="842a0-109">You need the following:</span></span>

* <span data-ttu-id="842a0-110">An IDE, depending on your project's back end:</span><span class="sxs-lookup"><span data-stu-id="842a0-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="842a0-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span><span class="sxs-lookup"><span data-stu-id="842a0-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="842a0-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span><span class="sxs-lookup"><span data-stu-id="842a0-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="842a0-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="842a0-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="842a0-114">Complete the [Android quick start].</span><span class="sxs-lookup"><span data-stu-id="842a0-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="842a0-115">Create a project that supports Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="842a0-115">Create a project that supports Firebase Cloud Messaging</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="842a0-116">Configure a notification hub</span><span class="sxs-lookup"><span data-stu-id="842a0-116">Configure a notification hub</span></span>

[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="842a0-117">Configure Azure to send push notifications</span><span class="sxs-lookup"><span data-stu-id="842a0-117">Configure Azure to send push notifications</span></span>

[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="842a0-118">Enable push notifications for the server project</span><span class="sxs-lookup"><span data-stu-id="842a0-118">Enable push notifications for the server project</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="842a0-119">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="842a0-119">Add push notifications to your app</span></span>

<span data-ttu-id="842a0-120">In this section, you update your client Android app to handle push notifications.</span><span class="sxs-lookup"><span data-stu-id="842a0-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="842a0-121">Verify Android SDK version</span><span class="sxs-lookup"><span data-stu-id="842a0-121">Verify Android SDK version</span></span>

[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="842a0-122">Your next step is to install Google Play services.</span><span class="sxs-lookup"><span data-stu-id="842a0-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="842a0-123">Firebase Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span><span class="sxs-lookup"><span data-stu-id="842a0-123">Firebase Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="842a0-124">If you are testing with an older device, consult [Add Firebase to Your Android Project] to determine how low you can set this value, and set it appropriately.</span><span class="sxs-lookup"><span data-stu-id="842a0-124">If you are testing with an older device, consult [Add Firebase to Your Android Project] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-firebase-cloud-messaging-to-the-project"></a><span data-ttu-id="842a0-125">Add Firebase Cloud Messaging to the project</span><span class="sxs-lookup"><span data-stu-id="842a0-125">Add Firebase Cloud Messaging to the project</span></span>

[!INCLUDE [Add Firebase Cloud Messaging](../../includes/app-service-mobile-add-firebase-cloud-messaging.md)]

### <a name="add-code"></a><span data-ttu-id="842a0-126">Add code</span><span class="sxs-lookup"><span data-stu-id="842a0-126">Add code</span></span>

[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="842a0-127">Test the app against the published mobile service</span><span class="sxs-lookup"><span data-stu-id="842a0-127">Test the app against the published mobile service</span></span>

<span data-ttu-id="842a0-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span><span class="sxs-lookup"><span data-stu-id="842a0-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="842a0-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="842a0-129">Next steps</span></span>

<span data-ttu-id="842a0-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="842a0-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="842a0-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="842a0-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="842a0-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span><span class="sxs-lookup"><span data-stu-id="842a0-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="842a0-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="842a0-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="842a0-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span><span class="sxs-lookup"><span data-stu-id="842a0-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="842a0-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="842a0-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android quick start]: app-service-mobile-android-get-started.md
[Add Firebase to Your Android Project]:https://firebase.google.com/docs/android/setup
