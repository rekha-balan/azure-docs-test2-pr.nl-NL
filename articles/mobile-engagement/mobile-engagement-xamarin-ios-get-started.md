---
title: Get Started with Azure Mobile Engagement for Xamarin.iOS
description: Learn how to use Azure Mobile Engagement with Analytics and Push Notifications for Xamarin.iOS Apps.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b2ec9355f9a4d53c86d3df489a2adfa87bd4d897
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661919"
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="85983-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span><span class="sxs-lookup"><span data-stu-id="85983-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="85983-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users in a Xamarin.iOS application.</span><span class="sxs-lookup"><span data-stu-id="85983-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="85983-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="85983-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="85983-106">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="85983-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="85983-107">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="85983-107">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="85983-108">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="85983-108">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="85983-109">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="85983-109">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="85983-110">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="85983-110">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="85983-111">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="85983-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="85983-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="85983-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="85983-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="85983-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <a id="setup-azme"></a><span data-ttu-id="85983-114">Setup Mobile Engagement for your iOS app</span><span class="sxs-lookup"><span data-stu-id="85983-114">Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="85983-115">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="85983-115">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="85983-116">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span><span class="sxs-lookup"><span data-stu-id="85983-116">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span>

<span data-ttu-id="85983-117">We will create a basic app with Xamarin to demonstrate the integration:</span><span class="sxs-lookup"><span data-stu-id="85983-117">We will create a basic app with Xamarin to demonstrate the integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="85983-118">Create a new Xamarin.iOS project</span><span class="sxs-lookup"><span data-stu-id="85983-118">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="85983-119">Launch Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="85983-119">Launch Xamarin Studio.</span></span> <span data-ttu-id="85983-120">Go to **File** -> **New** -> **Solution**</span><span class="sxs-lookup"><span data-stu-id="85983-120">Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="85983-121">Select **Single View App**, make sure the selected language is **C#** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="85983-121">Select **Single View App**, make sure the selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="85983-122">Fill in the **App Name** and the **Organization Identifier** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="85983-122">Fill in the **App Name** and the **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="85983-123">Make sure that the publishing profile you eventually use to deploy your iOS app is using an App ID which matches exactly with the Bundle Identifier you have here.</span><span class="sxs-lookup"><span data-stu-id="85983-123">Make sure that the publishing profile you eventually use to deploy your iOS app is using an App ID which matches exactly with the Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="85983-124">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="85983-124">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="85983-125">Xamarin Studio will create the demo app in which we will integrate Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="85983-125">Xamarin Studio will create the demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="85983-126">Connect your app to Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="85983-126">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="85983-127">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span><span class="sxs-lookup"><span data-stu-id="85983-127">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="85983-128">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span><span class="sxs-lookup"><span data-stu-id="85983-128">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="85983-129">Open **AppDelegate.cs** and add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="85983-129">Open **AppDelegate.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="85983-130">In the **FinishedLaunching** method, add the following to initialize the connection with Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="85983-130">In the **FinishedLaunching** method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="85983-131">Make sure to add your **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="85983-131">Make sure to add your **ConnectionString**.</span></span> <span data-ttu-id="85983-132">This code also uses a dummy **NotificationIcon** which is added by the Mobile Engagement SDK which you may want to replace.</span><span class="sxs-lookup"><span data-stu-id="85983-132">This code also uses a dummy **NotificationIcon** which is added by the Mobile Engagement SDK which you may want to replace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a><span data-ttu-id="85983-133">Enabling real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="85983-133">Enabling real-time monitoring</span></span>
<span data-ttu-id="85983-134">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="85983-134">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="85983-135">Open **ViewController.cs** and add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="85983-135">Open **ViewController.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="85983-136">Replace the class from which `ViewController` inherits from `UIViewController` to `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="85983-136">Replace the class from which `ViewController` inherits from `UIViewController` to `EngagementViewController`.</span></span> 

## <a id="monitor"></a><span data-ttu-id="85983-137">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="85983-137">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="85983-138">Enable push notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="85983-138">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="85983-139">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span><span class="sxs-lookup"><span data-stu-id="85983-139">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="85983-140">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="85983-140">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="85983-141">The following sections set up your app to receive them.</span><span class="sxs-lookup"><span data-stu-id="85983-141">The following sections set up your app to receive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="85983-142">Modify your Application Delegate</span><span class="sxs-lookup"><span data-stu-id="85983-142">Modify your Application Delegate</span></span>
1. <span data-ttu-id="85983-143">Open the **AppDelegate.cs** and add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="85983-143">Open the **AppDelegate.cs** and add the following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="85983-144">Now inside the `FinishedLaunching` method, add the following to register for push messages after `EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="85983-144">Now inside the `FinishedLaunching` method, add the following to register for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="85983-145">Finally - update or add the following methods:</span><span class="sxs-lookup"><span data-stu-id="85983-145">Finally - update or add the following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed to register for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="85983-146">In your **Info.plist** file in the solution, confirm that the **Bundle Identifier** matches with the **App ID** you have in your provisioning profile in the Apple Dev Center.</span><span class="sxs-lookup"><span data-stu-id="85983-146">In your **Info.plist** file in the solution, confirm that the **Bundle Identifier** matches with the **App ID** you have in your provisioning profile in the Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="85983-147">In the same **Info.plist** file, make sure that you have checked the **Enable Background Modes** and **Remote Notifications**.</span><span class="sxs-lookup"><span data-stu-id="85983-147">In the same **Info.plist** file, make sure that you have checked the **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="85983-148">Run the app on the device you have associated with this publishing profile.</span><span class="sxs-lookup"><span data-stu-id="85983-148">Run the app on the device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png








