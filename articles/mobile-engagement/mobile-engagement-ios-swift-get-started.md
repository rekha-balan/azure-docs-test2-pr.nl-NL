---
title: Get Started with Azure Mobile Engagement for iOS in Swift | Microsoft Docs
description: Learn how to use Azure Mobile Engagement with Analytics and Push Notifications for iOS Apps.
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 4fbded71bfd27b27f7d9f0d14b82f2c88d9a1d9d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670575"
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="839d1-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span><span class="sxs-lookup"><span data-stu-id="839d1-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="839d1-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span><span class="sxs-lookup"><span data-stu-id="839d1-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="839d1-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="839d1-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="839d1-106">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="839d1-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="839d1-107">XCode 8, which you can install from your MAC App Store</span><span class="sxs-lookup"><span data-stu-id="839d1-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="839d1-108">the [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="839d1-108">the [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="839d1-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span><span class="sxs-lookup"><span data-stu-id="839d1-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="839d1-110">This tutorial uses Swift version 3.0.</span><span class="sxs-lookup"><span data-stu-id="839d1-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="839d1-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span><span class="sxs-lookup"><span data-stu-id="839d1-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="839d1-112">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="839d1-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="839d1-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="839d1-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="839d1-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="839d1-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <a id="setup-azme"></a><span data-ttu-id="839d1-115">Setup Mobile Engagement for your iOS app</span><span class="sxs-lookup"><span data-stu-id="839d1-115">Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="839d1-116">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="839d1-116">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="839d1-117">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span><span class="sxs-lookup"><span data-stu-id="839d1-117">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="839d1-118">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="839d1-118">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="839d1-119">We will create a basic app with XCode to demonstrate the integration:</span><span class="sxs-lookup"><span data-stu-id="839d1-119">We will create a basic app with XCode to demonstrate the integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="839d1-120">Create a new iOS project</span><span class="sxs-lookup"><span data-stu-id="839d1-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="839d1-121">Connect your app to Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="839d1-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="839d1-122">Download the [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="839d1-122">Download the [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="839d1-123">Extract the .tar.gz file to a folder in your computer</span><span class="sxs-lookup"><span data-stu-id="839d1-123">Extract the .tar.gz file to a folder in your computer</span></span>
3. <span data-ttu-id="839d1-124">Right click the project and select "Add files to ..."</span><span class="sxs-lookup"><span data-stu-id="839d1-124">Right click the project and select "Add files to ..."</span></span>
   
    ![][1]
4. <span data-ttu-id="839d1-125">Navigate to the folder where you extracted the SDK and select the `EngagementSDK` folder then press OK.</span><span class="sxs-lookup"><span data-stu-id="839d1-125">Navigate to the folder where you extracted the SDK and select the `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="839d1-126">Open the `Build Phases` tab and in the `Link Binary With Libraries` menu add the frameworks as shown below:</span><span class="sxs-lookup"><span data-stu-id="839d1-126">Open the `Build Phases` tab and in the `Link Binary With Libraries` menu add the frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="839d1-127">Create a Bridging header to be able to use the SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span><span class="sxs-lookup"><span data-stu-id="839d1-127">Create a Bridging header to be able to use the SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="839d1-128">Edit the bridging header file to expose Mobile Engagement Objective-C code to your Swift code, add the following imports :</span><span class="sxs-lookup"><span data-stu-id="839d1-128">Edit the bridging header file to expose Mobile Engagement Objective-C code to your Swift code, add the following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="839d1-129">Under Build Settings, make sure the Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path to this header.</span><span class="sxs-lookup"><span data-stu-id="839d1-129">Under Build Settings, make sure the Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path to this header.</span></span> <span data-ttu-id="839d1-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on the path)**</span><span class="sxs-lookup"><span data-stu-id="839d1-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on the path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="839d1-131">Go back to the Azure portal in your app's *Connection Info* page and copy the Connection String</span><span class="sxs-lookup"><span data-stu-id="839d1-131">Go back to the Azure portal in your app's *Connection Info* page and copy the Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="839d1-132">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate</span><span class="sxs-lookup"><span data-stu-id="839d1-132">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a><span data-ttu-id="839d1-133">Enabling real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="839d1-133">Enabling real-time monitoring</span></span>
<span data-ttu-id="839d1-134">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="839d1-134">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="839d1-135">Open the **ViewController.swift** file and replace the base class of **ViewController** to be **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="839d1-135">Open the **ViewController.swift** file and replace the base class of **ViewController** to be **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a><span data-ttu-id="839d1-136">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="839d1-136">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="839d1-137">Enabling Push Notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="839d1-137">Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="839d1-138">Mobile Engagement allows you to interact and REACH with your users with Push Notifications and In-app Messaging in the context of campaigns.</span><span class="sxs-lookup"><span data-stu-id="839d1-138">Mobile Engagement allows you to interact and REACH with your users with Push Notifications and In-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="839d1-139">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="839d1-139">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="839d1-140">The following sections will setup your app to receive them.</span><span class="sxs-lookup"><span data-stu-id="839d1-140">The following sections will setup your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="839d1-141">Enable your app to receive Silent Push Notifications</span><span class="sxs-lookup"><span data-stu-id="839d1-141">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="839d1-142">Add the Reach library to your project</span><span class="sxs-lookup"><span data-stu-id="839d1-142">Add the Reach library to your project</span></span>
1. <span data-ttu-id="839d1-143">Right click your project</span><span class="sxs-lookup"><span data-stu-id="839d1-143">Right click your project</span></span>
2. <span data-ttu-id="839d1-144">Select `Add file to ...`</span><span class="sxs-lookup"><span data-stu-id="839d1-144">Select `Add file to ...`</span></span>
3. <span data-ttu-id="839d1-145">Navigate to the folder where you extracted the SDK</span><span class="sxs-lookup"><span data-stu-id="839d1-145">Navigate to the folder where you extracted the SDK</span></span>
4. <span data-ttu-id="839d1-146">Select the `EngagementReach` folder</span><span class="sxs-lookup"><span data-stu-id="839d1-146">Select the `EngagementReach` folder</span></span>
5. <span data-ttu-id="839d1-147">Click Add</span><span class="sxs-lookup"><span data-stu-id="839d1-147">Click Add</span></span>
6. <span data-ttu-id="839d1-148">Edit the bridging header file to expose Mobile Engagement Objective-C Reach headers and add the following imports :</span><span class="sxs-lookup"><span data-stu-id="839d1-148">Edit the bridging header file to expose Mobile Engagement Objective-C Reach headers and add the following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="839d1-149">Modify your Application Delegate</span><span class="sxs-lookup"><span data-stu-id="839d1-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="839d1-150">Inside  the `didFinishLaunchingWithOptions` -  create a reach module and pass it to your existing Engagement initialization line:</span><span class="sxs-lookup"><span data-stu-id="839d1-150">Inside  the `didFinishLaunchingWithOptions` -  create a reach module and pass it to your existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="839d1-151">Enable your app to receive APNS Push Notifications</span><span class="sxs-lookup"><span data-stu-id="839d1-151">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="839d1-152">Add the following line to the `didFinishLaunchingWithOptions` method:</span><span class="sxs-lookup"><span data-stu-id="839d1-152">Add the following line to the `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="839d1-153">Add the `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span><span class="sxs-lookup"><span data-stu-id="839d1-153">Add the `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="839d1-154">Add the `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span><span class="sxs-lookup"><span data-stu-id="839d1-154">Add the `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-swift-get-started/add-bridging-header.png






