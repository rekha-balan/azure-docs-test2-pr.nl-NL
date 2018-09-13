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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Get Started with Azure Mobile Engagement for iOS apps in Objective C
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.
In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).

This tutorial requires the following:

* XCode 8, which you can install from your MAC App Store
* the [Mobile Engagement iOS SDK]

Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.

> [!NOTE]
> To complete this tutorial, you must have an active Azure account. If you don't have an account, you can create a free trial account in just a couple of minutes. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Setup Mobile Engagement for your iOS app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Connect your app to the Mobile Engagement backend
This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification. The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)

We will create a basic app with XCode to demonstrate the integration.

### <a name="create-a-new-ios-project"></a>Create a new iOS project
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a>Connect your app to the Mobile Engagement backend
1. Download the [Mobile Engagement iOS SDK].
2. Extract the .tar.gz file to a folder in your computer.
3. Right-click the project, and then select **Add files to**.
   
    ![][1]
4. Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, and then press **OK**.
   
    ![][2]
5. Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:
   
    ![][3]
6. Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.
   
    ![][4]
7. Add the following line of code in your **AppDelegate.m** file.
   
        #import "EngagementAgent.h"
8. Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues. 

## <a id="monitor"></a>Enable real-time monitoring
In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.

1. Open the **ViewController.h** file and import **EngagementViewController.h**:
   
    `# import "EngagementViewController.h"`
2. Now replace the super class of the **ViewController** interface by `EngagementViewController`:
   
    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>Connect app with real-time monitoring
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Enable push notifications and in-app messaging
Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns. This module is called REACH in the Mobile Engagement portal.
The following sections set up your app to receive them.

### <a name="enable-your-app-to-receive-silent-push-notifications"></a>Enable your app to receive Silent Push Notifications
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a>Add the Reach library to your project
1. Right-click your project.
2. Select **Add file to**.
3. Navigate to the folder where you extracted the SDK.
4. Select the `EngagementReach` folder.
5. Click **Add**.

### <a name="modify-your-application-delegate"></a>Modify your Application Delegate
1. Back in **AppDeletegate.m** file, import the Engagement Reach module.
   
        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a>Enable your app to receive APNS Push Notifications
1. Add the following line to the `application:didFinishLaunchingWithOptions` method:
   
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
2. Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:
   
        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
   
           NSLog(@"Failed to get token, error: %@", error);
        }
4. Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:
   
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





