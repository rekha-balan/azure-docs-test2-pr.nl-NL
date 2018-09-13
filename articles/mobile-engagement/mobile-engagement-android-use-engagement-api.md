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
# <a name="how-to-use-the-engagement-api-on-android"></a>How to Use the Engagement API on Android
This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md). It provides in depth details about how to use the Engagement API to report your application statistics.

Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.

If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.

The Engagement API is provided by the `EngagementAgent` class. An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).

## <a name="engagement-concepts"></a>Engagement concepts
The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.

### <a name="session-and-activity"></a>`Session` and `Activity`
If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*. These few seconds are called the "session timeout".

An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.

But *activities* can also be controlled manually by using the Engagement API. This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).

## <a name="reporting-activities"></a>Reporting Activities
> [!IMPORTANT]
> You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.
> 
> 

### <a name="user-starts-a-new-activity"></a>User starts a new Activity
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

You need to call `startActivity()` each time the user activity changes. The first call to this function starts a new user session.

The best place to call this function is on each activity `onResume` callback.

### <a name="user-ends-his-current-activity"></a>User ends his current Activity
            EngagementAgent.getInstance(this).endActivity();

You need to call `endActivity()` at least once when the user finishes his last activity. This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).

The best place to call this function is on each activity `onPause` callback.

## <a name="reporting-events"></a>Reporting Events
### <a name="session-events"></a>Session events
Session events are usually used to report the actions performed by a user during his session.

**Example without extra data:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Example with extra data:**

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

### <a name="standalone-events"></a>Standalone Events
Contrary to session events, standalone events can occur outside of the context of a session.

**Example:**

Suppose you want to report events occurring when a broadcast receiver is triggered:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Reporting Errors
### <a name="session-errors"></a>Session errors
Session errors are usually used to report the errors impacting the user during his session.

**Example:**

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

### <a name="standalone-errors"></a>Standalone errors
Contrary to session errors, standalone errors can occur outside of the context of a session.

**Example:**

The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Reporting Jobs
### <a name="example"></a>Example
Suppose you want to report the duration of your login process:

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

### <a name="report-errors-during-a-job"></a>Report Errors during a Job
Errors can be related to a running job instead of being related to the current user session.

**Example:**

Suppose you want to report an error during you login process:

[...] public void signIn(Context context, ...) {

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

### <a name="reporting-events-during-a-job"></a>Reporting Events during a job
Events can be related to a running job instead of being related to the current user session.

**Example:**

Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server. The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.

The user can receive messages from his friends, this is a job event.

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

## <a name="extra-parameters"></a>Extra parameters
Arbitrary data can be attached to events, errors, activities and jobs.

This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents). Note that a Bundle can contain arrays or another Bundle instances.

> [!IMPORTANT]
> If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string. Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array. You should convert them into standard arrays before using it in extra parameters.
> 
> 

### <a name="example"></a>Example
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Limits
#### <a name="keys"></a>Keys
Each key in the `Bundle` must match the following regular expression:

`^[a-zA-Z][a-zA-Z_0-9]*`

It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).

#### <a name="size"></a>Size
Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).

In the previous example, the JSON sent to the server is 58 characters long:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Reporting Application Information
You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.

Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.

Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).

### <a name="example"></a>Example
Here is a code sample to send user gender and birthdate:

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>Limits
#### <a name="keys"></a>Keys
Each key in the `Bundle` must match the following regular expression:

`^[a-zA-Z][a-zA-Z_0-9]*`

It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).

#### <a name="size"></a>Size
Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).

In the previous example, the JSON sent to the server is 44 characters long:

            {"expiration":"2016-12-07","status":"premium"}
