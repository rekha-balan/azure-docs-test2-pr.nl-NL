---
title: Azure Mobile Engagement iOS SDK Reach Integration | Microsoft Docs
description: Latest updates and procedures for iOS SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 7e24bbc1832c6a85181c943e4e1c705785358527
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563884"
---
# <a name="how-to-integrate-engagement-reach-on-ios"></a><span data-ttu-id="e7367-103">How to Integrate Engagement Reach on iOS</span><span class="sxs-lookup"><span data-stu-id="e7367-103">How to Integrate Engagement Reach on iOS</span></span>
<span data-ttu-id="e7367-104">You must follow the integration procedure described in the [How to Integrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span><span class="sxs-lookup"><span data-stu-id="e7367-104">You must follow the integration procedure described in the [How to Integrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="e7367-105">This documentation requires XCode 8.</span><span class="sxs-lookup"><span data-stu-id="e7367-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="e7367-106">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="e7367-106">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="e7367-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span><span class="sxs-lookup"><span data-stu-id="e7367-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="e7367-108">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span><span class="sxs-lookup"><span data-stu-id="e7367-108">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="e7367-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span><span class="sxs-lookup"><span data-stu-id="e7367-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="e7367-110">You should switch to XCode 8 as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="e7367-110">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="e7367-111">Enable your app to receive Silent Push Notifications</span><span class="sxs-lookup"><span data-stu-id="e7367-111">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="e7367-112">Integration steps</span><span class="sxs-lookup"><span data-stu-id="e7367-112">Integration steps</span></span>
### <a name="embed-the-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="e7367-113">Embed the Engagement Reach SDK into your iOS project</span><span class="sxs-lookup"><span data-stu-id="e7367-113">Embed the Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="e7367-114">Add the Reach sdk in your Xcode project.</span><span class="sxs-lookup"><span data-stu-id="e7367-114">Add the Reach sdk in your Xcode project.</span></span> <span data-ttu-id="e7367-115">In Xcode, go to **Project \> Add to project** and choose the `EngagementReach` folder.</span><span class="sxs-lookup"><span data-stu-id="e7367-115">In Xcode, go to **Project \> Add to project** and choose the `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="e7367-116">Modify your Application Delegate</span><span class="sxs-lookup"><span data-stu-id="e7367-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="e7367-117">At the top of your implementation file, import the Engagement Reach module:</span><span class="sxs-lookup"><span data-stu-id="e7367-117">At the top of your implementation file, import the Engagement Reach module:</span></span>
  
      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="e7367-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it to your existing Engagement initialization line:</span><span class="sxs-lookup"><span data-stu-id="e7367-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it to your existing Engagement initialization line:</span></span>
  
      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]
  
        return YES;
      }
