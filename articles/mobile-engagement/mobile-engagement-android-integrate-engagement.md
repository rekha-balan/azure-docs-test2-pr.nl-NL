---
title: Azure Mobile Engagement Android SDK Integration
description: Latest updates and procedures for Android SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564273"
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="24c5e-103">How to Integrate Engagement on Android</span><span class="sxs-lookup"><span data-stu-id="24c5e-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="24c5e-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span><span class="sxs-lookup"><span data-stu-id="24c5e-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).
> 
> 

<span data-ttu-id="24c5e-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span><span class="sxs-lookup"><span data-stu-id="24c5e-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="24c5e-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span><span class="sxs-lookup"><span data-stu-id="24c5e-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="24c5e-112">Embed the Engagement SDK and service into your Android project</span><span class="sxs-lookup"><span data-stu-id="24c5e-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="24c5e-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span><span class="sxs-lookup"><span data-stu-id="24c5e-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> If you build your application package with ProGuard, you need to keep some classes. You can use the following configuration snippet:
> 
> -keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
> 
> <methods>; }
> 
> 

<span data-ttu-id="24c5e-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span><span class="sxs-lookup"><span data-stu-id="24c5e-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="24c5e-119">The connection string for your application is displayed on Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="24c5e-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="24c5e-120">If missing, add the following Android permissions (before the `<application>` tag):</span><span class="sxs-lookup"><span data-stu-id="24c5e-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="24c5e-121">Add the following section (between the `<application>` and `</application>` tags):</span><span class="sxs-lookup"><span data-stu-id="24c5e-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="24c5e-122">Change `<Your application name>` by the name of your application.</span><span class="sxs-lookup"><span data-stu-id="24c5e-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone. It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).
> 
> 

<span data-ttu-id="24c5e-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span><span class="sxs-lookup"><span data-stu-id="24c5e-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service. It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).
> 
> 

<span data-ttu-id="24c5e-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span><span class="sxs-lookup"><span data-stu-id="24c5e-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="24c5e-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="24c5e-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="24c5e-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span><span class="sxs-lookup"><span data-stu-id="24c5e-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="24c5e-131">Basic reporting</span><span class="sxs-lookup"><span data-stu-id="24c5e-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="24c5e-132">Recommended method: overload your `Activity` classes</span><span class="sxs-lookup"><span data-stu-id="24c5e-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="24c5e-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="24c5e-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="24c5e-134">**Without Engagement :**</span><span class="sxs-lookup"><span data-stu-id="24c5e-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="24c5e-135">**With Engagement :**</span><span class="sxs-lookup"><span data-stu-id="24c5e-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.
> 
> 

<span data-ttu-id="24c5e-137">You can find these classes in the `src` folder, and can copy them into your project.</span><span class="sxs-lookup"><span data-stu-id="24c5e-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="24c5e-138">The classes are also in the **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="24c5e-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="24c5e-139">Alternate method: call `startActivity()` and `endActivity()` manually</span><span class="sxs-lookup"><span data-stu-id="24c5e-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="24c5e-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span><span class="sxs-lookup"><span data-stu-id="24c5e-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed). Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities. This is the only way to be sure that sessions will not be leaked. If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).
> 
> 

