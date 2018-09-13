---
title: Add push notifications to your Xamarin.Android app | Microsoft Docs
description: Learn how to use Azure App Service and Azure Notification Hubs to send push notifications to your Xamarin.Android app
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: adrianha
editor: ''
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c1d429b50d693c8529af5b8cdff75f6a439bc4ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556696"
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="802c1-103">Add push notifications to your Xamarin.Android app</span><span class="sxs-lookup"><span data-stu-id="802c1-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="802c1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="802c1-104">Overview</span></span>
<span data-ttu-id="802c1-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="802c1-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="802c1-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span><span class="sxs-lookup"><span data-stu-id="802c1-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="802c1-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="802c1-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="802c1-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="802c1-108">Prerequisites</span></span>
<span data-ttu-id="802c1-109">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="802c1-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="802c1-110">An active Google account.</span><span class="sxs-lookup"><span data-stu-id="802c1-110">An active Google account.</span></span> <span data-ttu-id="802c1-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="802c1-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="802c1-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="802c1-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <a name="configure-hub"></a><span data-ttu-id="802c1-113">Configure a Notification Hub</span><span class="sxs-lookup"><span data-stu-id="802c1-113">Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a><span data-ttu-id="802c1-114">Enable Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="802c1-114">Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="802c1-115">Configure Azure to send push requests</span><span class="sxs-lookup"><span data-stu-id="802c1-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a><span data-ttu-id="802c1-116">Update the server project to send push notifications</span><span class="sxs-lookup"><span data-stu-id="802c1-116">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a><span data-ttu-id="802c1-117">Configure the client project for push notifications</span><span class="sxs-lookup"><span data-stu-id="802c1-117">Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a><span data-ttu-id="802c1-118">Add push notifications code to your app</span><span class="sxs-lookup"><span data-stu-id="802c1-118">Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a><span data-ttu-id="802c1-119">Test push notifications in your app</span><span class="sxs-lookup"><span data-stu-id="802c1-119">Test push notifications in your app</span></span>
<span data-ttu-id="802c1-120">You can test the app by using a virtual device in the emulator.</span><span class="sxs-lookup"><span data-stu-id="802c1-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="802c1-121">There are additional configuration steps required when running on an emulator.</span><span class="sxs-lookup"><span data-stu-id="802c1-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="802c1-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span><span class="sxs-lookup"><span data-stu-id="802c1-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="802c1-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span><span class="sxs-lookup"><span data-stu-id="802c1-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="802c1-124">Run the todolist app as before and insert a new todo item.</span><span class="sxs-lookup"><span data-stu-id="802c1-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="802c1-125">This time, a notification icon is displayed in the notification area.</span><span class="sxs-lookup"><span data-stu-id="802c1-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="802c1-126">You can open the notification drawer to view the full text of the notification.</span><span class="sxs-lookup"><span data-stu-id="802c1-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/



