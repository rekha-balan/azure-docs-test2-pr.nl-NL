---
title: How to Use the Engagement API on Android
description: Latest Android SDK - How to Use the Engagement API on Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: d353cd2fe47c54a0282cc5bb1b22b4a56e0cd82c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556247"
---
# <a name="how-to-use-the-engagement-api-on-android"></a><span data-ttu-id="daef3-103">How to Use the Engagement API on Android</span><span class="sxs-lookup"><span data-stu-id="daef3-103">How to Use the Engagement API on Android</span></span>
<span data-ttu-id="daef3-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="daef3-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="daef3-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span><span class="sxs-lookup"><span data-stu-id="daef3-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="daef3-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span><span class="sxs-lookup"><span data-stu-id="daef3-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="daef3-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span><span class="sxs-lookup"><span data-stu-id="daef3-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="daef3-108">The Engagement API is provided by the `EngagementAgent` class.</span><span class="sxs-lookup"><span data-stu-id="daef3-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="daef3-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span><span class="sxs-lookup"><span data-stu-id="daef3-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="daef3-110">Engagement concepts</span><span class="sxs-lookup"><span data-stu-id="daef3-110">Engagement concepts</span></span>
<span data-ttu-id="daef3-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span><span class="sxs-lookup"><span data-stu-id="daef3-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="daef3-112">`Session` and `Activity`</span><span class="sxs-lookup"><span data-stu-id="daef3-112">`Session` and `Activity`</span></span>
<span data-ttu-id="daef3-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span><span class="sxs-lookup"><span data-stu-id="daef3-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="daef3-114">These few seconds are called the "session timeout".</span><span class="sxs-lookup"><span data-stu-id="daef3-114">These few seconds are called the "session timeout".</span></span>

<span data-ttu-id="daef3-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span><span class="sxs-lookup"><span data-stu-id="daef3-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span></span>

<span data-ttu-id="daef3-116">But *activities* can also be controlled manually by using the Engagement API.</span><span class="sxs-lookup"><span data-stu-id="daef3-116">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="daef3-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span><span class="sxs-lookup"><span data-stu-id="daef3-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="daef3-118">Reporting Activities</span><span class="sxs-lookup"><span data-stu-id="daef3-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="daef3-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span><span class="sxs-lookup"><span data-stu-id="daef3-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="daef3-120">User starts a new Activity</span><span class="sxs-lookup"><span data-stu-id="daef3-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="daef3-121">You need to call `startActivity()` each time the user activity changes.</span><span class="sxs-lookup"><span data-stu-id="daef3-121">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="daef3-122">The first call to this function starts a new user session.</span><span class="sxs-lookup"><span data-stu-id="daef3-122">The first call to this function starts a new user session.</span></span>

<span data-ttu-id="daef3-123">The best place to call this function is on each activity `onResume` callback.</span><span class="sxs-lookup"><span data-stu-id="daef3-123">The best place to call this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="daef3-124">User ends his current Activity</span><span class="sxs-lookup"><span data-stu-id="daef3-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="daef3-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span><span class="sxs-lookup"><span data-stu-id="daef3-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="daef3-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span><span class="sxs-lookup"><span data-stu-id="daef3-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span></span>

<span data-ttu-id="daef3-127">The best place to call this function is on each activity `onPause` callback.</span><span class="sxs-lookup"><span data-stu-id="daef3-127">The best place to call this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="daef3-128">Reporting Events</span><span class="sxs-lookup"><span data-stu-id="daef3-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="daef3-129">Session events</span><span class="sxs-lookup"><span data-stu-id="daef3-129">Session events</span></span>
<span data-ttu-id="daef3-130">Session events are usually used to report the actions performed by a user during his session.</span><span class="sxs-lookup"><span data-stu-id="daef3-130">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="daef3-131">**Example without extra data:**</span><span class="sxs-lookup"><span data-stu-id="daef3-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="daef3-132">**Example with extra data:**</span><span class="sxs-lookup"><span data-stu-id="daef3-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="daef3-133">Standalone Events</span><span class="sxs-lookup"><span data-stu-id="daef3-133">Standalone Events</span></span>
<span data-ttu-id="daef3-134">Contrary to session events, standalone events can occur outside of the context of a session.</span><span class="sxs-lookup"><span data-stu-id="daef3-134">Contrary to session events, standalone events can occur outside of the context of a session.</span></span>

<span data-ttu-id="daef3-135">**Example:**</span><span class="sxs-lookup"><span data-stu-id="daef3-135">**Example:**</span></span>

