---
title: Add push notifications to your Xamarin.iOS app with Azure App Service
description: Learn how to use Azure App Service to send push notifications to your Xamarin.iOS app
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: adrianha
editor: ''
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 72e187b8817616a466fa5eae992a7705abf24940
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552619"
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="91c5f-103">Add push notifications to your Xamarin.iOS App</span><span class="sxs-lookup"><span data-stu-id="91c5f-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="91c5f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="91c5f-104">Overview</span></span>
<span data-ttu-id="91c5f-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="91c5f-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="91c5f-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span><span class="sxs-lookup"><span data-stu-id="91c5f-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="91c5f-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="91c5f-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91c5f-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91c5f-108">Prerequisites</span></span>
* <span data-ttu-id="91c5f-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="91c5f-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="91c5f-110">A physical iOS device.</span><span class="sxs-lookup"><span data-stu-id="91c5f-110">A physical iOS device.</span></span> <span data-ttu-id="91c5f-111">Push notifications are not supported by the iOS simulator.</span><span class="sxs-lookup"><span data-stu-id="91c5f-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="91c5f-112">Register the app for push notifications on Apple's developer portal</span><span class="sxs-lookup"><span data-stu-id="91c5f-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="91c5f-113">Configure your Mobile App to send push notifications</span><span class="sxs-lookup"><span data-stu-id="91c5f-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="91c5f-114">Update the server project to send push notifications</span><span class="sxs-lookup"><span data-stu-id="91c5f-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="91c5f-115">Configure your Xamarin.iOS project</span><span class="sxs-lookup"><span data-stu-id="91c5f-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="91c5f-116">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="91c5f-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="91c5f-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span><span class="sxs-lookup"><span data-stu-id="91c5f-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="91c5f-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span><span class="sxs-lookup"><span data-stu-id="91c5f-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="91c5f-119">In **AppDelegate**, override the **FinishedLaunching** event:</span><span class="sxs-lookup"><span data-stu-id="91c5f-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="91c5f-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span><span class="sxs-lookup"><span data-stu-id="91c5f-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="91c5f-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span><span class="sxs-lookup"><span data-stu-id="91c5f-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="91c5f-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="91c5f-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="91c5f-123">Then, override the **DidReceivedRemoteNotification** event:</span><span class="sxs-lookup"><span data-stu-id="91c5f-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="91c5f-124">Your app is now updated to support push notifications.</span><span class="sxs-lookup"><span data-stu-id="91c5f-124">Your app is now updated to support push notifications.</span></span>

## <a name="test"></a><span data-ttu-id="91c5f-125">Test push notifications in your app</span><span class="sxs-lookup"><span data-stu-id="91c5f-125">Test push notifications in your app</span></span>
1. <span data-ttu-id="91c5f-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span><span class="sxs-lookup"><span data-stu-id="91c5f-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="91c5f-127">You must explicitly accept push notifications from your app.</span><span class="sxs-lookup"><span data-stu-id="91c5f-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="91c5f-128">This request only occurs the first time that the app runs.</span><span class="sxs-lookup"><span data-stu-id="91c5f-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="91c5f-129">In the app, type a task, and then click the plus (**+**) icon.</span><span class="sxs-lookup"><span data-stu-id="91c5f-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="91c5f-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span><span class="sxs-lookup"><span data-stu-id="91c5f-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="91c5f-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span><span class="sxs-lookup"><span data-stu-id="91c5f-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="91c5f-132">You have successfully completed this tutorial.</span><span class="sxs-lookup"><span data-stu-id="91c5f-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



