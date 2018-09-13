---
title: Advanced reporting options for Azure Mobile Engagement Android SDK
description: Describes how to do advanced reporting to capture analytics for Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549318"
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="04a17-103">Advanced Reporting with Engagement on Android</span><span class="sxs-lookup"><span data-stu-id="04a17-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="04a17-108">This topic describes additional reporting scenarios in your Android application.</span><span class="sxs-lookup"><span data-stu-id="04a17-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="04a17-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="04a17-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04a17-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04a17-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="04a17-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span><span class="sxs-lookup"><span data-stu-id="04a17-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="04a17-112">Modifying your `Activity` classes</span><span class="sxs-lookup"><span data-stu-id="04a17-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="04a17-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span><span class="sxs-lookup"><span data-stu-id="04a17-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="04a17-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="04a17-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.
> 
> 

<span data-ttu-id="04a17-116">You can find these classes in the `src` folder, and can copy them into your project.</span><span class="sxs-lookup"><span data-stu-id="04a17-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="04a17-117">The classes are also in the **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="04a17-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="04a17-118">Alternate method: call `startActivity()` and `endActivity()` manually</span><span class="sxs-lookup"><span data-stu-id="04a17-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="04a17-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span><span class="sxs-lookup"><span data-stu-id="04a17-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed). Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities. This is the only way to be sure that sessions are not leaked. If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).
> 
> 

<span data-ttu-id="04a17-124">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="04a17-124">Here is an example:</span></span>

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

<span data-ttu-id="04a17-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span><span class="sxs-lookup"><span data-stu-id="04a17-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="04a17-126">Using Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="04a17-126">Using Application.onCreate()</span></span>
<span data-ttu-id="04a17-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span><span class="sxs-lookup"><span data-stu-id="04a17-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="04a17-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span><span class="sxs-lookup"><span data-stu-id="04a17-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="04a17-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span><span class="sxs-lookup"><span data-stu-id="04a17-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="04a17-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="04a17-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="04a17-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span><span class="sxs-lookup"><span data-stu-id="04a17-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="04a17-132">Tags in the AndroidManifest.xml file</span><span class="sxs-lookup"><span data-stu-id="04a17-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="04a17-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span><span class="sxs-lookup"><span data-stu-id="04a17-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="04a17-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="04a17-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="04a17-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span><span class="sxs-lookup"><span data-stu-id="04a17-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="04a17-136">Building with ProGuard</span><span class="sxs-lookup"><span data-stu-id="04a17-136">Building with ProGuard</span></span>
<span data-ttu-id="04a17-137">If you build your application package with ProGuard, you need to keep some classes.</span><span class="sxs-lookup"><span data-stu-id="04a17-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="04a17-138">You can use the following configuration snippet:</span><span class="sxs-lookup"><span data-stu-id="04a17-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