<span data-ttu-id="24c5e-145">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="24c5e-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="24c5e-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span><span class="sxs-lookup"><span data-stu-id="24c5e-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="24c5e-147">Test</span><span class="sxs-lookup"><span data-stu-id="24c5e-147">Test</span></span>
<span data-ttu-id="24c5e-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span><span class="sxs-lookup"><span data-stu-id="24c5e-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="24c5e-149">The next sections are optional.</span><span class="sxs-lookup"><span data-stu-id="24c5e-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="24c5e-150">Location reporting</span><span class="sxs-lookup"><span data-stu-id="24c5e-150">Location reporting</span></span>
<span data-ttu-id="24c5e-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span><span class="sxs-lookup"><span data-stu-id="24c5e-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="24c5e-152">Lazy area location reporting</span><span class="sxs-lookup"><span data-stu-id="24c5e-152">Lazy area location reporting</span></span>
<span data-ttu-id="24c5e-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span><span class="sxs-lookup"><span data-stu-id="24c5e-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="24c5e-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span><span class="sxs-lookup"><span data-stu-id="24c5e-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="24c5e-155">The device area is reported at most once per session.</span><span class="sxs-lookup"><span data-stu-id="24c5e-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="24c5e-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span><span class="sxs-lookup"><span data-stu-id="24c5e-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="24c5e-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span><span class="sxs-lookup"><span data-stu-id="24c5e-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="24c5e-158">They can also be used as criterion in Reach campaigns.</span><span class="sxs-lookup"><span data-stu-id="24c5e-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="24c5e-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span><span class="sxs-lookup"><span data-stu-id="24c5e-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="24c5e-160">You also need to add the following permission if missing:</span><span class="sxs-lookup"><span data-stu-id="24c5e-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="24c5e-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span><span class="sxs-lookup"><span data-stu-id="24c5e-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="24c5e-162">Real time location reporting</span><span class="sxs-lookup"><span data-stu-id="24c5e-162">Real time location reporting</span></span>
<span data-ttu-id="24c5e-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span><span class="sxs-lookup"><span data-stu-id="24c5e-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="24c5e-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span><span class="sxs-lookup"><span data-stu-id="24c5e-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="24c5e-165">Real time locations are *NOT* used to compute statistics.</span><span class="sxs-lookup"><span data-stu-id="24c5e-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="24c5e-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span><span class="sxs-lookup"><span data-stu-id="24c5e-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="24c5e-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span><span class="sxs-lookup"><span data-stu-id="24c5e-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="24c5e-168">You also need to add the following permission if missing:</span><span class="sxs-lookup"><span data-stu-id="24c5e-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="24c5e-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span><span class="sxs-lookup"><span data-stu-id="24c5e-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="24c5e-170">GPS based reporting</span><span class="sxs-lookup"><span data-stu-id="24c5e-170">GPS based reporting</span></span>
<span data-ttu-id="24c5e-171">By default, real time location reporting only uses network based locations.</span><span class="sxs-lookup"><span data-stu-id="24c5e-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="24c5e-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span><span class="sxs-lookup"><span data-stu-id="24c5e-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="24c5e-173">You also need to add the following permission if missing:</span><span class="sxs-lookup"><span data-stu-id="24c5e-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="24c5e-174">Background reporting</span><span class="sxs-lookup"><span data-stu-id="24c5e-174">Background reporting</span></span>
<span data-ttu-id="24c5e-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span><span class="sxs-lookup"><span data-stu-id="24c5e-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="24c5e-176">To enable the reporting also in background, use the configuration object:</span><span class="sxs-lookup"><span data-stu-id="24c5e-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> When the application runs in background, only network based locations are reported, even if you enabled the GPS.
> 
> 

