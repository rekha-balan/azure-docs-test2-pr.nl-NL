---
title: Get Started with Azure Mobile Engagement for iOS in Objective C | Microsoft Docs
description: Learn how to use Azure Mobile Engagement with analytics and push notifications for iOS apps.
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/05/2016
ms.author: piyushjo
ms.openlocfilehash: 789e0c5126a640d699802578e5ea5cb3a2cd45b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564686"
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="9666d-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span><span class="sxs-lookup"><span data-stu-id="9666d-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="9666d-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span><span class="sxs-lookup"><span data-stu-id="9666d-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="9666d-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="9666d-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="9666d-106">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="9666d-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="9666d-107">XCode 8, which you can install from your MAC App Store</span><span class="sxs-lookup"><span data-stu-id="9666d-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="9666d-108">the [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="9666d-108">the [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="9666d-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span><span class="sxs-lookup"><span data-stu-id="9666d-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="9666d-110">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="9666d-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9666d-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="9666d-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9666d-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="9666d-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
> 
> 

## <a id="setup-azme"></a><span data-ttu-id="9666d-113">Setup Mobile Engagement for your iOS app</span><span class="sxs-lookup"><span data-stu-id="9666d-113">Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="9666d-114">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="9666d-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="9666d-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span><span class="sxs-lookup"><span data-stu-id="9666d-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="9666d-116">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9666d-116">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="9666d-117">We will create a basic app with XCode to demonstrate the integration.</span><span class="sxs-lookup"><span data-stu-id="9666d-117">We will create a basic app with XCode to demonstrate the integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="9666d-118">Create a new iOS project</span><span class="sxs-lookup"><span data-stu-id="9666d-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="9666d-119">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="9666d-119">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="9666d-120">Download the [Mobile Engagement iOS SDK].</span><span class="sxs-lookup"><span data-stu-id="9666d-120">Download the [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="9666d-121">Extract the .tar.gz file to a folder in your computer.</span><span class="sxs-lookup"><span data-stu-id="9666d-121">Extract the .tar.gz file to a folder in your computer.</span></span>
3. <span data-ttu-id="9666d-122">Right-click the project, and then select **Add files to**.</span><span class="sxs-lookup"><span data-stu-id="9666d-122">Right-click the project, and then select **Add files to**.</span></span>
   
    ![][1]
4. <span data-ttu-id="9666d-123">Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, and then press **OK**.</span><span class="sxs-lookup"><span data-stu-id="9666d-123">Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, and then press **OK**.</span></span>
   
    ![][2]
5. <span data-ttu-id="9666d-124">Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:</span><span class="sxs-lookup"><span data-stu-id="9666d-124">Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="9666d-125">Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.</span><span class="sxs-lookup"><span data-stu-id="9666d-125">Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.</span></span>
   
    ![][4]
7. <span data-ttu-id="9666d-126">Add the following line of code in your **AppDelegate.m** file.</span><span class="sxs-lookup"><span data-stu-id="9666d-126">Add the following line of code in your **AppDelegate.m** file.</span></span>
   
        #import "EngagementAgent.h"
8. <span data-ttu-id="9666d-127">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.</span><span class="sxs-lookup"><span data-stu-id="9666d-127">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.</span></span>
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="9666d-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues.</span><span class="sxs-lookup"><span data-stu-id="9666d-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues.</span></span> 

## <a id="monitor"></a><span data-ttu-id="9666d-129">Enable real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="9666d-129">Enable real-time monitoring</span></span>
<span data-ttu-id="9666d-130">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="9666d-130">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="9666d-131">Open the **ViewController.h** file and import **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="9666d-131">Open the **ViewController.h** file and import **EngagementViewController.h**:</span></span>
   
    `# import "EngagementViewController.h"`
2. <span data-ttu-id="9666d-132">Now replace the super class of the **ViewController** interface by `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="9666d-132">Now replace the super class of the **ViewController** interface by `EngagementViewController`:</span></span>
   
    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a><span data-ttu-id="9666d-133">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="9666d-133">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="9666d-134">Enable push notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="9666d-134">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="9666d-135">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span><span class="sxs-lookup"><span data-stu-id="9666d-135">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="9666d-136">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="9666d-136">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="9666d-137">The following sections set up your app to receive them.</span><span class="sxs-lookup"><span data-stu-id="9666d-137">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="9666d-138">Enable your app to receive Silent Push Notifications</span><span class="sxs-lookup"><span data-stu-id="9666d-138">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="9666d-139">Add the Reach library to your project</span><span class="sxs-lookup"><span data-stu-id="9666d-139">Add the Reach library to your project</span></span>
1. <span data-ttu-id="9666d-140">Right-click your project.</span><span class="sxs-lookup"><span data-stu-id="9666d-140">Right-click your project.</span></span>
2. <span data-ttu-id="9666d-141">Select **Add file to**.</span><span class="sxs-lookup"><span data-stu-id="9666d-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="9666d-142">Navigate to the folder where you extracted the SDK.</span><span class="sxs-lookup"><span data-stu-id="9666d-142">Navigate to the folder where you extracted the SDK.</span></span>
4. <span data-ttu-id="9666d-143">Select the `EngagementReach` folder.</span><span class="sxs-lookup"><span data-stu-id="9666d-143">Select the `EngagementReach` folder.</span></span>
5. <span data-ttu-id="9666d-144">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="9666d-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="9666d-145">Modify your Application Delegate</span><span class="sxs-lookup"><span data-stu-id="9666d-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="9666d-146">Back in **AppDeletegate.m** file, import the Engagement Reach module.</span><span class="sxs-lookup"><span data-stu-id="9666d-146">Back in **AppDeletegate.m** file, import the Engagement Reach module.</span></span>
   
        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="9666d-147">Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:</span><span class="sxs-lookup"><span data-stu-id="9666d-147">Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:</span></span>
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="9666d-148">Enable your app to receive APNS Push Notifications</span><span class="sxs-lookup"><span data-stu-id="9666d-148">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="9666d-149">Add the following line to the `application:didFinishLaunchingWithOptions` method:</span><span class="sxs-lookup"><span data-stu-id="9666d-149">Add the following line to the `application:didFinishLaunchingWithOptions` method:</span></span>
   
        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. <span data-ttu-id="9666d-150">Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span><span class="sxs-lookup"><span data-stu-id="9666d-150">Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="9666d-151">Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span><span class="sxs-lookup"><span data-stu-id="9666d-151">Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>
   
        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
   
           NSLog(@"Failed to get token, error: %@", error);
        }
4. <span data-ttu-id="9666d-152">Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span><span class="sxs-lookup"><span data-stu-id="9666d-152">Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>
   
        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-ios-get-started/app-connection-info-page.png





