---
title: Push notifications to Xamarin.Android apps using Azure Notification Hubs | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs to send push notifications to a Xamarin Android application.
author: dimazaid
manager: kpiteira
editor: spelluru
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: tutorial
ms.custom: mvc
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: 94e8e813b537d304e62854b81979d433d0645115
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819239"
---
# <a name="tutorial-push-notifications-to-xamarinandroid-apps-using-azure-notification-hubs"></a><span data-ttu-id="f6ad8-103">Tutorial: Push notifications to Xamarin.Android apps using Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="f6ad8-103">Tutorial: Push notifications to Xamarin.Android apps using Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="f6ad8-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f6ad8-104">Overview</span></span>
<span data-ttu-id="f6ad8-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span></span> <span data-ttu-id="f6ad8-106">You create a blank Xamarin.Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="f6ad8-106">You create a blank Xamarin.Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="f6ad8-107">You use your notification hub to broadcast push notifications to all the devices running your app.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-107">You use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="f6ad8-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="f6ad8-109">In this tutorial, you take the following steps:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-109">In this tutorial, you take the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f6ad8-110">Create a Firebase project and enable Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="f6ad8-110">Create a Firebase project and enable Firebase Cloud Messaging</span></span>
> * <span data-ttu-id="f6ad8-111">Create a notification hub</span><span class="sxs-lookup"><span data-stu-id="f6ad8-111">Create a notification hub</span></span>
> * <span data-ttu-id="f6ad8-112">Create a Xamarin.Android app and connect it to the notification hub</span><span class="sxs-lookup"><span data-stu-id="f6ad8-112">Create a Xamarin.Android app and connect it to the notification hub</span></span>
> * <span data-ttu-id="f6ad8-113">Send test notifications from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f6ad8-113">Send test notifications from the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6ad8-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f6ad8-114">Prerequisites</span></span>

- <span data-ttu-id="f6ad8-115">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-115">**Azure subscription**.</span></span> <span data-ttu-id="f6ad8-116">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-116">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
- <span data-ttu-id="f6ad8-117">[Visual Studio with Xamarin] on Windows or [Visual Studio for Mac] on OS X.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-117">[Visual Studio with Xamarin] on Windows or [Visual Studio for Mac] on OS X.</span></span>
- <span data-ttu-id="f6ad8-118">Active Google account</span><span class="sxs-lookup"><span data-stu-id="f6ad8-118">Active Google account</span></span>

## <a name="create-a-firebase-project-and-enable-firebase-cloud-messaging"></a><span data-ttu-id="f6ad8-119">Create a Firebase project and enable Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="f6ad8-119">Create a Firebase project and enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="create-a-notification-hub"></a><span data-ttu-id="f6ad8-120">Create a notification hub</span><span class="sxs-lookup"><span data-stu-id="f6ad8-120">Create a notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

### <a name="configure-gcm-settings-for-the-notification-hub"></a><span data-ttu-id="f6ad8-121">Configure GCM settings for the notification hub</span><span class="sxs-lookup"><span data-stu-id="f6ad8-121">Configure GCM settings for the notification hub</span></span>

