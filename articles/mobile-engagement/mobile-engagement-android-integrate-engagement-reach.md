---
title: Azure Mobile Engagement Android SDK Integration
description: Latest updates and procedures for Android SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 15e3b7481992de61e61c6e3c12e55aef75ac3783
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562745"
---
# <a name="how-to-integrate-engagement-reach-on-android"></a><span data-ttu-id="3b92e-103">How to Integrate Engagement Reach on Android</span><span class="sxs-lookup"><span data-stu-id="3b92e-103">How to Integrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3b92e-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span><span class="sxs-lookup"><span data-stu-id="3b92e-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="3b92e-105">Standard integration</span><span class="sxs-lookup"><span data-stu-id="3b92e-105">Standard integration</span></span>
<span data-ttu-id="3b92e-106">The Reach SDK requires the **Android Support library (v4)**.</span><span class="sxs-lookup"><span data-stu-id="3b92e-106">The Reach SDK requires the **Android Support library (v4)**.</span></span>

<span data-ttu-id="3b92e-107">The fastest way to add the library to your project in **Eclipse** is `Right click on your project -> Android Tools -> Add Support Library...`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-107">The fastest way to add the library to your project in **Eclipse** is `Right click on your project -> Android Tools -> Add Support Library...`.</span></span>

<span data-ttu-id="3b92e-108">If you don't use Eclipse, you can read the instructions [here].</span><span class="sxs-lookup"><span data-stu-id="3b92e-108">If you don't use Eclipse, you can read the instructions [here].</span></span>

<span data-ttu-id="3b92e-109">Copy Reach resource files from the SDK in your project :</span><span class="sxs-lookup"><span data-stu-id="3b92e-109">Copy Reach resource files from the SDK in your project :</span></span>

* <span data-ttu-id="3b92e-110">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span><span class="sxs-lookup"><span data-stu-id="3b92e-110">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span></span>
* <span data-ttu-id="3b92e-111">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span><span class="sxs-lookup"><span data-stu-id="3b92e-111">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span></span>

<span data-ttu-id="3b92e-112">Edit your `AndroidManifest.xml` file:</span><span class="sxs-lookup"><span data-stu-id="3b92e-112">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="3b92e-113">Add the following section (between the `<application>` and `</application>` tags):</span><span class="sxs-lookup"><span data-stu-id="3b92e-113">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* <span data-ttu-id="3b92e-114">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span><span class="sxs-lookup"><span data-stu-id="3b92e-114">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="3b92e-115">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span><span class="sxs-lookup"><span data-stu-id="3b92e-115">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="3b92e-116">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span><span class="sxs-lookup"><span data-stu-id="3b92e-116">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="3b92e-117">Android prevents system notifications without icons from being shown.</span><span class="sxs-lookup"><span data-stu-id="3b92e-117">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="3b92e-118">So if you omit this section, your end users will not be able to receive them.</span><span class="sxs-lookup"><span data-stu-id="3b92e-118">So if you omit this section, your end users will not be able to receive them.</span></span>
> 
> 

* <span data-ttu-id="3b92e-119">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span><span class="sxs-lookup"><span data-stu-id="3b92e-119">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="3b92e-120">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span><span class="sxs-lookup"><span data-stu-id="3b92e-120">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="3b92e-121">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="3b92e-121">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="3b92e-122">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span><span class="sxs-lookup"><span data-stu-id="3b92e-122">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span></span> <span data-ttu-id="3b92e-123">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="3b92e-123">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="3b92e-124">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span><span class="sxs-lookup"><span data-stu-id="3b92e-124">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span></span>
* <span data-ttu-id="3b92e-125">If you build your application using **ProGuard** and have errors related to the Android Support library or the Engagement jar, add the following lines to your `proguard.cfg` file:</span><span class="sxs-lookup"><span data-stu-id="3b92e-125">If you build your application using **ProGuard** and have errors related to the Android Support library or the Engagement jar, add the following lines to your `proguard.cfg` file:</span></span>
  
          -dontwarn android.**
          -keep class android.support.v4.** { *; }

## <a name="native-push"></a><span data-ttu-id="3b92e-126">Native Push</span><span class="sxs-lookup"><span data-stu-id="3b92e-126">Native Push</span></span>
<span data-ttu-id="3b92e-127">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span><span class="sxs-lookup"><span data-stu-id="3b92e-127">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span></span>

<span data-ttu-id="3b92e-128">We support two services on Android:</span><span class="sxs-lookup"><span data-stu-id="3b92e-128">We support two services on Android:</span></span>