* <span data-ttu-id="e7367-119">Modify **'icon.png'** string with the image name you want as your notification icon.</span><span class="sxs-lookup"><span data-stu-id="e7367-119">Modify **'icon.png'** string with the image name you want as your notification icon.</span></span>
* <span data-ttu-id="e7367-120">If you want to use the option *Update badge value* in Reach campaigns or if you want to use native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let the Reach module manage the badge icon itself (it will automatically clear the application badge and also reset the value stored by Engagement every time the application is started or foregrounded).</span><span class="sxs-lookup"><span data-stu-id="e7367-120">If you want to use the option *Update badge value* in Reach campaigns or if you want to use native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let the Reach module manage the badge icon itself (it will automatically clear the application badge and also reset the value stored by Engagement every time the application is started or foregrounded).</span></span> <span data-ttu-id="e7367-121">This is done by adding the following line after Reach module initialization:</span><span class="sxs-lookup"><span data-stu-id="e7367-121">This is done by adding the following line after Reach module initialization:</span></span>
  
      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="e7367-122">If you want to handle Reach data push, you must let your Application delegate conform to the `AEReachDataPushDelegate` protocol.</span><span class="sxs-lookup"><span data-stu-id="e7367-122">If you want to handle Reach data push, you must let your Application delegate conform to the `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="e7367-123">Add the following line after Reach module initialization:</span><span class="sxs-lookup"><span data-stu-id="e7367-123">Add the following line after Reach module initialization:</span></span>
  
      [reach setDataPushDelegate:self];
* <span data-ttu-id="e7367-124">Then you can implement the methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span><span class="sxs-lookup"><span data-stu-id="e7367-124">Then you can implement the methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>
  
      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }
  
      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a><span data-ttu-id="e7367-125">Category</span><span class="sxs-lookup"><span data-stu-id="e7367-125">Category</span></span>
<span data-ttu-id="e7367-126">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span><span class="sxs-lookup"><span data-stu-id="e7367-126">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="e7367-127">This is useful if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span><span class="sxs-lookup"><span data-stu-id="e7367-127">This is useful if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

<span data-ttu-id="e7367-128">**Your application is now ready to receive and display reach contents!**</span><span class="sxs-lookup"><span data-stu-id="e7367-128">**Your application is now ready to receive and display reach contents!**</span></span>

## <a name="how-to-receive-announcements-and-polls-at-any-time"></a><span data-ttu-id="e7367-129">How to receive announcements and polls at any time</span><span class="sxs-lookup"><span data-stu-id="e7367-129">How to receive announcements and polls at any time</span></span>
<span data-ttu-id="e7367-130">Engagement can send Reach notifications to your end users at any time by using the Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="e7367-130">Engagement can send Reach notifications to your end users at any time by using the Apple Push Notification Service.</span></span>

<span data-ttu-id="e7367-131">To enable this functionality, you'll have to prepare your application for Apple push notifications and modify your application delegate.</span><span class="sxs-lookup"><span data-stu-id="e7367-131">To enable this functionality, you'll have to prepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="e7367-132">Prepare your application for Apple push notifications</span><span class="sxs-lookup"><span data-stu-id="e7367-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="e7367-133">Please follow the guide : [How to Prepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="e7367-133">Please follow the guide : [How to Prepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-the-necessary-client-code"></a><span data-ttu-id="e7367-134">Add the necessary client code</span><span class="sxs-lookup"><span data-stu-id="e7367-134">Add the necessary client code</span></span>
<span data-ttu-id="e7367-135">*At this point your application should have a registered Apple push certificate in the Engagement frontend.*</span><span class="sxs-lookup"><span data-stu-id="e7367-135">*At this point your application should have a registered Apple push certificate in the Engagement frontend.*</span></span>

<span data-ttu-id="e7367-136">If it's not done already, you need to register your application to receive push notifications.</span><span class="sxs-lookup"><span data-stu-id="e7367-136">If it's not done already, you need to register your application to receive push notifications.</span></span>

* <span data-ttu-id="e7367-137">Import the `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="e7367-137">Import the `User Notification` framework:</span></span>
  
        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="e7367-138">Add the following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="e7367-138">Add the following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>
  
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

<span data-ttu-id="e7367-139">Then, You need to provide to Engagement the device token returned by Apple servers.</span><span class="sxs-lookup"><span data-stu-id="e7367-139">Then, You need to provide to Engagement the device token returned by Apple servers.</span></span> <span data-ttu-id="e7367-140">This is done in the method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span><span class="sxs-lookup"><span data-stu-id="e7367-140">This is done in the method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="e7367-141">Finally, you have to inform the Engagement SDK when your application receives a remote notification.</span><span class="sxs-lookup"><span data-stu-id="e7367-141">Finally, you have to inform the Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="e7367-142">To do that, call the method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span><span class="sxs-lookup"><span data-stu-id="e7367-142">To do that, call the method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!NOTE]
> <span data-ttu-id="e7367-143">The method above is introduced in iOS 7.</span><span class="sxs-lookup"><span data-stu-id="e7367-143">The method above is introduced in iOS 7.</span></span> <span data-ttu-id="e7367-144">If you are targeting iOS <7, make sure to implement method `application:didReceiveRemoteNotification:` in your application delegate and call `applicationDidReceiveRemoteNotification` on the EngagementAgent by passing nil instead of the `handler` argument:</span><span class="sxs-lookup"><span data-stu-id="e7367-144">If you are targeting iOS <7, make sure to implement method `application:didReceiveRemoteNotification:` in your application delegate and call `applicationDidReceiveRemoteNotification` on the EngagementAgent by passing nil instead of the `handler` argument:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="e7367-145">By default, Engagement Reach controls the completionHandler.</span><span class="sxs-lookup"><span data-stu-id="e7367-145">By default, Engagement Reach controls the completionHandler.</span></span> <span data-ttu-id="e7367-146">If you want to manually respond to the `handler` block in your code, you can pass nil for the `handler` argument and control the completion block yourself.</span><span class="sxs-lookup"><span data-stu-id="e7367-146">If you want to manually respond to the `handler` block in your code, you can pass nil for the `handler` argument and control the completion block yourself.</span></span> <span data-ttu-id="e7367-147">See the `UIBackgroundFetchResult` type for a list of possible values.</span><span class="sxs-lookup"><span data-stu-id="e7367-147">See the `UIBackgroundFetchResult` type for a list of possible values.</span></span>
> 
> 