1. <span data-ttu-id="f6ad8-122">Select **Google (GCM)** in the **NOTIFICATION SETTINGS** section.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-122">Select **Google (GCM)** in the **NOTIFICATION SETTINGS** section.</span></span> 
2. <span data-ttu-id="f6ad8-123">Enter the **Legacy server key** you noted down from the Google Firebase Console.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-123">Enter the **Legacy server key** you noted down from the Google Firebase Console.</span></span> 
3. <span data-ttu-id="f6ad8-124">Select **Save** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-124">Select **Save** on the toolbar.</span></span> 

    ![](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="f6ad8-125">Your notification hub is configured to work with FCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-125">Your notification hub is configured to work with FCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span></span>

## <a name="create-xamarinandroid-app-and-connect-it-to-notification-hub"></a><span data-ttu-id="f6ad8-126">Create Xamarin.Android app and connect it to notification hub</span><span class="sxs-lookup"><span data-stu-id="f6ad8-126">Create Xamarin.Android app and connect it to notification hub</span></span>

### <a name="create-visual-studio-project-and-add-nuget-packages"></a><span data-ttu-id="f6ad8-127">Create Visual Studio project and add NuGet packages</span><span class="sxs-lookup"><span data-stu-id="f6ad8-127">Create Visual Studio project and add NuGet packages</span></span>
1. <span data-ttu-id="f6ad8-128">In Visual Studio, point to **File**, select **New**, and then select **Project**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-128">In Visual Studio, point to **File**, select **New**, and then select **Project**.</span></span> 
   
      ![Visual Studio- Create new Android project](./media/partner-xamarin-notification-hubs-android-get-started/new-project-dialog.png)
2. <span data-ttu-id="f6ad8-130">In the **Solution Explorer** window, expand **Properties**, and click **AndroidManifest.xml**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-130">In the **Solution Explorer** window, expand **Properties**, and click **AndroidManifest.xml**.</span></span> <span data-ttu-id="f6ad8-131">Update the package name to match the package name you entered when adding Firebase Cloud Messaging to your project in the Google Firebase Console.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-131">Update the package name to match the package name you entered when adding Firebase Cloud Messaging to your project in the Google Firebase Console.</span></span> 

      ![Package name in GCM](./media/partner-xamarin-notification-hubs-android-get-started/package-name-gcm.png)
3. <span data-ttu-id="f6ad8-133">Right-click your project, and select **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-133">Right-click your project, and select **Manage NuGet Packages...**.</span></span> 
4. <span data-ttu-id="f6ad8-134">Select the **Browse** tab. Search for **Xamarin.GooglePlayServices.Base**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-134">Select the **Browse** tab. Search for **Xamarin.GooglePlayServices.Base**.</span></span> <span data-ttu-id="f6ad8-135">Select **Xamarin.GooglePlayServices.Base** in the result list.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-135">Select **Xamarin.GooglePlayServices.Base** in the result list.</span></span> <span data-ttu-id="f6ad8-136">Then, select **Install**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-136">Then, select **Install**.</span></span> 

      ![Google Play Services NuGet](./media/partner-xamarin-notification-hubs-android-get-started/google-play-services-nuget.png)
5. <span data-ttu-id="f6ad8-138">In the **NuGet Package Manager** window, search for **Xamarin.Firebase.Messaging**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-138">In the **NuGet Package Manager** window, search for **Xamarin.Firebase.Messaging**.</span></span> <span data-ttu-id="f6ad8-139">Select **Xamarin.Firebase.Messaging** in the result list.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-139">Select **Xamarin.Firebase.Messaging** in the result list.</span></span> <span data-ttu-id="f6ad8-140">Then, select **Install**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-140">Then, select **Install**.</span></span> 
6. <span data-ttu-id="f6ad8-141">Now, search for **Xamarin.Azure.NotificationHubs.Android**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-141">Now, search for **Xamarin.Azure.NotificationHubs.Android**.</span></span> <span data-ttu-id="f6ad8-142">Select **Xamarin.Azure.NotificationHubs.Android** in the result list.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-142">Select **Xamarin.Azure.NotificationHubs.Android** in the result list.</span></span> <span data-ttu-id="f6ad8-143">Then, select **Install**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-143">Then, select **Install**.</span></span> 

### <a name="add-the-google-services-json-file"></a><span data-ttu-id="f6ad8-144">Add the Google Services JSON File</span><span class="sxs-lookup"><span data-stu-id="f6ad8-144">Add the Google Services JSON File</span></span>

1. <span data-ttu-id="f6ad8-145">Copy **google-services.json** that you downloaded from the Google Firebase Console to the project folder.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-145">Copy **google-services.json** that you downloaded from the Google Firebase Console to the project folder.</span></span>
2. <span data-ttu-id="f6ad8-146">Add **google-services.json** to the project.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-146">Add **google-services.json** to the project.</span></span>
3. <span data-ttu-id="f6ad8-147">Select **google-services.json** in the **Solution Explorer** window.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-147">Select **google-services.json** in the **Solution Explorer** window.</span></span>
4. <span data-ttu-id="f6ad8-148">In the **Properties** pane, set the Build Action to **GoogleServicesJson**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-148">In the **Properties** pane, set the Build Action to **GoogleServicesJson**.</span></span> <span data-ttu-id="f6ad8-149">If you don't see **GoogleServicesJson**, close Visual Studio, relaunch it, reopen the project, and retry.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-149">If you don't see **GoogleServicesJson**, close Visual Studio, relaunch it, reopen the project, and retry.</span></span> 

      ![GoogleServicesJson build action](./media/partner-xamarin-notification-hubs-android-get-started/google-services-json-build-action.png)

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="f6ad8-151">Set up notification hubs in your project</span><span class="sxs-lookup"><span data-stu-id="f6ad8-151">Set up notification hubs in your project</span></span>

#### <a name="registering-with-firebase-cloud-messaging"></a><span data-ttu-id="f6ad8-152">Registering with Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="f6ad8-152">Registering with Firebase Cloud Messaging</span></span>

<span data-ttu-id="f6ad8-153">Open the **AndroidManifest.xml** file and insert the following `<receiver>` elements into the `<application>` element:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-153">Open the **AndroidManifest.xml** file and insert the following `<receiver>` elements into the `<application>` element:</span></span>

        <receiver android:name="com.google.firebase.iid.FirebaseInstanceIdInternalReceiver" android:exported="false" />
        <receiver android:name="com.google.firebase.iid.FirebaseInstanceIdReceiver" android:exported="true" android:permission="com.google.android.c2dm.permission.SEND">
          <intent-filter>
            <action android:name="com.google.android.c2dm.intent.RECEIVE" />
            <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
            <category android:name="${applicationId}" />
          </intent-filter>
        </receiver>

1. <span data-ttu-id="f6ad8-154">Gather the following information for your Android app and notification hub:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-154">Gather the following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="f6ad8-155">**Listen connection string**: On the dashboard in the [Azure portal], choose **View connection strings**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-155">**Listen connection string**: On the dashboard in the [Azure portal], choose **View connection strings**.</span></span> <span data-ttu-id="f6ad8-156">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-156">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="f6ad8-157">**Hub name**: Name of your hub from the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="f6ad8-157">**Hub name**: Name of your hub from the [Azure portal].</span></span> <span data-ttu-id="f6ad8-158">For example, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-158">For example, *mynotificationhub2*.</span></span>
     
2. <span data-ttu-id="f6ad8-159">Right-click your **project** in the **Solution Explorer** window, point to **Add**, and select **Class**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-159">Right-click your **project** in the **Solution Explorer** window, point to **Add**, and select **Class**.</span></span> 
4. <span data-ttu-id="f6ad8-160">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-160">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span></span> <span data-ttu-id="f6ad8-161">Replace the placeholders with your values.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-161">Replace the placeholders with your values.</span></span>
    
    ```csharp
        public static class Constants
        {
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
        }
    ```
3. <span data-ttu-id="f6ad8-162">Add the following using statements to **MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-162">Add the following using statements to **MainActivity.cs**:</span></span>
   
    ```csharp
        using Android.Util;
    ```
4. <span data-ttu-id="f6ad8-163">Add an instance variable to **MainActivity.cs** that will be used to show an alert dialog when the app is running:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-163">Add an instance variable to **MainActivity.cs** that will be used to show an alert dialog when the app is running:</span></span>
   
    ```csharp
        public const string TAG = "MainActivity";
    ```
5. <span data-ttu-id="f6ad8-164">Add the following code to `OnCreate` in **MainActivity.cs** after `base.OnCreate(savedInstanceState)`:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-164">Add the following code to `OnCreate` in **MainActivity.cs** after `base.OnCreate(savedInstanceState)`:</span></span>

    ```csharp   
        if (Intent.Extras != null)
        {
            foreach (var key in Intent.Extras.KeySet())
            {
                if(key!=null)
                {
                    var value = Intent.Extras.GetString(key);
                    Log.Debug(TAG, "Key: {0} Value: {1}", key, value);
                }
            }
        }
    ```
7. <span data-ttu-id="f6ad8-165">Create a new class, **MyFirebaseIIDService** like you created the **Constants** class.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-165">Create a new class, **MyFirebaseIIDService** like you created the **Constants** class.</span></span> 
8. <span data-ttu-id="f6ad8-166">Add the following using statements to **MyFirebaseIIDService.cs**:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-166">Add the following using statements to **MyFirebaseIIDService.cs**:</span></span>
   
    ```csharp
    using Android.App;
    using Android.Util;
    using WindowsAzure.Messaging;
    using Firebase.Iid;
    ```

9. <span data-ttu-id="f6ad8-167">In **MyFirebaseIIDService.cs**, add the following **class** declaration, and have your class inherit from **FirebaseInstanceIdService**:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-167">In **MyFirebaseIIDService.cs**, add the following **class** declaration, and have your class inherit from **FirebaseInstanceIdService**:</span></span>
   
    ```csharp
        [Service]
        [IntentFilter(new[] { "com.google.firebase.INSTANCE_ID_EVENT" })]
        public class MyFirebaseIIDService : FirebaseInstanceIdService
    ```
10. <span data-ttu-id="f6ad8-168">In **MyFirebaseIIDService.cs**, add the following code:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-168">In **MyFirebaseIIDService.cs**, add the following code:</span></span>
   
    ```csharp
        const string TAG = "MyFirebaseIIDService";
        NotificationHub hub;

        public override void OnTokenRefresh()
        {
            var refreshedToken = FirebaseInstanceId.Instance.Token;
            Log.Debug(TAG, "FCM token: " + refreshedToken);
            SendRegistrationToServer(refreshedToken);
        }

        void SendRegistrationToServer(string token)
        {
            // Register with Notification Hubs
            hub = new NotificationHub(Constants.NotificationHubName,
                                      Constants.ListenConnectionString, this);

            var tags = new List<string>() { };
            var regID = hub.Register(token, tags.ToArray()).RegistrationId;

            Log.Debug(TAG, $"Successful registration of ID {regID}");
        }
    ```
11. <span data-ttu-id="f6ad8-169">Create another new class for your project, name it **MyFirebaseMessagingService**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-169">Create another new class for your project, name it **MyFirebaseMessagingService**.</span></span>
12. <span data-ttu-id="f6ad8-170">Add the following using statements to **MyFirebaseMessagingService.cs**.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-170">Add the following using statements to **MyFirebaseMessagingService.cs**.</span></span>
    
    ```csharp
        using Android.App;
        using Android.Util;
        using Firebase.Messaging;
    ```
13. <span data-ttu-id="f6ad8-171">Add the following above your class declaration, and have your class inherit from **FirebaseMessagingService**:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-171">Add the following above your class declaration, and have your class inherit from **FirebaseMessagingService**:</span></span>
    
    ```csharp
        [Service]
        [IntentFilter(new[] { "com.google.firebase.MESSAGING_EVENT" })]
        public class MyFirebaseMessagingService : FirebaseMessagingService
    ```    
14. <span data-ttu-id="f6ad8-172">Add the following code to **MyFirebaseMessagingService.cs**:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-172">Add the following code to **MyFirebaseMessagingService.cs**:</span></span>
    
    ```csharp
        const string TAG = "MyFirebaseMsgService";
        public override void OnMessageReceived(RemoteMessage message)
        {
            Log.Debug(TAG, "From: " + message.From);
            if(message.GetNotification()!= null)
            {
                //These is how most messages will be received
                Log.Debug(TAG, "Notification Message Body: " + message.GetNotification().Body);
                SendNotification(message.GetNotification().Body);
            }
            else 
            {
                //Only used for debugging payloads sent from the Azure portal
                SendNotification(message.Data.Values.First());

            }

        }

        void SendNotification(string messageBody)
        {
            var intent = new Intent(this, typeof(MainActivity));
            intent.AddFlags(ActivityFlags.ClearTop);
            var pendingIntent = PendingIntent.GetActivity(this, 0, intent, PendingIntentFlags.OneShot);

            var notificationBuilder = new Notification.Builder(this)
                        .SetContentTitle("FCM Message")
                        .SetSmallIcon(Resource.Drawable.ic_launcher)
                        .SetContentText(messageBody)
                        .SetAutoCancel(true)
                        .SetContentIntent(pendingIntent);

            var notificationManager = NotificationManager.FromContext(this);

            notificationManager.Notify(0, notificationBuilder.Build());
        }
    ```
15. <span data-ttu-id="f6ad8-173">**Build** your project.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-173">**Build** your project.</span></span> 
16. <span data-ttu-id="f6ad8-174">**Run** your app on your device or loaded emulator</span><span class="sxs-lookup"><span data-stu-id="f6ad8-174">**Run** your app on your device or loaded emulator</span></span>

## <a name="send-test-notification-from-the-azure-portal"></a><span data-ttu-id="f6ad8-175">Send test notification from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f6ad8-175">Send test notification from the Azure portal</span></span>
<span data-ttu-id="f6ad8-176">You can test receiving notifications in your app with the *Test Send* option in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="f6ad8-176">You can test receiving notifications in your app with the *Test Send* option in the [Azure portal].</span></span> <span data-ttu-id="f6ad8-177">It sends a test push notification to your device.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-177">It sends a test push notification to your device.</span></span>

![Azure portal - Test Send](media/partner-xamarin-notification-hubs-android-get-started/send-test-notification.png)

<span data-ttu-id="f6ad8-179">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET through a compatible library.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-179">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="f6ad8-180">If a library is not available for your back-end, you can also use the REST API directly to send notification messages.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-180">If a library is not available for your back-end, you can also use the REST API directly to send notification messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6ad8-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6ad8-181">Next steps</span></span>
<span data-ttu-id="f6ad8-182">In this tutorial, you sent broadcast notifications to all your Android devices registered with the backend.</span><span class="sxs-lookup"><span data-stu-id="f6ad8-182">In this tutorial, you sent broadcast notifications to all your Android devices registered with the backend.</span></span> <span data-ttu-id="f6ad8-183">To learn how to push notifications to specific Android devices, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="f6ad8-183">To learn how to push notifications to specific Android devices, advance to the following tutorial:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="f6ad8-184">Push notifications to specific devices</span><span class="sxs-lookup"><span data-stu-id="f6ad8-184">Push notifications to specific devices</span></span>](notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md)


<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app to the Notification Hub]: #connecting-app
[Run your app with the emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png
[24]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-xamarin-android-app-options.png
[25]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-google-services-json.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-test-send.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js
[Visual Studio with Xamarin]: https://docs.microsoft.com/visualstudio/install/install-visual-studio
[Visual Studio for Mac]: https://www.visualstudio.com/vs/visual-studio-mac/

[Azure portal]: https://portal.azure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Android]: http://msdn.microsoft.com/library/dn282661.aspx

[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[GitHub]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid
