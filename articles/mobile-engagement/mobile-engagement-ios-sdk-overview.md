---
title: Azure Mobile Engagement iOS SDK Overview | Microsoft Docs
description: Latest updates and procedures for iOS SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: cd70b0b5656bef08a8be1c1a67754b203cceb905
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556541"
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="d416b-103">iOS SDK for Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d416b-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="d416b-104">Start here to get all the details on how to integrate Azure Mobile Engagement in an iOS App.</span><span class="sxs-lookup"><span data-stu-id="d416b-104">Start here to get all the details on how to integrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="d416b-105">If you'd like to give it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d416b-105">If you'd like to give it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="d416b-106">Click to see the [SDK Content](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="d416b-106">Click to see the [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="d416b-107">Integration procedures</span><span class="sxs-lookup"><span data-stu-id="d416b-107">Integration procedures</span></span>
1. <span data-ttu-id="d416b-108">Start here: [How to integrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="d416b-108">Start here: [How to integrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="d416b-109">For Notifications: [How to integrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="d416b-109">For Notifications: [How to integrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="d416b-110">Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="d416b-110">Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="d416b-111">Release notes</span><span class="sxs-lookup"><span data-stu-id="d416b-111">Release notes</span></span>
### <a name="401-12132016"></a><span data-ttu-id="d416b-112">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="d416b-112">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="d416b-113">Improved log delivery in background.</span><span class="sxs-lookup"><span data-stu-id="d416b-113">Improved log delivery in background.</span></span>

<span data-ttu-id="d416b-114">For earlier version please see the [complete release notes](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="d416b-114">For earlier version please see the [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="d416b-115">Upgrade procedures</span><span class="sxs-lookup"><span data-stu-id="d416b-115">Upgrade procedures</span></span>
<span data-ttu-id="d416b-116">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span><span class="sxs-lookup"><span data-stu-id="d416b-116">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="d416b-117">You may have to follow several procedures if you missed several versions of the SDK see the complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="d416b-117">You may have to follow several procedures if you missed several versions of the SDK see the complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="d416b-118">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span><span class="sxs-lookup"><span data-stu-id="d416b-118">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-to-400"></a><span data-ttu-id="d416b-119">From 3.0.0 to 4.0.0</span><span class="sxs-lookup"><span data-stu-id="d416b-119">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="d416b-120">XCode 8</span><span class="sxs-lookup"><span data-stu-id="d416b-120">XCode 8</span></span>
<span data-ttu-id="d416b-121">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span><span class="sxs-lookup"><span data-stu-id="d416b-121">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="d416b-122">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="d416b-122">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="d416b-123">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span><span class="sxs-lookup"><span data-stu-id="d416b-123">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="d416b-124">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span><span class="sxs-lookup"><span data-stu-id="d416b-124">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="d416b-125">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span><span class="sxs-lookup"><span data-stu-id="d416b-125">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="d416b-126">You should switch to XCode 8 as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="d416b-126">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

#### <a name="usernotifications-framework"></a><span data-ttu-id="d416b-127">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="d416b-127">UserNotifications framework</span></span>
<span data-ttu-id="d416b-128">You need to add the `UserNotifications` framework in your Build Phases.</span><span class="sxs-lookup"><span data-stu-id="d416b-128">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="d416b-129">in the project explorer, open your project pane and select the correct target.</span><span class="sxs-lookup"><span data-stu-id="d416b-129">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="d416b-130">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span><span class="sxs-lookup"><span data-stu-id="d416b-130">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="d416b-131">Application push capability</span><span class="sxs-lookup"><span data-stu-id="d416b-131">Application push capability</span></span>
<span data-ttu-id="d416b-132">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span><span class="sxs-lookup"><span data-stu-id="d416b-132">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

#### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="d416b-133">Add the new iOS 10 notification registration code</span><span class="sxs-lookup"><span data-stu-id="d416b-133">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="d416b-134">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span><span class="sxs-lookup"><span data-stu-id="d416b-134">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span> 

<span data-ttu-id="d416b-135">Import the `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="d416b-135">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="d416b-136">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span><span class="sxs-lookup"><span data-stu-id="d416b-136">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="d416b-137">by :</span><span class="sxs-lookup"><span data-stu-id="d416b-137">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="d416b-138">Resolve UNUserNotificationCenter delegate conflicts</span><span class="sxs-lookup"><span data-stu-id="d416b-138">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="d416b-139">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span><span class="sxs-lookup"><span data-stu-id="d416b-139">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="d416b-140">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span><span class="sxs-lookup"><span data-stu-id="d416b-140">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="d416b-141">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span><span class="sxs-lookup"><span data-stu-id="d416b-141">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="d416b-142">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span><span class="sxs-lookup"><span data-stu-id="d416b-142">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="d416b-143">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span><span class="sxs-lookup"><span data-stu-id="d416b-143">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="d416b-144">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span><span class="sxs-lookup"><span data-stu-id="d416b-144">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="d416b-145">There are two ways to achieve this.</span><span class="sxs-lookup"><span data-stu-id="d416b-145">There are two ways to achieve this.</span></span>

<span data-ttu-id="d416b-146">Proposal 1, simply by forwarding your delegate calls to the SDK:</span><span class="sxs-lookup"><span data-stu-id="d416b-146">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="d416b-147">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span><span class="sxs-lookup"><span data-stu-id="d416b-147">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="d416b-148">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span><span class="sxs-lookup"><span data-stu-id="d416b-148">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="d416b-149">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span><span class="sxs-lookup"><span data-stu-id="d416b-149">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="d416b-150">For instance, if you implemented the above proposal 1:</span><span class="sxs-lookup"><span data-stu-id="d416b-150">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