### <a name="full-example"></a><span data-ttu-id="e7367-148">Full example</span><span class="sxs-lookup"><span data-stu-id="e7367-148">Full example</span></span>
<span data-ttu-id="e7367-149">Here is a full example of integration:</span><span class="sxs-lookup"><span data-stu-id="e7367-149">Here is a full example of integration:</span></span>

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="e7367-150">Resolve UNUserNotificationCenter delegate conflicts</span><span class="sxs-lookup"><span data-stu-id="e7367-150">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="e7367-151">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span><span class="sxs-lookup"><span data-stu-id="e7367-151">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="e7367-152">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span><span class="sxs-lookup"><span data-stu-id="e7367-152">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="e7367-153">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span><span class="sxs-lookup"><span data-stu-id="e7367-153">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="e7367-154">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span><span class="sxs-lookup"><span data-stu-id="e7367-154">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="e7367-155">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span><span class="sxs-lookup"><span data-stu-id="e7367-155">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="e7367-156">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span><span class="sxs-lookup"><span data-stu-id="e7367-156">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="e7367-157">There are two ways to achieve this.</span><span class="sxs-lookup"><span data-stu-id="e7367-157">There are two ways to achieve this.</span></span>

<span data-ttu-id="e7367-158">Proposal 1, simply by forwarding your delegate calls to the SDK:</span><span class="sxs-lookup"><span data-stu-id="e7367-158">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

<span data-ttu-id="e7367-159">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span><span class="sxs-lookup"><span data-stu-id="e7367-159">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> <span data-ttu-id="e7367-160">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span><span class="sxs-lookup"><span data-stu-id="e7367-160">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="e7367-161">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span><span class="sxs-lookup"><span data-stu-id="e7367-161">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="e7367-162">For instance, if you implemented the above proposal 1:</span><span class="sxs-lookup"><span data-stu-id="e7367-162">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="e7367-163">How to customize campaigns</span><span class="sxs-lookup"><span data-stu-id="e7367-163">How to customize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="e7367-164">Notifications</span><span class="sxs-lookup"><span data-stu-id="e7367-164">Notifications</span></span>
<span data-ttu-id="e7367-165">There are two types of notifications: system and in-app notifications.</span><span class="sxs-lookup"><span data-stu-id="e7367-165">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="e7367-166">System notifications are handled by iOS, and cannot be customized.</span><span class="sxs-lookup"><span data-stu-id="e7367-166">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="e7367-167">In-app notifications are made of a view that is dynamically added to the current application window.</span><span class="sxs-lookup"><span data-stu-id="e7367-167">In-app notifications are made of a view that is dynamically added to the current application window.</span></span> <span data-ttu-id="e7367-168">This is called a notification overlay.</span><span class="sxs-lookup"><span data-stu-id="e7367-168">This is called a notification overlay.</span></span> <span data-ttu-id="e7367-169">Notification overlays are great for a fast integration because they does not require you to modify any view in your application.</span><span class="sxs-lookup"><span data-stu-id="e7367-169">Notification overlays are great for a fast integration because they does not require you to modify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="e7367-170">Layout</span><span class="sxs-lookup"><span data-stu-id="e7367-170">Layout</span></span>
<span data-ttu-id="e7367-171">To modify the look of your in-app notifications, you can simply modify the file `AENotificationView.xib` to your needs, as long as you keep the tag values and types of the existing subviews.</span><span class="sxs-lookup"><span data-stu-id="e7367-171">To modify the look of your in-app notifications, you can simply modify the file `AENotificationView.xib` to your needs, as long as you keep the tag values and types of the existing subviews.</span></span>