* <span data-ttu-id="3b92e-129">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span><span class="sxs-lookup"><span data-stu-id="3b92e-129">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="3b92e-130">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span><span class="sxs-lookup"><span data-stu-id="3b92e-130">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="3b92e-131">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span><span class="sxs-lookup"><span data-stu-id="3b92e-131">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="3b92e-132">But when submitting to Amazon, they may reject your application if they find GCM code.</span><span class="sxs-lookup"><span data-stu-id="3b92e-132">But when submitting to Amazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="3b92e-133">You should use multiple APKs in that case.</span><span class="sxs-lookup"><span data-stu-id="3b92e-133">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="3b92e-134">**Your application is now ready to receive and display reach campaigns!**</span><span class="sxs-lookup"><span data-stu-id="3b92e-134">**Your application is now ready to receive and display reach campaigns!**</span></span>

## <a name="how-to-handle-data-push"></a><span data-ttu-id="3b92e-135">How to handle data push</span><span class="sxs-lookup"><span data-stu-id="3b92e-135">How to handle data push</span></span>
### <a name="integration"></a><span data-ttu-id="3b92e-136">Integration</span><span class="sxs-lookup"><span data-stu-id="3b92e-136">Integration</span></span>
<span data-ttu-id="3b92e-137">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span><span class="sxs-lookup"><span data-stu-id="3b92e-137">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="3b92e-138">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span><span class="sxs-lookup"><span data-stu-id="3b92e-138">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="3b92e-139">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="3b92e-139">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="3b92e-140">Category</span><span class="sxs-lookup"><span data-stu-id="3b92e-140">Category</span></span>
<span data-ttu-id="3b92e-141">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span><span class="sxs-lookup"><span data-stu-id="3b92e-141">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="3b92e-142">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span><span class="sxs-lookup"><span data-stu-id="3b92e-142">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="3b92e-143">Callbacks' return parameter</span><span class="sxs-lookup"><span data-stu-id="3b92e-143">Callbacks' return parameter</span></span>
<span data-ttu-id="3b92e-144">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="3b92e-144">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="3b92e-145">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span><span class="sxs-lookup"><span data-stu-id="3b92e-145">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span></span> <span data-ttu-id="3b92e-146">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span><span class="sxs-lookup"><span data-stu-id="3b92e-146">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span></span>
* <span data-ttu-id="3b92e-147">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span><span class="sxs-lookup"><span data-stu-id="3b92e-147">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span></span>
* <span data-ttu-id="3b92e-148">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span><span class="sxs-lookup"><span data-stu-id="3b92e-148">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span></span> <span data-ttu-id="3b92e-149">For example, return `false` when the received data is invalid.</span><span class="sxs-lookup"><span data-stu-id="3b92e-149">For example, return `false` when the received data is invalid.</span></span>
* <span data-ttu-id="3b92e-150">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span><span class="sxs-lookup"><span data-stu-id="3b92e-150">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="3b92e-151">The return type is used only for the Reach statistics:</span><span class="sxs-lookup"><span data-stu-id="3b92e-151">The return type is used only for the Reach statistics:</span></span>

* <span data-ttu-id="3b92e-152">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-152">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="3b92e-153">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-153">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span></span>

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="3b92e-154">How to customize campaigns</span><span class="sxs-lookup"><span data-stu-id="3b92e-154">How to customize campaigns</span></span>
<span data-ttu-id="3b92e-155">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span><span class="sxs-lookup"><span data-stu-id="3b92e-155">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span></span>

