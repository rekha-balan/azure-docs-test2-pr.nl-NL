---
title: Azure Mobile Engagement iOS SDK Upgrade Procedure | Microsoft Docs
description: Latest updates and procedures for iOS SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554126"
---
# <a name="upgrade-procedures"></a><span data-ttu-id="fd293-103">Upgrade procedures</span><span class="sxs-lookup"><span data-stu-id="fd293-103">Upgrade procedures</span></span>
<span data-ttu-id="fd293-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span><span class="sxs-lookup"><span data-stu-id="fd293-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="fd293-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span><span class="sxs-lookup"><span data-stu-id="fd293-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="fd293-106">From 3.0.0 to 4.0.0</span><span class="sxs-lookup"><span data-stu-id="fd293-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="fd293-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="fd293-107">XCode 8</span></span>
<span data-ttu-id="fd293-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span><span class="sxs-lookup"><span data-stu-id="fd293-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="fd293-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="fd293-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="fd293-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span><span class="sxs-lookup"><span data-stu-id="fd293-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="fd293-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span><span class="sxs-lookup"><span data-stu-id="fd293-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="fd293-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span><span class="sxs-lookup"><span data-stu-id="fd293-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="fd293-113">You should switch to XCode 8 as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="fd293-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="fd293-114">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="fd293-114">UserNotifications framework</span></span>
<span data-ttu-id="fd293-115">You need to add the `UserNotifications` framework in your Build Phases.</span><span class="sxs-lookup"><span data-stu-id="fd293-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="fd293-116">in the project explorer, open your project pane and select the correct target.</span><span class="sxs-lookup"><span data-stu-id="fd293-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="fd293-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span><span class="sxs-lookup"><span data-stu-id="fd293-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="fd293-118">Application push capability</span><span class="sxs-lookup"><span data-stu-id="fd293-118">Application push capability</span></span>
<span data-ttu-id="fd293-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span><span class="sxs-lookup"><span data-stu-id="fd293-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="fd293-120">Add the new iOS 10 notification registration code</span><span class="sxs-lookup"><span data-stu-id="fd293-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="fd293-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span><span class="sxs-lookup"><span data-stu-id="fd293-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="fd293-122">Import the `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="fd293-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="fd293-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span><span class="sxs-lookup"><span data-stu-id="fd293-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="fd293-124">by :</span><span class="sxs-lookup"><span data-stu-id="fd293-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="fd293-125">Resolve UNUserNotificationCenter delegate conflicts</span><span class="sxs-lookup"><span data-stu-id="fd293-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="fd293-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span><span class="sxs-lookup"><span data-stu-id="fd293-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="fd293-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span><span class="sxs-lookup"><span data-stu-id="fd293-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="fd293-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span><span class="sxs-lookup"><span data-stu-id="fd293-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="fd293-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span><span class="sxs-lookup"><span data-stu-id="fd293-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="fd293-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span><span class="sxs-lookup"><span data-stu-id="fd293-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="fd293-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span><span class="sxs-lookup"><span data-stu-id="fd293-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="fd293-132">There are two ways to achieve this.</span><span class="sxs-lookup"><span data-stu-id="fd293-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="fd293-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span><span class="sxs-lookup"><span data-stu-id="fd293-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="fd293-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span><span class="sxs-lookup"><span data-stu-id="fd293-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="fd293-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span><span class="sxs-lookup"><span data-stu-id="fd293-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="fd293-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span><span class="sxs-lookup"><span data-stu-id="fd293-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="fd293-137">For instance, if you implemented the above proposal 1:</span><span class="sxs-lookup"><span data-stu-id="fd293-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="fd293-138">From 2.0.0 to 3.0.0</span><span class="sxs-lookup"><span data-stu-id="fd293-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="fd293-139">Dropped support for iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="fd293-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="fd293-140">Starting from this version the deployment target of your application must be at least iOS 6.</span><span class="sxs-lookup"><span data-stu-id="fd293-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="fd293-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span><span class="sxs-lookup"><span data-stu-id="fd293-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="fd293-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span><span class="sxs-lookup"><span data-stu-id="fd293-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="fd293-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span><span class="sxs-lookup"><span data-stu-id="fd293-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="fd293-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span><span class="sxs-lookup"><span data-stu-id="fd293-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="fd293-145">From 1.16.0 to 2.0.0</span><span class="sxs-lookup"><span data-stu-id="fd293-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="fd293-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fd293-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="fd293-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span><span class="sxs-lookup"><span data-stu-id="fd293-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd293-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span><span class="sxs-lookup"><span data-stu-id="fd293-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="fd293-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span><span class="sxs-lookup"><span data-stu-id="fd293-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="fd293-150">Agent</span><span class="sxs-lookup"><span data-stu-id="fd293-150">Agent</span></span>
<span data-ttu-id="fd293-151">The method `registerApp:` has been replaced by the new method `init:`.</span><span class="sxs-lookup"><span data-stu-id="fd293-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="fd293-152">Your application delegate must be updated accordingly and use connection string:</span><span class="sxs-lookup"><span data-stu-id="fd293-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="fd293-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span><span class="sxs-lookup"><span data-stu-id="fd293-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="fd293-154">Class Name Changes</span><span class="sxs-lookup"><span data-stu-id="fd293-154">Class Name Changes</span></span>
<span data-ttu-id="fd293-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span><span class="sxs-lookup"><span data-stu-id="fd293-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="fd293-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span><span class="sxs-lookup"><span data-stu-id="fd293-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="fd293-157">Example:</span><span class="sxs-lookup"><span data-stu-id="fd293-157">Example:</span></span>

* <span data-ttu-id="fd293-158">`CPModule.h` is renamed to `AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="fd293-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="fd293-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span><span class="sxs-lookup"><span data-stu-id="fd293-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="fd293-160">Examples:</span><span class="sxs-lookup"><span data-stu-id="fd293-160">Examples:</span></span>

* <span data-ttu-id="fd293-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="fd293-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="fd293-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="fd293-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="fd293-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="fd293-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="fd293-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="fd293-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>