<span data-ttu-id="e7367-172">By default, in-app notifications are presented at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="e7367-172">By default, in-app notifications are presented at the bottom of the screen.</span></span> <span data-ttu-id="e7367-173">If you prefer to display them at the top of screen, edit the provided `AENotificationView.xib` and change the `AutoSizing` property of the main view so it can be kept at the top of its superview.</span><span class="sxs-lookup"><span data-stu-id="e7367-173">If you prefer to display them at the top of screen, edit the provided `AENotificationView.xib` and change the `AutoSizing` property of the main view so it can be kept at the top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="e7367-174">Categories</span><span class="sxs-lookup"><span data-stu-id="e7367-174">Categories</span></span>
<span data-ttu-id="e7367-175">When you modify the provided layout, you modify the look of all your notifications.</span><span class="sxs-lookup"><span data-stu-id="e7367-175">When you modify the provided layout, you modify the look of all your notifications.</span></span> <span data-ttu-id="e7367-176">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span><span class="sxs-lookup"><span data-stu-id="e7367-176">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="e7367-177">A category can be specified when you create a Reach campaign.</span><span class="sxs-lookup"><span data-stu-id="e7367-177">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="e7367-178">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span><span class="sxs-lookup"><span data-stu-id="e7367-178">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="e7367-179">To register a category handler for your notifications, you need to add a call once the reach module is initialized.</span><span class="sxs-lookup"><span data-stu-id="e7367-179">To register a category handler for your notifications, you need to add a call once the reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="e7367-180">`myNotifier` must be an instance of an object that conforms to the protocol `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="e7367-180">`myNotifier` must be an instance of an object that conforms to the protocol `AENotifier`.</span></span>

<span data-ttu-id="e7367-181">You can implement the protocol methods by yourself or you can choose to reimplement the existing class `AEDefaultNotifier` which already performs most of the work.</span><span class="sxs-lookup"><span data-stu-id="e7367-181">You can implement the protocol methods by yourself or you can choose to reimplement the existing class `AEDefaultNotifier` which already performs most of the work.</span></span>

<span data-ttu-id="e7367-182">For example, if you want to redefine the notification view for a specific category, you can follow this example:</span><span class="sxs-lookup"><span data-stu-id="e7367-182">For example, if you want to redefine the notification view for a specific category, you can follow this example:</span></span>

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

<span data-ttu-id="e7367-183">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span><span class="sxs-lookup"><span data-stu-id="e7367-183">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="e7367-184">If the method is not able to find a corresponding `.xib`, the notification will not be displayed and Engagement will output a message in the console.</span><span class="sxs-lookup"><span data-stu-id="e7367-184">If the method is not able to find a corresponding `.xib`, the notification will not be displayed and Engagement will output a message in the console.</span></span>

<span data-ttu-id="e7367-185">The provided nib file should respect the following rules:</span><span class="sxs-lookup"><span data-stu-id="e7367-185">The provided nib file should respect the following rules:</span></span>

* <span data-ttu-id="e7367-186">It should only contain one view.</span><span class="sxs-lookup"><span data-stu-id="e7367-186">It should only contain one view.</span></span>
* <span data-ttu-id="e7367-187">Subviews should be of the same types as the ones inside the provided nib file named `AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="e7367-187">Subviews should be of the same types as the ones inside the provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="e7367-188">Subviews should have the same tags as the ones inside the provided nib file named `AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="e7367-188">Subviews should have the same tags as the ones inside the provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="e7367-189">Just copy the provided nib file, named `AENotificationView.xib`, and start working from there.</span><span class="sxs-lookup"><span data-stu-id="e7367-189">Just copy the provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="e7367-190">But be careful, the view inside this nib file is associated to the class `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="e7367-190">But be careful, the view inside this nib file is associated to the class `AENotificationView`.</span></span> <span data-ttu-id="e7367-191">This class redefined the method `layoutSubViews` to move and resize its subviews according to context.</span><span class="sxs-lookup"><span data-stu-id="e7367-191">This class redefined the method `layoutSubViews` to move and resize its subviews according to context.</span></span> <span data-ttu-id="e7367-192">You may want to replace it with an `UIView` or you custom view class.</span><span class="sxs-lookup"><span data-stu-id="e7367-192">You may want to replace it with an `UIView` or you custom view class.</span></span>
> 
> 