<span data-ttu-id="3b92e-156">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span><span class="sxs-lookup"><span data-stu-id="3b92e-156">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="3b92e-157">Some views are just used to hide or show areas so their type may be changed.</span><span class="sxs-lookup"><span data-stu-id="3b92e-157">Some views are just used to hide or show areas so their type may be changed.</span></span> <span data-ttu-id="3b92e-158">Please check the source code if you intend to change the type of a view in the provided layouts.</span><span class="sxs-lookup"><span data-stu-id="3b92e-158">Please check the source code if you intend to change the type of a view in the provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="3b92e-159">Notifications</span><span class="sxs-lookup"><span data-stu-id="3b92e-159">Notifications</span></span>
<span data-ttu-id="3b92e-160">There are two types of notifications: system and in-app notifications which use different layout files.</span><span class="sxs-lookup"><span data-stu-id="3b92e-160">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="3b92e-161">System notifications</span><span class="sxs-lookup"><span data-stu-id="3b92e-161">System notifications</span></span>
<span data-ttu-id="3b92e-162">To customize system notifications you need to use the **categories**.</span><span class="sxs-lookup"><span data-stu-id="3b92e-162">To customize system notifications you need to use the **categories**.</span></span> <span data-ttu-id="3b92e-163">You can jump to [Categories](#categories).</span><span class="sxs-lookup"><span data-stu-id="3b92e-163">You can jump to [Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="3b92e-164">In-app notifications</span><span class="sxs-lookup"><span data-stu-id="3b92e-164">In-app notifications</span></span>
<span data-ttu-id="3b92e-165">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-165">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span></span> <span data-ttu-id="3b92e-166">This is called a notification overlay.</span><span class="sxs-lookup"><span data-stu-id="3b92e-166">This is called a notification overlay.</span></span> <span data-ttu-id="3b92e-167">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span><span class="sxs-lookup"><span data-stu-id="3b92e-167">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span></span>

<span data-ttu-id="3b92e-168">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span><span class="sxs-lookup"><span data-stu-id="3b92e-168">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="3b92e-169">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-169">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="3b92e-170">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span><span class="sxs-lookup"><span data-stu-id="3b92e-170">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="3b92e-171">Include notification layout as part of an activity layout</span><span class="sxs-lookup"><span data-stu-id="3b92e-171">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="3b92e-172">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span><span class="sxs-lookup"><span data-stu-id="3b92e-172">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="3b92e-173">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span><span class="sxs-lookup"><span data-stu-id="3b92e-173">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span></span>

<span data-ttu-id="3b92e-174">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span><span class="sxs-lookup"><span data-stu-id="3b92e-174">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span></span> <span data-ttu-id="3b92e-175">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-175">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="3b92e-176">**Before Engagement integration :**</span><span class="sxs-lookup"><span data-stu-id="3b92e-176">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="3b92e-177">**After Engagement integration :**</span><span class="sxs-lookup"><span data-stu-id="3b92e-177">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="3b92e-178">In this example we added a parent container since the original layout used a list view as the top level element.</span><span class="sxs-lookup"><span data-stu-id="3b92e-178">In this example we added a parent container since the original layout used a list view as the top level element.</span></span> <span data-ttu-id="3b92e-179">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-179">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="3b92e-180">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span><span class="sxs-lookup"><span data-stu-id="3b92e-180">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="3b92e-181">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span><span class="sxs-lookup"><span data-stu-id="3b92e-181">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span></span> <span data-ttu-id="3b92e-182">This is a known issue.</span><span class="sxs-lookup"><span data-stu-id="3b92e-182">This is a known issue.</span></span> <span data-ttu-id="3b92e-183">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span><span class="sxs-lookup"><span data-stu-id="3b92e-183">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="3b92e-184">Disabling application notification per activity</span><span class="sxs-lookup"><span data-stu-id="3b92e-184">Disabling application notification per activity</span></span>
<span data-ttu-id="3b92e-185">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span><span class="sxs-lookup"><span data-stu-id="3b92e-185">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a> <span data-ttu-id="3b92e-186">Categories</span><span class="sxs-lookup"><span data-stu-id="3b92e-186">Categories</span></span>
<span data-ttu-id="3b92e-187">When you modify the provided layouts, you modify the look of all your notifications.</span><span class="sxs-lookup"><span data-stu-id="3b92e-187">When you modify the provided layouts, you modify the look of all your notifications.</span></span> <span data-ttu-id="3b92e-188">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span><span class="sxs-lookup"><span data-stu-id="3b92e-188">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="3b92e-189">A category can be specified when you create a Reach campaign.</span><span class="sxs-lookup"><span data-stu-id="3b92e-189">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="3b92e-190">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span><span class="sxs-lookup"><span data-stu-id="3b92e-190">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="3b92e-191">To register a category handler for your notifications, you need to add a call when the application is initialized.</span><span class="sxs-lookup"><span data-stu-id="3b92e-191">To register a category handler for your notifications, you need to add a call when the application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b92e-192">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span><span class="sxs-lookup"><span data-stu-id="3b92e-192">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="3b92e-193">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="3b92e-193">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="3b92e-194">The `MyNotifier` object is the implementation of the notification category handler.</span><span class="sxs-lookup"><span data-stu-id="3b92e-194">The `MyNotifier` object is the implementation of the notification category handler.</span></span> <span data-ttu-id="3b92e-195">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-195">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="3b92e-196">Note that the same notifier can handle several categories, you can register them like this:</span><span class="sxs-lookup"><span data-stu-id="3b92e-196">Note that the same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="3b92e-197">To replace the default category implementation, you can register your implementation like in the following example:</span><span class="sxs-lookup"><span data-stu-id="3b92e-197">To replace the default category implementation, you can register your implementation like in the following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="3b92e-198">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-198">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="3b92e-199">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span><span class="sxs-lookup"><span data-stu-id="3b92e-199">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="3b92e-200">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span><span class="sxs-lookup"><span data-stu-id="3b92e-200">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="3b92e-201">In-app notifications</span><span class="sxs-lookup"><span data-stu-id="3b92e-201">In-app notifications</span></span>
<span data-ttu-id="3b92e-202">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span><span class="sxs-lookup"><span data-stu-id="3b92e-202">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="3b92e-203">**Example of `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="3b92e-203">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="3b92e-204">As you can see, the overlay view identifier is different than the standard one.</span><span class="sxs-lookup"><span data-stu-id="3b92e-204">As you can see, the overlay view identifier is different than the standard one.</span></span> <span data-ttu-id="3b92e-205">It is important that each layout use a unique identifier for overlays.</span><span class="sxs-lookup"><span data-stu-id="3b92e-205">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="3b92e-206">**Example of `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="3b92e-206">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="3b92e-207">As you can see, the notification area view identifier is different than the standard one.</span><span class="sxs-lookup"><span data-stu-id="3b92e-207">As you can see, the notification area view identifier is different than the standard one.</span></span> <span data-ttu-id="3b92e-208">It is important that each layout uses a unique identifier for notification areas.</span><span class="sxs-lookup"><span data-stu-id="3b92e-208">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="3b92e-209">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="3b92e-209">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span></span> <span data-ttu-id="3b92e-210">We did not change the standard identifiers used in the notification area itself.</span><span class="sxs-lookup"><span data-stu-id="3b92e-210">We did not change the standard identifiers used in the notification area itself.</span></span>

<span data-ttu-id="3b92e-211">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span><span class="sxs-lookup"><span data-stu-id="3b92e-211">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="3b92e-212">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span><span class="sxs-lookup"><span data-stu-id="3b92e-212">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="3b92e-213">System notifications</span><span class="sxs-lookup"><span data-stu-id="3b92e-213">System notifications</span></span>
<span data-ttu-id="3b92e-214">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span><span class="sxs-lookup"><span data-stu-id="3b92e-214">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span></span>

<span data-ttu-id="3b92e-215">For example:</span><span class="sxs-lookup"><span data-stu-id="3b92e-215">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="3b92e-216">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span><span class="sxs-lookup"><span data-stu-id="3b92e-216">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span></span>

<span data-ttu-id="3b92e-217">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-217">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span></span> <span data-ttu-id="3b92e-218">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-218">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="3b92e-219">Here is a correct example of such an implementation:</span><span class="sxs-lookup"><span data-stu-id="3b92e-219">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice the call to get the right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="3b92e-220">Notification only announcements</span><span class="sxs-lookup"><span data-stu-id="3b92e-220">Notification only announcements</span></span>
<span data-ttu-id="3b92e-221">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-221">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span></span> <span data-ttu-id="3b92e-222">Using this method allows you to tune the flags easily.</span><span class="sxs-lookup"><span data-stu-id="3b92e-222">Using this method allows you to tune the flags easily.</span></span>

<span data-ttu-id="3b92e-223">For example to add the `SINGLE_TOP` flag:</span><span class="sxs-lookup"><span data-stu-id="3b92e-223">For example to add the `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="3b92e-224">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span><span class="sxs-lookup"><span data-stu-id="3b92e-224">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="3b92e-225">You should consider that when customizing the intent.</span><span class="sxs-lookup"><span data-stu-id="3b92e-225">You should consider that when customizing the intent.</span></span>

<span data-ttu-id="3b92e-226">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span><span class="sxs-lookup"><span data-stu-id="3b92e-226">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="3b92e-227">Notification life cycle</span><span class="sxs-lookup"><span data-stu-id="3b92e-227">Notification life cycle</span></span>
<span data-ttu-id="3b92e-228">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span><span class="sxs-lookup"><span data-stu-id="3b92e-228">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="3b92e-229">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span><span class="sxs-lookup"><span data-stu-id="3b92e-229">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="3b92e-230">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span><span class="sxs-lookup"><span data-stu-id="3b92e-230">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="3b92e-231">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span><span class="sxs-lookup"><span data-stu-id="3b92e-231">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span></span>

<span data-ttu-id="3b92e-232">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span><span class="sxs-lookup"><span data-stu-id="3b92e-232">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="3b92e-233">The following examples illustrate some cases where the default behavior is bypassed:</span><span class="sxs-lookup"><span data-stu-id="3b92e-233">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="3b92e-234">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span><span class="sxs-lookup"><span data-stu-id="3b92e-234">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="3b92e-235">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span><span class="sxs-lookup"><span data-stu-id="3b92e-235">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span></span>
* <span data-ttu-id="3b92e-236">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span><span class="sxs-lookup"><span data-stu-id="3b92e-236">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="3b92e-237">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span><span class="sxs-lookup"><span data-stu-id="3b92e-237">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="3b92e-238">This is reported in statistics and next campaigns can now be processed.</span><span class="sxs-lookup"><span data-stu-id="3b92e-238">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="3b92e-239">Announcements and polls</span><span class="sxs-lookup"><span data-stu-id="3b92e-239">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="3b92e-240">Layouts</span><span class="sxs-lookup"><span data-stu-id="3b92e-240">Layouts</span></span>
<span data-ttu-id="3b92e-241">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span><span class="sxs-lookup"><span data-stu-id="3b92e-241">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="3b92e-242">These files share two common layouts for the title area and the button area.</span><span class="sxs-lookup"><span data-stu-id="3b92e-242">These files share two common layouts for the title area and the button area.</span></span> <span data-ttu-id="3b92e-243">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span><span class="sxs-lookup"><span data-stu-id="3b92e-243">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span></span> <span data-ttu-id="3b92e-244">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span><span class="sxs-lookup"><span data-stu-id="3b92e-244">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span></span>

<span data-ttu-id="3b92e-245">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span><span class="sxs-lookup"><span data-stu-id="3b92e-245">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="3b92e-246">Categories</span><span class="sxs-lookup"><span data-stu-id="3b92e-246">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="3b92e-247">Alternate layouts</span><span class="sxs-lookup"><span data-stu-id="3b92e-247">Alternate layouts</span></span>
<span data-ttu-id="3b92e-248">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span><span class="sxs-lookup"><span data-stu-id="3b92e-248">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="3b92e-249">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span><span class="sxs-lookup"><span data-stu-id="3b92e-249">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="3b92e-250">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span><span class="sxs-lookup"><span data-stu-id="3b92e-250">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span></span>

<span data-ttu-id="3b92e-251">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span><span class="sxs-lookup"><span data-stu-id="3b92e-251">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span></span>

<span data-ttu-id="3b92e-252">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span><span class="sxs-lookup"><span data-stu-id="3b92e-252">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class to use R.layout.my_text_announcement
              }
            }

<span data-ttu-id="3b92e-253">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span><span class="sxs-lookup"><span data-stu-id="3b92e-253">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="3b92e-254">Web announcements and polls can be customized in a similar fashion.</span><span class="sxs-lookup"><span data-stu-id="3b92e-254">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="3b92e-255">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span><span class="sxs-lookup"><span data-stu-id="3b92e-255">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in the intent is the data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="3b92e-256">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span><span class="sxs-lookup"><span data-stu-id="3b92e-256">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="3b92e-257">Implementation from scratch</span><span class="sxs-lookup"><span data-stu-id="3b92e-257">Implementation from scratch</span></span>
<span data-ttu-id="3b92e-258">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span><span class="sxs-lookup"><span data-stu-id="3b92e-258">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span></span> <span data-ttu-id="3b92e-259">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span><span class="sxs-lookup"><span data-stu-id="3b92e-259">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span></span>

<span data-ttu-id="3b92e-260">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span><span class="sxs-lookup"><span data-stu-id="3b92e-260">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

<span data-ttu-id="3b92e-261">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span><span class="sxs-lookup"><span data-stu-id="3b92e-261">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span></span>

<span data-ttu-id="3b92e-262">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span><span class="sxs-lookup"><span data-stu-id="3b92e-262">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="3b92e-263">For statistics, you should report the content is displayed in the `onResume` event:</span><span class="sxs-lookup"><span data-stu-id="3b92e-263">For statistics, you should report the content is displayed in the `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark the content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="3b92e-264">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span><span class="sxs-lookup"><span data-stu-id="3b92e-264">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span></span>

<span data-ttu-id="3b92e-265">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span><span class="sxs-lookup"><span data-stu-id="3b92e-265">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span></span>

<span data-ttu-id="3b92e-266">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span><span class="sxs-lookup"><span data-stu-id="3b92e-266">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span></span>

<span data-ttu-id="3b92e-267">Here is the interesting part of the implementation:</span><span class="sxs-lookup"><span data-stu-id="3b92e-267">Here is the interesting part of the implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have to check anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="3b92e-268">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span><span class="sxs-lookup"><span data-stu-id="3b92e-268">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