<span data-ttu-id="daef3-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span><span class="sxs-lookup"><span data-stu-id="daef3-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="daef3-137">Reporting Errors</span><span class="sxs-lookup"><span data-stu-id="daef3-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="daef3-138">Session errors</span><span class="sxs-lookup"><span data-stu-id="daef3-138">Session errors</span></span>
<span data-ttu-id="daef3-139">Session errors are usually used to report the errors impacting the user during his session.</span><span class="sxs-lookup"><span data-stu-id="daef3-139">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="daef3-140">**Example:**</span><span class="sxs-lookup"><span data-stu-id="daef3-140">**Example:**</span></span>

            /** The user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* The user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="daef3-141">Standalone errors</span><span class="sxs-lookup"><span data-stu-id="daef3-141">Standalone errors</span></span>
<span data-ttu-id="daef3-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span><span class="sxs-lookup"><span data-stu-id="daef3-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

<span data-ttu-id="daef3-143">**Example:**</span><span class="sxs-lookup"><span data-stu-id="daef3-143">**Example:**</span></span>

<span data-ttu-id="daef3-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span><span class="sxs-lookup"><span data-stu-id="daef3-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="daef3-145">Reporting Jobs</span><span class="sxs-lookup"><span data-stu-id="daef3-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="daef3-146">Example</span><span class="sxs-lookup"><span data-stu-id="daef3-146">Example</span></span>
<span data-ttu-id="daef3-147">Suppose you want to report the duration of your login process:</span><span class="sxs-lookup"><span data-stu-id="daef3-147">Suppose you want to report the duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="daef3-148">Report Errors during a Job</span><span class="sxs-lookup"><span data-stu-id="daef3-148">Report Errors during a Job</span></span>
<span data-ttu-id="daef3-149">Errors can be related to a running job instead of being related to the current user session.</span><span class="sxs-lookup"><span data-stu-id="daef3-149">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="daef3-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="daef3-150">**Example:**</span></span>

<span data-ttu-id="daef3-151">Suppose you want to report an error during you login process:</span><span class="sxs-lookup"><span data-stu-id="daef3-151">Suppose you want to report an error during you login process:</span></span>

<span data-ttu-id="daef3-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="daef3-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try to sign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report the error to Engagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="daef3-153">Reporting Events during a job</span><span class="sxs-lookup"><span data-stu-id="daef3-153">Reporting Events during a job</span></span>
<span data-ttu-id="daef3-154">Events can be related to a running job instead of being related to the current user session.</span><span class="sxs-lookup"><span data-stu-id="daef3-154">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="daef3-155">**Example:**</span><span class="sxs-lookup"><span data-stu-id="daef3-155">**Example:**</span></span>

<span data-ttu-id="daef3-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span><span class="sxs-lookup"><span data-stu-id="daef3-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="daef3-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span><span class="sxs-lookup"><span data-stu-id="daef3-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="daef3-158">The user can receive messages from his friends, this is a job event.</span><span class="sxs-lookup"><span data-stu-id="daef3-158">The user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="daef3-159">Extra parameters</span><span class="sxs-lookup"><span data-stu-id="daef3-159">Extra parameters</span></span>
<span data-ttu-id="daef3-160">Arbitrary data can be attached to events, errors, activities and jobs.</span><span class="sxs-lookup"><span data-stu-id="daef3-160">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="daef3-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span><span class="sxs-lookup"><span data-stu-id="daef3-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="daef3-162">Note that a Bundle can contain arrays or another Bundle instances.</span><span class="sxs-lookup"><span data-stu-id="daef3-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="daef3-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span><span class="sxs-lookup"><span data-stu-id="daef3-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span></span> <span data-ttu-id="daef3-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="daef3-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="daef3-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span><span class="sxs-lookup"><span data-stu-id="daef3-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="daef3-166">You should convert them into standard arrays before using it in extra parameters.</span><span class="sxs-lookup"><span data-stu-id="daef3-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="daef3-167">Example</span><span class="sxs-lookup"><span data-stu-id="daef3-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="daef3-168">Limits</span><span class="sxs-lookup"><span data-stu-id="daef3-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="daef3-169">Keys</span><span class="sxs-lookup"><span data-stu-id="daef3-169">Keys</span></span>
<span data-ttu-id="daef3-170">Each key in the `Bundle` must match the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="daef3-170">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="daef3-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span><span class="sxs-lookup"><span data-stu-id="daef3-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="daef3-172">Size</span><span class="sxs-lookup"><span data-stu-id="daef3-172">Size</span></span>
<span data-ttu-id="daef3-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span><span class="sxs-lookup"><span data-stu-id="daef3-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="daef3-174">In the previous example, the JSON sent to the server is 58 characters long:</span><span class="sxs-lookup"><span data-stu-id="daef3-174">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="daef3-175">Reporting Application Information</span><span class="sxs-lookup"><span data-stu-id="daef3-175">Reporting Application Information</span></span>
<span data-ttu-id="daef3-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span><span class="sxs-lookup"><span data-stu-id="daef3-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="daef3-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span><span class="sxs-lookup"><span data-stu-id="daef3-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="daef3-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span><span class="sxs-lookup"><span data-stu-id="daef3-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="daef3-179">Example</span><span class="sxs-lookup"><span data-stu-id="daef3-179">Example</span></span>
<span data-ttu-id="daef3-180">Here is a code sample to send user gender and birthdate:</span><span class="sxs-lookup"><span data-stu-id="daef3-180">Here is a code sample to send user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="daef3-181">Limits</span><span class="sxs-lookup"><span data-stu-id="daef3-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="daef3-182">Keys</span><span class="sxs-lookup"><span data-stu-id="daef3-182">Keys</span></span>
<span data-ttu-id="daef3-183">Each key in the `Bundle` must match the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="daef3-183">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="daef3-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span><span class="sxs-lookup"><span data-stu-id="daef3-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="daef3-185">Size</span><span class="sxs-lookup"><span data-stu-id="daef3-185">Size</span></span>
<span data-ttu-id="daef3-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span><span class="sxs-lookup"><span data-stu-id="daef3-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="daef3-187">In the previous example, the JSON sent to the server is 44 characters long:</span><span class="sxs-lookup"><span data-stu-id="daef3-187">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
