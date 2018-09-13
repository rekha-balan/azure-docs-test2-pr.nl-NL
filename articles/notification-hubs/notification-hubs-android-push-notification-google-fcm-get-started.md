---
title: Sending push notifications to Android with Azure Notification Hubs and Firebase Cloud Messaging | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs and Firebase Cloud Messaging to push notifications to Android devices.
services: notification-hubs
documentationcenter: android
keywords: push notifications,push notification,android push notification,fcm,firebase cloud messaging
author: ysxu
manager: erikre
editor: ''
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: 0b63be879b24fb38c40c796183050116f36beed4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552266"
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="31112-104">Sending push notifications to Android with Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="31112-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="31112-105">Overview</span><span class="sxs-lookup"><span data-stu-id="31112-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="31112-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="31112-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="31112-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications to Android with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="31112-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications to Android with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="31112-108">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to send push notifications to an Android application.</span><span class="sxs-lookup"><span data-stu-id="31112-108">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to send push notifications to an Android application.</span></span>
<span data-ttu-id="31112-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="31112-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="31112-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span><span class="sxs-lookup"><span data-stu-id="31112-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31112-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31112-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="31112-112">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="31112-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="31112-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="31112-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="31112-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="31112-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="31112-115">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="31112-115">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="31112-116">Android 2.3 or higher for Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="31112-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="31112-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="31112-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="31112-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="31112-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="31112-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span><span class="sxs-lookup"><span data-stu-id="31112-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="31112-120">Create a new Android Studio Project</span><span class="sxs-lookup"><span data-stu-id="31112-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="31112-121">In Android Studio, start a new Android Studio project.</span><span class="sxs-lookup"><span data-stu-id="31112-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="31112-122">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span><span class="sxs-lookup"><span data-stu-id="31112-122">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="31112-123">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="31112-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="31112-124">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="31112-124">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="31112-125">Create a project that supports Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="31112-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="31112-126">Configure a new notification hub</span><span class="sxs-lookup"><span data-stu-id="31112-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="31112-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="31112-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="31112-128">In the **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="31112-128">In the **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="31112-129">Enter the FCM server key you copied earlier from the [Firebase console](https://firebase.google.com/console/) and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="31112-129">Enter the FCM server key you copied earlier from the [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="31112-131">Your notification hub is now configured to work with Firebase Cloud Messagin, and you have the connection strings to both register your app to receive and send push notifications.</span><span class="sxs-lookup"><span data-stu-id="31112-131">Your notification hub is now configured to work with Firebase Cloud Messagin, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <a id="connecting-app"></a><span data-ttu-id="31112-132">Connect your app to the notification hub</span><span class="sxs-lookup"><span data-stu-id="31112-132">Connect your app to the notification hub</span></span>
### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="31112-133">Add Google Play services to the project</span><span class="sxs-lookup"><span data-stu-id="31112-133">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="31112-134">Adding Azure Notification Hubs libraries</span><span class="sxs-lookup"><span data-stu-id="31112-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="31112-135">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span><span class="sxs-lookup"><span data-stu-id="31112-135">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="31112-136">Add the following repository after the **dependencies** section.</span><span class="sxs-lookup"><span data-stu-id="31112-136">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="31112-137">Updating the AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="31112-137">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="31112-138">To support FCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="31112-138">To support FCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="31112-139">In this tutorial we will name the class `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="31112-139">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="31112-140">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="31112-140">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="31112-141">Once we have received our FCM registration token from the FirebaseInstanceId API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="31112-141">Once we have received our FCM registration token from the FirebaseInstanceId API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="31112-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="31112-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="31112-143">This service will also be responsible for refreshing our FCM registration token.</span><span class="sxs-lookup"><span data-stu-id="31112-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="31112-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="31112-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="31112-145">We will also define a receiver to receive notifications.</span><span class="sxs-lookup"><span data-stu-id="31112-145">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="31112-146">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="31112-146">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="31112-147">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span><span class="sxs-lookup"><span data-stu-id="31112-147">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="31112-148">Add the following necessary FCM related permissions below the  `</application>` tag.</span><span class="sxs-lookup"><span data-stu-id="31112-148">Add the following necessary FCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="31112-149">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span><span class="sxs-lookup"><span data-stu-id="31112-149">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="31112-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="31112-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="31112-151">Adding code</span><span class="sxs-lookup"><span data-stu-id="31112-151">Adding code</span></span>
1. <span data-ttu-id="31112-152">In the Project View, expand **app** > **src** > **main** > **java**.</span><span class="sxs-lookup"><span data-stu-id="31112-152">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="31112-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span><span class="sxs-lookup"><span data-stu-id="31112-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="31112-154">Add a new class named `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="31112-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - new Java class](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="31112-156">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span><span class="sxs-lookup"><span data-stu-id="31112-156">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="31112-157">**SenderId**: The Sender Id you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="31112-157">**SenderId**: The Sender Id you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="31112-158">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span><span class="sxs-lookup"><span data-stu-id="31112-158">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="31112-159">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="31112-159">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="31112-160">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="31112-160">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="31112-161">`NotificationSettings` code:</span><span class="sxs-lookup"><span data-stu-id="31112-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="31112-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="31112-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="31112-163">}</span><span class="sxs-lookup"><span data-stu-id="31112-163">}</span></span>
2. <span data-ttu-id="31112-164">Using the steps above, add another new class named `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="31112-164">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="31112-165">This will be our Instance ID listener service implementation.</span><span class="sxs-lookup"><span data-stu-id="31112-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="31112-166">The code for this class will call our `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span><span class="sxs-lookup"><span data-stu-id="31112-166">The code for this class will call our `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="31112-167">Add another new class to your project named, `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="31112-167">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="31112-168">This will be the implementation for our `IntentService` that will handle [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="31112-168">This will be the implementation for our `IntentService` that will handle [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="31112-169">Use the following code for this class.</span><span class="sxs-lookup"><span data-stu-id="31112-169">Use the following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {
   
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if the token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete registration", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="31112-170">In your `MainActivity` class, add the following `import` statements above the class declaration.</span><span class="sxs-lookup"><span data-stu-id="31112-170">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="31112-171">Add the following private members at the top of the class.</span><span class="sxs-lookup"><span data-stu-id="31112-171">Add the following private members at the top of the class.</span></span> <span data-ttu-id="31112-172">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="31112-172">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="31112-173">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span><span class="sxs-lookup"><span data-stu-id="31112-173">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="31112-174">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span><span class="sxs-lookup"><span data-stu-id="31112-174">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="31112-175">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span><span class="sxs-lookup"><span data-stu-id="31112-175">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="31112-176">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span><span class="sxs-lookup"><span data-stu-id="31112-176">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="31112-177">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span><span class="sxs-lookup"><span data-stu-id="31112-177">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="31112-178">In your activity_main.xml layout, add the following id for that control.</span><span class="sxs-lookup"><span data-stu-id="31112-178">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="31112-179">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="31112-179">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="31112-180">Add another new class to your project named `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="31112-180">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="31112-181">Add the following import statements at the top of `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="31112-181">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="31112-182">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="31112-182">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="31112-183">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span><span class="sxs-lookup"><span data-stu-id="31112-183">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="31112-184">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span><span class="sxs-lookup"><span data-stu-id="31112-184">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="31112-185">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span><span class="sxs-lookup"><span data-stu-id="31112-185">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="31112-186">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span><span class="sxs-lookup"><span data-stu-id="31112-186">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="31112-187">Run the app on your device and verify it registers successfully with the notification hub.</span><span class="sxs-lookup"><span data-stu-id="31112-187">Run the app on your device and verify it registers successfully with the notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="31112-188">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance Id service is called.</span><span class="sxs-lookup"><span data-stu-id="31112-188">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="31112-189">The refresh should intiate a successful registration with the notification hub.</span><span class="sxs-lookup"><span data-stu-id="31112-189">The refresh should intiate a successful registration with the notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="31112-190">Sending push notifications</span><span class="sxs-lookup"><span data-stu-id="31112-190">Sending push notifications</span></span>
<span data-ttu-id="31112-191">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span><span class="sxs-lookup"><span data-stu-id="31112-191">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure Notification Hubs - Test Send](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="31112-193">(Optional) Send push notifications directly from the app</span><span class="sxs-lookup"><span data-stu-id="31112-193">(Optional) Send push notifications directly from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="31112-194">This example of sending notifications from the client app is provided for learning purposes only.</span><span class="sxs-lookup"><span data-stu-id="31112-194">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="31112-195">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span><span class="sxs-lookup"><span data-stu-id="31112-195">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="31112-196">Normally, you would send notifications using a backend server.</span><span class="sxs-lookup"><span data-stu-id="31112-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="31112-197">For some cases, you might want to be able to send push notifications directly from the client application.</span><span class="sxs-lookup"><span data-stu-id="31112-197">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="31112-198">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="31112-198">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="31112-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="31112-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="31112-200">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span><span class="sxs-lookup"><span data-stu-id="31112-200">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="31112-201">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span><span class="sxs-lookup"><span data-stu-id="31112-201">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="31112-202">Add this code at the bottom, just before `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="31112-202">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="31112-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="31112-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="31112-204">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span><span class="sxs-lookup"><span data-stu-id="31112-204">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="31112-205">Add these at the bottom of the file, just before `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="31112-205">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="31112-206">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span><span class="sxs-lookup"><span data-stu-id="31112-206">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="31112-207">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span><span class="sxs-lookup"><span data-stu-id="31112-207">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="31112-208">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span><span class="sxs-lookup"><span data-stu-id="31112-208">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="31112-209">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span><span class="sxs-lookup"><span data-stu-id="31112-209">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="31112-210">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span><span class="sxs-lookup"><span data-stu-id="31112-210">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="31112-211">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span><span class="sxs-lookup"><span data-stu-id="31112-211">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="31112-212">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span><span class="sxs-lookup"><span data-stu-id="31112-212">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="31112-213">The following code is an example implementation.</span><span class="sxs-lookup"><span data-stu-id="31112-213">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="31112-214">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span><span class="sxs-lookup"><span data-stu-id="31112-214">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="31112-215">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span><span class="sxs-lookup"><span data-stu-id="31112-215">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="31112-216">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span><span class="sxs-lookup"><span data-stu-id="31112-216">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="31112-217">Testing your app</span><span class="sxs-lookup"><span data-stu-id="31112-217">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="31112-218">Push notifications in the emulator</span><span class="sxs-lookup"><span data-stu-id="31112-218">Push notifications in the emulator</span></span>
<span data-ttu-id="31112-219">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span><span class="sxs-lookup"><span data-stu-id="31112-219">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="31112-220">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span><span class="sxs-lookup"><span data-stu-id="31112-220">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="31112-221">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="31112-221">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="31112-222">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span><span class="sxs-lookup"><span data-stu-id="31112-222">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="31112-223">Running the application</span><span class="sxs-lookup"><span data-stu-id="31112-223">Running the application</span></span>
1. <span data-ttu-id="31112-224">Run the app and notice that the registration ID is reported for a successful registration.</span><span class="sxs-lookup"><span data-stu-id="31112-224">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="31112-225">Enter a notification message to be sent to all Android devices that have registered with the hub.</span><span class="sxs-lookup"><span data-stu-id="31112-225">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
       ![Testing on Android - sending a message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="31112-226">Press **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="31112-226">Press **Send Notification**.</span></span> <span data-ttu-id="31112-227">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span><span class="sxs-lookup"><span data-stu-id="31112-227">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="31112-228">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span><span class="sxs-lookup"><span data-stu-id="31112-228">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="31112-229">Those can be viewed by swiping down from the upper-left corner.</span><span class="sxs-lookup"><span data-stu-id="31112-229">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
       ![Testing on Android - notifications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="31112-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="31112-230">Next steps</span></span>
<span data-ttu-id="31112-231">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span><span class="sxs-lookup"><span data-stu-id="31112-231">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="31112-232">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span><span class="sxs-lookup"><span data-stu-id="31112-232">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="31112-233">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span><span class="sxs-lookup"><span data-stu-id="31112-233">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="31112-234">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span><span class="sxs-lookup"><span data-stu-id="31112-234">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Guidance]: notification-hubs-push-notification-overview.md
[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure Portal]: https://portal.azure.com








