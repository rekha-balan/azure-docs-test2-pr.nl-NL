---
title: Location Reporting for Azure Mobile Engagement Android SDK
description: Describes how to configure location reporting for Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 777d5719cce505b55dfb61c91dcac7e713b077a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552252"
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="3b512-103">Location Reporting for Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="3b512-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="3b512-105">This topic describes how to do location reporting for your Android application.</span><span class="sxs-lookup"><span data-stu-id="3b512-105">This topic describes how to do location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b512-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b512-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="3b512-107">Location reporting</span><span class="sxs-lookup"><span data-stu-id="3b512-107">Location reporting</span></span>
<span data-ttu-id="3b512-108">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span><span class="sxs-lookup"><span data-stu-id="3b512-108">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="3b512-109">Lazy area location reporting</span><span class="sxs-lookup"><span data-stu-id="3b512-109">Lazy area location reporting</span></span>
<span data-ttu-id="3b512-110">Lazy area location reporting enables reporting the country, region, and locality associated with devices.</span><span class="sxs-lookup"><span data-stu-id="3b512-110">Lazy area location reporting enables reporting the country, region, and locality associated with devices.</span></span> <span data-ttu-id="3b512-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span><span class="sxs-lookup"><span data-stu-id="3b512-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="3b512-112">The device area is reported at most once per session.</span><span class="sxs-lookup"><span data-stu-id="3b512-112">The device area is reported at most once per session.</span></span> <span data-ttu-id="3b512-113">The GPS is never used, and thus this type of location report has low impact on the battery.</span><span class="sxs-lookup"><span data-stu-id="3b512-113">The GPS is never used, and thus this type of location report has low impact on the battery.</span></span>

<span data-ttu-id="3b512-114">Reported areas are used to compute geographic statistics about users, sessions, events, and errors.</span><span class="sxs-lookup"><span data-stu-id="3b512-114">Reported areas are used to compute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="3b512-115">They can also be used as criterion in Reach campaigns.</span><span class="sxs-lookup"><span data-stu-id="3b512-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="3b512-116">You enable lazy area location reporting by using the configuration previously mentioned in this procedure:</span><span class="sxs-lookup"><span data-stu-id="3b512-116">You enable lazy area location reporting by using the configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="3b512-117">You also need to specify a location permission.</span><span class="sxs-lookup"><span data-stu-id="3b512-117">You also need to specify a location permission.</span></span> <span data-ttu-id="3b512-118">This code uses ``COARSE`` permission:</span><span class="sxs-lookup"><span data-stu-id="3b512-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="3b512-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span><span class="sxs-lookup"><span data-stu-id="3b512-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="3b512-120">Real-time location reporting</span><span class="sxs-lookup"><span data-stu-id="3b512-120">Real-time location reporting</span></span>
<span data-ttu-id="3b512-121">Real-time location reporting enables reporting the latitude and longitude associated with devices.</span><span class="sxs-lookup"><span data-stu-id="3b512-121">Real-time location reporting enables reporting the latitude and longitude associated with devices.</span></span> <span data-ttu-id="3b512-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span><span class="sxs-lookup"><span data-stu-id="3b512-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="3b512-123">The reporting is only active when the application runs in foreground (for example, during a session).</span><span class="sxs-lookup"><span data-stu-id="3b512-123">The reporting is only active when the application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="3b512-124">Real-time locations are *NOT* used to compute statistics.</span><span class="sxs-lookup"><span data-stu-id="3b512-124">Real-time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="3b512-125">Their only purpose is to allow the use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span><span class="sxs-lookup"><span data-stu-id="3b512-125">Their only purpose is to allow the use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="3b512-126">To enable real-time location reporting, add a line of code to where you set the Engagement connection string in the launcher activity.</span><span class="sxs-lookup"><span data-stu-id="3b512-126">To enable real-time location reporting, add a line of code to where you set the Engagement connection string in the launcher activity.</span></span> <span data-ttu-id="3b512-127">The result looks like the following:</span><span class="sxs-lookup"><span data-stu-id="3b512-127">The result looks like the following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need to specify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="3b512-128">GPS based reporting</span><span class="sxs-lookup"><span data-stu-id="3b512-128">GPS based reporting</span></span>
<span data-ttu-id="3b512-129">By default, real-time location reporting only uses network-based locations.</span><span class="sxs-lookup"><span data-stu-id="3b512-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="3b512-130">To enable the use of GPS-based locations, which are far more precise, use the configuration object:</span><span class="sxs-lookup"><span data-stu-id="3b512-130">To enable the use of GPS-based locations, which are far more precise, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="3b512-131">You also need to add the following permission if missing:</span><span class="sxs-lookup"><span data-stu-id="3b512-131">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="3b512-132">Background reporting</span><span class="sxs-lookup"><span data-stu-id="3b512-132">Background reporting</span></span>
<span data-ttu-id="3b512-133">By default, real-time location reporting is only active when the application runs in foreground (for example, during a session).</span><span class="sxs-lookup"><span data-stu-id="3b512-133">By default, real-time location reporting is only active when the application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="3b512-134">To enable the reporting also in background, use this configuration object:</span><span class="sxs-lookup"><span data-stu-id="3b512-134">To enable the reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> When the application runs in background, only network-based locations are reported, even if you enabled the GPS.
> 
> 

