---
title: Advanced configuration for Azure Mobile Engagement Android SDK
description: Describes the advanced configuration options including the Android Manifest with Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0301f71c76872714aa1bf727a6c21dd7a63db036
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562744"
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="40011-103">Advanced configuration for Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="40011-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="40011-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span><span class="sxs-lookup"><span data-stu-id="40011-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40011-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="40011-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="40011-110">Permission Requirements</span><span class="sxs-lookup"><span data-stu-id="40011-110">Permission Requirements</span></span>
<span data-ttu-id="40011-111">Some options require specific permissions, all of which are listed here for reference, and in-line in the specific feature.</span><span class="sxs-lookup"><span data-stu-id="40011-111">Some options require specific permissions, all of which are listed here for reference, and in-line in the specific feature.</span></span> <span data-ttu-id="40011-112">Add these permissions to the AndroidManifest.xml of your project immediately before or after the `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="40011-112">Add these permissions to the AndroidManifest.xml of your project immediately before or after the `<application>` tag.</span></span>

<span data-ttu-id="40011-113">The permission code needs to look like the following, where you fill in the appropriate permission from the table that follows.</span><span class="sxs-lookup"><span data-stu-id="40011-113">The permission code needs to look like the following, where you fill in the appropriate permission from the table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="40011-114">Permission</span><span class="sxs-lookup"><span data-stu-id="40011-114">Permission</span></span> | <span data-ttu-id="40011-115">When used</span><span class="sxs-lookup"><span data-stu-id="40011-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="40011-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="40011-116">INTERNET</span></span> |<span data-ttu-id="40011-117">Required.</span><span class="sxs-lookup"><span data-stu-id="40011-117">Required.</span></span> <span data-ttu-id="40011-118">For basic reporting</span><span class="sxs-lookup"><span data-stu-id="40011-118">For basic reporting</span></span> |
| <span data-ttu-id="40011-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="40011-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="40011-120">Required.</span><span class="sxs-lookup"><span data-stu-id="40011-120">Required.</span></span> <span data-ttu-id="40011-121">For basic reporting</span><span class="sxs-lookup"><span data-stu-id="40011-121">For basic reporting</span></span> |
| <span data-ttu-id="40011-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="40011-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="40011-123">Required.</span><span class="sxs-lookup"><span data-stu-id="40011-123">Required.</span></span> <span data-ttu-id="40011-124">To show up the notifications center after device reboot</span><span class="sxs-lookup"><span data-stu-id="40011-124">To show up the notifications center after device reboot</span></span> |
| <span data-ttu-id="40011-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="40011-125">WAKE_LOCK</span></span> |<span data-ttu-id="40011-126">Recommended.</span><span class="sxs-lookup"><span data-stu-id="40011-126">Recommended.</span></span> <span data-ttu-id="40011-127">Enables collecting data when using WiFi or when screen is off</span><span class="sxs-lookup"><span data-stu-id="40011-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="40011-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="40011-128">VIBRATE</span></span> |<span data-ttu-id="40011-129">Optional.</span><span class="sxs-lookup"><span data-stu-id="40011-129">Optional.</span></span> <span data-ttu-id="40011-130">Enables vibration when notifications are received</span><span class="sxs-lookup"><span data-stu-id="40011-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="40011-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="40011-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="40011-132">Optional.</span><span class="sxs-lookup"><span data-stu-id="40011-132">Optional.</span></span> <span data-ttu-id="40011-133">Enables Android Big Picture Notification</span><span class="sxs-lookup"><span data-stu-id="40011-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="40011-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="40011-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="40011-135">Optional.</span><span class="sxs-lookup"><span data-stu-id="40011-135">Optional.</span></span> <span data-ttu-id="40011-136">Enables Android Big Picture Notification</span><span class="sxs-lookup"><span data-stu-id="40011-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="40011-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="40011-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="40011-138">Optional.</span><span class="sxs-lookup"><span data-stu-id="40011-138">Optional.</span></span> <span data-ttu-id="40011-139">Enables Real-time location reporting</span><span class="sxs-lookup"><span data-stu-id="40011-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="40011-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="40011-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="40011-141">Optional.</span><span class="sxs-lookup"><span data-stu-id="40011-141">Optional.</span></span> <span data-ttu-id="40011-142">Enables GPS-based location reporting</span><span class="sxs-lookup"><span data-stu-id="40011-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="40011-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="40011-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="40011-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need to also use ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="40011-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need to also use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="40011-145">Android Manifest configuration options</span><span class="sxs-lookup"><span data-stu-id="40011-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="40011-146">Crash report</span><span class="sxs-lookup"><span data-stu-id="40011-146">Crash report</span></span>
<span data-ttu-id="40011-147">To disable crash reports, add this code between the `<application>` and `</application>` tags:</span><span class="sxs-lookup"><span data-stu-id="40011-147">To disable crash reports, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="40011-148">Burst threshold</span><span class="sxs-lookup"><span data-stu-id="40011-148">Burst threshold</span></span>
<span data-ttu-id="40011-149">By default, the Engagement service reports logs in real time.</span><span class="sxs-lookup"><span data-stu-id="40011-149">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="40011-150">If your application report logs vary frequently, it is better to buffer the logs and to report them all at once on a regular time base (called "burst mode").</span><span class="sxs-lookup"><span data-stu-id="40011-150">If your application report logs vary frequently, it is better to buffer the logs and to report them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="40011-151">To do so, add this code between the `<application>` and `</application>` tags:</span><span class="sxs-lookup"><span data-stu-id="40011-151">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="40011-152">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span><span class="sxs-lookup"><span data-stu-id="40011-152">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="40011-153">Your burst threshold should be no longer than 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="40011-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="40011-154">Session timeout</span><span class="sxs-lookup"><span data-stu-id="40011-154">Session timeout</span></span>
 <span data-ttu-id="40011-155">You can end an activity by pressing the **Home** or **Back** key, by setting the phone idle or by jumping into another application.</span><span class="sxs-lookup"><span data-stu-id="40011-155">You can end an activity by pressing the **Home** or **Back** key, by setting the phone idle or by jumping into another application.</span></span> <span data-ttu-id="40011-156">By default, a session is ended ten seconds after the end of its last activity.</span><span class="sxs-lookup"><span data-stu-id="40011-156">By default, a session is ended ten seconds after the end of its last activity.</span></span> <span data-ttu-id="40011-157">This avoids a session split each time the user exits and returns to the application quickly, which can happen when the user picks up an image, checks a notification, etc. You may want to modify this parameter.</span><span class="sxs-lookup"><span data-stu-id="40011-157">This avoids a session split each time the user exits and returns to the application quickly, which can happen when the user picks up an image, checks a notification, etc. You may want to modify this parameter.</span></span> <span data-ttu-id="40011-158">To do so, add this code between the `<application>` and `</application>` tags:</span><span class="sxs-lookup"><span data-stu-id="40011-158">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="40011-159">Disable log reporting</span><span class="sxs-lookup"><span data-stu-id="40011-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="40011-160">Using a method call</span><span class="sxs-lookup"><span data-stu-id="40011-160">Using a method call</span></span>
<span data-ttu-id="40011-161">If you want Engagement to stop sending logs, you can call:</span><span class="sxs-lookup"><span data-stu-id="40011-161">If you want Engagement to stop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="40011-162">This call is persistent: it uses a shared preferences file.</span><span class="sxs-lookup"><span data-stu-id="40011-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="40011-163">If Engagement is active when you call this function, it may take one minute for the service to stop.</span><span class="sxs-lookup"><span data-stu-id="40011-163">If Engagement is active when you call this function, it may take one minute for the service to stop.</span></span> <span data-ttu-id="40011-164">However it won't launch the service at all the next time you launch the application.</span><span class="sxs-lookup"><span data-stu-id="40011-164">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="40011-165">You can enable log reporting again by calling the same function with `true`.</span><span class="sxs-lookup"><span data-stu-id="40011-165">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="40011-166">Integration in your own `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="40011-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="40011-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="40011-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="40011-168">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="40011-168">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="40011-169">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span><span class="sxs-lookup"><span data-stu-id="40011-169">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="40011-170">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file.</span><span class="sxs-lookup"><span data-stu-id="40011-170">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file.</span></span> <span data-ttu-id="40011-171">Use the same mode as in your `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="40011-171">Use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="40011-172">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span><span class="sxs-lookup"><span data-stu-id="40011-172">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="40011-173">Engagement always uses the `engagement:key` boolean key within the preferences file for managing this setting.</span><span class="sxs-lookup"><span data-stu-id="40011-173">Engagement always uses the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="40011-174">The following example of `AndroidManifest.xml` shows the default values:</span><span class="sxs-lookup"><span data-stu-id="40011-174">The following example of `AndroidManifest.xml` shows the default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="40011-175">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span><span class="sxs-lookup"><span data-stu-id="40011-175">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