<span data-ttu-id="24c5e-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span><span class="sxs-lookup"><span data-stu-id="24c5e-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="24c5e-179">You also need to add the following permission if missing:</span><span class="sxs-lookup"><span data-stu-id="24c5e-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="24c5e-180">Android M permissions</span><span class="sxs-lookup"><span data-stu-id="24c5e-180">Android M permissions</span></span>
<span data-ttu-id="24c5e-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span><span class="sxs-lookup"><span data-stu-id="24c5e-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="24c5e-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span><span class="sxs-lookup"><span data-stu-id="24c5e-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="24c5e-183">Otherwise it will be turned on by default.</span><span class="sxs-lookup"><span data-stu-id="24c5e-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="24c5e-184">The user can enable/disable those permissions from the device settings menu.</span><span class="sxs-lookup"><span data-stu-id="24c5e-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="24c5e-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span><span class="sxs-lookup"><span data-stu-id="24c5e-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="24c5e-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span><span class="sxs-lookup"><span data-stu-id="24c5e-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="24c5e-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span><span class="sxs-lookup"><span data-stu-id="24c5e-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="24c5e-188">The external storage is used only for Reach big picture feature.</span><span class="sxs-lookup"><span data-stu-id="24c5e-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="24c5e-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span><span class="sxs-lookup"><span data-stu-id="24c5e-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="24c5e-190">For the location features, you should request permissions to user using a standard system dialog.</span><span class="sxs-lookup"><span data-stu-id="24c5e-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="24c5e-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span><span class="sxs-lookup"><span data-stu-id="24c5e-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="24c5e-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="24c5e-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="24c5e-193">Advanced reporting</span><span class="sxs-lookup"><span data-stu-id="24c5e-193">Advanced reporting</span></span>
<span data-ttu-id="24c5e-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span><span class="sxs-lookup"><span data-stu-id="24c5e-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="24c5e-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span><span class="sxs-lookup"><span data-stu-id="24c5e-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="24c5e-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span><span class="sxs-lookup"><span data-stu-id="24c5e-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="24c5e-197">Advanced configuration (in AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="24c5e-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="24c5e-198">Wake locks</span><span class="sxs-lookup"><span data-stu-id="24c5e-198">Wake locks</span></span>
<span data-ttu-id="24c5e-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span><span class="sxs-lookup"><span data-stu-id="24c5e-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="24c5e-200">Crash report</span><span class="sxs-lookup"><span data-stu-id="24c5e-200">Crash report</span></span>
<span data-ttu-id="24c5e-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span><span class="sxs-lookup"><span data-stu-id="24c5e-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="24c5e-202">Burst threshold</span><span class="sxs-lookup"><span data-stu-id="24c5e-202">Burst threshold</span></span>
<span data-ttu-id="24c5e-203">By default, the Engagement service reports logs in real time.</span><span class="sxs-lookup"><span data-stu-id="24c5e-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="24c5e-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span><span class="sxs-lookup"><span data-stu-id="24c5e-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="24c5e-205">To do so, add this (between the `<application>` and `</application>` tags):</span><span class="sxs-lookup"><span data-stu-id="24c5e-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="24c5e-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span><span class="sxs-lookup"><span data-stu-id="24c5e-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="24c5e-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="24c5e-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="24c5e-208">Session timeout</span><span class="sxs-lookup"><span data-stu-id="24c5e-208">Session timeout</span></span>
<span data-ttu-id="24c5e-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span><span class="sxs-lookup"><span data-stu-id="24c5e-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="24c5e-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span><span class="sxs-lookup"><span data-stu-id="24c5e-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="24c5e-211">You may want to modify this parameter.</span><span class="sxs-lookup"><span data-stu-id="24c5e-211">You may want to modify this parameter.</span></span> <span data-ttu-id="24c5e-212">To do so, add this (between the `<application>` and `</application>` tags):</span><span class="sxs-lookup"><span data-stu-id="24c5e-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="24c5e-213">Disable log reporting</span><span class="sxs-lookup"><span data-stu-id="24c5e-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="24c5e-214">Using a method call</span><span class="sxs-lookup"><span data-stu-id="24c5e-214">Using a method call</span></span>
<span data-ttu-id="24c5e-215">If you want Engagement to stop sending logs, you can call:</span><span class="sxs-lookup"><span data-stu-id="24c5e-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="24c5e-216">This call is persistent: it uses a shared preferences file.</span><span class="sxs-lookup"><span data-stu-id="24c5e-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="24c5e-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span><span class="sxs-lookup"><span data-stu-id="24c5e-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="24c5e-218">However it won't launch the service at all the next time you launch the application.</span><span class="sxs-lookup"><span data-stu-id="24c5e-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="24c5e-219">You can enable log reporting again by calling the same function with `true`.</span><span class="sxs-lookup"><span data-stu-id="24c5e-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="24c5e-220">Integration in your own `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="24c5e-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="24c5e-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="24c5e-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="24c5e-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="24c5e-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="24c5e-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span><span class="sxs-lookup"><span data-stu-id="24c5e-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="24c5e-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="24c5e-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="24c5e-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span><span class="sxs-lookup"><span data-stu-id="24c5e-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="24c5e-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span><span class="sxs-lookup"><span data-stu-id="24c5e-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="24c5e-227">The following example of `AndroidManifest.xml` shows the default values:</span><span class="sxs-lookup"><span data-stu-id="24c5e-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="24c5e-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span><span class="sxs-lookup"><span data-stu-id="24c5e-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094