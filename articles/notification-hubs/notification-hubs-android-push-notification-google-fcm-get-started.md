---
title: Push notifications to Android apps using Azure Notification Hubs and Firebase Cloud Messaging | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs and Google Firebase Cloud Messaging to push notifications to Android devices.
services: notification-hubs
documentationcenter: android
keywords: push notifications,push notification,android push notification,fcm,firebase cloud messaging
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: tutorial
ms.custom: mvc
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: 2bc085989ff3bbbc50042c46b338f748a10aa87e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44829283"
---
# <a name="tutorial-push-notifications-to-android-devices-by-using-azure-notification-hubs-and-google-firebase-cloud-messaging"></a><span data-ttu-id="db9fb-104">Tutorial: Push notifications to Android devices by using Azure Notification Hubs and Google Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="db9fb-104">Tutorial: Push notifications to Android devices by using Azure Notification Hubs and Google Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

> [!IMPORTANT]
> <span data-ttu-id="db9fb-105">This article demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="db9fb-105">This article demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="db9fb-106">If you are still using Google Cloud Messaging (GCM), see [Push notifications to Android devices with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="db9fb-106">If you are still using Google Cloud Messaging (GCM), see [Push notifications to Android devices with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>

<span data-ttu-id="db9fb-107">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to push notifications to an Android application.</span><span class="sxs-lookup"><span data-stu-id="db9fb-107">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to push notifications to an Android application.</span></span> <span data-ttu-id="db9fb-108">In this tutorial, you create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="db9fb-108">In this tutorial, you create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

<span data-ttu-id="db9fb-109">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span><span class="sxs-lookup"><span data-stu-id="db9fb-109">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

<span data-ttu-id="db9fb-110">In this tutorial, you take the following steps:</span><span class="sxs-lookup"><span data-stu-id="db9fb-110">In this tutorial, you take the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db9fb-111">Create an Android Studio project.</span><span class="sxs-lookup"><span data-stu-id="db9fb-111">Create an Android Studio project.</span></span>
> * <span data-ttu-id="db9fb-112">Create a Firebase project that supports Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="db9fb-112">Create a Firebase project that supports Firebase Cloud Messaging.</span></span>
> * <span data-ttu-id="db9fb-113">Create a notification hub.</span><span class="sxs-lookup"><span data-stu-id="db9fb-113">Create a notification hub.</span></span>
> * <span data-ttu-id="db9fb-114">Connect your app to the notification hub.</span><span class="sxs-lookup"><span data-stu-id="db9fb-114">Connect your app to the notification hub.</span></span>
> * <span data-ttu-id="db9fb-115">Test the app.</span><span class="sxs-lookup"><span data-stu-id="db9fb-115">Test the app.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db9fb-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="db9fb-116">Prerequisites</span></span>
<span data-ttu-id="db9fb-117">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="db9fb-117">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="db9fb-118">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="db9fb-118">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="db9fb-119">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="db9fb-119">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

* <span data-ttu-id="db9fb-120">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="db9fb-120">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="db9fb-121">Android 2.3 or higher for Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="db9fb-121">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="db9fb-122">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="db9fb-122">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="db9fb-123">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="db9fb-123">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="db9fb-124">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span><span class="sxs-lookup"><span data-stu-id="db9fb-124">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-an-android-studio-project"></a><span data-ttu-id="db9fb-125">Create an Android Studio Project</span><span class="sxs-lookup"><span data-stu-id="db9fb-125">Create an Android Studio Project</span></span>
1. <span data-ttu-id="db9fb-126">In Android Studio, start a new Android Studio project.</span><span class="sxs-lookup"><span data-stu-id="db9fb-126">In Android Studio, start a new Android Studio project.</span></span>
   
    ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="db9fb-128">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span><span class="sxs-lookup"><span data-stu-id="db9fb-128">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="db9fb-129">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="db9fb-129">Then click **Next**.</span></span>
   
    ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="db9fb-131">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="db9fb-131">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-firebase-project-that-supports-fcm"></a><span data-ttu-id="db9fb-132">Create a Firebase project that supports FCM</span><span class="sxs-lookup"><span data-stu-id="db9fb-132">Create a Firebase project that supports FCM</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="db9fb-133">Configure a notification hub</span><span class="sxs-lookup"><span data-stu-id="db9fb-133">Configure a notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

### <a name="configure-firebase-cloud-messaging-settings-for-the-hub"></a><span data-ttu-id="db9fb-134">Configure Firebase Cloud Messaging settings for the hub</span><span class="sxs-lookup"><span data-stu-id="db9fb-134">Configure Firebase Cloud Messaging settings for the hub</span></span>
1. <span data-ttu-id="db9fb-135">Select **Google (GCM)** in the **NOTIFICATION SETTINGS** category.</span><span class="sxs-lookup"><span data-stu-id="db9fb-135">Select **Google (GCM)** in the **NOTIFICATION SETTINGS** category.</span></span> 
2. <span data-ttu-id="db9fb-136">Enter the API key (FCM server key) you copied earlier from the [Firebase console](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="db9fb-136">Enter the API key (FCM server key) you copied earlier from the [Firebase console](https://firebase.google.com/console/).</span></span>
3. <span data-ttu-id="db9fb-137">Select **Save** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="db9fb-137">Select **Save** on the toolbar.</span></span>

    ![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="db9fb-139">Your notification hub is now configured to work with Firebase Cloud Messaging, and you have the connection strings to both register your app to receive and send push notifications.</span><span class="sxs-lookup"><span data-stu-id="db9fb-139">Your notification hub is now configured to work with Firebase Cloud Messaging, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <a id="connecting-app"></a><span data-ttu-id="db9fb-140">Connect your app to the notification hub</span><span class="sxs-lookup"><span data-stu-id="db9fb-140">Connect your app to the notification hub</span></span>
### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="db9fb-141">Add Google Play services to the project</span><span class="sxs-lookup"><span data-stu-id="db9fb-141">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="db9fb-142">Adding Azure Notification Hubs libraries</span><span class="sxs-lookup"><span data-stu-id="db9fb-142">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="db9fb-143">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span><span class="sxs-lookup"><span data-stu-id="db9fb-143">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
    ```java
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
    ```

2. <span data-ttu-id="db9fb-144">Add the following repository after the **dependencies** section.</span><span class="sxs-lookup"><span data-stu-id="db9fb-144">Add the following repository after the **dependencies** section.</span></span>
   
    ```java
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }
    ```

### <a name="add-google-firebase-support"></a><span data-ttu-id="db9fb-145">Add Google Firebase support</span><span class="sxs-lookup"><span data-stu-id="db9fb-145">Add Google Firebase support</span></span>

1. <span data-ttu-id="db9fb-146">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span><span class="sxs-lookup"><span data-stu-id="db9fb-146">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
    ```java
        compile 'com.google.firebase:firebase-core:12.0.0'
    ```

2. <span data-ttu-id="db9fb-147">Add the following plugin at the end of the file.</span><span class="sxs-lookup"><span data-stu-id="db9fb-147">Add the following plugin at the end of the file.</span></span> 
   
    ```java
    apply plugin: 'com.google.gms.google-services'
    ```

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="db9fb-148">Updating the AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="db9fb-148">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="db9fb-149">To support FCM, you must implement an Instance ID listener service in your code, which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="db9fb-149">To support FCM, you must implement an Instance ID listener service in your code, which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="db9fb-150">In this tutorial, the name of the class is `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="db9fb-150">In this tutorial, the name of the class is `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="db9fb-151">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="db9fb-151">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
    ```xml
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
    ```

2. <span data-ttu-id="db9fb-152">Once you have received your FCM registration token from the FirebaseInstanceId API, you use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="db9fb-152">Once you have received your FCM registration token from the FirebaseInstanceId API, you use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="db9fb-153">You support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="db9fb-153">You support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="db9fb-154">This service is also responsible for refreshing your FCM registration token.</span><span class="sxs-lookup"><span data-stu-id="db9fb-154">This service is also responsible for refreshing your FCM registration token.</span></span>
   
    <span data-ttu-id="db9fb-155">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="db9fb-155">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
    ```xml
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
    ```

3. <span data-ttu-id="db9fb-156">You need to also define a receiver to receive notifications.</span><span class="sxs-lookup"><span data-stu-id="db9fb-156">You need to also define a receiver to receive notifications.</span></span> <span data-ttu-id="db9fb-157">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span><span class="sxs-lookup"><span data-stu-id="db9fb-157">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="db9fb-158">Replace the `<your package>` placeholder with your actual package name shown at the top of the `AndroidManifest.xml` file.</span><span class="sxs-lookup"><span data-stu-id="db9fb-158">Replace the `<your package>` placeholder with your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>

    ```xml
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
    ```

4. <span data-ttu-id="db9fb-159">Add the following necessary FCM-related permissions below the  `</application>` tag.</span><span class="sxs-lookup"><span data-stu-id="db9fb-159">Add the following necessary FCM-related permissions below the  `</application>` tag.</span></span> 
   
    <span data-ttu-id="db9fb-160">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="db9fb-160">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
    ```xml
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    ```

### <a name="adding-code"></a><span data-ttu-id="db9fb-161">Adding code</span><span class="sxs-lookup"><span data-stu-id="db9fb-161">Adding code</span></span>
1. <span data-ttu-id="db9fb-162">In the Project View, expand **app** > **src** > **main** > **java**.</span><span class="sxs-lookup"><span data-stu-id="db9fb-162">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="db9fb-163">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span><span class="sxs-lookup"><span data-stu-id="db9fb-163">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="db9fb-164">Add a new class named `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="db9fb-164">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - new Java class](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="db9fb-166">Make sure to update these three placeholders in the following code for the `NotificationSettings` class:</span><span class="sxs-lookup"><span data-stu-id="db9fb-166">Make sure to update these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="db9fb-167">**SenderId**: The Sender ID you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="db9fb-167">**SenderId**: The Sender ID you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="db9fb-168">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span><span class="sxs-lookup"><span data-stu-id="db9fb-168">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="db9fb-169">You can copy that connection string by clicking **Access Policies** in your hub on the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="db9fb-169">You can copy that connection string by clicking **Access Policies** in your hub on the [Azure portal].</span></span>
   * <span data-ttu-id="db9fb-170">**HubName**: Use the name of your notification hub that appears in the hub page in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="db9fb-170">**HubName**: Use the name of your notification hub that appears in the hub page in the [Azure portal].</span></span>
     
     <span data-ttu-id="db9fb-171">`NotificationSettings` code:</span><span class="sxs-lookup"><span data-stu-id="db9fb-171">`NotificationSettings` code:</span></span>
     
    ```java
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       }
    ```

2. <span data-ttu-id="db9fb-172">Using the steps preceding, add another new class named `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="db9fb-172">Using the steps preceding, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="db9fb-173">This class is your Instance ID listener service implementation.</span><span class="sxs-lookup"><span data-stu-id="db9fb-173">This class is your Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="db9fb-174">The code for this class calls your `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span><span class="sxs-lookup"><span data-stu-id="db9fb-174">The code for this class calls your `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
    ```java
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
    ```

1. <span data-ttu-id="db9fb-175">Add another new class to your project named, `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="db9fb-175">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="db9fb-176">This class implements the `IntentService` interface, and handles [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="db9fb-176">This class implements the `IntentService` interface, and handles [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="db9fb-177">Use the following code for this class.</span><span class="sxs-lookup"><span data-stu-id="db9fb-177">Use the following code for this class.</span></span>
   
    ```java
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
   
                    // Storing the registration ID that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/documentation/articles/notification-hubs-routing-tag-expressions/
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
                        // Refer to : https://azure.microsoft.com/documentation/articles/notification-hubs-routing-tag-expressions/
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
    ```

2. <span data-ttu-id="db9fb-178">In your `MainActivity` class, add the following `import` statements above the class declaration.</span><span class="sxs-lookup"><span data-stu-id="db9fb-178">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
    ```java
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
    ```
3. <span data-ttu-id="db9fb-179">Add the following private members at the top of the class.</span><span class="sxs-lookup"><span data-stu-id="db9fb-179">Add the following private members at the top of the class.</span></span> <span data-ttu-id="db9fb-180">You use these fields to [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="db9fb-180">You use these fields to [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
    ```java
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
    ```

4. <span data-ttu-id="db9fb-181">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span><span class="sxs-lookup"><span data-stu-id="db9fb-181">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
    ```java
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
    ```

5. <span data-ttu-id="db9fb-182">In your `MainActivity` class, add the following code that checks for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span><span class="sxs-lookup"><span data-stu-id="db9fb-182">In your `MainActivity` class, add the following code that checks for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span></span>
   
    ```java
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
    ```

6. <span data-ttu-id="db9fb-183">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span><span class="sxs-lookup"><span data-stu-id="db9fb-183">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
    ```java
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
    ```

7. <span data-ttu-id="db9fb-184">To verify app state and report status in your app, add these additional methods to the `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="db9fb-184">To verify app state and report status in your app, add these additional methods to the `MainActivity`.</span></span>
   
    ```java
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
    ```

8. <span data-ttu-id="db9fb-185">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span><span class="sxs-lookup"><span data-stu-id="db9fb-185">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="db9fb-186">In your activity_main.xml layout, add the following ID for that control.</span><span class="sxs-lookup"><span data-stu-id="db9fb-186">In your activity_main.xml layout, add the following ID for that control.</span></span>
   
    ```java
       android:id="@+id/text_hello"
    ```

9. <span data-ttu-id="db9fb-187">Next you add a subclass for your receiver you defined in the AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="db9fb-187">Next you add a subclass for your receiver you defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="db9fb-188">Add another new class to your project named `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="db9fb-188">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="db9fb-189">Add the following import statements at the top of `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="db9fb-189">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
    ```java
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
    ```

11. <span data-ttu-id="db9fb-190">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="db9fb-190">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="db9fb-191">This code overrides the `OnReceive` method, so the handler reports notifications that are received.</span><span class="sxs-lookup"><span data-stu-id="db9fb-191">This code overrides the `OnReceive` method, so the handler reports notifications that are received.</span></span> <span data-ttu-id="db9fb-192">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span><span class="sxs-lookup"><span data-stu-id="db9fb-192">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="db9fb-193">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span><span class="sxs-lookup"><span data-stu-id="db9fb-193">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
    ```java
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
    ```

12. <span data-ttu-id="db9fb-194">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span><span class="sxs-lookup"><span data-stu-id="db9fb-194">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="db9fb-195">Run the app on your device and verify it registers successfully with the notification hub.</span><span class="sxs-lookup"><span data-stu-id="db9fb-195">Run the app on your device and verify it registers successfully with the notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="db9fb-196">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance ID service is called.</span><span class="sxs-lookup"><span data-stu-id="db9fb-196">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance ID service is called.</span></span> <span data-ttu-id="db9fb-197">The refresh should initiate a successful registration with the notification hub.</span><span class="sxs-lookup"><span data-stu-id="db9fb-197">The refresh should initiate a successful registration with the notification hub.</span></span>
    > 
    > 

## <a name="test-the-app"></a><span data-ttu-id="db9fb-198">Test the app</span><span class="sxs-lookup"><span data-stu-id="db9fb-198">Test the app</span></span>
### <a name="test-send-notification-from-the-notification-hub"></a><span data-ttu-id="db9fb-199">Test send notification from the notification hub</span><span class="sxs-lookup"><span data-stu-id="db9fb-199">Test send notification from the notification hub</span></span>
<span data-ttu-id="db9fb-200">You can send push notifications from the [Azure portal] by doing the following actions:</span><span class="sxs-lookup"><span data-stu-id="db9fb-200">You can send push notifications from the [Azure portal] by doing the following actions:</span></span> 

1. <span data-ttu-id="db9fb-201">Select **Test Send** in the **Troubleshooting** section.</span><span class="sxs-lookup"><span data-stu-id="db9fb-201">Select **Test Send** in the **Troubleshooting** section.</span></span>
2. <span data-ttu-id="db9fb-202">For **Platforms**, select **Android**.</span><span class="sxs-lookup"><span data-stu-id="db9fb-202">For **Platforms**, select **Android**.</span></span> 
3. <span data-ttu-id="db9fb-203">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="db9fb-203">Select **Send**.</span></span>  <span data-ttu-id="db9fb-204">You do not see a notification on the Android device yet because you haven't run the mobile app on it.</span><span class="sxs-lookup"><span data-stu-id="db9fb-204">You do not see a notification on the Android device yet because you haven't run the mobile app on it.</span></span> <span data-ttu-id="db9fb-205">After you run the mobile app, select **Send** button again to see the notification message.</span><span class="sxs-lookup"><span data-stu-id="db9fb-205">After you run the mobile app, select **Send** button again to see the notification message.</span></span> 
4. <span data-ttu-id="db9fb-206">See the **result** of the operation in the list at the bottom.</span><span class="sxs-lookup"><span data-stu-id="db9fb-206">See the **result** of the operation in the list at the bottom.</span></span> 

    ![Azure Notification Hubs - Test Send](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)


[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]


### <a name="run-the-mobile-app"></a><span data-ttu-id="db9fb-208">Run the mobile app</span><span class="sxs-lookup"><span data-stu-id="db9fb-208">Run the mobile app</span></span>
<span data-ttu-id="db9fb-209">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span><span class="sxs-lookup"><span data-stu-id="db9fb-209">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="db9fb-210">If your image doesn't support native Google APIs, you end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span><span class="sxs-lookup"><span data-stu-id="db9fb-210">If your image doesn't support native Google APIs, you end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="db9fb-211">In addition, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="db9fb-211">In addition, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="db9fb-212">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span><span class="sxs-lookup"><span data-stu-id="db9fb-212">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

1. <span data-ttu-id="db9fb-213">Run the app and notice that the registration ID is reported for a successful registration.</span><span class="sxs-lookup"><span data-stu-id="db9fb-213">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
    ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="db9fb-215">Enter a notification message to be sent to all Android devices that have registered with the hub.</span><span class="sxs-lookup"><span data-stu-id="db9fb-215">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
    ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="db9fb-217">Press **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="db9fb-217">Press **Send Notification**.</span></span> <span data-ttu-id="db9fb-218">Any devices that have the app running shows an `AlertDialog` instance with the push notification message.</span><span class="sxs-lookup"><span data-stu-id="db9fb-218">Any devices that have the app running shows an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="db9fb-219">Devices that don't have the app running but were previously registered for push notifications receive a notification in the Android Notification Manager.</span><span class="sxs-lookup"><span data-stu-id="db9fb-219">Devices that don't have the app running but were previously registered for push notifications receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="db9fb-220">The notifications can be viewed by swiping down from the upper-left corner.</span><span class="sxs-lookup"><span data-stu-id="db9fb-220">The notifications can be viewed by swiping down from the upper-left corner.</span></span>
   
    ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="db9fb-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="db9fb-222">Next steps</span></span>
<span data-ttu-id="db9fb-223">In this tutorial, you used Firebase Cloud Messaging to push notifications to Android devices.</span><span class="sxs-lookup"><span data-stu-id="db9fb-223">In this tutorial, you used Firebase Cloud Messaging to push notifications to Android devices.</span></span> <span data-ttu-id="db9fb-224">To learn how to push notifications by using Google Cloud Messaging, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="db9fb-224">To learn how to push notifications by using Google Cloud Messaging, advance to the following tutorial:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="db9fb-225">Push notifications to Android devices using Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="db9fb-225">Push notifications to Android devices using Google Cloud Messaging</span></span>](notification-hubs-android-push-notification-google-gcm-get-started.md)


<!-- Images. -->


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Notification Hubs Guidance]: notification-hubs-push-notification-overview.md
[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure portal]: https://portal.azure.com
