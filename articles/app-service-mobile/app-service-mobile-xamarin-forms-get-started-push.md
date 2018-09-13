---
title: Add push notifications to your Xamarin.Forms app | Microsoft Docs
description: Learn how to use Azure services to send multi-platform push notifications to your Xamarin.Forms apps.
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: adrianha
editor: ''
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: f1fe97c6b3e2d28b7e17d035bc7e3ecced8a0d0f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553099"
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="4e663-103">Add push notifications to your Xamarin.Forms app</span><span class="sxs-lookup"><span data-stu-id="4e663-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="4e663-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4e663-104">Overview</span></span>
<span data-ttu-id="4e663-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4e663-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="4e663-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="4e663-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="4e663-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span><span class="sxs-lookup"><span data-stu-id="4e663-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="4e663-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4e663-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e663-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4e663-109">Prerequisites</span></span>
<span data-ttu-id="4e663-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span><span class="sxs-lookup"><span data-stu-id="4e663-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="4e663-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="4e663-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <a name="configure-hub"></a><span data-ttu-id="4e663-112">Configure a notification hub</span><span class="sxs-lookup"><span data-stu-id="4e663-112">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="4e663-113">Update the server project to send push notifications</span><span class="sxs-lookup"><span data-stu-id="4e663-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="4e663-114">Configure and run the Android project (optional)</span><span class="sxs-lookup"><span data-stu-id="4e663-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="4e663-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span><span class="sxs-lookup"><span data-stu-id="4e663-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="4e663-116">Enable Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="4e663-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="4e663-117">Configure the Mobile Apps back end to send push requests by using FCM</span><span class="sxs-lookup"><span data-stu-id="4e663-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="4e663-118">Add push notifications to the Android project</span><span class="sxs-lookup"><span data-stu-id="4e663-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="4e663-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span><span class="sxs-lookup"><span data-stu-id="4e663-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="4e663-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span><span class="sxs-lookup"><span data-stu-id="4e663-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="4e663-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**. Then search for the **Google Cloud Messaging Client** component and add it to the project.</span><span class="sxs-lookup"><span data-stu-id="4e663-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**. Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="4e663-122">This component supports push notifications for a Xamarin Android project.</span><span class="sxs-lookup"><span data-stu-id="4e663-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="4e663-123">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span><span class="sxs-lookup"><span data-stu-id="4e663-123">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="4e663-124">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="4e663-124">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="4e663-125">Add a new **CreateAndShowDialog** helper method, as follows:</span><span class="sxs-lookup"><span data-stu-id="4e663-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="4e663-126">Add the following code to the **MainActivity** class:</span><span class="sxs-lookup"><span data-stu-id="4e663-126">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="4e663-127">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span><span class="sxs-lookup"><span data-stu-id="4e663-127">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="4e663-128">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span><span class="sxs-lookup"><span data-stu-id="4e663-128">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="4e663-129">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span><span class="sxs-lookup"><span data-stu-id="4e663-129">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. <span data-ttu-id="4e663-130">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span><span class="sxs-lookup"><span data-stu-id="4e663-130">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="4e663-131">Add the following class definition to the namespace.</span><span class="sxs-lookup"><span data-stu-id="4e663-131">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="4e663-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span><span class="sxs-lookup"><span data-stu-id="4e663-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="4e663-133">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span><span class="sxs-lookup"><span data-stu-id="4e663-133">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="4e663-134">Add the following code to the **GcmService** class.</span><span class="sxs-lookup"><span data-stu-id="4e663-134">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="4e663-135">This overrides the **OnRegistered** event handler and implements a **Register** method.</span><span class="sxs-lookup"><span data-stu-id="4e663-135">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    <span data-ttu-id="4e663-136">Note that this code uses the `messageParam` parameter in the template registration.</span><span class="sxs-lookup"><span data-stu-id="4e663-136">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="4e663-137">Add the following code that implements **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="4e663-137">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="4e663-138">This handles incoming notifications and sends them to the notification manager to be displayed.</span><span class="sxs-lookup"><span data-stu-id="4e663-138">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="4e663-139">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span><span class="sxs-lookup"><span data-stu-id="4e663-139">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="4e663-140">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span><span class="sxs-lookup"><span data-stu-id="4e663-140">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="4e663-141">Test push notifications in your Android app</span><span class="sxs-lookup"><span data-stu-id="4e663-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="4e663-142">The first two steps are required only when you're testing on an emulator.</span><span class="sxs-lookup"><span data-stu-id="4e663-142">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="4e663-143">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span><span class="sxs-lookup"><span data-stu-id="4e663-143">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="4e663-144">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span><span class="sxs-lookup"><span data-stu-id="4e663-144">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="4e663-145">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span><span class="sxs-lookup"><span data-stu-id="4e663-145">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="4e663-146">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span><span class="sxs-lookup"><span data-stu-id="4e663-146">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="4e663-147">Click **Run** to build the project and start the app on your Android device or emulator.</span><span class="sxs-lookup"><span data-stu-id="4e663-147">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="4e663-148">In the app, type a task, and then click the plus (**+**) icon.</span><span class="sxs-lookup"><span data-stu-id="4e663-148">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="4e663-149">Verify that a notification is received when an item is added.</span><span class="sxs-lookup"><span data-stu-id="4e663-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="4e663-150">Configure and run the iOS project (optional)</span><span class="sxs-lookup"><span data-stu-id="4e663-150">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="4e663-151">This section is for running the Xamarin iOS project for iOS devices.</span><span class="sxs-lookup"><span data-stu-id="4e663-151">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="4e663-152">You can skip this section if you are not working with iOS devices.</span><span class="sxs-lookup"><span data-stu-id="4e663-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="4e663-153">Configure the notification hub for APNS</span><span class="sxs-lookup"><span data-stu-id="4e663-153">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="4e663-154">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e663-154">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="4e663-155">Add push notifications to your iOS app</span><span class="sxs-lookup"><span data-stu-id="4e663-155">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="4e663-156">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span><span class="sxs-lookup"><span data-stu-id="4e663-156">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="4e663-157">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span><span class="sxs-lookup"><span data-stu-id="4e663-157">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. <span data-ttu-id="4e663-158">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span><span class="sxs-lookup"><span data-stu-id="4e663-158">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    <span data-ttu-id="4e663-159">This method handles incoming notifications while the app is running.</span><span class="sxs-lookup"><span data-stu-id="4e663-159">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="4e663-160">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span><span class="sxs-lookup"><span data-stu-id="4e663-160">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="4e663-161">This enables support for remote notifications and requests push registration.</span><span class="sxs-lookup"><span data-stu-id="4e663-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="4e663-162">Your app is now updated to support push notifications.</span><span class="sxs-lookup"><span data-stu-id="4e663-162">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="4e663-163">Test push notifications in your iOS app</span><span class="sxs-lookup"><span data-stu-id="4e663-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="4e663-164">Right-click the iOS project, and click **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="4e663-164">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="4e663-165">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span><span class="sxs-lookup"><span data-stu-id="4e663-165">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="4e663-166">Then click **OK** to accept push notifications.</span><span class="sxs-lookup"><span data-stu-id="4e663-166">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4e663-167">You must explicitly accept push notifications from your app.</span><span class="sxs-lookup"><span data-stu-id="4e663-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="4e663-168">This request only occurs the first time that the app runs.</span><span class="sxs-lookup"><span data-stu-id="4e663-168">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="4e663-169">In the app, type a task, and then click the plus (**+**) icon.</span><span class="sxs-lookup"><span data-stu-id="4e663-169">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="4e663-170">Verify that a notification is received, and then click **OK** to dismiss the notification.</span><span class="sxs-lookup"><span data-stu-id="4e663-170">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="4e663-171">Configure and run Windows projects (optional)</span><span class="sxs-lookup"><span data-stu-id="4e663-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="4e663-172">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span><span class="sxs-lookup"><span data-stu-id="4e663-172">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="4e663-173">These steps also support Universal Windows Platform (UWP) projects.</span><span class="sxs-lookup"><span data-stu-id="4e663-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="4e663-174">You can skip this section if you are not working with Windows devices.</span><span class="sxs-lookup"><span data-stu-id="4e663-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="4e663-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span><span class="sxs-lookup"><span data-stu-id="4e663-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="4e663-176">Configure the notification hub for WNS</span><span class="sxs-lookup"><span data-stu-id="4e663-176">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="4e663-177">Add push notifications to your Windows app</span><span class="sxs-lookup"><span data-stu-id="4e663-177">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="4e663-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span><span class="sxs-lookup"><span data-stu-id="4e663-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="4e663-179">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span><span class="sxs-lookup"><span data-stu-id="4e663-179">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="4e663-180">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span><span class="sxs-lookup"><span data-stu-id="4e663-180">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    <span data-ttu-id="4e663-181">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span><span class="sxs-lookup"><span data-stu-id="4e663-181">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="4e663-182">A template notification that supports *messageParam* will be delivered to this client.</span><span class="sxs-lookup"><span data-stu-id="4e663-182">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="4e663-183">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span><span class="sxs-lookup"><span data-stu-id="4e663-183">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="4e663-184">Then add the following line of code at the end of the method:</span><span class="sxs-lookup"><span data-stu-id="4e663-184">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="4e663-185">This ensures that the push notification registration is created or refreshed every time the app is launched.</span><span class="sxs-lookup"><span data-stu-id="4e663-185">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="4e663-186">It's important to do this to guarantee that the WNS push channel is always active.</span><span class="sxs-lookup"><span data-stu-id="4e663-186">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="4e663-187">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="4e663-187">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="4e663-188">Build the app and verify you have no errors.</span><span class="sxs-lookup"><span data-stu-id="4e663-188">Build the app and verify you have no errors.</span></span> <span data-ttu-id="4e663-189">Your client app should now register for the template notifications from the Mobile Apps back end.</span><span class="sxs-lookup"><span data-stu-id="4e663-189">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="4e663-190">Repeat this section for every Windows project in your solution.</span><span class="sxs-lookup"><span data-stu-id="4e663-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="4e663-191">Test push notifications in your Windows app</span><span class="sxs-lookup"><span data-stu-id="4e663-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="4e663-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span><span class="sxs-lookup"><span data-stu-id="4e663-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="4e663-193">Press the **Run** button to build the project and start the app.</span><span class="sxs-lookup"><span data-stu-id="4e663-193">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="4e663-194">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span><span class="sxs-lookup"><span data-stu-id="4e663-194">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="4e663-195">Verify that a notification is received when the item is added.</span><span class="sxs-lookup"><span data-stu-id="4e663-195">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e663-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e663-196">Next steps</span></span>
<span data-ttu-id="4e663-197">You can learn more about push notifications:</span><span class="sxs-lookup"><span data-stu-id="4e663-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="4e663-198">Diagnose push notification issues</span><span class="sxs-lookup"><span data-stu-id="4e663-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="4e663-199">There are various reasons why notifications may get dropped or do not end up on devices.</span><span class="sxs-lookup"><span data-stu-id="4e663-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="4e663-200">This topic shows you how to analyze and figure out the root cause of push notification failures.</span><span class="sxs-lookup"><span data-stu-id="4e663-200">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="4e663-201">You can also continue on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="4e663-201">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="4e663-202">Add authentication to your app </span><span class="sxs-lookup"><span data-stu-id="4e663-202">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="4e663-203">Learn how to authenticate users of your app with an identity provider.</span><span class="sxs-lookup"><span data-stu-id="4e663-203">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="4e663-204">Enable offline sync for your app</span><span class="sxs-lookup"><span data-stu-id="4e663-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="4e663-205">Learn how to add offline support for your app by using a Mobile Apps back end.</span><span class="sxs-lookup"><span data-stu-id="4e663-205">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="4e663-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="4e663-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