<span data-ttu-id="e7367-193">If you need deeper customization of your notifications(if you want for instance to load your view directly from the code), it is recommended to take a look at the provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="e7367-193">If you need deeper customization of your notifications(if you want for instance to load your view directly from the code), it is recommended to take a look at the provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="e7367-194">Note that you can use the same notifier for multiple categories.</span><span class="sxs-lookup"><span data-stu-id="e7367-194">Note that you can use the same notifier for multiple categories.</span></span>

<span data-ttu-id="e7367-195">You can also redefined the default notifier like this:</span><span class="sxs-lookup"><span data-stu-id="e7367-195">You can also redefined the default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="e7367-196">Notification handling</span><span class="sxs-lookup"><span data-stu-id="e7367-196">Notification handling</span></span>
<span data-ttu-id="e7367-197">When using the default category, some life cycle methods are called on the `AEReachContent` object to report statistics and update the campaign state:</span><span class="sxs-lookup"><span data-stu-id="e7367-197">When using the default category, some life cycle methods are called on the `AEReachContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="e7367-198">When the notification is displayed in application, the `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span><span class="sxs-lookup"><span data-stu-id="e7367-198">When the notification is displayed in application, the `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="e7367-199">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span><span class="sxs-lookup"><span data-stu-id="e7367-199">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="e7367-200">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated action is performed.</span><span class="sxs-lookup"><span data-stu-id="e7367-200">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated action is performed.</span></span>

<span data-ttu-id="e7367-201">If your implementation of `AENotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span><span class="sxs-lookup"><span data-stu-id="e7367-201">If your implementation of `AENotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="e7367-202">The following examples illustrate some cases where the default behavior is bypassed:</span><span class="sxs-lookup"><span data-stu-id="e7367-202">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="e7367-203">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span><span class="sxs-lookup"><span data-stu-id="e7367-203">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="e7367-204">You overrode `prepareNotificationView:forContent:`, be sure to map at least `onNotificationActioned` or `onNotificationExited` to one of your U.I controls.</span><span class="sxs-lookup"><span data-stu-id="e7367-204">You overrode `prepareNotificationView:forContent:`, be sure to map at least `onNotificationActioned` or `onNotificationExited` to one of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="e7367-205">If `handleNotification:` throws an exception, the content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span><span class="sxs-lookup"><span data-stu-id="e7367-205">If `handleNotification:` throws an exception, the content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="e7367-206">Include notification as part of an existing view</span><span class="sxs-lookup"><span data-stu-id="e7367-206">Include notification as part of an existing view</span></span>
<span data-ttu-id="e7367-207">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span><span class="sxs-lookup"><span data-stu-id="e7367-207">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="e7367-208">If you're not satisfied with the overlay system in some of your views, you can customize it for these views.</span><span class="sxs-lookup"><span data-stu-id="e7367-208">If you're not satisfied with the overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="e7367-209">You can decide to include our notification layout in your existing views.</span><span class="sxs-lookup"><span data-stu-id="e7367-209">You can decide to include our notification layout in your existing views.</span></span> <span data-ttu-id="e7367-210">To do so, there is two implementation styles:</span><span class="sxs-lookup"><span data-stu-id="e7367-210">To do so, there is two implementation styles:</span></span>

1. <span data-ttu-id="e7367-211">Add the notification view using interface builder</span><span class="sxs-lookup"><span data-stu-id="e7367-211">Add the notification view using interface builder</span></span>
   
   * <span data-ttu-id="e7367-212">Open *Interface Builder*</span><span class="sxs-lookup"><span data-stu-id="e7367-212">Open *Interface Builder*</span></span>
   * <span data-ttu-id="e7367-213">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want the notification to appear</span><span class="sxs-lookup"><span data-stu-id="e7367-213">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want the notification to appear</span></span>
   * <span data-ttu-id="e7367-214">Set the Tag value for this view to : **36822491**</span><span class="sxs-lookup"><span data-stu-id="e7367-214">Set the Tag value for this view to : **36822491**</span></span>
2. <span data-ttu-id="e7367-215">Add the notification view programmatically.</span><span class="sxs-lookup"><span data-stu-id="e7367-215">Add the notification view programmatically.</span></span> <span data-ttu-id="e7367-216">Just add the following code when your view has been initialized:</span><span class="sxs-lookup"><span data-stu-id="e7367-216">Just add the following code when your view has been initialized:</span></span>
   
       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values to your needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="e7367-217">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="e7367-217">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="e7367-218">The default notifier automatically detects that the notification layout is included in this view and will not add an overlay for it.</span><span class="sxs-lookup"><span data-stu-id="e7367-218">The default notifier automatically detects that the notification layout is included in this view and will not add an overlay for it.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="e7367-219">Announcements and polls</span><span class="sxs-lookup"><span data-stu-id="e7367-219">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="e7367-220">Layouts</span><span class="sxs-lookup"><span data-stu-id="e7367-220">Layouts</span></span>
<span data-ttu-id="e7367-221">You can modify the files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep the tag values and types of the existing subviews.</span><span class="sxs-lookup"><span data-stu-id="e7367-221">You can modify the files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep the tag values and types of the existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="e7367-222">Categories</span><span class="sxs-lookup"><span data-stu-id="e7367-222">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="e7367-223">Alternate layouts</span><span class="sxs-lookup"><span data-stu-id="e7367-223">Alternate layouts</span></span>
<span data-ttu-id="e7367-224">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span><span class="sxs-lookup"><span data-stu-id="e7367-224">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="e7367-225">To create a category for an announcement, you must extend **AEAnnouncementViewController** and register it once the reach module has been initialized:</span><span class="sxs-lookup"><span data-stu-id="e7367-225">To create a category for an announcement, you must extend **AEAnnouncementViewController** and register it once the reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="e7367-226">Each time a user will click on a notification for an announcement with the category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling the method `initWithAnnouncement:` and the view will be added to the current application window.</span><span class="sxs-lookup"><span data-stu-id="e7367-226">Each time a user will click on a notification for an announcement with the category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling the method `initWithAnnouncement:` and the view will be added to the current application window.</span></span>
> 
> 

<span data-ttu-id="e7367-227">In your implementation of the `AEAnnouncementViewController` class you will have to read the property `announcement` to initialize your subviews.</span><span class="sxs-lookup"><span data-stu-id="e7367-227">In your implementation of the `AEAnnouncementViewController` class you will have to read the property `announcement` to initialize your subviews.</span></span> <span data-ttu-id="e7367-228">Consider the example below, where two labels are initialized using `title` and `body` properties of the `AEReachAnnouncement` class:</span><span class="sxs-lookup"><span data-stu-id="e7367-228">Consider the example below, where two labels are initialized using `title` and `body` properties of the `AEReachAnnouncement` class:</span></span>

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

<span data-ttu-id="e7367-229">If you don't want to load your views by yourself but you just want to reuse the default announcement view layout, you can simply make your custom view controller extends the provided class `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="e7367-229">If you don't want to load your views by yourself but you just want to reuse the default announcement view layout, you can simply make your custom view controller extends the provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="e7367-230">In that case, duplicate the nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="e7367-230">In that case, duplicate the nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="e7367-231">To replace the default category of announcements, simply register your custom view controller for the category defined in `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="e7367-231">To replace the default category of announcements, simply register your custom view controller for the category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="e7367-232">Polls can be customized the same way :</span><span class="sxs-lookup"><span data-stu-id="e7367-232">Polls can be customized the same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="e7367-233">This time, the provided `MyCustomPollViewController` must extend `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="e7367-233">This time, the provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="e7367-234">Or you can choose to extend from the default controller: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="e7367-234">Or you can choose to extend from the default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7367-235">Don't forget to call either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before the view controller is dismissed.</span><span class="sxs-lookup"><span data-stu-id="e7367-235">Don't forget to call either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before the view controller is dismissed.</span></span> <span data-ttu-id="e7367-236">Otherwise, statistics won't be sent (i.e. no analytics on the campaign) and more importantly next campaigns will not be notified until the application process is restarted.</span><span class="sxs-lookup"><span data-stu-id="e7367-236">Otherwise, statistics won't be sent (i.e. no analytics on the campaign) and more importantly next campaigns will not be notified until the application process is restarted.</span></span>
> 
> 

##### <a name="implementation-example"></a><span data-ttu-id="e7367-237">Implementation example</span><span class="sxs-lookup"><span data-stu-id="e7367-237">Implementation example</span></span>
<span data-ttu-id="e7367-238">In this implementation the custom announcement view is loaded from an external xib file.</span><span class="sxs-lookup"><span data-stu-id="e7367-238">In this implementation the custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="e7367-239">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span><span class="sxs-lookup"><span data-stu-id="e7367-239">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
