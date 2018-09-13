---
title: Get Started with Azure Mobile Engagement for Cordova/Phonegap
description: Learn how to use Azure Mobile Engagement with Analytics and Push Notifications for Cordova/Phonegap apps.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a535871923a8e7992d97478e2903f200a651f35b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554631"
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="67a8f-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="67a8f-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="67a8f-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span><span class="sxs-lookup"><span data-stu-id="67a8f-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="67a8f-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="67a8f-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="67a8f-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span><span class="sxs-lookup"><span data-stu-id="67a8f-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="67a8f-107">We will deploy this to an iOS or Android device for testing.</span><span class="sxs-lookup"><span data-stu-id="67a8f-107">We will deploy this to an iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="67a8f-108">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="67a8f-108">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="67a8f-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="67a8f-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="67a8f-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="67a8f-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="67a8f-111">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="67a8f-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="67a8f-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span><span class="sxs-lookup"><span data-stu-id="67a8f-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span></span>
* <span data-ttu-id="67a8f-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span><span class="sxs-lookup"><span data-stu-id="67a8f-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span></span>
* <span data-ttu-id="67a8f-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span><span class="sxs-lookup"><span data-stu-id="67a8f-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="67a8f-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span><span class="sxs-lookup"><span data-stu-id="67a8f-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="67a8f-116">Mobile Engagement Cordova Plugin</span><span class="sxs-lookup"><span data-stu-id="67a8f-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="67a8f-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="67a8f-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <a id="setup-azme"></a><span data-ttu-id="67a8f-118">Setup Mobile Engagement for your Cordova app</span><span class="sxs-lookup"><span data-stu-id="67a8f-118">Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="67a8f-119">Connecting your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="67a8f-119">Connecting your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="67a8f-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span><span class="sxs-lookup"><span data-stu-id="67a8f-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="67a8f-121">We will create a basic app with Cordova to demonstrate the integration:</span><span class="sxs-lookup"><span data-stu-id="67a8f-121">We will create a basic app with Cordova to demonstrate the integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="67a8f-122">Create a new Cordova project</span><span class="sxs-lookup"><span data-stu-id="67a8f-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="67a8f-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span><span class="sxs-lookup"><span data-stu-id="67a8f-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span></span> <span data-ttu-id="67a8f-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span><span class="sxs-lookup"><span data-stu-id="67a8f-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="67a8f-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span><span class="sxs-lookup"><span data-stu-id="67a8f-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="67a8f-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span><span class="sxs-lookup"><span data-stu-id="67a8f-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span></span> <span data-ttu-id="67a8f-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span><span class="sxs-lookup"><span data-stu-id="67a8f-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="67a8f-128">Add the Cordova Console plugin.</span><span class="sxs-lookup"><span data-stu-id="67a8f-128">Add the Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="67a8f-129">Connect your app to Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="67a8f-129">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="67a8f-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span><span class="sxs-lookup"><span data-stu-id="67a8f-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers the app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="67a8f-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="67a8f-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="67a8f-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span><span class="sxs-lookup"><span data-stu-id="67a8f-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span></span>

## <a id="monitor"></a><span data-ttu-id="67a8f-133">Enabling real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="67a8f-133">Enabling real-time monitoring</span></span>
1. <span data-ttu-id="67a8f-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span><span class="sxs-lookup"><span data-stu-id="67a8f-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="67a8f-135">Run the application:</span><span class="sxs-lookup"><span data-stu-id="67a8f-135">Run the application:</span></span>
   
   * <span data-ttu-id="67a8f-136">**For iOS**</span><span class="sxs-lookup"><span data-stu-id="67a8f-136">**For iOS**</span></span>
     
       <span data-ttu-id="67a8f-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span><span class="sxs-lookup"><span data-stu-id="67a8f-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="67a8f-138">**For Android**</span><span class="sxs-lookup"><span data-stu-id="67a8f-138">**For Android**</span></span>
     
       <span data-ttu-id="67a8f-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span><span class="sxs-lookup"><span data-stu-id="67a8f-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span></span>
     
           cordova run android
3. <span data-ttu-id="67a8f-140">You can see the following in the console logs:</span><span class="sxs-lookup"><span data-stu-id="67a8f-140">You can see the following in the console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a><span data-ttu-id="67a8f-141">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="67a8f-141">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="67a8f-142">Enabling Push Notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="67a8f-142">Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="67a8f-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span><span class="sxs-lookup"><span data-stu-id="67a8f-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="67a8f-144">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="67a8f-144">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="67a8f-145">The following sections will setup your app to receive them.</span><span class="sxs-lookup"><span data-stu-id="67a8f-145">The following sections will setup your app to receive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="67a8f-146">Configure Push credentials for Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="67a8f-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="67a8f-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span><span class="sxs-lookup"><span data-stu-id="67a8f-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="67a8f-148">Navigate to your Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="67a8f-148">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="67a8f-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span><span class="sxs-lookup"><span data-stu-id="67a8f-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="67a8f-150">You will land in the settings page in your Engagement Portal.</span><span class="sxs-lookup"><span data-stu-id="67a8f-150">You will land in the settings page in your Engagement Portal.</span></span> <span data-ttu-id="67a8f-151">From there click on the **Native Push** section:</span><span class="sxs-lookup"><span data-stu-id="67a8f-151">From there click on the **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="67a8f-152">Configure iOS Certificate/GCM Server API Key</span><span class="sxs-lookup"><span data-stu-id="67a8f-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="67a8f-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="67a8f-153">**[iOS]**</span></span>
   
    <span data-ttu-id="67a8f-154">a.</span><span class="sxs-lookup"><span data-stu-id="67a8f-154">a.</span></span> <span data-ttu-id="67a8f-155">Select your .p12, upload it and type your password:</span><span class="sxs-lookup"><span data-stu-id="67a8f-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="67a8f-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="67a8f-156">**[Android]**</span></span>
   
    <span data-ttu-id="67a8f-157">a.</span><span class="sxs-lookup"><span data-stu-id="67a8f-157">a.</span></span> <span data-ttu-id="67a8f-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="67a8f-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-the-cordova-app"></a><span data-ttu-id="67a8f-159">Enable push notifications in the Cordova app</span><span class="sxs-lookup"><span data-stu-id="67a8f-159">Enable push notifications in the Cordova app</span></span>
<span data-ttu-id="67a8f-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span><span class="sxs-lookup"><span data-stu-id="67a8f-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-the-app"></a><span data-ttu-id="67a8f-161">Run the app</span><span class="sxs-lookup"><span data-stu-id="67a8f-161">Run the app</span></span>
<span data-ttu-id="67a8f-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="67a8f-162">**[iOS]**</span></span>

1. <span data-ttu-id="67a8f-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span><span class="sxs-lookup"><span data-stu-id="67a8f-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span></span> <span data-ttu-id="67a8f-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span><span class="sxs-lookup"><span data-stu-id="67a8f-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span></span> <span data-ttu-id="67a8f-165">Open up the native .xcodeproj file in XCode.</span><span class="sxs-lookup"><span data-stu-id="67a8f-165">Open up the native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="67a8f-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span><span class="sxs-lookup"><span data-stu-id="67a8f-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span></span> <span data-ttu-id="67a8f-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span><span class="sxs-lookup"><span data-stu-id="67a8f-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span></span> 
3. <span data-ttu-id="67a8f-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span><span class="sxs-lookup"><span data-stu-id="67a8f-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span></span> <span data-ttu-id="67a8f-169">Grant the permission.</span><span class="sxs-lookup"><span data-stu-id="67a8f-169">Grant the permission.</span></span> 

<span data-ttu-id="67a8f-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="67a8f-170">**[Android]**</span></span>

<span data-ttu-id="67a8f-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span><span class="sxs-lookup"><span data-stu-id="67a8f-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span></span> 

    cordova run android

## <a id="send"></a><span data-ttu-id="67a8f-172">Send a notification to your app</span><span class="sxs-lookup"><span data-stu-id="67a8f-172">Send a notification to your app</span></span>
<span data-ttu-id="67a8f-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span><span class="sxs-lookup"><span data-stu-id="67a8f-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span></span>

1. <span data-ttu-id="67a8f-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span><span class="sxs-lookup"><span data-stu-id="67a8f-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="67a8f-175">Click **New Announcement** to create your push campaign</span><span class="sxs-lookup"><span data-stu-id="67a8f-175">Click **New Announcement** to create your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="67a8f-176">Provide inputs to create your campaign **[Android]**</span><span class="sxs-lookup"><span data-stu-id="67a8f-176">Provide inputs to create your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="67a8f-177">Provide a **Name** for your campaign.</span><span class="sxs-lookup"><span data-stu-id="67a8f-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="67a8f-178">Select the **Delivery Type** as *System notification* *Simple*</span><span class="sxs-lookup"><span data-stu-id="67a8f-178">Select the **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="67a8f-179">Select the **Delivery time** as *"Any Time"*</span><span class="sxs-lookup"><span data-stu-id="67a8f-179">Select the **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="67a8f-180">Provide a **Title** for your notification which will be the first line in the push.</span><span class="sxs-lookup"><span data-stu-id="67a8f-180">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="67a8f-181">Provide a **Message** for your notification which will serve as the message body.</span><span class="sxs-lookup"><span data-stu-id="67a8f-181">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="67a8f-182">Provide inputs to create your campaign **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="67a8f-182">Provide inputs to create your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="67a8f-183">Provide a **Name** for your campaign.</span><span class="sxs-lookup"><span data-stu-id="67a8f-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="67a8f-184">Select the **Delivery time** as *"Out of app only"*</span><span class="sxs-lookup"><span data-stu-id="67a8f-184">Select the **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="67a8f-185">Provide a **Title** for your notification which will be the first line in the push.</span><span class="sxs-lookup"><span data-stu-id="67a8f-185">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="67a8f-186">Provide a **Message** for your notification which will serve as the message body.</span><span class="sxs-lookup"><span data-stu-id="67a8f-186">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="67a8f-187">Scroll down, and in the content section select **Notification only**</span><span class="sxs-lookup"><span data-stu-id="67a8f-187">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="67a8f-188">[Optional] You can also provide an Action URL.</span><span class="sxs-lookup"><span data-stu-id="67a8f-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="67a8f-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="67a8f-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="67a8f-190">You're done setting the most basic campaign possible.</span><span class="sxs-lookup"><span data-stu-id="67a8f-190">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="67a8f-191">Now scroll down again and click the **Create** button to save your campaign.</span><span class="sxs-lookup"><span data-stu-id="67a8f-191">Now scroll down again and click the **Create** button to save your campaign.</span></span>
8. <span data-ttu-id="67a8f-192">Finally **Activate** your campaign</span><span class="sxs-lookup"><span data-stu-id="67a8f-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="67a8f-193">You should now see a push notification on your device or emulator as part of this campaign.</span><span class="sxs-lookup"><span data-stu-id="67a8f-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <a id="next-steps"></a><span data-ttu-id="67a8f-194">Next Steps</span><span class="sxs-lookup"><span data-stu-id="67a8f-194">Next Steps</span></span>
[<span data-ttu-id="67a8f-195">Overview of all methods available with Cordova Mobile Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="67a8f-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/engage-button.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/api-key.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png