<span data-ttu-id="3b512-136">If the user reboots their device, the background location report is stopped.</span><span class="sxs-lookup"><span data-stu-id="3b512-136">If the user reboots their device, the background location report is stopped.</span></span> <span data-ttu-id="3b512-137">To make it automatically restart at boot time, add this code.</span><span class="sxs-lookup"><span data-stu-id="3b512-137">To make it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="3b512-138">You also need to add the following permission if missing:</span><span class="sxs-lookup"><span data-stu-id="3b512-138">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="3b512-139">Android M permissions</span><span class="sxs-lookup"><span data-stu-id="3b512-139">Android M permissions</span></span>
<span data-ttu-id="3b512-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span><span class="sxs-lookup"><span data-stu-id="3b512-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="3b512-141">If you target Android API level 23, the runtime permissions are turned off by default for new app installations.</span><span class="sxs-lookup"><span data-stu-id="3b512-141">If you target Android API level 23, the runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="3b512-142">Otherwise they are turned on by default.</span><span class="sxs-lookup"><span data-stu-id="3b512-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="3b512-143">You can enable/disable those permissions from the device settings menu.</span><span class="sxs-lookup"><span data-stu-id="3b512-143">You can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="3b512-144">Turning off permissions from the system menu kills the background processes of the application, which is a system behavior, and has no impact on ability to receive push in background.</span><span class="sxs-lookup"><span data-stu-id="3b512-144">Turning off permissions from the system menu kills the background processes of the application, which is a system behavior, and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="3b512-145">In the context of Mobile Engagement location reporting, the permissions that require approval at runtime are:</span><span class="sxs-lookup"><span data-stu-id="3b512-145">In the context of Mobile Engagement location reporting, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="3b512-146">Request permissions from the user using a standard system dialog.</span><span class="sxs-lookup"><span data-stu-id="3b512-146">Request permissions from the user using a standard system dialog.</span></span> <span data-ttu-id="3b512-147">If the user approves, tell ``EngagementAgent`` to take that change into account in real-time.</span><span class="sxs-lookup"><span data-stu-id="3b512-147">If the user approves, tell ``EngagementAgent`` to take that change into account in real-time.</span></span> <span data-ttu-id="3b512-148">Otherwise the change is processed the next time the user launches the application.</span><span class="sxs-lookup"><span data-stu-id="3b512-148">Otherwise the change is processed the next time the user launches the application.</span></span>

<span data-ttu-id="3b512-149">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="3b512-149">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
