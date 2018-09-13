---
title: Azure Mobile Engagement iOS SDK Integration | Microsoft Docs
description: Latest updates and procedures for iOS SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 09/14/2016
ms.author: piyushjo
ms.openlocfilehash: 58baae6fb3d338ef94caca79b9248afc0fb7f841
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562911"
---
# <a name="how-to-integrate-engagement-on-ios"></a><span data-ttu-id="c8833-103">How to Integrate Engagement on iOS</span><span class="sxs-lookup"><span data-stu-id="c8833-103">How to Integrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="c8833-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span><span class="sxs-lookup"><span data-stu-id="c8833-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="c8833-109">The Engagement SDK requires iOS6+ and Xcode 8: the deployment target of your application must be at least iOS 6.</span><span class="sxs-lookup"><span data-stu-id="c8833-109">The Engagement SDK requires iOS6+ and Xcode 8: the deployment target of your application must be at least iOS 6.</span></span>

> [!NOTE]
> If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). There is a known bug on the Reach module of this previous version while running on iOS 10 devices see [the reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details. If you choose to use the SDK v3.2.4 then just skip the `UserNotifications.framework` import in the next step.
> 
> 

<span data-ttu-id="c8833-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span><span class="sxs-lookup"><span data-stu-id="c8833-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="c8833-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span><span class="sxs-lookup"><span data-stu-id="c8833-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="c8833-115">Embed the Engagement SDK into your iOS project</span><span class="sxs-lookup"><span data-stu-id="c8833-115">Embed the Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="c8833-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="c8833-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="c8833-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span><span class="sxs-lookup"><span data-stu-id="c8833-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span></span>
* <span data-ttu-id="c8833-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span><span class="sxs-lookup"><span data-stu-id="c8833-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="c8833-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span><span class="sxs-lookup"><span data-stu-id="c8833-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span></span>
  
  * <span data-ttu-id="c8833-120">`UserNotifications.framework` - set the link as `Optional`</span><span class="sxs-lookup"><span data-stu-id="c8833-120">`UserNotifications.framework` - set the link as `Optional`</span></span>
  * <span data-ttu-id="c8833-121">`AdSupport.framework` - set the link as `Optional`</span><span class="sxs-lookup"><span data-stu-id="c8833-121">`AdSupport.framework` - set the link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> The AdSupport framework can be removed. Engagement needs this framework to collect the IDFA. However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> to comply with the new Apple policy regarding this ID.
> 
> 

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="c8833-125">Initialize the Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="c8833-125">Initialize the Engagement SDK</span></span>
<span data-ttu-id="c8833-126">You need to modify your Application Delegate:</span><span class="sxs-lookup"><span data-stu-id="c8833-126">You need to modify your Application Delegate:</span></span>

* <span data-ttu-id="c8833-127">At the top of your implementation file, import the Engagement agent:</span><span class="sxs-lookup"><span data-stu-id="c8833-127">At the top of your implementation file, import the Engagement agent:</span></span>
  
      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="c8833-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="c8833-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>
  
      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="c8833-129">Basic reporting</span><span class="sxs-lookup"><span data-stu-id="c8833-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="c8833-130">Recommended method: overload your `UIViewController` classes</span><span class="sxs-lookup"><span data-stu-id="c8833-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="c8833-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="c8833-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="c8833-132">**Without Engagement :**</span><span class="sxs-lookup"><span data-stu-id="c8833-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="c8833-133">**With Engagement :**</span><span class="sxs-lookup"><span data-stu-id="c8833-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="c8833-134">Alternate method: call `startActivity()` manually</span><span class="sxs-lookup"><span data-stu-id="c8833-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="c8833-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span><span class="sxs-lookup"><span data-stu-id="c8833-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> The iOS SDK automatically calls the `endActivity()` method when the application is closed. Thus, it is *HIGHLY* recommended to call the `startActivity` method whenever the activity of the user change, and to *NEVER* call the `endActivity` method, since calling this method forces the current session to be ended.
> 
> 

## <a name="location-reporting"></a><span data-ttu-id="c8833-138">Location reporting</span><span class="sxs-lookup"><span data-stu-id="c8833-138">Location reporting</span></span>
<span data-ttu-id="c8833-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span><span class="sxs-lookup"><span data-stu-id="c8833-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span></span> <span data-ttu-id="c8833-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span><span class="sxs-lookup"><span data-stu-id="c8833-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span></span>

<span data-ttu-id="c8833-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span><span class="sxs-lookup"><span data-stu-id="c8833-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="c8833-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="c8833-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="c8833-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="c8833-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="c8833-144">Lazy area location reporting</span><span class="sxs-lookup"><span data-stu-id="c8833-144">Lazy area location reporting</span></span>
<span data-ttu-id="c8833-145">Lazy area location reporting allows to report the country, region and locality associated to devices.</span><span class="sxs-lookup"><span data-stu-id="c8833-145">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="c8833-146">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span><span class="sxs-lookup"><span data-stu-id="c8833-146">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="c8833-147">The device area is reported at most once per session.</span><span class="sxs-lookup"><span data-stu-id="c8833-147">The device area is reported at most once per session.</span></span> <span data-ttu-id="c8833-148">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span><span class="sxs-lookup"><span data-stu-id="c8833-148">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="c8833-149">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span><span class="sxs-lookup"><span data-stu-id="c8833-149">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="c8833-150">They can also be used as criterion in Reach campaigns.</span><span class="sxs-lookup"><span data-stu-id="c8833-150">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="c8833-151">The last known area reported for a device can be retrieved thanks to the [Device API].</span><span class="sxs-lookup"><span data-stu-id="c8833-151">The last known area reported for a device can be retrieved thanks to the [Device API].</span></span>

<span data-ttu-id="c8833-152">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span><span class="sxs-lookup"><span data-stu-id="c8833-152">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="c8833-153">Real time location reporting</span><span class="sxs-lookup"><span data-stu-id="c8833-153">Real time location reporting</span></span>
<span data-ttu-id="c8833-154">Real time location reporting allows to report the latitude and longitude associated to devices.</span><span class="sxs-lookup"><span data-stu-id="c8833-154">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="c8833-155">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span><span class="sxs-lookup"><span data-stu-id="c8833-155">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="c8833-156">Real time locations are *NOT* used to compute statistics.</span><span class="sxs-lookup"><span data-stu-id="c8833-156">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="c8833-157">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span><span class="sxs-lookup"><span data-stu-id="c8833-157">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="c8833-158">To enable real time location reporting, add the following line after initializing the Engagement agent:</span><span class="sxs-lookup"><span data-stu-id="c8833-158">To enable real time location reporting, add the following line after initializing the Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="c8833-159">GPS based reporting</span><span class="sxs-lookup"><span data-stu-id="c8833-159">GPS based reporting</span></span>
<span data-ttu-id="c8833-160">By default, real time location reporting only uses network based locations.</span><span class="sxs-lookup"><span data-stu-id="c8833-160">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="c8833-161">To enable the use of GPS based locations (which are far more precise), add:</span><span class="sxs-lookup"><span data-stu-id="c8833-161">To enable the use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="c8833-162">Background reporting</span><span class="sxs-lookup"><span data-stu-id="c8833-162">Background reporting</span></span>
<span data-ttu-id="c8833-163">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span><span class="sxs-lookup"><span data-stu-id="c8833-163">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="c8833-164">To enable the reporting also in background, add:</span><span class="sxs-lookup"><span data-stu-id="c8833-164">To enable the reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> When the application runs in background, only network based locations are reported, even if you enabled the GPS.
> 
> 

<span data-ttu-id="c8833-166">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span><span class="sxs-lookup"><span data-stu-id="c8833-166">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span></span> <span data-ttu-id="c8833-167">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span><span class="sxs-lookup"><span data-stu-id="c8833-167">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="c8833-168">Advanced reporting</span><span class="sxs-lookup"><span data-stu-id="c8833-168">Advanced reporting</span></span>
<span data-ttu-id="c8833-169">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span><span class="sxs-lookup"><span data-stu-id="c8833-169">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="c8833-170">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span><span class="sxs-lookup"><span data-stu-id="c8833-170">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="c8833-171">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span><span class="sxs-lookup"><span data-stu-id="c8833-171">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="c8833-172">Disable IDFA collection</span><span class="sxs-lookup"><span data-stu-id="c8833-172">Disable IDFA collection</span></span>
<span data-ttu-id="c8833-173">By default, Engagement will use the [IDFA] to uniquely identify a user.</span><span class="sxs-lookup"><span data-stu-id="c8833-173">By default, Engagement will use the [IDFA] to uniquely identify a user.</span></span> <span data-ttu-id="c8833-174">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span><span class="sxs-lookup"><span data-stu-id="c8833-174">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span></span> <span data-ttu-id="c8833-175">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span><span class="sxs-lookup"><span data-stu-id="c8833-175">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span></span> <span data-ttu-id="c8833-176">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span><span class="sxs-lookup"><span data-stu-id="c8833-176">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span></span>

<span data-ttu-id="c8833-177">Integration in the **prefix.pch** file:</span><span class="sxs-lookup"><span data-stu-id="c8833-177">Integration in the **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="c8833-178">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span><span class="sxs-lookup"><span data-stu-id="c8833-178">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span></span> <span data-ttu-id="c8833-179">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span><span class="sxs-lookup"><span data-stu-id="c8833-179">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="c8833-180">Disable log reporting</span><span class="sxs-lookup"><span data-stu-id="c8833-180">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="c8833-181">Using a method call</span><span class="sxs-lookup"><span data-stu-id="c8833-181">Using a method call</span></span>
<span data-ttu-id="c8833-182">If you want Engagement to stop sending logs, you can call:</span><span class="sxs-lookup"><span data-stu-id="c8833-182">If you want Engagement to stop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="c8833-183">This call is persistent: it uses `NSUserDefaults` to store the information.</span><span class="sxs-lookup"><span data-stu-id="c8833-183">This call is persistent: it uses `NSUserDefaults` to store the information.</span></span>

<span data-ttu-id="c8833-184">You can enable log reporting again by calling the same function with `YES`.</span><span class="sxs-lookup"><span data-stu-id="c8833-184">You can enable log reporting again by calling the same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="c8833-185">Integration in your settings bundle</span><span class="sxs-lookup"><span data-stu-id="c8833-185">Integration in your settings bundle</span></span>
<span data-ttu-id="c8833-186">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span><span class="sxs-lookup"><span data-stu-id="c8833-186">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="c8833-187">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="c8833-187">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="c8833-188">The following example of `Settings.bundle` shows how to implement it:</span><span class="sxs-lookup"><span data-stu-id="c8833-188">The following example of `Settings.bundle` shows how to implement it:</span></span>

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
