---
title: Add push notifications to your Android app with Mobile Apps | Microsoft Docs
description: Learn how to use Mobile Apps to send push notifications to your Android app.
services: app-service\mobile
documentationcenter: android
manager: adrianha
editor: ''
author: ysxu
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 02d7b744090f296957006b4d12a724345b0b1c6d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662191"
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="add9f-103">Add push notifications to your Android app</span><span class="sxs-lookup"><span data-stu-id="add9f-103">Add push notifications to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="add9f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="add9f-104">Overview</span></span>
<span data-ttu-id="add9f-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="add9f-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="add9f-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span><span class="sxs-lookup"><span data-stu-id="add9f-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="add9f-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="add9f-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="add9f-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="add9f-108">Prerequisites</span></span>
<span data-ttu-id="add9f-109">You need the following:</span><span class="sxs-lookup"><span data-stu-id="add9f-109">You need the following:</span></span>

* <span data-ttu-id="add9f-110">An IDE, depending on your project's back end:</span><span class="sxs-lookup"><span data-stu-id="add9f-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="add9f-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span><span class="sxs-lookup"><span data-stu-id="add9f-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="add9f-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span><span class="sxs-lookup"><span data-stu-id="add9f-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="add9f-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="add9f-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="add9f-114">Complete the [Android quick start].</span><span class="sxs-lookup"><span data-stu-id="add9f-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="add9f-115">Create a project that supports Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="add9f-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="add9f-116">Configure a notification hub</span><span class="sxs-lookup"><span data-stu-id="add9f-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="add9f-117">Configure Azure to send push notifications</span><span class="sxs-lookup"><span data-stu-id="add9f-117">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="add9f-118">Enable push notifications for the server project</span><span class="sxs-lookup"><span data-stu-id="add9f-118">Enable push notifications for the server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="add9f-119">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="add9f-119">Add push notifications to your app</span></span>
<span data-ttu-id="add9f-120">In this section, you update your client Android app to handle push notifications.</span><span class="sxs-lookup"><span data-stu-id="add9f-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="add9f-121">Verify Android SDK version</span><span class="sxs-lookup"><span data-stu-id="add9f-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="add9f-122">Your next step is to install Google Play services.</span><span class="sxs-lookup"><span data-stu-id="add9f-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="add9f-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span><span class="sxs-lookup"><span data-stu-id="add9f-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="add9f-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span><span class="sxs-lookup"><span data-stu-id="add9f-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="add9f-125">Add Google Play services to the project</span><span class="sxs-lookup"><span data-stu-id="add9f-125">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="add9f-126">Add code</span><span class="sxs-lookup"><span data-stu-id="add9f-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="add9f-127">Test the app against the published mobile service</span><span class="sxs-lookup"><span data-stu-id="add9f-127">Test the app against the published mobile service</span></span>
<span data-ttu-id="add9f-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span><span class="sxs-lookup"><span data-stu-id="add9f-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="add9f-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="add9f-129">Next steps</span></span>
<span data-ttu-id="add9f-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="add9f-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="add9f-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="add9f-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="add9f-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span><span class="sxs-lookup"><span data-stu-id="add9f-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="add9f-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="add9f-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="add9f-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span><span class="sxs-lookup"><span data-stu-id="add9f-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="add9f-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="add9f-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android quick start]: app-service-mobile-android-get-started.md

[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup
