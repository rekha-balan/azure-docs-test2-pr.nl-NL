---
title: Add Push Notifications to Apache Cordova App with Azure Mobile Apps | Microsoft Docs
description: Learn how to use Azure Mobile Apps to send push notifications to your Apache Cordova app.
services: app-service\mobile
documentationcenter: javascript
manager: adrianha
editor: ''
author: ysxu
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: yuaxu
ms.openlocfilehash: 22f424bf4ef86cbfdaafaa9c8963e00381528af8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552301"
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="5ed4b-103">Add push notifications to your Apache Cordova app</span><span class="sxs-lookup"><span data-stu-id="5ed4b-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="5ed4b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5ed4b-104">Overview</span></span>
<span data-ttu-id="5ed4b-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="5ed4b-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="5ed4b-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="5ed4b-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ed4b-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5ed4b-108">Prerequisites</span></span>
<span data-ttu-id="5ed4b-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="5ed4b-110">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="5ed4b-111">A PC with [Visual Studio Community 2015][2] or later versions.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="5ed4b-112">[Visual Studio Tools for Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="5ed4b-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="5ed4b-113">An [active Azure account][3].</span><span class="sxs-lookup"><span data-stu-id="5ed4b-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="5ed4b-114">A completed [Apache Cordova quick start][5] project.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="5ed4b-115">(Android) A [Google account][6] with a verified email address.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="5ed4b-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span><span class="sxs-lookup"><span data-stu-id="5ed4b-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="5ed4b-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <a name="configure-hub"></a><span data-ttu-id="5ed4b-118">Configure a notification hub</span><span class="sxs-lookup"><span data-stu-id="5ed4b-118">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="5ed4b-119">[Watch a video showing steps in this section][9]</span><span class="sxs-lookup"><span data-stu-id="5ed4b-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="5ed4b-120">Update the server project</span><span class="sxs-lookup"><span data-stu-id="5ed4b-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a><span data-ttu-id="5ed4b-121">Modify your Cordova app</span><span class="sxs-lookup"><span data-stu-id="5ed4b-121">Modify your Cordova app</span></span>
<span data-ttu-id="5ed4b-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="5ed4b-123">Update the Cordova version in your project.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="5ed4b-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="5ed4b-125">To update the project:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-125">To update the project:</span></span>

* <span data-ttu-id="5ed4b-126">Right-click `config.xml` to open the configuration designer.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="5ed4b-127">Select the Platforms tab.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="5ed4b-128">Choose 6.1.1 in the **Cordova CLI** text box.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="5ed4b-129">Choose **Build**, then **Build Solution** to update the project.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="5ed4b-130">Install the push plugin</span><span class="sxs-lookup"><span data-stu-id="5ed4b-130">Install the push plugin</span></span>
<span data-ttu-id="5ed4b-131">Apache Cordova applications do not natively handle device or network capabilities.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="5ed4b-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="5ed4b-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="5ed4b-134">You can install the push plugin in one of these ways:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="5ed4b-135">**From the command-prompt:**</span><span class="sxs-lookup"><span data-stu-id="5ed4b-135">**From the command-prompt:**</span></span>

<span data-ttu-id="5ed4b-136">Execute the following command:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="5ed4b-137">**From within Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="5ed4b-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="5ed4b-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="5ed4b-139">Click the arrow next to the installation source.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="5ed4b-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="5ed4b-141">Otherwise, enter a placeholder value, like 777777.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="5ed4b-142">If you are targeting Android, you can update this value in config.xml later.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="5ed4b-143">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-143">Click **Add**.</span></span>

<span data-ttu-id="5ed4b-144">The push plugin is now installed.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="5ed4b-145">Install the device plugin</span><span class="sxs-lookup"><span data-stu-id="5ed4b-145">Install the device plugin</span></span>
<span data-ttu-id="5ed4b-146">Follow the same procedure you used to install the push plugin.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="5ed4b-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span><span class="sxs-lookup"><span data-stu-id="5ed4b-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="5ed4b-148">You need this plugin to obtain the platform name.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="5ed4b-149">Register your device on application start-up</span><span class="sxs-lookup"><span data-stu-id="5ed4b-149">Register your device on application start-up</span></span>
<span data-ttu-id="5ed4b-150">Initially, we include some minimal code for Android.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="5ed4b-151">Later, modify the app to run on iOS or Windows 10.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="5ed4b-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="5ed4b-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="5ed4b-154">You can call `registerForPushNotifications()` as often as is required.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="5ed4b-155">Add the new **registerForPushNotifications** method as follows:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="5ed4b-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span><span class="sxs-lookup"><span data-stu-id="5ed4b-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="5ed4b-157">(Optional) Configure and run the app on Android</span><span class="sxs-lookup"><span data-stu-id="5ed4b-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="5ed4b-158">Complete this section to enable push notifications for Android.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-158">Complete this section to enable push notifications for Android.</span></span>

#### <a name="enable-gcm"></a><span data-ttu-id="5ed4b-159">Enable Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="5ed4b-159">Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="5ed4b-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a><span data-ttu-id="5ed4b-161">Configure the Mobile App backend to send push requests using FCM</span><span class="sxs-lookup"><span data-stu-id="5ed4b-161">Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="5ed4b-162">Configure your Cordova app for Android</span><span class="sxs-lookup"><span data-stu-id="5ed4b-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="5ed4b-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span><span class="sxs-lookup"><span data-stu-id="5ed4b-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="5ed4b-164">Open index.js and update the code to use your numeric project ID.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a><span data-ttu-id="5ed4b-165">Configure your Android device for USB debugging</span><span class="sxs-lookup"><span data-stu-id="5ed4b-165">Configure your Android device for USB debugging</span></span>
<span data-ttu-id="5ed4b-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="5ed4b-167">Perform the following steps on your Android phone:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="5ed4b-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span><span class="sxs-lookup"><span data-stu-id="5ed4b-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="5ed4b-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="5ed4b-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="5ed4b-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="5ed4b-171">However, the techniques are common across any modern Android release.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="5ed4b-172">Install Google Play Services</span><span class="sxs-lookup"><span data-stu-id="5ed4b-172">Install Google Play Services</span></span>
<span data-ttu-id="5ed4b-173">The push plugin relies on Android Google Play Services for push notifications.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="5ed4b-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="5ed4b-175">Android 2.3 or higher</span><span class="sxs-lookup"><span data-stu-id="5ed4b-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="5ed4b-176">Google Repository revision 27 or higher</span><span class="sxs-lookup"><span data-stu-id="5ed4b-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="5ed4b-177">Google Play Services 9.0.2 or higher</span><span class="sxs-lookup"><span data-stu-id="5ed4b-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="5ed4b-178">Click **Install Packages** and wait for the installation to complete.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="5ed4b-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span><span class="sxs-lookup"><span data-stu-id="5ed4b-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="5ed4b-180">Test push notifications in the app on Android</span><span class="sxs-lookup"><span data-stu-id="5ed4b-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="5ed4b-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="5ed4b-182">You can test from the same device or from a second device, as long as you are using the same backend.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="5ed4b-183">Test your Cordova app on the Android platform in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="5ed4b-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="5ed4b-185">Instead of **Google Android Emulator**, select **Device**.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="5ed4b-186">Visual Studio deploys the application to the device and then runs the application.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="5ed4b-187">You can then interact with the application on the device.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="5ed4b-188">Improve your development experience.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-188">Improve your development experience.</span></span>  <span data-ttu-id="5ed4b-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="5ed4b-190">Mobizen projects your Android screen to a web browser on your PC.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="5ed4b-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="5ed4b-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="5ed4b-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="5ed4b-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="5ed4b-195">Run the todolist app as before and insert a new todo item.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="5ed4b-196">This time, a notification icon is displayed in the notification area.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="5ed4b-197">You can open the notification drawer to view the full text of the notification.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="5ed4b-198">(Optional) Configure and run on iOS</span><span class="sxs-lookup"><span data-stu-id="5ed4b-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="5ed4b-199">This section is for running the Cordova project on iOS devices.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="5ed4b-200">If you are not working with iOS devices, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="5ed4b-201">Install and run the iOS remote build agent on a Mac or cloud service</span><span class="sxs-lookup"><span data-stu-id="5ed4b-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="5ed4b-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="5ed4b-203">Make sure you can build the app for iOS.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="5ed4b-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="5ed4b-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="5ed4b-206">For more info, see [Run your iOS app in the cloud][21].</span><span class="sxs-lookup"><span data-stu-id="5ed4b-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="5ed4b-207">XCode 7 or greater is required to use the push plugin on iOS.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="5ed4b-208">Find the ID to use as your App ID</span><span class="sxs-lookup"><span data-stu-id="5ed4b-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="5ed4b-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="5ed4b-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="5ed4b-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="5ed4b-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="5ed4b-213">The ID in the widget element must match the App ID on the developer portal.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="5ed4b-214">Register the app for push notifications on Apple's developer portal</span><span class="sxs-lookup"><span data-stu-id="5ed4b-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="5ed4b-215">Watch a video showing similar steps</span><span class="sxs-lookup"><span data-stu-id="5ed4b-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="5ed4b-216">Configure Azure to send push notifications</span><span class="sxs-lookup"><span data-stu-id="5ed4b-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="5ed4b-217">Verify that your App ID matches your Cordova app</span><span class="sxs-lookup"><span data-stu-id="5ed4b-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="5ed4b-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="5ed4b-219">However, if the IDs don't match, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="5ed4b-220">Delete the platforms folder from your project.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="5ed4b-221">Delete the plugins folder from your project.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="5ed4b-222">Delete the node_modules folder from your project.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="5ed4b-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="5ed4b-224">Rebuild your project.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="5ed4b-225">Test push notifications in your iOS app</span><span class="sxs-lookup"><span data-stu-id="5ed4b-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="5ed4b-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="5ed4b-227">You can run on an iOS device connected to your PC using iTunes.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="5ed4b-228">The iOS Simulator does not support push notifications.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="5ed4b-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5ed4b-230">The app requests confirmation for push notifications during the first run.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="5ed4b-231">In the app, type a task, and then click the plus (+) icon.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="5ed4b-232">Verify that a notification is received, then click OK to dismiss the notification.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="5ed4b-233">(Optional) Configure and run on Windows</span><span class="sxs-lookup"><span data-stu-id="5ed4b-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="5ed4b-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span><span class="sxs-lookup"><span data-stu-id="5ed4b-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="5ed4b-235">If you are not working with Windows devices, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="5ed4b-236">Register your Windows app for push notifications with WNS</span><span class="sxs-lookup"><span data-stu-id="5ed4b-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="5ed4b-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span><span class="sxs-lookup"><span data-stu-id="5ed4b-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="5ed4b-238">[Watch a video showing similar steps][13]</span><span class="sxs-lookup"><span data-stu-id="5ed4b-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="5ed4b-239">Configure the notification hub for WNS</span><span class="sxs-lookup"><span data-stu-id="5ed4b-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="5ed4b-240">Configure your Cordova app to support Windows push notifications</span><span class="sxs-lookup"><span data-stu-id="5ed4b-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="5ed4b-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="5ed4b-242">To support push notifications in your default (debug) builds, open build.json file.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="5ed4b-243">Copy the "release" configuration to your debug configuration.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="5ed4b-244">After the update, the build.json should contain the following code:</span><span class="sxs-lookup"><span data-stu-id="5ed4b-244">After the update, the build.json should contain the following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="5ed4b-245">Build the app and verify that you have no errors.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="5ed4b-246">Your client app should now register for the notifications from the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="5ed4b-247">Repeat this section for every Windows project in your solution.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="5ed4b-248">Test push notifications in your Windows app</span><span class="sxs-lookup"><span data-stu-id="5ed4b-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="5ed4b-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="5ed4b-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="5ed4b-251">Press the Run button to build the project and start the app.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="5ed4b-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="5ed4b-253">Verify that a notification is received when the item is added.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-253">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ed4b-254">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5ed4b-254">Next Steps</span></span>
* <span data-ttu-id="5ed4b-255">Read about [Notification Hubs][17] to learn about push notifications.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="5ed4b-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="5ed4b-257">Learn how to use the SDKs.</span><span class="sxs-lookup"><span data-stu-id="5ed4b-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="5ed4b-258">[Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="5ed4b-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="5ed4b-259">[ASP.NET Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="5ed4b-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="5ed4b-260">[Node.js Server SDK][16]</span><span class="sxs-lookup"><span data-stu-id="5ed4b-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/




