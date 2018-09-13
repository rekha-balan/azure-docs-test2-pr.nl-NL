---
title: Get started with Azure Notification Hubs for Kindle apps | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs to send push notifications to a Kindle application.
services: notification-hubs
documentationcenter: ''
author: ysxu
manager: erikre
editor: ''
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: ccd3878f8bc39739cce682635b73f2960693e214
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552589"
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="7897c-103">Get started with Notification Hubs for Kindle apps</span><span class="sxs-lookup"><span data-stu-id="7897c-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="7897c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7897c-104">Overview</span></span>
<span data-ttu-id="7897c-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span><span class="sxs-lookup"><span data-stu-id="7897c-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="7897c-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="7897c-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7897c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7897c-107">Prerequisites</span></span>
<span data-ttu-id="7897c-108">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="7897c-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="7897c-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span><span class="sxs-lookup"><span data-stu-id="7897c-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="7897c-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span><span class="sxs-lookup"><span data-stu-id="7897c-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="7897c-111">Add a new app to the developer portal</span><span class="sxs-lookup"><span data-stu-id="7897c-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="7897c-112">First, create an app in the [Amazon developer portal].</span><span class="sxs-lookup"><span data-stu-id="7897c-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="7897c-113">Copy the **Application Key**.</span><span class="sxs-lookup"><span data-stu-id="7897c-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="7897c-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span><span class="sxs-lookup"><span data-stu-id="7897c-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="7897c-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span><span class="sxs-lookup"><span data-stu-id="7897c-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="7897c-116">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7897c-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="7897c-117">Click **Security Profiles** to view the security profile that you just created.</span><span class="sxs-lookup"><span data-stu-id="7897c-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="7897c-118">Copy the **Client ID** and **Client Secret** values for later use.</span><span class="sxs-lookup"><span data-stu-id="7897c-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="7897c-119">Create an API key</span><span class="sxs-lookup"><span data-stu-id="7897c-119">Create an API key</span></span>
1. <span data-ttu-id="7897c-120">Open a command prompt with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="7897c-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="7897c-121">Navigate to the Android SDK folder.</span><span class="sxs-lookup"><span data-stu-id="7897c-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="7897c-122">Enter the following command:</span><span class="sxs-lookup"><span data-stu-id="7897c-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="7897c-123">For the **keystore** password, type **android**.</span><span class="sxs-lookup"><span data-stu-id="7897c-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="7897c-124">Copy the **MD5** fingerprint.</span><span class="sxs-lookup"><span data-stu-id="7897c-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="7897c-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span><span class="sxs-lookup"><span data-stu-id="7897c-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="7897c-126">Add credentials to the hub</span><span class="sxs-lookup"><span data-stu-id="7897c-126">Add credentials to the hub</span></span>
<span data-ttu-id="7897c-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span><span class="sxs-lookup"><span data-stu-id="7897c-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="7897c-128">Set up your application</span><span class="sxs-lookup"><span data-stu-id="7897c-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="7897c-129">When you're creating an application, use at least API Level 17.</span><span class="sxs-lookup"><span data-stu-id="7897c-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="7897c-130">Add the ADM libraries to your Eclipse project:</span><span class="sxs-lookup"><span data-stu-id="7897c-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="7897c-131">To obtain the ADM library, [download the SDK].</span><span class="sxs-lookup"><span data-stu-id="7897c-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="7897c-132">Extract the SDK zip file.</span><span class="sxs-lookup"><span data-stu-id="7897c-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="7897c-133">In Eclipse, right-click your project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="7897c-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="7897c-134">Select **Java Build Path** on the left, and then select the \*\*Libraries \*\*tab at the top.</span><span class="sxs-lookup"><span data-stu-id="7897c-134">Select **Java Build Path** on the left, and then select the \*\*Libraries \*\*tab at the top.</span></span> <span data-ttu-id="7897c-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span><span class="sxs-lookup"><span data-stu-id="7897c-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="7897c-136">Download the NotificationHubs Android SDK (link).</span><span class="sxs-lookup"><span data-stu-id="7897c-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="7897c-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7897c-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="7897c-138">Edit your app manifest to support ADM:</span><span class="sxs-lookup"><span data-stu-id="7897c-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="7897c-139">Add the Amazon namespace in the root manifest element:</span><span class="sxs-lookup"><span data-stu-id="7897c-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="7897c-140">Add permissions as the first element under the manifest element.</span><span class="sxs-lookup"><span data-stu-id="7897c-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="7897c-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span><span class="sxs-lookup"><span data-stu-id="7897c-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="7897c-142">Insert the following element as the first child of the application element.</span><span class="sxs-lookup"><span data-stu-id="7897c-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="7897c-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span><span class="sxs-lookup"><span data-stu-id="7897c-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="7897c-144">Create your ADM message handler</span><span class="sxs-lookup"><span data-stu-id="7897c-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="7897c-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="7897c-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="7897c-146">Add the following `import` statements:</span><span class="sxs-lookup"><span data-stu-id="7897c-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="7897c-147">Add the following code in the class that you created.</span><span class="sxs-lookup"><span data-stu-id="7897c-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="7897c-148">Remember to substitute the hub name and connection string (listen):</span><span class="sxs-lookup"><span data-stu-id="7897c-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="7897c-149">Add the following code to the `OnMessage()` method:</span><span class="sxs-lookup"><span data-stu-id="7897c-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="7897c-150">Add the following code to the `OnRegistered` method:</span><span class="sxs-lookup"><span data-stu-id="7897c-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="7897c-151">Add the following code to the `OnUnregistered` method:</span><span class="sxs-lookup"><span data-stu-id="7897c-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="7897c-152">In the `MainActivity` method, add the following import statement:</span><span class="sxs-lookup"><span data-stu-id="7897c-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="7897c-153">Add the following code at the end of the `OnCreate` method:</span><span class="sxs-lookup"><span data-stu-id="7897c-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="7897c-154">Add your API key to your app</span><span class="sxs-lookup"><span data-stu-id="7897c-154">Add your API key to your app</span></span>
1. <span data-ttu-id="7897c-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span><span class="sxs-lookup"><span data-stu-id="7897c-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="7897c-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span><span class="sxs-lookup"><span data-stu-id="7897c-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="7897c-157">Run the app</span><span class="sxs-lookup"><span data-stu-id="7897c-157">Run the app</span></span>
1. <span data-ttu-id="7897c-158">Start the emulator.</span><span class="sxs-lookup"><span data-stu-id="7897c-158">Start the emulator.</span></span>
2. <span data-ttu-id="7897c-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span><span class="sxs-lookup"><span data-stu-id="7897c-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="7897c-160">In Eclipse, run the app.</span><span class="sxs-lookup"><span data-stu-id="7897c-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="7897c-161">If a problem occurs, check the time of the emulator (or device).</span><span class="sxs-lookup"><span data-stu-id="7897c-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="7897c-162">The time value must be accurate.</span><span class="sxs-lookup"><span data-stu-id="7897c-162">The time value must be accurate.</span></span> <span data-ttu-id="7897c-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span><span class="sxs-lookup"><span data-stu-id="7897c-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="7897c-164">Send a message</span><span class="sxs-lookup"><span data-stu-id="7897c-164">Send a message</span></span>
<span data-ttu-id="7897c-165">To send a message by using .NET:</span><span class="sxs-lookup"><span data-stu-id="7897c-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[Amazon developer portal]: https://developer.amazon.com/home.html
[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png








